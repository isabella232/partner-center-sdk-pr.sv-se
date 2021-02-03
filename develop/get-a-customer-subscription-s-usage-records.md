---
title: Hämta alla prenumerationsanvändningsposter för en kund
description: Du kan använda SubscriptionMonthlyUsageRecord-resurs samlingen för att hämta prenumerations användnings poster för en kund av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 765ea16ff58b462d83ae3b8764b8b34c3ef804dc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769144"
---
# <a name="get-subscription-usage-records-for-a-customer"></a>Hämta prenumerations användnings poster för en kund

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan använda **SubscriptionMonthlyUsageRecord** -resurs samlingen för att hämta prenumerations användnings poster för en kund av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden. Den här resursen representerar alla prenumerationer för kunden. För en kund med en Azure-plan returnerar den här resursen en lista över dessa planer (inte enskilda Azure-prenumerationer).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

För att hämta prenumerations användnings poster för en kund av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden.:

1. Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .

2. Anropa sedan egenskapen **Subscriptions** och egenskapen **UsageRecords** . Slutför genom att anropa metoderna Get () eller GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

Ett exempel finns i följande avsnitt:

- Exempel: [konsol test app](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Klass: **GetSubscriptionUsageRecords.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/usagerecords http/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta kundens beräknade användnings information.

| Namn                   | Typ     | Obligatorisk | Beskrivning                           |
|------------------------|----------|----------|---------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Ett GUID som motsvarar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en **SubscriptionMonthlyUsageRecord** -resurs i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Svars exempel för Microsoft Azure (MS-AZR-0145P)-prenumerationer

I det här exemplet har kunden köpt ett **145P Azure PayG** -erbjudande.

*För kunder med Microsoft Azure-prenumerationer (MS-AZR-0145P) sker ingen ändring i API-svaret.*

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
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords/",
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
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 2,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-7d58-6654-69fa-0797198155d3",
            "id": "11111111-7d58-6654-69fa-0797198155d3",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        },
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "id": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
