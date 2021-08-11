---
title: Köp ett tillägg till en prenumeration
description: Så här köper du ett tillägg till en befintlig prenumeration.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5227b917faf663c129b1abed1d10318620667e9b47524eb8c91867fb6b453ee8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997370"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Köp ett tillägg till en prenumeration

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government

Så här köper du ett tillägg till en befintlig prenumeration.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett prenumerations-ID. Det här är den befintliga prenumeration som du kan köpa ett tilläggserbjudande för.

- Ett erbjudande-ID som identifierar tilläggserbjudandet att köpa.

## <a name="purchasing-an-add-on-through-code"></a>Köpa ett tillägg via kod

När du köper ett tillägg till en prenumeration uppdaterar du den ursprungliga prenumerationsordern med beställningen för tillägget. I följande är customerId kund-ID, subscriptionId är prenumerations-ID och addOnOfferId är erbjudandets ID för tillägget.

Här är stegen:

1.  Hämta ett gränssnitt för åtgärderna för prenumerationen.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Använd gränssnittet för att instansiera ett prenumerationsobjekt. Då får du information om den överordnade prenumerationen, inklusive order-ID:t.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Instansiera ett nytt [**Order-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) Den här orderinstansen används för att uppdatera den ursprungliga ordern som användes för att köpa prenumerationen. Lägg till ett objekt på en rad i den ordning som representerar tillägget.
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  Uppdatera den ursprungliga beställningen för prenumerationen med den nya beställningen för tillägget.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Om du vill köpa ett tillägg börjar du med att hämta ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och [**metoden Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera prenumerationen som har tilläggserbjudandet. Använd det [**gränssnittet för**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) att hämta prenumerationsinformationen genom att anropa [**Hämta**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Prenumerationsinformationen innehåller order-ID:t för prenumerationsordern, vilket är ordern som ska uppdateras med tillägget.

Skapa sedan en instans av ett nytt [**orderobjekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) och fyll i det med en enda [**LineItem-instans**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) som innehåller informationen för att identifiera tillägget, enligt följande kodfragment. Du använder det här nya objektet för att uppdatera prenumerationsordningen med tillägget . Anropa slutligen [**Patch-metoden**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) för att uppdatera prenumerationsordern, efter att först ha identifierat kunden med [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) och ordern [**med Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK Samples **Class**: AddSubscriptionAddOn.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod    | URI för förfrågan                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande parametrar för att identifiera kunden och ordern.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **kund-klient-id** | **guid** | Y        | Värdet är ett GUID-formaterat **kundklient-id** som identifierar kunden. |
| **order-id**           | **guid** | Y        | Orderidentifieraren.                                                              |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I följande tabeller beskrivs egenskaperna i begärandetexten.

## <a name="order"></a>Beställning

| Namn                | Typ             | Obligatorisk | Beskrivning                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | sträng           | N        | Order-ID:t.                                        |
| ReferenceCustomerId | sträng           | Y        | Kund-ID:t.                                     |
| LineItems           | matris med objekt | Y        | En matris med [OrderLineItem-objekt.](#orderlineitem) |
| CreationDate        | sträng           | N        | Det datum då ordern skapades i datum/tid-format. |
| Attribut          | objekt           | N        | Innehåller "ObjectType": "Order".                      |

## <a name="orderlineitem"></a>OrderLineItem

| Namn                 | Typ   | Obligatorisk | Beskrivning                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | antal | Y        | Radobjektets nummer, som börjar med 0.                       |
| OfferId              | sträng | Y        | Erbjudandets ID för tillägget.                                  |
| SubscriptionId       | sträng | N        | ID för den köpta tilläggsprenumerationen.                 |
| ParentSubscriptionId | sträng | Y        | ID:t för den överordnade prenumerationen som har tilläggserbjudandet. |
| FriendlyName         | sträng | N        | Det egna namnet för det här radobjektet.                        |
| Kvantitet             | antal | Y        | Antalet licenser.                                      |
| PartnerIdOnRecord    | sträng | N        | MPN-ID för partnern i posten.                         |
| Attribut           | objekt | N        | Innehåller "ObjectType": "OrderLineItem".                      |

### <a name="request-example"></a>Exempel på begäran

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den uppdaterade prenumerationsordningen i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
