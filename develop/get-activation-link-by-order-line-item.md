---
title: Hämta aktiveringslänk efter orderradsobjekt
description: Hämtar en prenumerationsaktiveringslänk efter orderradobjekt.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 61cb6659961cfeb22d3b0fe7ad5dd8533d5f72dda76fe96e64b4c64f39ece397
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994157"
---
# <a name="get-activation-link-by-order-line-item"></a>Hämta aktiveringslänk efter orderradsobjekt

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Hämtar en aktiveringslänk för en kommersiell marknadsplatsprenumeration via orderradsartikelnumret.

På instrumentpanelen i Partnercenter kan du göra detta  genom att välja antingen en specifik prenumeration **under** Prenumeration på huvudsidan eller genom att välja länken Gå till **Publisher:s** webbplats bredvid prenumerationen som ska aktiveras på **sidan Prenumerationer.**

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Slutförd order med produkt som behöver aktivering.

## <a name="c"></a>C\#

Om du vill hämta ett radobjekts aktiveringslänk använder du [**samlingen IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropar [**metoden ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det valda kund-ID:t. Anropa sedan egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) och [**metoden ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) med din angivna  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id). Anropa sedan metoden [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** med radobjektets nummeridentifierare.  Anropa slutligen **metoden ActivationLinks().**

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling [kundresurser](customer-resources.md#customer) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
