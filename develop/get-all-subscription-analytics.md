---
title: Hämta all information om prenumerationsanalys
description: Hämta all information om prenumerations analys.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768754"
---
# <a name="get-all-subscription-analytics-information"></a>Hämta all information om prenumerationsanalys

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Den här artikeln beskriver hur du hämtar all information om prenumerations analys för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan |
|--------|-------------|
| **TA** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

I följande tabell visas valfria parametrar och beskrivningar:

| Parameter | Typ |  Description |
|-----------|------|--------------|
| top | int | Det antal rader med data som ska returneras i begäran. Om värdet inte anges, är det högsta värdet och standardvärdet `10000` . Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data. |
| hoppa över | int | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att växla mellan stora data mängder. Till exempel `top=10000` och `skip=0` hämtar de första 10000 raderna med data `top=10000` och `skip=10000` hämtar nästa 10000 rader med data. |
| filter | sträng | En eller flera instruktioner som filtrerar raderna i svaret. Varje filter instruktion innehåller ett fält namn från svars texten och ett värde som är kopplat till **`eq`** , **`ne`** , eller för vissa fält, **`contains`** operatorn. Instruktioner kan kombineras med hjälp av **`and`** eller **`or`** . Sträng värden måste omges av enkla citat tecken i **filter** parametern. I följande avsnitt finns en lista över fält som kan filtreras och de operatorer som stöds med dessa fält. |
| aggregationLevel | sträng | Anger det tidsintervall som aggregerade data ska hämtas från. Kan vara en av följande strängar: **dag**, **vecka** eller **månad**. Om värdet inte anges är standardvärdet **dateRange**. Den här parametern gäller endast när ett datum fält skickas som en del av **groupBy** -parametern. |
| groupBy | sträng | En instruktion som endast tillämpar data agg regering på de angivna fälten. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling [**prenumerations**](partner-center-analytics-resources.md#subscription-resource) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>Se även

- [Partnercenter-analys – resurser](partner-center-analytics-resources.md)
