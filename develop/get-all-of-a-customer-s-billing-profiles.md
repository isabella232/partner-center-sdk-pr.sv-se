---
title: Hämta en kunds faktureringsprofil
description: Hämtar faktureringsprofilen för en kund. På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först välja en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 2f5c1cbdf059c4277a8a15d500b54f7fdf2c8e211c4c4f583e71d44b8cfca571
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993953"
---
# <a name="get-a-customers-billing-profile"></a>Hämta en kunds faktureringsprofil

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Hämtar faktureringsprofilen för en kund.

På instrumentpanelen i Partnercenter kan den här åtgärden utföras genom att först [välja en kund.](get-a-customer-by-name.md) Välj Sedan Konto under kundens namn i det vänstra **sidofältet.** Faktureringsprofilen finns under rubriken **Faktureringsinformation.**

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill hämta en kunds faktureringsprofil använder du [**din IPartner.Customers-samling**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och [**anropar metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) Anropa sedan egenskapen [**Profiler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) följt av [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) Fakturering. Anropa slutligen metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** PartnerSDK.FeatureSamples-klass: GetCustomerBillingProfile.cs 

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att hämta faktureringsprofilen.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-klient-id** | **guid** | Y        | Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling [profilresurser](profile-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
