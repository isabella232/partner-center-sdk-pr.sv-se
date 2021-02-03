---
title: Uppdatera automatisk förnyelse för en prenumeration på kommersiell marknadsplats
description: Uppdatera egenskapen autoförnyelse för en prenumerations resurs som matchar kund-och prenumerations-ID.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dccec57901ea4ea429b74044e3b6c28178c43f6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769585"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="20392-103">Uppdatera automatisk förnyelse för en prenumeration på kommersiell marknadsplats</span><span class="sxs-lookup"><span data-stu-id="20392-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="20392-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="20392-104">**Applies To**</span></span>

- <span data-ttu-id="20392-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="20392-105">Partner Center</span></span>

<span data-ttu-id="20392-106">Uppdatera egenskapen autoförnyelse för en [prenumerations](subscription-resources.md) resurs för en extern marknads plats som matchar kund-och prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="20392-106">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="20392-107">På Partner Center-instrumentpanelen utförs den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="20392-107">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="20392-108">Välj sedan den prenumeration som du vill uppdatera.</span><span class="sxs-lookup"><span data-stu-id="20392-108">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="20392-109">Aktivera slutligen alternativet för **Automatisk förnyelse** och välj sedan **Skicka**.</span><span class="sxs-lookup"><span data-stu-id="20392-109">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20392-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="20392-110">Prerequisites</span></span>

- <span data-ttu-id="20392-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="20392-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="20392-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="20392-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="20392-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="20392-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="20392-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="20392-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="20392-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="20392-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="20392-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="20392-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="20392-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="20392-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="20392-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="20392-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="20392-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="20392-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="20392-120">C\#</span><span class="sxs-lookup"><span data-stu-id="20392-120">C\#</span></span>

<span data-ttu-id="20392-121">Om du vill uppdatera en kunds prenumeration [hämtar du först prenumerationen](get-a-subscription-by-id.md)och anger sedan prenumerationens [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) -egenskap.</span><span class="sxs-lookup"><span data-stu-id="20392-121">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="20392-122">När ändringen har gjorts använder du din **IAggregatePartner. Customers** -samling och anropar metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="20392-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="20392-123">Anropa sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="20392-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="20392-124">Sedan avslutar du genom att anropa **patch-metoden ()** .</span><span class="sxs-lookup"><span data-stu-id="20392-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="20392-125">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="20392-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="20392-126">**Projekt**: PartnerSDK. FeatureSample- **klass**: UpdateSubscription.CS</span><span class="sxs-lookup"><span data-stu-id="20392-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="20392-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="20392-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="20392-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="20392-128">Request syntax</span></span>

| <span data-ttu-id="20392-129">Metod</span><span class="sxs-lookup"><span data-stu-id="20392-129">Method</span></span>    | <span data-ttu-id="20392-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="20392-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="20392-131">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="20392-131">**PATCH**</span></span> | <span data-ttu-id="20392-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="20392-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="20392-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="20392-133">URI parameter</span></span>

<span data-ttu-id="20392-134">Den här tabellen visar den obligatoriska Frågeparametern för att pausa prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="20392-134">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="20392-135">Namn</span><span class="sxs-lookup"><span data-stu-id="20392-135">Name</span></span>                    | <span data-ttu-id="20392-136">Typ</span><span class="sxs-lookup"><span data-stu-id="20392-136">Type</span></span>     | <span data-ttu-id="20392-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="20392-137">Required</span></span> | <span data-ttu-id="20392-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="20392-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="20392-139">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="20392-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="20392-140">**LED**</span><span class="sxs-lookup"><span data-stu-id="20392-140">**GUID**</span></span> | <span data-ttu-id="20392-141">Y</span><span class="sxs-lookup"><span data-stu-id="20392-141">Y</span></span>        | <span data-ttu-id="20392-142">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="20392-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="20392-143">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="20392-143">**id-for-subscription**</span></span> | <span data-ttu-id="20392-144">**LED**</span><span class="sxs-lookup"><span data-stu-id="20392-144">**GUID**</span></span> | <span data-ttu-id="20392-145">Y</span><span class="sxs-lookup"><span data-stu-id="20392-145">Y</span></span>        | <span data-ttu-id="20392-146">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="20392-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="20392-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="20392-147">Request headers</span></span>

<span data-ttu-id="20392-148">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="20392-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="20392-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="20392-149">Request body</span></span>

<span data-ttu-id="20392-150">En fullständig **prenumerations** resurs för en kommersiell marknads plats krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="20392-150">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="20392-151">Se till att egenskapen **AutoRenewEnabled** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="20392-151">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="20392-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="20392-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="20392-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="20392-153">REST response</span></span>

<span data-ttu-id="20392-154">Om det lyckas returnerar den här metoden uppdaterade [prenumerations](subscription-resources.md) resurs egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="20392-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="20392-155">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="20392-155">Response success and error codes</span></span>

<span data-ttu-id="20392-156">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="20392-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="20392-157">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="20392-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="20392-158">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="20392-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="20392-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="20392-159">Response example</span></span>

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
