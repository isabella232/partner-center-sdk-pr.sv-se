---
title: Hämta prenumerationsanalys via sökfråga
description: Så här hämtar du information om prenumerationsanalys filtrerad efter en sökfråga.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548744"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Hämta information om prenumerationsanalys filtrerad efter en sökfråga

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här hämtar du prenumerationsanalysinformation för dina kunder filtrerade efter en sökfråga.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan |
|--------|-------------|
| **Få** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string} |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande obligatoriska sökvägsparameter för att identifiera din organisation och filtrera sökningen.

| Namn | Typ | Obligatorisk | Beskrivning |
|------|------|----------|-------------|
| filter_string | sträng | Ja | Filtret som ska tillämpas på prenumerationsanalysen. Se avsnitten Filtersyntax och Filterfält för syntax, fält och operatorer som ska användas i den här parametern. |

### <a name="filter-syntax"></a>Filtersyntax

Filterparametern måste bestå av en serie kombinationer av fält, värde och operator. Flera kombinationer kan kombineras med operatorerna **`and`** **`or`** eller .

Ett okodat exempel ser ut så här:

- Sträng: `?filter=Field operator 'Value'`
- Boolean: `?filter=Field operator Value`
- Innehåller `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Filterfält

Filterparametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje -instruktion innehåller ett fält och värde som är associerade med **`eq`** **`ne`** operatorerna eller . Vissa fält stöder också **`contains`** operatorerna **`gt`** , , , och **`lt`** **`ge`** **`le`** . Instruktioner kan kombineras med **`and`** operatorerna **`or`** eller .

Följande är exempel på filtersträngar:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

I följande tabell visas en lista över de fält som stöds och stödoperatorer för filterparametern. Strängvärden måste omges av enkla citattecken.

| Parameter | Operatorer som stöds | Beskrivning |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Ett värde som anger om prenumerationen förnyas automatiskt. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Det datum då prenumerationen upphör. |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Det datum då prenumerationen skapades. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationens aktuella status ändras. |
| customerMarket | `eq`, `ne` | Land/region som kunden gör affärer i. |
| customerName | `contains` | Namnet på kunden. |
| customerTenantId | `eq`, `ne` | En GUID-formaterad sträng som identifierar kundens klientorganisation. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen avetableades. Standardvärdet är null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen startar. |
| friendlyName | `contains` | Namnet på prenumerationen. |
| id | `eq`, `ne` | En GUID-formaterad sträng som identifierar prenumerationen. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen senast förnyades. Standardvärdet är null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen senast användes. Standardvärdet är null. |
| partnerId | `eq`, `ne` | MPN-ID: t. För en direktåterförsäljare är det här värdet PARTNERns MPN-ID. För en indirekt återförsäljare blir det här värdet MPN-ID:t för den indirekta återförsäljaren. |
| partnerName | sträng | Namnet på den partner som prenumerationen köptes för |
| Productname | `contains`, `eq`, `ne` | Namnet på produkten. |
| providerName | sträng | När prenumerationstransaktionen är för den indirekta återförsäljaren är providernamnet den indirekta leverantör som köpte prenumerationen.|
| status | `eq`, `ne` | Prenumerationsstatus. Värden som stöds är: "ACTIVE", "SUSPENDED" eller "DEPROVISIONED". |
| subscriptionType | `eq`, `ne` | Prenumerationstyp. **Obs!** Det här fältet är case-sensitive. Värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då utvärderingsperioden för prenumerationen startade. Standardvärdet är null. |
| trialToDateConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Det datum då prenumerationen konverteras från utvärderingsversion till betald. Standardvärdet är null. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten en samling [prenumerationsresurser](partner-center-analytics-resources.md#subscription-resource) som uppfyller filtervillkoren.

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
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a>Se även

- [Partnercenter-analys – resurser](partner-center-analytics-resources.md)
