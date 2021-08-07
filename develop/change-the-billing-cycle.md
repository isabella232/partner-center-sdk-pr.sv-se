---
title: Ändra faktureringscykeln
description: Lär dig hur du uppdaterar en kundprenumeration till månatlig eller årlig fakturering med hjälp av Partner Center-API:er. Du kan också göra detta från instrumentpanelen i Partnercenter.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: c45d599ace7895c03bc163cddde7cbb057ff60a06c58af39a2baacb3d557e72e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992168"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Ändra faktureringsperioden för en kundprenumeration

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Uppdaterar en [beställning från](order-resources.md) månatlig till årlig fakturering eller från årlig till månatlig fakturering.

Den här åtgärden kan utföras på instrumentpanelen i Partnercenter genom att gå till kundens prenumerationsinformationssida. Där ser du ett alternativ som definierar den aktuella faktureringsperioden för prenumerationen med möjlighet att ändra och skicka den.

**Utanför omfånget** för den här artikeln:

- Ändra faktureringsperioden för utvärderingsversioner
- Ändra faktureringscyklerna för icke-årliga erbjudanden (månadsvis, sex år) & Azure-prenumerationer
- Ändra faktureringscyklerna för inaktiva prenumerationer
- Ändra faktureringscykler för Microsoft onlinetjänster licensbaserade prenumerationer

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Ett order-ID.

## <a name="c"></a>C\#

Om du vill ändra frekvensen för faktureringsperioden uppdaterar du egenskapen [**Order.BillingCycle.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod    | URI för förfrågan                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

I den här tabellen visas den frågeparameter som krävs för att ändra antalet för prenumerationen.

| Namn                   | Typ | Obligatorisk | Beskrivning                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **kund-klient-id** | GUID |    Y     | Ett **GUID-formaterat kundklient-ID** som identifierar kunden |
| **order-id**           | GUID |    Y     | Orderidentifieraren                                                 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I följande tabeller beskrivs egenskaperna i begärandetexten.

### <a name="order"></a>Beställning

| Egenskap           | Typ             | Obligatorisk | Beskrivning                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | sträng           |    N     | En orderidentifierare som anges när ordern har skapats |
|ReferenceCustomerId | sträng           |    Y     | Kundidentifieraren                                                    |
| BillingCycle       | sträng           |    Y     | Anger med vilken frekvens partnern faktureras för den här beställningen. Värden som stöds är de medlemsnamn som finns [i BillingCycleType](product-resources.md#billingcycletype). |
| LineItems          | matris med objekt |    Y     | En matris med [OrderLineItem-resurser](#orderlineitem)                      |
| CreationDate       | datetime         |    N     | Datumet då ordern skapades i datum/tid-format                        |
| Attribut         | Objekt           |    N     | Innehåller "ObjectType": "OrderLineItem"                                     |

### <a name="orderlineitem"></a>OrderLineItem

| Egenskap             | Typ   | Obligatorisk | Beskrivning                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | antal |    Y     | Radobjektets nummer, som börjar med 0                                              |
| OfferId              | sträng |    Y     | ID för erbjudandet                                                                |
| SubscriptionId       | sträng |    Y     | ID för prenumerationen                                                         |
| FriendlyName         | sträng |    N     | Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydighet |
| Kvantitet             | antal |    Y     | Antalet licenser eller instanser                                                |
| PartnerIdOnRecord    | sträng |    N     | MPN-ID:t för postpartnern                                                |
| Attribut           | Objekt |    N     | Innehåller "ObjectType": "OrderLineItem"                                             |

### <a name="request-example"></a>Exempel på begäran

Uppdatera till årlig fakturering

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
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
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

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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
    "billingCycle": "Annual",
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
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
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