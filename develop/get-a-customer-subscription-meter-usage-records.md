---
title: Hämta användningsdata för prenumeration efter mätare
description: Du kan använda MeterUsageRecord resurs samling för att få användnings poster för mätare för en kund för specifika Azure-tjänster eller-resurser under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769147"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>Hämta användningsdata för prenumeration efter mätare

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan använda **MeterUsageRecord** resurs samling för att få användnings poster för mätare för en kund för specifika Azure-tjänster eller-resurser under den aktuella fakturerings perioden. Den här resurs samlingen representerar en sammanställd summa för varje mätare för den aktuella fakturerings perioden i hela Azure-planen.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID

*Den nya vägen motsvarar `subscriptions/{subscription-id}/usagerecords/resources` , som fortsätter att fungera enbart för Microsoft Azure (MS-AZR-0145P)-prenumerationer.* Den nya vägen stöder både Microsoft Azure (MS-AZR-0145P)-prenumerationer och Azure-planer. För att få den här informationen för din Azure-plan måste du växla till den nya vägen. Förutom de egenskaper som anges i följande avsnitt, är svaret detsamma som den gamla vägen.

## <a name="c"></a>C\#

Så här hämtar du mätar användnings poster för en kund för en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden:

1. Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .

2. Anropa egenskapen Subscriptions och **UsageRecords**, sedan egenskapen **meters** . Slutför genom att anropa metoderna Get () eller GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

Ett exempel finns i följande exempel:

- Exempel: [konsol test app](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Klass: **GetSubscriptionUsageRecordsByMeter.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/meterusagerecords http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Den här tabellen innehåller de frågeparametrar som krävs för att hämta kundens beräknade användnings information.

| Namn                   | Typ     | Obligatorisk | Beskrivning                               |
|------------------------|----------|----------|-------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Ett GUID som motsvarar kunden.     |
| **prenumerations-ID**    | **guid** | Y        | Ett GUID som motsvarar ID: t för en [prenumerations resurs](subscription-resources.md#subscription)för partner Center, som representerar en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan. *För prenumerations resurser i Azure plan anger du **plan-ID** som **prenumerations-ID** i den här vägen.* |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden **en \<MeterUsageRecord> PagedResourceCollection** -resurs i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Svars exempel för Microsoft Azure (MS-AZR-0145P)-prenumerationer

I det här exemplet har kunden köpt **145P Azure-PayG**.

*För kunder med en Microsoft Azure-prenumeration (MS-AZR-0145P) sker ingen ändring i API-svaret.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Exempel på REST-svar för Azure-prenumeration

I det här exemplet har kunden köpt en Azure-prenumeration.

*För kunder med Azure-planer finns följande ändringar i API-svaret:*

- **currencyLocale** ersätts med **CurrencyCode**
- **usdTotalCost** är ett nytt fält

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
