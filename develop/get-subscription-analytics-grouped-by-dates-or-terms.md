---
title: Hämta prenumerationsanalys grupperade efter datum eller villkor
description: Så här hämtar du prenumerationsanalysinformation grupperad efter datum eller villkor.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8192a9863d53ec8697a7341cd38c69200614bd4a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548727"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Hämta prenumerationsanalys grupperade efter datum eller villkor

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här hämtar du prenumerationsanalysinformation för dina kunder grupperade efter datum eller villkor.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan |
|--------|-------------|
| **Få** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries} |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande obligatoriska sökvägsparametrar för att identifiera din organisation och gruppera resultaten.

| Namn | Typ | Obligatorisk | Beskrivning |
|------|------|----------|-------------|
| groupby_queries | par med strängar och dateTime | Ja | Termerna och datumen för att filtrera resultatet. |

### <a name="groupby-syntax"></a>GroupBy-syntax

Gruppera efter parameter måste bestå av en serie kommaavgränsade fältvärden.

Ett okodat exempel ser ut så här:

```http
?groupby=termField1,dateField1,termField2
```

I följande tabell visas en lista över de fält som stöds för gruppera efter.

| Fält | Typ | Beskrivning |
|-------|------|-------------|
| customerTenantId | sträng | En GUID-formaterad sträng som identifierar kundens klientorganisation. |
| customerName | sträng | Namnet på kunden. |
| customerMarket | sträng | Land/region som kunden gör affärer i. |
| id | sträng | En GUID-formaterad sträng som identifierar prenumerationen. |
| status | sträng | Prenumerationsstatus. Värden som stöds är: "ACTIVE", "SUSPENDED" eller "DEPROVISIONED". |
| Productname | sträng | Namnet på produkten. |
| subscriptionType | sträng | Prenumerationstyp. Obs! Det här fältet är case-sensitive. Värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Boolesk | Ett värde som anger om prenumerationen förnyas automatiskt. |
| partnerId  | sträng | MPN-ID: t. För en direktåterförsäljare är den här parametern MPN-ID för partnern. För en indirekt återförsäljare är den här parametern MPN-ID:t för den indirekta återförsäljaren. |
| friendlyName | sträng | Namnet på prenumerationen. |
| partnerName | sträng | Namnet på den partner som prenumerationen köptes för |
| providerName | sträng | När prenumerationstransaktionen är för den indirekta återförsäljaren är providernamnet den indirekta leverantör som köpte prenumerationen.
| creationDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen skapades. |
| effectiveStartDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen startar. |
| commitmentEndDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen upphör. |
| currentStateEndDate | sträng i UTC-datum/tid-format | Det datum då prenumerationens aktuella status ändras. |
| trialToDateConversionDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen konverteras från utvärderingsversion till betald. Standardvärdet är null. |
| trialStartDate | sträng i UTC-datum/tid-format | Det datum då utvärderingsperioden för prenumerationen startade. Standardvärdet är null. |
| lastUsageDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen senast användes. Standardvärdet är null. |
| deprovisionedDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen avetableades. Standardvärdet är null. |
| lastRenewalDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen senast förnyades. Standardvärdet är null. |

### <a name="filter-fields"></a>Filterfält

I följande tabell visas valfria filterfält och deras beskrivningar:

| Fält | Typ |  Beskrivning |
|-------|------|--------------|
| top | int | Antalet rader med data som ska returneras i begäran. Om värdet inte anges är det högsta värdet och standardvärdet 10000. Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa sida med data. |
| hoppa över | int | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att bläddra igenom stora datamängder. Till exempel hämtar top=10000 och skip=0 de första 10 000 raderna med data, top=10000 och skip=10000 hämtar de nästa 10 000 raderna med data. |
| filter | sträng | En eller flera instruktioner som filtrerar raderna i svaret. Varje filtersats innehåller ett fältnamn från svarstexten och ett värde som är associerade med **`eq`** **`ne`** operatorn , eller för vissa **`contains`** fält. Instruktioner kan kombineras med **`and`** hjälp av eller **`or`** . Strängvärden måste omges av enkla citattecken i filterparametern. I följande avsnitt finns en lista över fält som kan filtreras och de operatorer som stöds med dessa fält. |
| aggregationLevel | sträng | Anger det tidsperiod som aggregerade data ska hämtas för. Kan vara någon av följande strängar: **dag,** **vecka** eller **månad.** Om värdet inte anges är standardvärdet **dateRange**. **Obs!** Den här parametern gäller endast när ett datumfält skickas som en del av parametern groupBy. |
| groupBy | sträng | En instruktion som endast tillämpar dataaggregering på de angivna fälten. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten en samling [prenumerationsresurser](partner-center-analytics-resources.md#subscription-resource) grupperade efter de angivna termerna och datumen.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>Se även

[Partnercenter-analys – resurser](partner-center-analytics-resources.md)
