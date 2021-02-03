---
title: Hämta prenumerations analys per Sök fråga
description: Hämta information om prenumerations analys som filtrerats av en Sök fråga.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769054"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Hämta information om prenumerationsanalys filtrerad efter en sökfråga

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hämta information om prenumerations analys för dina kunder filtrerat efter en Sök fråga.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan |
|--------|-------------|
| **TA** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? filter = {filter_string} |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande obligatoriska Sök vägs parameter för att identifiera din organisation och filtrera sökningen.

| Namn | Typ | Obligatorisk | Beskrivning |
|------|------|----------|-------------|
| filter_string | sträng | Yes | Filtret som ska användas för prenumerations analysen. Se avsnitten filtrera syntax och filter fält för syntax, fält och operatorer som ska användas i den här parametern. |

### <a name="filter-syntax"></a>Filter-syntax

Filter parametern måste bestå av en serie av kombinationer av fält, värde och operatorer. Flera kombinationer kan kombineras med hjälp av **`and`** eller- **`or`** operatorer.

Ett avkodat exempel ser ut så här:

- Nollängd `?filter=Field operator 'Value'`
- Booleskt `?filter=Field operator Value`
- Ingår `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Filter fält

Filter parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje instruktion innehåller ett fält och ett värde som är associerat **`eq`** med **`ne`** operatorerna eller. Vissa fält har även stöd **`contains`** för **`gt`** operatorerna,,, **`lt`** **`ge`** och **`le`** . Instruktioner kan kombineras med hjälp av **`and`** eller- **`or`** operatorer.

Följande är exempel på filter strängar:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

I följande tabell visas en lista över de fält och support operatörer som stöds för filter parametern. Sträng värden måste omges av enkla citat tecken.

| Parameter | Operatorer som stöds | Description |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Ett värde som anger om prenumerationen förnyas automatiskt. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Det datum då prenumerationen slutar. |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Det datum då prenumerationen skapades. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationens aktuella status kommer att ändras. |
| customerMarket | `eq`, `ne` | Landet/regionen som kunden gör affärer med. |
| customerName | `contains` | Namnet på kunden. |
| customerTenantId | `eq`, `ne` | En GUID-formaterad sträng som identifierar kundens klient organisation. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen avetablerades. Standardvärdet är null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen startar. |
| friendlyName | `contains` | Namnet på prenumerationen. |
| id | `eq`, `ne` | En GUID-formaterad sträng som identifierar prenumerationen. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen senast förnyades. Standardvärdet är null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då prenumerationen senast användes. Standardvärdet är null. |
| Partner | `eq`, `ne` | MPN-ID. För en direkt åter försäljare är det här värdet MPN-ID för partnern. För en indirekt åter försäljare är det här värdet MPN-ID: t för den indirekta åter försäljaren. |
| partnerName | sträng | Namnet på partnern som prenumerationen köptes för |
| Namn | `contains`, `eq`, `ne` | Produktens namn. |
| providerName | sträng | När prenumerations transaktionen är för den indirekta åter försäljaren är Providerns namn den indirekta providern som köpte prenumerationen.|
| status | `eq`, `ne` | Prenumerationens status. De värden som stöds är: "aktiv", "inaktive rad" eller "deetablerat". |
| subscriptionType | `eq`, `ne` | Prenumerations typ. **Obs!** det här fältet är Skift läges känsligt. De värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Det datum då utvärderings perioden för prenumerationen startades. Standardvärdet är null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Det datum då prenumerationen konverteras från utvärderings versionen till betald. Standardvärdet är null. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas innehåller svars texten en samling [prenumerations](partner-center-analytics-resources.md#subscription-resource) resurser som uppfyller filter kriterierna.

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
