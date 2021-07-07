---
title: Skapa en kundvagn med tillägg
description: Lär dig hur du använder Partner Center-API:er för att lägga till en kundorder med tillägg via en kundvagn. Artikeln delar krav och steg för att skapa en kundvagn med tillägg.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 513a9607b9194c36253630c91de9622325317c3a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973765"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Skapa en kundvagn med tillägg till en kundbeställning

Du kan köpa tillägg via en kundvagn. Mer information om vad som för närvarande är tillgängligt för försäljning finns [i Partnererbjudanden i Molnlösningsleverantör program](/partner-center/csp-offers).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Med en kundvagn kan du köpa ett baserbjudande och motsvarande tillägg. Följ dessa steg för att skapa en kundvagn:

1. Skapa en instans av [**ett kundvagnsobjekt.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)

2. Skapa en lista över [**CartLineItem-objekt**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) som representerar baserbjudandet och tilldela listan till kundvagnens [**lineItems-egenskap.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)

3. Under varje baserbjudandes kundvagnsradsobjekt fyller du i listan **med AddOnItems** med andra **CartLineItem-objekt** som var och en representerar ett tillägg som ska köpas mot baserbjudandet.

4. Hämta ett gränssnitt för kundvagnsåtgärder med [**hjälp av IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) för att anropa [**metoden ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och hämta sedan gränssnittet från **egenskapen Cart.**

5. Anropa slutligen metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) för att skapa kundvagnen.

### <a name="c-example"></a>\#C-exempel

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

Följ de här stegen för att skapa en kundvagn som aktiverar köp av tillägg mot befintliga basprenumerationerna:

1. Skapa en **kundvagn** med en ny **CartLineItem** som innehåller prenumerations-ID:t i **egenskapen ProvisioningContext** med nyckeln "ParentSubscriptionId".

2. Anropa metoden **Create** eller **CreateAsync.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1                        |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande sökvägsparameter för att identifiera kunden.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-id** | sträng   | Ja      | Ett GUID-formaterat kund-ID som identifierar kunden.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs [egenskaperna för](cart-resources.md) Kundvagn i begärandetexten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sträng           | No              | En kundvagnsidentifierare som anges när kundvagnen har skapats.                                  |
| creationTimeStamp     | DateTime         | Inga              | Datumet då kundvagnen skapades i datum/tid-format. Tillämpas när kundvagnen har skapats.         |
| lastModifiedTimeStamp | DateTime         | Inga              | Datum då kundvagnen senast uppdaterades i datum/tid-format. Tillämpas när kundvagnen har skapats.    |
| expirationTimeStamp   | DateTime         | Inga              | Datumet då kundvagnen upphör att gälla i datum/tid-format.  Tillämpas när kundvagnen har skapats.            |
| lastModifiedUser      | sträng           | No              | Den användare som senast uppdaterade kundvagnen. Tillämpas när kundvagnen har skapats.                             |
| lineItems             | Matris med objekt | Ja             | En matris med [CartLineItem-resurser.](cart-resources.md#cartlineitem)                                             |

I den här tabellen beskrivs [egenskaperna för CartLineItem](cart-resources.md#cartlineitem) i begärandetexten.

| Egenskap             | Typ                             | Beskrivning                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sträng                           | En unik identifierare för ett kundvagnsradsobjekt. Tillämpas när kundvagnen har skapats.                                                                   |
| catalogId            | sträng                           | Katalogobjektets identifierare.                                                                                                                          |
| friendlyName         | sträng                           | Valfritt. Det egna namnet för det objekt som definierats av partnern för att undvika tvetydighet.                                                                 |
| quantity             | int                              | Antalet licenser eller instanser.                                                                                                                  |
| currencyCode         | sträng                           | Valutakoden.                                                                                                                                    |
| billingCycle         | Objekt                           | Den typ av faktureringsperiod som angetts för den aktuella perioden.                                                                                                 |
| deltagare         | Lista över objektsträngpar      | En samling PartnerId on Record (MPN ID) för köpet.                                                                                          |
| provisioningContext  | Ordlista<sträng, sträng>       | En kontext som används för etablering av erbjudande.                                                                                                             |
| orderGroup           | sträng                           | En grupp som anger vilka objekt som kan placeras tillsammans.                                                                                               |
| addonItems           | Lista över **CartLineItem-objekt** | En samling kundvagnsradsobjekt för tillägg som ska köpas mot basprenumerationen som är resultatet av den överordnade kundvagnsradens köp. |
| fel                | Objekt                           | Tillämpas efter att kundvagnen har skapats om det finns ett fel.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>Exempel på begäran (ny basprenumeration)

I följande REST-exempel visas hur du skapar en kundvagn med tillägg för en ny basprenumeration.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a>Exempel på begäran (befintlig basprenumeration)

I följande REST-exempel visas hur du lägger till tillägg till en befintlig basprenumeration.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den [ifyllda kundvagnsresursen](cart-resources.md) i svarstexten.

#### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

#### <a name="response-example-new-base-subscription"></a>Svarsexempel (ny basprenumeration)

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a>Svarsexempel (befintlig basprenumeration)

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
