---
title: Avbryta en prenumeration på kommersiell marknadsplats
description: Lär dig hur du använder Partner Center-API:er för att avbryta en prenumerationsresurs på den kommersiella marknadsplatsen som matchar en kund och ett prenumerations-ID.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 95fa265a3c103d1ec55066f12a3ede7fdb2d0170
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974292"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="db46f-103">Avbryta en prenumeration på den kommersiella marknadsplatsen med partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="db46f-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="db46f-104">I den här artikeln beskrivs hur du kan [](subscription-resources.md) använda Partnercenter-API:et för att avbryta en prenumerationsresurs på den kommersiella marknadsplatsen som matchar kund- och prenumerations-ID:t.</span><span class="sxs-lookup"><span data-stu-id="db46f-104">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db46f-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="db46f-105">Prerequisites</span></span>

- <span data-ttu-id="db46f-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="db46f-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="db46f-107">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="db46f-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="db46f-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db46f-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="db46f-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="db46f-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="db46f-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="db46f-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="db46f-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="db46f-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="db46f-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="db46f-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="db46f-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db46f-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="db46f-114">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="db46f-114">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="db46f-115">Instrumentpanelsmetod i Partnercenter</span><span class="sxs-lookup"><span data-stu-id="db46f-115">Partner Center dashboard method</span></span>

<span data-ttu-id="db46f-116">Så här avbryter du en prenumeration på den kommersiella marknadsplatsen på instrumentpanelen i Partnercenter:</span><span class="sxs-lookup"><span data-stu-id="db46f-116">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="db46f-117">[Välj en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="db46f-117">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="db46f-118">Välj den prenumeration som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="db46f-118">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="db46f-119">Välj alternativet **Avbryt prenumeration** och välj sedan **Skicka**.</span><span class="sxs-lookup"><span data-stu-id="db46f-119">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="db46f-120">C\#</span><span class="sxs-lookup"><span data-stu-id="db46f-120">C\#</span></span>

<span data-ttu-id="db46f-121">Så här avbryter du en kunds prenumeration:</span><span class="sxs-lookup"><span data-stu-id="db46f-121">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="db46f-122">[Hämta prenumerationen efter ID](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="db46f-122">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="db46f-123">Ändra prenumerationens [**statusegenskap.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)</span><span class="sxs-lookup"><span data-stu-id="db46f-123">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="db46f-124">Information om **statuskoder** finns i [SubscriptionStatus-uppräkning.](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="db46f-124">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="db46f-125">När ändringen har gjorts använder du din **`IAggregatePartner.Customers`** samling och anropar **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="db46f-125">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="db46f-126">Anropa egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="db46f-126">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="db46f-127">Anropa **metoden Patch().**</span><span class="sxs-lookup"><span data-stu-id="db46f-127">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="db46f-128">Exempelkonsoltestapp</span><span class="sxs-lookup"><span data-stu-id="db46f-128">Sample console test app</span></span>

<span data-ttu-id="db46f-129">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="db46f-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="db46f-130">**Project:** PartnerSDK.FeatureSample-klass: UpdateSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="db46f-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="db46f-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="db46f-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="db46f-132">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="db46f-132">Request syntax</span></span>

| <span data-ttu-id="db46f-133">Metod</span><span class="sxs-lookup"><span data-stu-id="db46f-133">Method</span></span>    | <span data-ttu-id="db46f-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="db46f-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="db46f-135">**Patch**</span><span class="sxs-lookup"><span data-stu-id="db46f-135">**PATCH**</span></span> | <span data-ttu-id="db46f-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="db46f-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="db46f-137">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="db46f-137">URI parameter</span></span>

<span data-ttu-id="db46f-138">I den här tabellen visas frågeparametern som krävs för att pausa prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="db46f-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="db46f-139">Namn</span><span class="sxs-lookup"><span data-stu-id="db46f-139">Name</span></span>                    | <span data-ttu-id="db46f-140">Typ</span><span class="sxs-lookup"><span data-stu-id="db46f-140">Type</span></span>     | <span data-ttu-id="db46f-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="db46f-141">Required</span></span> | <span data-ttu-id="db46f-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="db46f-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="db46f-143">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="db46f-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="db46f-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="db46f-144">**guid**</span></span> | <span data-ttu-id="db46f-145">Y</span><span class="sxs-lookup"><span data-stu-id="db46f-145">Y</span></span>        | <span data-ttu-id="db46f-146">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="db46f-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="db46f-147">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="db46f-147">**id-for-subscription**</span></span> | <span data-ttu-id="db46f-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="db46f-148">**guid**</span></span> | <span data-ttu-id="db46f-149">Y</span><span class="sxs-lookup"><span data-stu-id="db46f-149">Y</span></span>        | <span data-ttu-id="db46f-150">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="db46f-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="db46f-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="db46f-151">Request headers</span></span>

<span data-ttu-id="db46f-152">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="db46f-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="db46f-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="db46f-153">Request body</span></span>

<span data-ttu-id="db46f-154">En fullständig **prenumerationsresurs** krävs i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="db46f-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="db46f-155">Kontrollera att **egenskapen Status** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="db46f-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="db46f-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="db46f-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [{
        "type": "Full",
        "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
    }],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "publisherName": "publisher Name",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {"objectType": "Subscription"},
}
```

## <a name="rest-response"></a><span data-ttu-id="db46f-157">REST-svar</span><span class="sxs-lookup"><span data-stu-id="db46f-157">REST response</span></span>

<span data-ttu-id="db46f-158">Om det lyckas returnerar den här metoden [borttagna](subscription-resources.md) prenumerationsresursegenskaper i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="db46f-158">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="db46f-159">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="db46f-159">Response success and error codes</span></span>

<span data-ttu-id="db46f-160">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="db46f-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="db46f-161">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="db46f-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="db46f-162">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="db46f-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="db46f-163">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="db46f-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1322
Content-Type: application/json; charset=utf-8
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
X-Locale: en-US

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [
        {
            "type": "Full",
            "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
        }
    ],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "links": {
        "product": {
            "uri": "/products/DZH318Z0BXWC?country=US",
            "method": "GET",
            "headers": []
        },
        "sku": {
            "uri": "/products/DZH318Z0BXWC/skus/0001?country=US",
            "method": "GET",
            "headers": []
        },
        "availability": {
            "uri": "/products/DZH318Z0BXWC/skus/0001/availabilities/DZH318Z0BMJX?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/5921f00a-32c0-4457-aaa1-e8018c650895/subscriptions/6e7aa601-629e-461b-8933-0898c3cc3c7c",
            "method": "GET",
            "headers": []
        }
    },
    "publisherName": "publishe rName",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {
        "etag": "",
        "objectType": "Subscription"
    }
}
```
