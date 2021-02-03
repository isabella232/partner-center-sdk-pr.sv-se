---
title: Skapa en kundvagn med tillägg
description: 'Lär dig hur du använder API: er för partner Center för att lägga till en kund order med tillägg via en kundvagn. Artikeln delar krav och steg för att skapa en kundvagn med tilläggsprogram.'
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770131"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Skapa en kundvagn med tillägg till en kund order

**Gäller för:**

- Partnercenter

Du kan köpa tillägg via en kundvagn. Mer information om vad som för närvarande är tillgängligt för försäljning finns [i partner erbjudanden i Cloud Solution Provider-programmet](/partner-center/csp-offers).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

En varukorg gör det möjligt att köpa ett bas erbjudande och dess motsvarande tillägg. Följ de här stegen för att skapa en kundvagn:

1. Instansiera ett [**vagn**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) objekt.

2. Skapa en lista med [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) -objekt som representerar bas erbjudandet och tilldela listan till vagnens [**rad objekt**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) -egenskap.

3. Under varje bas erbjudandes rad artikel fyller du i listan över **AddOnItems** med andra **CartLineItem** -objekt som var och en representerar ett tillägg som ska köpas mot bas erbjudandet.

4. Få ett gränssnitt till shopping operationer genom att använda [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) för att anropa metoden [**ICustomerCollection. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och sedan hämta gränssnittet från egenskapen **kundvagn** .

5. Anropa slutligen metoden [**create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) för att skapa vagnen.

### <a name="c-example"></a>C- \# exempel

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

Följ de här stegen för att skapa en varukorg som gör det möjligt att köpa tillägg mot befintliga bas prenumerationer:

1. Skapa en **varukorg** med en ny **CartLineItem** som innehåller prenumerations-ID: t i egenskapen **ProvisioningContext** med nyckeln "ParentSubscriptionId".

2. Anropa metoden **create** eller **CreateAsync** .

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

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1                        |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parameter för att identifiera kunden.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-ID** | sträng   | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs egenskaperna för [kundvagn](cart-resources.md) i begär ande texten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sträng           | No              | Ett kundvagn-ID som anges när vagnen skapas.                                  |
| creationTimeStamp     | DateTime         | No              | Datumet då vagnen skapades i datum-/tids format. Används när vagnen har skapats.         |
| lastModifiedTimeStamp | DateTime         | No              | Datumet då vagnen senast uppdaterades i datum-/tids format. Används när vagnen har skapats.    |
| expirationTimeStamp   | DateTime         | No              | Datumet då vagnen upphör att gälla, i datum-/tids format.  Används när vagnen har skapats.            |
| lastModifiedUser      | sträng           | No              | Den användare som senast uppdaterade vagnen. Används när vagnen har skapats.                             |
| Rad objekt             | Objekt mat ris | Yes             | En matris med [CartLineItem](cart-resources.md#cartlineitem) -resurser.                                             |

I den här tabellen beskrivs egenskaperna för [CartLineItem](cart-resources.md#cartlineitem) i begär ande texten.

| Egenskap             | Typ                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sträng                           | En unik identifierare för ett vagn rads objekt. Används när vagnen har skapats.                                                                   |
| catalogId            | sträng                           | Katalog objekt identifierare.                                                                                                                          |
| friendlyName         | sträng                           | Valfritt. Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.                                                                 |
| quantity             | int                              | Antalet licenser eller instanser.                                                                                                                  |
| currencyCode         | sträng                           | Valuta koden.                                                                                                                                    |
| billingCycle         | Objekt                           | Typ av fakturerings cykel som angetts för den aktuella perioden.                                                                                                 |
| deltagare         | Lista med objekt sträng par      | En samling partner on Record (MPNID) på köpet.                                                                                          |
| provisioningContext  | Ord listans<sträng, sträng>       | En kontext som används för etablering av erbjudande.                                                                                                             |
| orderGroup           | sträng                           | En grupp som visar vilka objekt som kan placeras tillsammans.                                                                                               |
| addonItems           | Lista över **CartLineItem** -objekt | En samling av vagn rads objekt för tillägg som kommer att köpas mot bas prenumerationen som är resultatet av den överordnade vagnens rad objekts inköp. |
| fel                | Objekt                           | Tillämpas efter att kundvagn har skapats i händelse av ett fel.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>Exempel på begäran (ny bas prenumeration)

I följande REST-exempel visas hur du skapar en kundvagn med tilläggs objekt för en ny bas prenumeration.

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

#### <a name="request-example-existing-base-subscription"></a>Exempel på begäran (befintlig bas prenumeration)

I följande REST-exempel visas hur du lägger till tillägg i en befintlig bas prenumeration.

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

Om det lyckas returnerar den här metoden den fyllda kund [vagns](cart-resources.md) resursen i svars texten.

#### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

#### <a name="response-example-new-base-subscription"></a>Svars exempel (ny bas prenumeration)

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

#### <a name="response-example-existing-base-subscription"></a>Svars exempel (befintlig bas prenumeration)

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
