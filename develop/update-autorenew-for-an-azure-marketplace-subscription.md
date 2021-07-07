---
title: Uppdatera automatisk förnyelse för en prenumeration på kommersiell marknadsplats
description: Uppdatera egenskapen autorenew för en prenumerationsresurs som matchar kunden och prenumerations-ID:t.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cc0b4c4bff5e8762ffcc2552b2e9e36bcf93686c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446674"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="214d0-103">Uppdatera automatisk förnyelse för en prenumeration på kommersiell marknadsplats</span><span class="sxs-lookup"><span data-stu-id="214d0-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="214d0-104">Uppdatera egenskapen autorenew för en prenumerationsresurs [på](subscription-resources.md) den kommersiella marknadsplatsen som matchar kund- och prenumerations-ID:t.</span><span class="sxs-lookup"><span data-stu-id="214d0-104">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="214d0-105">I instrumentpanelen i Partnercenter utförs den här åtgärden genom att först [välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="214d0-105">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="214d0-106">Välj sedan den prenumeration som du vill uppdatera.</span><span class="sxs-lookup"><span data-stu-id="214d0-106">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="214d0-107">Växla slutligen alternativet **Förnya automatiskt och** välj sedan **Skicka**.</span><span class="sxs-lookup"><span data-stu-id="214d0-107">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="214d0-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="214d0-108">Prerequisites</span></span>

- <span data-ttu-id="214d0-109">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="214d0-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="214d0-110">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="214d0-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="214d0-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="214d0-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="214d0-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="214d0-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="214d0-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="214d0-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="214d0-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="214d0-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="214d0-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="214d0-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="214d0-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="214d0-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="214d0-117">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="214d0-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="214d0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="214d0-118">C\#</span></span>

<span data-ttu-id="214d0-119">Om du vill uppdatera en kunds prenumeration hämtar du [först](get-a-subscription-by-id.md)prenumerationen och anger sedan prenumerationens [**egenskap autoRenewEnabled.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled)</span><span class="sxs-lookup"><span data-stu-id="214d0-119">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="214d0-120">När ändringen har gjorts använder du samlingen **IAggregatePartner.Customers** och anropar **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="214d0-120">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="214d0-121">Anropa sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="214d0-121">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="214d0-122">Avsluta sedan med att anropa **metoden Patch().**</span><span class="sxs-lookup"><span data-stu-id="214d0-122">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="214d0-123">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="214d0-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="214d0-124">**Project:** PartnerSDK.FeatureSample-klass: UpdateSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="214d0-124">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="214d0-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="214d0-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="214d0-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="214d0-126">Request syntax</span></span>

| <span data-ttu-id="214d0-127">Metod</span><span class="sxs-lookup"><span data-stu-id="214d0-127">Method</span></span>    | <span data-ttu-id="214d0-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="214d0-128">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="214d0-129">**Patch**</span><span class="sxs-lookup"><span data-stu-id="214d0-129">**PATCH**</span></span> | <span data-ttu-id="214d0-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="214d0-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="214d0-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="214d0-131">URI parameter</span></span>

<span data-ttu-id="214d0-132">I den här tabellen visas frågeparametern som krävs för att pausa prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="214d0-132">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="214d0-133">Namn</span><span class="sxs-lookup"><span data-stu-id="214d0-133">Name</span></span>                    | <span data-ttu-id="214d0-134">Typ</span><span class="sxs-lookup"><span data-stu-id="214d0-134">Type</span></span>     | <span data-ttu-id="214d0-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="214d0-135">Required</span></span> | <span data-ttu-id="214d0-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="214d0-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="214d0-137">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="214d0-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="214d0-138">**Guid**</span><span class="sxs-lookup"><span data-stu-id="214d0-138">**GUID**</span></span> | <span data-ttu-id="214d0-139">Y</span><span class="sxs-lookup"><span data-stu-id="214d0-139">Y</span></span>        | <span data-ttu-id="214d0-140">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="214d0-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="214d0-141">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="214d0-141">**id-for-subscription**</span></span> | <span data-ttu-id="214d0-142">**Guid**</span><span class="sxs-lookup"><span data-stu-id="214d0-142">**GUID**</span></span> | <span data-ttu-id="214d0-143">Y</span><span class="sxs-lookup"><span data-stu-id="214d0-143">Y</span></span>        | <span data-ttu-id="214d0-144">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="214d0-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="214d0-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="214d0-145">Request headers</span></span>

<span data-ttu-id="214d0-146">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="214d0-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="214d0-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="214d0-147">Request body</span></span>

<span data-ttu-id="214d0-148">En fullständig prenumerationsresurs **för** den kommersiella marknadsplatsen krävs i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="214d0-148">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="214d0-149">Kontrollera att egenskapen **AutoRenewEnabled** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="214d0-149">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="214d0-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="214d0-150">Request example</span></span>

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
    "status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="214d0-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="214d0-151">REST response</span></span>

<span data-ttu-id="214d0-152">Om det lyckas returnerar den här metoden [uppdaterade prenumerationsresursegenskaper](subscription-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="214d0-152">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="214d0-153">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="214d0-153">Response success and error codes</span></span>

<span data-ttu-id="214d0-154">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="214d0-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="214d0-155">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="214d0-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="214d0-156">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="214d0-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="214d0-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="214d0-157">Response example</span></span>

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
    "status": "active",
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
