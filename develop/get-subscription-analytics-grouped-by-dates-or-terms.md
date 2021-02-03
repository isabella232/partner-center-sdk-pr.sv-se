---
title: Hämta prenumerations analys grupperat efter datum eller villkor
description: Hur du hämtar information om prenumerations analys grupperat efter datum eller villkor.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769051"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Hämta prenumerations analys grupperat efter datum eller villkor

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hur du hämtar information om prenumerations analys för dina kunder grupperade efter datum eller villkor.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan |
|--------|-------------|
| **TA** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? groupby = {groupby_queries} |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande obligatoriska Sök vägs parametrar för att identifiera din organisation och gruppera resultatet.

| Namn | Typ | Obligatorisk | Beskrivning |
|------|------|----------|-------------|
| groupby_queries | par med strängar och dateTime | Yes | Villkoren och datumen för att filtrera resultatet. |

### <a name="groupby-syntax"></a>GroupBy-syntax

Group by-parametern måste bestå av en serie kommaavgränsade fält värden.

Ett avkodat exempel ser ut så här:

```http
?groupby=termField1,dateField1,termField2
```

I följande tabell visas en lista över de fält som stöds för Group by.

| Fält | Typ | Description |
|-------|------|-------------|
| customerTenantId | sträng | En GUID-formaterad sträng som identifierar kundens klient organisation. |
| customerName | sträng | Namnet på kunden. |
| customerMarket | sträng | Landet/regionen som kunden gör affärer med. |
| id | sträng | En GUID-formaterad sträng som identifierar prenumerationen. |
| status | sträng | Prenumerationens status. De värden som stöds är: "aktiv", "inaktive rad" eller "deetablerat". |
| Namn | sträng | Produktens namn. |
| subscriptionType | sträng | Prenumerations typ. Obs! det här fältet är Skift läges känsligt. De värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Boolesk | Ett värde som anger om prenumerationen förnyas automatiskt. |
| Partner  | sträng | MPN-ID. För en direkt åter försäljare är den här parametern MPN-ID för partnern. För en indirekt åter försäljare är den här parametern MPN-ID: t för den indirekta åter försäljaren. |
| friendlyName | sträng | Namnet på prenumerationen. |
| partnerName | sträng | Namnet på partnern som prenumerationen köptes för |
| providerName | sträng | När prenumerations transaktionen är för den indirekta åter försäljaren är Providerns namn den indirekta providern som köpte prenumerationen.
| creationDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen skapades. |
| effectiveStartDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen startar. |
| commitmentEndDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen slutar. |
| currentStateEndDate | sträng i UTC-datum/tid-format | Det datum då prenumerationens aktuella status kommer att ändras. |
| trialToPaidConversionDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen konverteras från utvärderings versionen till betald. Standardvärdet är null. |
| trialStartDate | sträng i UTC-datum/tid-format | Det datum då utvärderings perioden för prenumerationen startades. Standardvärdet är null. |
| lastUsageDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen senast användes. Standardvärdet är null. |
| deprovisionedDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen avetablerades. Standardvärdet är null. |
| lastRenewalDate | sträng i UTC-datum/tid-format | Det datum då prenumerationen senast förnyades. Standardvärdet är null. |

### <a name="filter-fields"></a>Filter fält

I följande tabell visas valfria filter fält och deras beskrivningar:

| Fält | Typ |  Description |
|-------|------|--------------|
| top | int | Det antal rader med data som ska returneras i begäran. Om värdet inte anges är det högsta värdet och standardvärdet 10000. Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data. |
| hoppa över | int | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att växla mellan stora data mängder. Till exempel Top = 10000 och Skip = 0 hämtar de första 10000 raderna med data, Top = 10000 och Skip = 10000 hämtar nästa 10000 rader med data. |
| filter | sträng | En eller flera instruktioner som filtrerar raderna i svaret. Varje filter instruktion innehåller ett fält namn från svars texten och ett värde som är kopplat till **`eq`** , **`ne`** , eller för vissa fält, **`contains`** operatorn. Instruktioner kan kombineras med hjälp av **`and`** eller **`or`** . Sträng värden måste omges av enkla citat tecken i filter parametern. I följande avsnitt finns en lista över fält som kan filtreras och de operatorer som stöds med dessa fält. |
| aggregationLevel | sträng | Anger det tidsintervall som aggregerade data ska hämtas från. Kan vara en av följande strängar: **dag**, **vecka** eller **månad**. Om värdet inte anges är standardvärdet **dateRange**. **Obs!** den här parametern gäller endast när ett datum fält skickas som en del av parametern groupBy. |
| groupBy | sträng | En instruktion som endast tillämpar data agg regering på de angivna fälten. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas innehåller svars texten en samling [prenumerations](partner-center-analytics-resources.md#subscription-resource) resurser grupperade enligt de angivna villkoren och datumen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

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
