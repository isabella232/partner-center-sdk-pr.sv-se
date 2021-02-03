---
title: Hämta en lista över tillägg för en prenumeration
description: Så här hämtar du en samling tillägg som en kund har valt att lägga till i prenumerationen.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4e62ad22cf30c34dedfeb628003c695e33b78758
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769336"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="f8300-103">Hämta en lista över tillägg för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="f8300-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="f8300-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="f8300-104">**Applies to:**</span></span>

- <span data-ttu-id="f8300-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="f8300-105">Partner Center</span></span>
- <span data-ttu-id="f8300-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="f8300-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f8300-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="f8300-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f8300-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f8300-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f8300-109">Den här artikeln beskriver hur du hämtar en samling tillägg som en kund har valt att lägga till i sin **[prenumerations](subscription-resources.md)** resurs.</span><span class="sxs-lookup"><span data-stu-id="f8300-109">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8300-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f8300-110">Prerequisites</span></span>

- <span data-ttu-id="f8300-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f8300-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f8300-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f8300-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f8300-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f8300-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f8300-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="f8300-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f8300-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="f8300-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f8300-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="f8300-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f8300-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="f8300-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f8300-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f8300-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f8300-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="f8300-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="f8300-120">C\#</span><span class="sxs-lookup"><span data-stu-id="f8300-120">C\#</span></span>

<span data-ttu-id="f8300-121">Hämta listan med tillägg för en kunds prenumeration:</span><span class="sxs-lookup"><span data-stu-id="f8300-121">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="f8300-122">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="f8300-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="f8300-123">Anropa egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="f8300-123">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="f8300-124">Anropa egenskapen [**addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) följt av [**Get ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span><span class="sxs-lookup"><span data-stu-id="f8300-124">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="f8300-125">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="f8300-125">For an example, see the following:</span></span>

- <span data-ttu-id="f8300-126">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f8300-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f8300-127">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="f8300-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="f8300-128">Klass: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="f8300-128">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f8300-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f8300-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f8300-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="f8300-130">Request syntax</span></span>

| <span data-ttu-id="f8300-131">Metod</span><span class="sxs-lookup"><span data-stu-id="f8300-131">Method</span></span>  | <span data-ttu-id="f8300-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f8300-132">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f8300-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="f8300-133">**GET**</span></span> | <span data-ttu-id="f8300-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/addons http/1.1</span><span class="sxs-lookup"><span data-stu-id="f8300-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="f8300-135">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="f8300-135">URI parameter</span></span>

<span data-ttu-id="f8300-136">Den här tabellen innehåller de frågeparametrar som krävs för att hämta listan med tilläggs komponenter för prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="f8300-136">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="f8300-137">Namn</span><span class="sxs-lookup"><span data-stu-id="f8300-137">Name</span></span>                    | <span data-ttu-id="f8300-138">Typ</span><span class="sxs-lookup"><span data-stu-id="f8300-138">Type</span></span>     | <span data-ttu-id="f8300-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="f8300-139">Required</span></span> | <span data-ttu-id="f8300-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="f8300-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="f8300-141">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="f8300-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="f8300-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="f8300-142">**guid**</span></span> | <span data-ttu-id="f8300-143">Y</span><span class="sxs-lookup"><span data-stu-id="f8300-143">Y</span></span>        | <span data-ttu-id="f8300-144">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="f8300-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="f8300-145">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="f8300-145">**id-for-subscription**</span></span> | <span data-ttu-id="f8300-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="f8300-146">**guid**</span></span> | <span data-ttu-id="f8300-147">Y</span><span class="sxs-lookup"><span data-stu-id="f8300-147">Y</span></span>        | <span data-ttu-id="f8300-148">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="f8300-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f8300-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f8300-149">Request headers</span></span>

<span data-ttu-id="f8300-150">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f8300-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f8300-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f8300-151">Request body</span></span>

<span data-ttu-id="f8300-152">Inga.</span><span class="sxs-lookup"><span data-stu-id="f8300-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f8300-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f8300-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="f8300-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f8300-154">REST response</span></span>

<span data-ttu-id="f8300-155">Om det lyckas returnerar den här metoden en samling resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="f8300-155">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f8300-156">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f8300-156">Response success and error codes</span></span>

<span data-ttu-id="f8300-157">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="f8300-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f8300-158">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f8300-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f8300-159">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f8300-159">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f8300-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f8300-160">Response example</span></span>

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
