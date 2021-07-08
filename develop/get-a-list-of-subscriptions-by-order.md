---
title: Hämta en lista över prenumerationer efter beställning
description: Hämtar en samling prenumerationsresurser som motsvarar en viss ordning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 011a92500d0c7ed44f86030febd1ea83be2c6474
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873964"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="13812-103">Hämta en lista över prenumerationer efter beställning</span><span class="sxs-lookup"><span data-stu-id="13812-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="13812-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="13812-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="13812-105">Hämtar en samling [prenumerationsresurser](subscription-resources.md) som motsvarar en viss ordning.</span><span class="sxs-lookup"><span data-stu-id="13812-105">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13812-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="13812-106">Prerequisites</span></span>

- <span data-ttu-id="13812-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="13812-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="13812-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="13812-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="13812-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="13812-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="13812-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="13812-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="13812-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="13812-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="13812-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="13812-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="13812-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="13812-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="13812-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="13812-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="13812-115">Ett order-ID.</span><span class="sxs-lookup"><span data-stu-id="13812-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="13812-116">C\#</span><span class="sxs-lookup"><span data-stu-id="13812-116">C\#</span></span>

<span data-ttu-id="13812-117">Om du vill hämta en lista över prenumerationer efter order använder du **samlingen IAggregatePartner.Customers** och **anropar metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="13812-117">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="13812-118">Anropa sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av **metoden ByOrder().**</span><span class="sxs-lookup"><span data-stu-id="13812-118">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="13812-119">Slutför genom att [**anropa Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) eller [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span><span class="sxs-lookup"><span data-stu-id="13812-119">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="13812-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="13812-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="13812-121">**Project:** PartnerSDK.FeatureSample-klass: SubscriptionsByOrder.cs </span><span class="sxs-lookup"><span data-stu-id="13812-121">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="13812-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="13812-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="13812-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="13812-123">Request syntax</span></span>

| <span data-ttu-id="13812-124">Metod</span><span class="sxs-lookup"><span data-stu-id="13812-124">Method</span></span>  | <span data-ttu-id="13812-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="13812-125">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="13812-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="13812-126">**GET**</span></span> | <span data-ttu-id="13812-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order \_ id={id-for-order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="13812-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="13812-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="13812-128">URI parameter</span></span>

<span data-ttu-id="13812-129">Den här tabellen innehåller frågeparametern som krävs för att hämta alla prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="13812-129">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="13812-130">Namn</span><span class="sxs-lookup"><span data-stu-id="13812-130">Name</span></span>                   | <span data-ttu-id="13812-131">Typ</span><span class="sxs-lookup"><span data-stu-id="13812-131">Type</span></span>     | <span data-ttu-id="13812-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="13812-132">Required</span></span> | <span data-ttu-id="13812-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="13812-133">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="13812-134">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="13812-134">**customer-tenant-id**</span></span> | <span data-ttu-id="13812-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="13812-135">**guid**</span></span> | <span data-ttu-id="13812-136">Y</span><span class="sxs-lookup"><span data-stu-id="13812-136">Y</span></span>        | <span data-ttu-id="13812-137">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="13812-137">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="13812-138">**id-for-order**</span><span class="sxs-lookup"><span data-stu-id="13812-138">**id-for-order**</span></span>       | <span data-ttu-id="13812-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="13812-139">**guid**</span></span> | <span data-ttu-id="13812-140">Y</span><span class="sxs-lookup"><span data-stu-id="13812-140">Y</span></span>        | <span data-ttu-id="13812-141">Ett GUID som motsvarar ordern.</span><span class="sxs-lookup"><span data-stu-id="13812-141">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="13812-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="13812-142">Request headers</span></span>

<span data-ttu-id="13812-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="13812-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="13812-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="13812-144">Request body</span></span>

<span data-ttu-id="13812-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="13812-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="13812-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="13812-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="13812-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="13812-147">REST response</span></span>

<span data-ttu-id="13812-148">Om det lyckas returnerar den här metoden en samling [prenumerationsresurser](subscription-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="13812-148">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="13812-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="13812-149">Response success and error codes</span></span>

<span data-ttu-id="13812-150">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="13812-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="13812-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="13812-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="13812-152">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="13812-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="13812-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="13812-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "Myofferpurchase",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "{id-for-order}",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
