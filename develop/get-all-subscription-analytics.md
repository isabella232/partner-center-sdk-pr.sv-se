---
title: Hämta all information om prenumerationsanalys
description: Så här hämtar du all prenumerationsanalysinformation.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760257"
---
# <a name="get-all-subscription-analytics-information"></a>Hämta all information om prenumerationsanalys

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Den här artikeln beskriver hur du hämtar all prenumerationsanalysinformation för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering endast med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan |
|--------|-------------|
| **Få** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

I följande tabell visas valfria parametrar och deras beskrivningar:

| Parameter | Typ |  Beskrivning |
|-----------|------|--------------|
| top | int | Antalet rader med data som ska returneras i begäran. Om värdet inte anges är det högsta värdet och standardvärdet `10000` . Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa datasida. |
| hoppa över | int | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att bläddra igenom stora datamängder. Till exempel `top=10000` hämtar och de första 10 000 raderna med data och hämtar de kommande `skip=0` `top=10000` `skip=10000` 10 000 raderna med data. |
| filter | sträng | En eller flera instruktioner som filtrerar raderna i svaret. Varje filtersats innehåller ett fältnamn från svarstexten och ett värde som är associerat med **`eq`** **`ne`** operatorn , eller för vissa **`contains`** fält. Instruktioner kan kombineras med **`and`** hjälp av eller **`or`** . Strängvärden måste omges av enkla citattecken i **filterparametern.** Se följande avsnitt för en lista över fält som kan filtreras och de operatorer som stöds med dessa fält. |
| aggregationLevel | sträng | Anger det tidsperiod som aggregerade data ska hämtas för. Kan vara någon av följande strängar: **dag,** **vecka** eller **månad**. Om värdet inte anges är standardvärdet **dateRange**. Den här parametern gäller endast när ett datumfält skickas som en del av **parametern groupBy.** |
| groupBy | sträng | En instruktion som endast tillämpar dataaggregering på de angivna fälten. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas innehåller svarstexten en samling [**prenumerationsresurser.**](partner-center-analytics-resources.md#subscription-resource)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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
