---
title: Köp ett tillägg till en prenumeration
description: Så här köper du ett tillägg till en befintlig prenumeration.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769657"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Köp ett tillägg till en prenumeration

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här köper du ett tillägg till en befintlig prenumeration.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID. Det här är den befintliga prenumerationen för vilken du kan köpa ett tilläggs erbjudande.

- Ett erbjudande-ID som identifierar tilläggs erbjudandet för köp.

## <a name="purchasing-an-add-on-through-code"></a>Köpa ett tillägg via kod

När du köper ett tillägg till en prenumeration uppdaterar du den ursprungliga prenumerations ordningen med ordern för tillägget. I följande är customerId kund-ID: t, subscriptionId är prenumerations-ID och addOnOfferId är erbjudande-ID för tillägget.

Här är stegen:

1.  Hämta ett gränssnitt till prenumerationens åtgärder.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Använd det gränssnittet för att instansiera ett prenumerations objekt. Detta hämtar information om överordnad prenumeration, inklusive order-ID.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Instansiera ett nytt [**order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objekt. Den här order instansen används för att uppdatera den ursprungliga order som används för att köpa prenumerationen. Lägg till ett enskilt rad objekt i den ordning som representerar tillägget.
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

4.  Uppdatera den ursprungliga ordningen för prenumerationen med den nya ordern för tillägget.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Om du vill köpa ett tillägg börjar du med att hämta ett gränssnitt till prenumerations åtgärderna genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera den prenumeration som har tilläggs erbjudandet. Använd det [**gränssnittet**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) för att hämta prenumerations informationen genom att anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Varför behöver du prenumerations informationen? Eftersom du behöver order-ID: t för prenumerations ordern. Det är den ordning som ska uppdateras med tillägget.

Sedan instansierar du ett nytt [**order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) -objekt och fyller det med en enda [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -instans som innehåller informationen för att identifiera tillägget, som du ser i följande kodfragment. Du använder det här nya objektet för att uppdatera prenumerations ordningen med tillägget. Slutligen kan du anropa [**korrigerings**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) metoden för att uppdatera prenumerations ordningen, efter att först ha identifierat kunden med [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) och ordern med [**Orders. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: AddSubscriptionAddOn.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **9.0a** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{order-ID} http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande parametrar för att identifiera kunden och ordern.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Värdet är ett GUID-formaterat **kund-Tenant-ID** som identifierar kunden. |
| **order-ID**           | **guid** | Y        | Order-ID.                                                              |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I följande tabeller beskrivs egenskaperna i begär ande texten.

## <a name="order"></a>Beställning

| Namn                | Typ             | Obligatorisk | Beskrivning                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | sträng           | N        | Order-ID.                                        |
| ReferenceCustomerId | sträng           | Y        | Kund-ID.                                     |
| Rad objekt           | objekt mat ris | Y        | En matris med [OrderLineItem](#orderlineitem) -objekt. |
| CreationDate        | sträng           | N        | Datumet då ordern skapades i datum-/tids format. |
| Attribut          | objekt           | N        | Innehåller "ObjectType": "order".                      |

## <a name="orderlineitem"></a>OrderLineItem

| Namn                 | Typ   | Obligatorisk | Beskrivning                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | antal | Y        | Rad objekts numret, från och med 0.                       |
| OfferId              | sträng | Y        | Erbjudande-ID för tillägget.                                  |
| SubscriptionId       | sträng | N        | ID: t för den tilläggs prenumeration som har köpts.                 |
| ParentSubscriptionId | sträng | Y        | ID för den överordnade prenumeration som har tilläggs erbjudandet. |
| FriendlyName         | sträng | N        | Det egna namnet för det här rad objektet.                        |
| Antal             | antal | Y        | Antalet licenser.                                      |
| PartnerIdOnRecord    | sträng | N        | MPN-ID: t för post partnern.                         |
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

Om det lyckas returnerar den här metoden den uppdaterade prenumerations ordningen i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

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
