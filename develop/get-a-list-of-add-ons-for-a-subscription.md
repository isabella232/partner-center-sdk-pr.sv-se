---
title: Hämta en lista över tillägg för en prenumeration
description: Hur du hämtar en samling tillägg som en kund har valt att lägga till i sin prenumeration.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: c627f595333a295048b02ec4326dcdc279d07b51
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874643"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="debf8-103">Hämta en lista över tillägg för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="debf8-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="debf8-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="debf8-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="debf8-105">Den här artikeln beskriver hur du hämtar en samling tillägg som en kund har valt att lägga till i sin **[prenumerationsresurs.](subscription-resources.md)**</span><span class="sxs-lookup"><span data-stu-id="debf8-105">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="debf8-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="debf8-106">Prerequisites</span></span>

- <span data-ttu-id="debf8-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="debf8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="debf8-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="debf8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="debf8-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="debf8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="debf8-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="debf8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="debf8-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="debf8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="debf8-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="debf8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="debf8-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="debf8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="debf8-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="debf8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="debf8-115">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="debf8-115">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="debf8-116">C\#</span><span class="sxs-lookup"><span data-stu-id="debf8-116">C\#</span></span>

<span data-ttu-id="debf8-117">Så här hämtar du listan över tillägg för en kunds prenumeration:</span><span class="sxs-lookup"><span data-stu-id="debf8-117">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="debf8-118">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="debf8-118">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="debf8-119">Anropa egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="debf8-119">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="debf8-120">Anropa egenskapen [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) följt av [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) eller [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span><span class="sxs-lookup"><span data-stu-id="debf8-120">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="debf8-121">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="debf8-121">For an example, see the following:</span></span>

- <span data-ttu-id="debf8-122">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="debf8-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="debf8-123">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="debf8-123">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="debf8-124">Klass: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="debf8-124">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="debf8-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="debf8-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="debf8-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="debf8-126">Request syntax</span></span>

| <span data-ttu-id="debf8-127">Metod</span><span class="sxs-lookup"><span data-stu-id="debf8-127">Method</span></span>  | <span data-ttu-id="debf8-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="debf8-128">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="debf8-129">**Få**</span><span class="sxs-lookup"><span data-stu-id="debf8-129">**GET**</span></span> | <span data-ttu-id="debf8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="debf8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="debf8-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="debf8-131">URI parameter</span></span>

<span data-ttu-id="debf8-132">I den här tabellen visas de frågeparametrar som krävs för att hämta listan över tillägg för prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="debf8-132">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="debf8-133">Namn</span><span class="sxs-lookup"><span data-stu-id="debf8-133">Name</span></span>                    | <span data-ttu-id="debf8-134">Typ</span><span class="sxs-lookup"><span data-stu-id="debf8-134">Type</span></span>     | <span data-ttu-id="debf8-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="debf8-135">Required</span></span> | <span data-ttu-id="debf8-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="debf8-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="debf8-137">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="debf8-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="debf8-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="debf8-138">**guid**</span></span> | <span data-ttu-id="debf8-139">Y</span><span class="sxs-lookup"><span data-stu-id="debf8-139">Y</span></span>        | <span data-ttu-id="debf8-140">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="debf8-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="debf8-141">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="debf8-141">**id-for-subscription**</span></span> | <span data-ttu-id="debf8-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="debf8-142">**guid**</span></span> | <span data-ttu-id="debf8-143">Y</span><span class="sxs-lookup"><span data-stu-id="debf8-143">Y</span></span>        | <span data-ttu-id="debf8-144">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="debf8-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="debf8-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="debf8-145">Request headers</span></span>

<span data-ttu-id="debf8-146">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="debf8-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="debf8-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="debf8-147">Request body</span></span>

<span data-ttu-id="debf8-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="debf8-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="debf8-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="debf8-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="debf8-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="debf8-150">REST response</span></span>

<span data-ttu-id="debf8-151">Om det lyckas returnerar den här metoden en samling resurser i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="debf8-151">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="debf8-152">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="debf8-152">Response success and error codes</span></span>

<span data-ttu-id="debf8-153">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="debf8-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="debf8-154">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="debf8-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="debf8-155">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="debf8-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="debf8-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="debf8-156">Response example</span></span>

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
        "entitlementId": "42226ed6-070a-4e0f-b80c-4cdfB3e97aa7",
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
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
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
