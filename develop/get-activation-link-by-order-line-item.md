---
title: Hämta aktiveringslänk efter orderradsobjekt
description: Hämtar en prenumerationsaktiveringslänk efter orderradobjekt.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa02a5a5b4a281b96e32ee6d239cc440cf8af4ec
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760784"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="bad8a-103">Hämta aktiveringslänk efter orderradsobjekt</span><span class="sxs-lookup"><span data-stu-id="bad8a-103">Get activation link by order line item</span></span>

<span data-ttu-id="bad8a-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bad8a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bad8a-105">Hämtar en aktiveringslänk för en kommersiell marknadsplatsprenumeration via orderradsartikelnumret.</span><span class="sxs-lookup"><span data-stu-id="bad8a-105">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="bad8a-106">På instrumentpanelen i Partnercenter kan du göra detta  genom att välja antingen en specifik prenumeration **under** Prenumeration på huvudsidan eller genom att välja länken Gå till **Publisher:s** webbplats bredvid prenumerationen som ska aktiveras på **sidan Prenumerationer.**</span><span class="sxs-lookup"><span data-stu-id="bad8a-106">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bad8a-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="bad8a-107">Prerequisites</span></span>

- <span data-ttu-id="bad8a-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bad8a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bad8a-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="bad8a-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="bad8a-110">Slutförd order med produkt som behöver aktivering.</span><span class="sxs-lookup"><span data-stu-id="bad8a-110">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="bad8a-111">C\#</span><span class="sxs-lookup"><span data-stu-id="bad8a-111">C\#</span></span>

<span data-ttu-id="bad8a-112">Om du vill hämta ett radobjekts aktiveringslänk använder du [**samlingen IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropar [**metoden ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det valda kund-ID:t.</span><span class="sxs-lookup"><span data-stu-id="bad8a-112">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="bad8a-113">Anropa sedan egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) och [**metoden ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) med din angivna  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span><span class="sxs-lookup"><span data-stu-id="bad8a-113">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="bad8a-114">Anropa sedan metoden [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** med radobjektets nummeridentifierare.</span><span class="sxs-lookup"><span data-stu-id="bad8a-114">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="bad8a-115">Anropa slutligen **metoden ActivationLinks().**</span><span class="sxs-lookup"><span data-stu-id="bad8a-115">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="bad8a-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="bad8a-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bad8a-117">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="bad8a-117">Request syntax</span></span>

| <span data-ttu-id="bad8a-118">Metod</span><span class="sxs-lookup"><span data-stu-id="bad8a-118">Method</span></span>  | <span data-ttu-id="bad8a-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="bad8a-119">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bad8a-120">**Få**</span><span class="sxs-lookup"><span data-stu-id="bad8a-120">**GET**</span></span> | <span data-ttu-id="bad8a-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bad8a-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bad8a-122">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="bad8a-122">Request headers</span></span>

<span data-ttu-id="bad8a-123">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bad8a-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bad8a-124">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="bad8a-124">Request body</span></span>

<span data-ttu-id="bad8a-125">Inga.</span><span class="sxs-lookup"><span data-stu-id="bad8a-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bad8a-126">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="bad8a-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="bad8a-127">REST-svar</span><span class="sxs-lookup"><span data-stu-id="bad8a-127">REST response</span></span>

<span data-ttu-id="bad8a-128">Om det lyckas returnerar den här metoden en samling [kundresurser](customer-resources.md#customer) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="bad8a-128">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bad8a-129">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="bad8a-129">Response success and error codes</span></span>

<span data-ttu-id="bad8a-130">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="bad8a-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bad8a-131">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="bad8a-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bad8a-132">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="bad8a-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bad8a-133">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="bad8a-133">Response example</span></span>

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
