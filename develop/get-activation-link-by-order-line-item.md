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
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="1fd13-103">Hämta aktiveringslänk efter orderradsobjekt</span><span class="sxs-lookup"><span data-stu-id="1fd13-103">Get activation link by order line item</span></span>

<span data-ttu-id="1fd13-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="1fd13-104">**Applies To**</span></span>

- <span data-ttu-id="1fd13-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="1fd13-105">Partner Center</span></span>
- <span data-ttu-id="1fd13-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="1fd13-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="1fd13-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="1fd13-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="1fd13-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1fd13-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1fd13-109">Hämtar en prenumerations aktiverings länk för en kommersiell marknads plats med order rads objekt numret.</span><span class="sxs-lookup"><span data-stu-id="1fd13-109">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="1fd13-110">På instrument panelen för partner Center kan du utföra den här åtgärden genom att välja antingen en **prenumeration** under **prenumerationen** på huvud sidan eller välja länken **gå till utgivarens webbplats** bredvid prenumerationen som ska aktive ras på **prenumerations** sidan.</span><span class="sxs-lookup"><span data-stu-id="1fd13-110">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fd13-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1fd13-111">Prerequisites</span></span>

- <span data-ttu-id="1fd13-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1fd13-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1fd13-113">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1fd13-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1fd13-114">Slutfört order med produkt som behöver aktive ras.</span><span class="sxs-lookup"><span data-stu-id="1fd13-114">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="1fd13-115">C\#</span><span class="sxs-lookup"><span data-stu-id="1fd13-115">C\#</span></span>

<span data-ttu-id="1fd13-116">Om du vill hämta en rad objekts aktiverings länk använder du din [**IAggregatePartner.**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling och anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det valda kund-ID: t.</span><span class="sxs-lookup"><span data-stu-id="1fd13-116">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="1fd13-117">Anropa sedan egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) och metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) med angivet  [**Ordernr**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span><span class="sxs-lookup"><span data-stu-id="1fd13-117">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="1fd13-118">Anropa sedan metoden [**rad objekt**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) med **ById ()** med rad objekt nummer identifieraren.</span><span class="sxs-lookup"><span data-stu-id="1fd13-118">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="1fd13-119">Anropa slutligen metoden **ActivationLinks ()** .</span><span class="sxs-lookup"><span data-stu-id="1fd13-119">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="1fd13-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1fd13-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1fd13-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="1fd13-121">Request syntax</span></span>

| <span data-ttu-id="1fd13-122">Metod</span><span class="sxs-lookup"><span data-stu-id="1fd13-122">Method</span></span>  | <span data-ttu-id="1fd13-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1fd13-123">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1fd13-124">**TA**</span><span class="sxs-lookup"><span data-stu-id="1fd13-124">**GET**</span></span> | <span data-ttu-id="1fd13-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Orders/{orderId}/lineitems/{lineItemNumber}/activationlinks http/1.1</span><span class="sxs-lookup"><span data-stu-id="1fd13-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1fd13-126">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1fd13-126">Request headers</span></span>

<span data-ttu-id="1fd13-127">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1fd13-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1fd13-128">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1fd13-128">Request body</span></span>

<span data-ttu-id="1fd13-129">Inga.</span><span class="sxs-lookup"><span data-stu-id="1fd13-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1fd13-130">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1fd13-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="1fd13-131">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1fd13-131">REST response</span></span>

<span data-ttu-id="1fd13-132">Om det lyckas returnerar den här metoden en samling [kund](customer-resources.md#customer) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="1fd13-132">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1fd13-133">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1fd13-133">Response success and error codes</span></span>

<span data-ttu-id="1fd13-134">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="1fd13-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1fd13-135">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1fd13-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1fd13-136">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1fd13-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1fd13-137">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1fd13-137">Response example</span></span>

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
