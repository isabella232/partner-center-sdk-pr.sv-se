---
title: Hämta en lista över prenumerationer efter beställning
description: Hämtar en samling prenumerations resurser som motsvarar en angiven ordning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 56b9c80021cace03976d410b2a6cd4c0eee18398
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769552"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="70b95-103">Hämta en lista över prenumerationer efter beställning</span><span class="sxs-lookup"><span data-stu-id="70b95-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="70b95-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="70b95-104">**Applies To**</span></span>

- <span data-ttu-id="70b95-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="70b95-105">Partner Center</span></span>
- <span data-ttu-id="70b95-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="70b95-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="70b95-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="70b95-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="70b95-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="70b95-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="70b95-109">Hämtar en samling [prenumerations](subscription-resources.md) resurser som motsvarar en angiven ordning.</span><span class="sxs-lookup"><span data-stu-id="70b95-109">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70b95-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="70b95-110">Prerequisites</span></span>

- <span data-ttu-id="70b95-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="70b95-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="70b95-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="70b95-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="70b95-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="70b95-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="70b95-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="70b95-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="70b95-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="70b95-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="70b95-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="70b95-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="70b95-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="70b95-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="70b95-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="70b95-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="70b95-119">Ett order-ID.</span><span class="sxs-lookup"><span data-stu-id="70b95-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="70b95-120">C\#</span><span class="sxs-lookup"><span data-stu-id="70b95-120">C\#</span></span>

<span data-ttu-id="70b95-121">Om du vill hämta en lista över prenumerationer efter ordning använder du din **IAggregatePartner. Customers** -samling och anropar metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="70b95-121">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="70b95-122">Anropa sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden **ByOrder ()** .</span><span class="sxs-lookup"><span data-stu-id="70b95-122">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="70b95-123">Avsluta genom att anropa [**Get ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span><span class="sxs-lookup"><span data-stu-id="70b95-123">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="70b95-124">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="70b95-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="70b95-125">**Projekt**: PartnerSDK. FeatureSample- **klass**: SubscriptionsByOrder.CS</span><span class="sxs-lookup"><span data-stu-id="70b95-125">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="70b95-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="70b95-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="70b95-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="70b95-127">Request syntax</span></span>

| <span data-ttu-id="70b95-128">Metod</span><span class="sxs-lookup"><span data-stu-id="70b95-128">Method</span></span>  | <span data-ttu-id="70b95-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="70b95-129">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="70b95-130">**TA**</span><span class="sxs-lookup"><span data-stu-id="70b95-130">**GET**</span></span> | <span data-ttu-id="70b95-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions? order \_ -ID = {ID-for-order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="70b95-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="70b95-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="70b95-132">URI parameter</span></span>

<span data-ttu-id="70b95-133">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta alla prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="70b95-133">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="70b95-134">Namn</span><span class="sxs-lookup"><span data-stu-id="70b95-134">Name</span></span>                   | <span data-ttu-id="70b95-135">Typ</span><span class="sxs-lookup"><span data-stu-id="70b95-135">Type</span></span>     | <span data-ttu-id="70b95-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="70b95-136">Required</span></span> | <span data-ttu-id="70b95-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="70b95-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="70b95-138">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="70b95-138">**customer-tenant-id**</span></span> | <span data-ttu-id="70b95-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="70b95-139">**guid**</span></span> | <span data-ttu-id="70b95-140">Y</span><span class="sxs-lookup"><span data-stu-id="70b95-140">Y</span></span>        | <span data-ttu-id="70b95-141">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="70b95-141">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="70b95-142">**ID-för-order**</span><span class="sxs-lookup"><span data-stu-id="70b95-142">**id-for-order**</span></span>       | <span data-ttu-id="70b95-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="70b95-143">**guid**</span></span> | <span data-ttu-id="70b95-144">Y</span><span class="sxs-lookup"><span data-stu-id="70b95-144">Y</span></span>        | <span data-ttu-id="70b95-145">Ett GUID som motsvarar ordern.</span><span class="sxs-lookup"><span data-stu-id="70b95-145">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="70b95-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="70b95-146">Request headers</span></span>

<span data-ttu-id="70b95-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="70b95-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="70b95-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="70b95-148">Request body</span></span>

<span data-ttu-id="70b95-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="70b95-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="70b95-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="70b95-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="70b95-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="70b95-151">REST response</span></span>

<span data-ttu-id="70b95-152">Om det lyckas returnerar den här metoden en samling [prenumerations](subscription-resources.md) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="70b95-152">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="70b95-153">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="70b95-153">Response success and error codes</span></span>

<span data-ttu-id="70b95-154">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="70b95-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="70b95-155">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="70b95-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="70b95-156">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="70b95-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="70b95-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="70b95-157">Response example</span></span>

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
