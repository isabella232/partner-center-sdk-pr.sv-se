---
title: Avbryta en prenumeration på kommersiell marknadsplats
description: 'Lär dig hur du använder API: er för partner Center för att avbryta en prenumeration på en kommersiell marknads plats som matchar ett kund-och prenumerations-ID'
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38708c17b31e39a5e7c436e0d76b4ebabbc3a801
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770077"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="468c7-103">Avbryta en prenumeration på kommersiell marknads plats med hjälp av API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="468c7-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="468c7-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="468c7-104">**Applies to:**</span></span>

- <span data-ttu-id="468c7-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="468c7-105">Partner Center</span></span>

<span data-ttu-id="468c7-106">Den här artikeln beskriver hur du kan använda Partner Center API för att avbryta en [prenumerations](subscription-resources.md) resurs för en kommersiell marknads plats som matchar kund-och prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="468c7-106">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="468c7-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="468c7-107">Prerequisites</span></span>

- <span data-ttu-id="468c7-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="468c7-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="468c7-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="468c7-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="468c7-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="468c7-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="468c7-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="468c7-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="468c7-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="468c7-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="468c7-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="468c7-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="468c7-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="468c7-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="468c7-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="468c7-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="468c7-116">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="468c7-116">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="468c7-117">Instrument panels metod för partner Center</span><span class="sxs-lookup"><span data-stu-id="468c7-117">Partner Center dashboard method</span></span>

<span data-ttu-id="468c7-118">Så här avbryter du en prenumeration på en kommersiell marknads plats på Partner Center-instrument panelen:</span><span class="sxs-lookup"><span data-stu-id="468c7-118">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="468c7-119">[Välj en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="468c7-119">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="468c7-120">Välj den prenumeration som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="468c7-120">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="468c7-121">Välj alternativet för att **avbryta prenumerationen** och välj sedan **Skicka**.</span><span class="sxs-lookup"><span data-stu-id="468c7-121">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="468c7-122">C\#</span><span class="sxs-lookup"><span data-stu-id="468c7-122">C\#</span></span>

<span data-ttu-id="468c7-123">Så här avbryter du en kunds prenumeration:</span><span class="sxs-lookup"><span data-stu-id="468c7-123">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="468c7-124">[Hämta prenumerationen efter ID](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="468c7-124">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="468c7-125">Ändra prenumerationens [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) egenskap.</span><span class="sxs-lookup"><span data-stu-id="468c7-125">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="468c7-126">Information om **status** koder finns i [SubscriptionStatus-uppräkning](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="468c7-126">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="468c7-127">När ändringen har gjorts använder du din **`IAggregatePartner.Customers`** samling och anropar metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="468c7-127">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="468c7-128">Anropa egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="468c7-128">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="468c7-129">Anropa **patch ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="468c7-129">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="468c7-130">Exempel program för konsol test</span><span class="sxs-lookup"><span data-stu-id="468c7-130">Sample console test app</span></span>

<span data-ttu-id="468c7-131">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="468c7-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="468c7-132">**Projekt**: PartnerSDK. FeatureSample- **klass**: UpdateSubscription.CS</span><span class="sxs-lookup"><span data-stu-id="468c7-132">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="468c7-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="468c7-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="468c7-134">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="468c7-134">Request syntax</span></span>

| <span data-ttu-id="468c7-135">Metod</span><span class="sxs-lookup"><span data-stu-id="468c7-135">Method</span></span>    | <span data-ttu-id="468c7-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="468c7-136">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="468c7-137">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="468c7-137">**PATCH**</span></span> | <span data-ttu-id="468c7-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="468c7-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="468c7-139">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="468c7-139">URI parameter</span></span>

<span data-ttu-id="468c7-140">Den här tabellen visar den obligatoriska Frågeparametern för att pausa prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="468c7-140">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="468c7-141">Namn</span><span class="sxs-lookup"><span data-stu-id="468c7-141">Name</span></span>                    | <span data-ttu-id="468c7-142">Typ</span><span class="sxs-lookup"><span data-stu-id="468c7-142">Type</span></span>     | <span data-ttu-id="468c7-143">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="468c7-143">Required</span></span> | <span data-ttu-id="468c7-144">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="468c7-144">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="468c7-145">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="468c7-145">**customer-tenant-id**</span></span>  | <span data-ttu-id="468c7-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="468c7-146">**guid**</span></span> | <span data-ttu-id="468c7-147">Y</span><span class="sxs-lookup"><span data-stu-id="468c7-147">Y</span></span>        | <span data-ttu-id="468c7-148">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="468c7-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="468c7-149">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="468c7-149">**id-for-subscription**</span></span> | <span data-ttu-id="468c7-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="468c7-150">**guid**</span></span> | <span data-ttu-id="468c7-151">Y</span><span class="sxs-lookup"><span data-stu-id="468c7-151">Y</span></span>        | <span data-ttu-id="468c7-152">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="468c7-152">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="468c7-153">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="468c7-153">Request headers</span></span>

<span data-ttu-id="468c7-154">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="468c7-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="468c7-155">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="468c7-155">Request body</span></span>

<span data-ttu-id="468c7-156">En fullständig **prenumerations** resurs krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="468c7-156">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="468c7-157">Se till att **status** egenskapen har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="468c7-157">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="468c7-158">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="468c7-158">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="468c7-159">REST-svar</span><span class="sxs-lookup"><span data-stu-id="468c7-159">REST response</span></span>

<span data-ttu-id="468c7-160">Om det lyckas returnerar den här metoden borttagna [prenumerations](subscription-resources.md) resurs egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="468c7-160">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="468c7-161">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="468c7-161">Response success and error codes</span></span>

<span data-ttu-id="468c7-162">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="468c7-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="468c7-163">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="468c7-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="468c7-164">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="468c7-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="468c7-165">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="468c7-165">Response example</span></span>

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
