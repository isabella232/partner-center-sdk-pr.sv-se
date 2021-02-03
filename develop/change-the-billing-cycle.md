---
title: Ändra faktureringscykeln
description: 'Lär dig hur du uppdaterar en kund prenumeration på månatlig eller årlig fakturering med hjälp av API: er för partner Center. Du kan också göra detta från instrument panelen för partner Center.'
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770089"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Ändra fakturerings cykel för kund prenumeration

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Uppdaterar en [order](order-resources.md) från månatlig till årlig fakturering eller från årlig till månatlig fakturering.

På instrument panelen för partner Center kan du utföra den här åtgärden genom att gå till en kunds prenumerations informations sida. Då visas ett alternativ som definierar den aktuella fakturerings perioden för prenumerationen med möjlighet att ändra och skicka den.

**Omfattas inte av** den här artikeln:

- Ändra fakturerings perioden för utvärderings versioner
- Ändra fakturerings cyklerna för eventuella icke-årliga period erbjudanden (månatligt, 6 år) & Azure-prenumerationer
- Ändra fakturerings cykler för inaktiva prenumerationer
- Ändra fakturerings cykler för licenserbaserade Microsoft onlinetjänster-baserade prenumerationer

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett order-ID.

## <a name="c"></a>C\#

Om du vill ändra frekvensen för fakturerings perioden uppdaterar du egenskapen [**order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .

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

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **9.0a** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{order-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Den här tabellen visar den obligatoriska Frågeparametern för att ändra antalet för prenumerationen.

| Namn                   | Typ | Obligatorisk | Beskrivning                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **kund-ID för klient organisation** | GUID |    Y     | Ett GUID-formaterat **kund-Tenant-ID** som identifierar kunden |
| **order-ID**           | GUID |    Y     | Order-ID                                                 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I följande tabeller beskrivs egenskaperna i begär ande texten.

### <a name="order"></a>Beställning

| Egenskap           | Typ             | Obligatorisk | Beskrivning                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | sträng           |    N     | En beställnings identifierare som anges när beställningen har skapats |
|ReferenceCustomerId | sträng           |    Y     | Kund-ID                                                    |
| BillingCycle       | sträng           |    Y     | Anger med vilken frekvens partnern faktureras för den här ordern. De värden som stöds är medlems namnen som finns i [BillingCycleType](product-resources.md#billingcycletype). |
| Rad objekt          | objekt mat ris |    Y     | En matris med [OrderLineItem](#orderlineitem) -resurser                      |
| CreationDate       | datetime         |    N     | Datumet då ordern skapades i datum-och tids format                        |
| Attribut         | Objekt           |    N     | Innehåller "ObjectType": "OrderLineItem"                                     |

### <a name="orderlineitem"></a>OrderLineItem

| Egenskap             | Typ   | Obligatorisk | Beskrivning                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | antal |    Y     | Rad objekts numret, från och med 0                                              |
| OfferId              | sträng |    Y     | ID för erbjudandet                                                                |
| SubscriptionId       | sträng |    Y     | ID för prenumerationen                                                         |
| FriendlyName         | sträng |    N     | Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate |
| Antal             | antal |    Y     | Antalet licenser eller instanser                                                |
| PartnerIdOnRecord    | sträng |    N     | MPN-ID för registrerad partner                                                |
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

Om det lyckas returnerar den här metoden den uppdaterade prenumerations ordningen i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

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