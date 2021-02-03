---
title: Hämta aktiveringslänk efter orderradsobjekt
description: Hämtar en prenumerations aktiverings länk per order rads objekt.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c0e84888870571cf6bd21306f527863f2aa7ee85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769267"
---
# <a name="get-activation-link-by-order-line-item"></a>Hämta aktiveringslänk efter orderradsobjekt

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hämtar en prenumerations aktiverings länk för en kommersiell marknads plats med order rads objekt numret.

På instrument panelen för partner Center kan du utföra den här åtgärden genom att välja antingen en **prenumeration** under **prenumerationen** på huvud sidan eller välja länken **gå till utgivarens webbplats** bredvid prenumerationen som ska aktive ras på **prenumerations** sidan.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Slutfört order med produkt som behöver aktive ras.

## <a name="c"></a>C\#

Om du vill hämta en rad objekts aktiverings länk använder du din [**IAggregatePartner.**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling och anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det valda kund-ID: t. Anropa sedan egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) och metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) med angivet  [**Ordernr**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id). Anropa sedan metoden [**rad objekt**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) med **ById ()** med rad objekt nummer identifieraren.  Anropa slutligen metoden **ActivationLinks ()** .

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Orders/{orderId}/lineitems/{lineItemNumber}/activationlinks http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas returnerar den här metoden en samling [kund](customer-resources.md#customer) resurser i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

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
