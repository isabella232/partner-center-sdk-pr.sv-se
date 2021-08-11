---
title: Hämta en användningssammanfattning för en partner
description: Du kan använda resursen PartnerUsageSummary för att hämta en partneranvändningssammanfattning för alla kunder som har köpt en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: e82c2220768b211b37fad4bbc675e347a25a59217aa881f4e4db2e4d586eb354
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993630"
---
# <a name="get-a-usage-summary-for-a-partner"></a>Hämta en användningssammanfattning för en partner

**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Du kan använda resursen **PartnerUsageSummary** för att hämta en partneranvändningssammanfattning för alla kunder som har köpt en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.

*Summan som returneras av det här API:et returnerar inte förbrukning för kunder som har en Azure-plan.* Planerat för utfasning i framtiden.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Så här hämtar du en användningssammanfattning för alla kunder som har köpt en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden:

1. Använd din **IAggregatePartner.**

2. Anropa egenskapen **UsageSummary** följt av **metoderna Get()** eller **GetAsync():**

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

Ett exempel finns i följande:

- Exempel: [Konsoltestapp](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Klass: **GetPartnerUsageSummary.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                         |
|---------|---------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden **en PartnerUsageSummary-resurs** i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```
