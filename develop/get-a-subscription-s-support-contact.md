---
title: Hämta en prenumerations supportkontakt
description: Så här hämtar du en prenumerations supportkontakt.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 448a60db236ddfbb090cd376bb0dc98e93d4c87342febbcc1958ccd6033fa900
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994174"
---
# <a name="get-a-subscriptions-support-contact"></a>Hämta en prenumerations supportkontakt

**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här hämtar du en prenumerations supportkontakt.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- En prenumerationsidentifierare.

## <a name="c"></a>C\#

För att få en prenumerations supportkontakt börjar du med att använda metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden. Hämta sedan ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID:t. Använd sedan egenskapen [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) för att hämta ett gränssnitt som stöder kontaktåtgärder och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta [**Objektet SupportContact.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact)

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK Samples **Class**: GetSubscriptionSupportContact.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökvägsparametrar för att identifiera kunden och prenumerationen.

| Namn            | Typ   | Obligatorisk | Beskrivning                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| kund-ID     | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden.           |
| prenumerations-id | sträng | Yes      | En GUID-formaterad sträng som identifierar utvärderingsprenumerationen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten [SupportContact-resursen.](subscription-resources.md#supportcontact)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
