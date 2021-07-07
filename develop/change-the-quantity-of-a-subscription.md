---
title: Ändra kvantiteten för en prenumeration
description: Lär dig hur du använder Partner Center-API:er för att ändra antalet licenser för en kundprenumeration. Du kan också göra detta på instrumentpanelen i Partnercenter.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d57ece4dd19ef2852f39130916222c54a9ccc85a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974105"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="95a38-104">Ändra antalet licenser i en kundprenumeration</span><span class="sxs-lookup"><span data-stu-id="95a38-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="95a38-105">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="95a38-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="95a38-106">Uppdaterar en [prenumeration](subscription-resources.md) för att öka eller minska antalet licenser.</span><span class="sxs-lookup"><span data-stu-id="95a38-106">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="95a38-107">På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först [välja en kund.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="95a38-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="95a38-108">Välj sedan den prenumeration som du vill byta namn på.</span><span class="sxs-lookup"><span data-stu-id="95a38-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="95a38-109">Slutför genom att ändra värdet i **fältet Kvantitet** och sedan välja **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="95a38-109">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95a38-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="95a38-110">Prerequisites</span></span>

- <span data-ttu-id="95a38-111">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="95a38-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95a38-112">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="95a38-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="95a38-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95a38-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="95a38-114">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="95a38-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="95a38-115">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="95a38-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="95a38-116">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="95a38-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="95a38-117">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="95a38-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="95a38-118">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95a38-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="95a38-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="95a38-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="95a38-120">C\#</span><span class="sxs-lookup"><span data-stu-id="95a38-120">C\#</span></span>

<span data-ttu-id="95a38-121">Om du vill ändra kvantiteten för en kunds prenumeration hämtar du [först prenumerationen](get-a-subscription-by-id.md)och ändrar sedan prenumerationens [**egenskap Quantity.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity)</span><span class="sxs-lookup"><span data-stu-id="95a38-121">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="95a38-122">När ändringen har gjorts använder du samlingen **IAggregatePartner.Customers** och anropar **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="95a38-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="95a38-123">Anropa sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="95a38-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="95a38-124">Avsluta sedan med att anropa **metoden Patch().**</span><span class="sxs-lookup"><span data-stu-id="95a38-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="95a38-125">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="95a38-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="95a38-126">**Project:** PartnerSDK.FeatureSample-klass: UpdateSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="95a38-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="95a38-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="95a38-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95a38-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="95a38-128">Request syntax</span></span>

| <span data-ttu-id="95a38-129">Metod</span><span class="sxs-lookup"><span data-stu-id="95a38-129">Method</span></span>    | <span data-ttu-id="95a38-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="95a38-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95a38-131">**Patch**</span><span class="sxs-lookup"><span data-stu-id="95a38-131">**PATCH**</span></span> | <span data-ttu-id="95a38-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="95a38-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="95a38-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="95a38-133">URI parameter</span></span>

<span data-ttu-id="95a38-134">I den här tabellen visas den frågeparameter som krävs för att ändra antalet för prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="95a38-134">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="95a38-135">Namn</span><span class="sxs-lookup"><span data-stu-id="95a38-135">Name</span></span>                    | <span data-ttu-id="95a38-136">Typ</span><span class="sxs-lookup"><span data-stu-id="95a38-136">Type</span></span>     | <span data-ttu-id="95a38-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="95a38-137">Required</span></span> | <span data-ttu-id="95a38-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="95a38-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="95a38-139">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="95a38-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="95a38-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="95a38-140">**guid**</span></span> | <span data-ttu-id="95a38-141">Y</span><span class="sxs-lookup"><span data-stu-id="95a38-141">Y</span></span>        | <span data-ttu-id="95a38-142">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="95a38-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="95a38-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="95a38-143">**id-for-subscription**</span></span> | <span data-ttu-id="95a38-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="95a38-144">**guid**</span></span> | <span data-ttu-id="95a38-145">Y</span><span class="sxs-lookup"><span data-stu-id="95a38-145">Y</span></span>        | <span data-ttu-id="95a38-146">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="95a38-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95a38-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="95a38-147">Request headers</span></span>

<span data-ttu-id="95a38-148">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="95a38-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95a38-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="95a38-149">Request body</span></span>

<span data-ttu-id="95a38-150">En fullständig **prenumerationsresurs** krävs i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="95a38-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="95a38-151">Kontrollera att egenskapen **Quantity** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="95a38-151">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="95a38-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="95a38-152">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="95a38-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="95a38-153">REST response</span></span>

<span data-ttu-id="95a38-154">Om det lyckas returnerar den här metoden **en HTTP-statuskod 200** och uppdaterade [prenumerationsresursegenskaper](subscription-resources.md)  i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="95a38-154">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95a38-155">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="95a38-155">Response success and error codes</span></span>

<span data-ttu-id="95a38-156">Varje svar returnerar en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="95a38-156">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95a38-157">Använd ett nätverksspårningsverktyg för att läsa statuskod, feltyp och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="95a38-157">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="95a38-158">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="95a38-158">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="95a38-159">När korrigeringsåtgärden tar längre tid än förväntat skickar Partnercenter statuskoden **HTTP-status 202** och ett platshuvud som pekar på var prenumerationen ska hämtas.</span><span class="sxs-lookup"><span data-stu-id="95a38-159">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="95a38-160">Du kan köra frågor mot prenumerationen regelbundet för att övervaka status- och kvantitetsändringar.</span><span class="sxs-lookup"><span data-stu-id="95a38-160">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="95a38-161">Svarsexempel</span><span class="sxs-lookup"><span data-stu-id="95a38-161">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="95a38-162">Svarsexempel 1</span><span class="sxs-lookup"><span data-stu-id="95a38-162">Response example 1</span></span>

<span data-ttu-id="95a38-163">Lyckad begäran med **statuskoden HTTP-status 200:**</span><span class="sxs-lookup"><span data-stu-id="95a38-163">Successful request with an **HTTP status 200** status code:</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

#### <a name="response-example-2"></a><span data-ttu-id="95a38-164">Svarsexempel 2</span><span class="sxs-lookup"><span data-stu-id="95a38-164">Response example 2</span></span>

<span data-ttu-id="95a38-165">Lyckad begäran med **statuskoden HTTP-status 202:**</span><span class="sxs-lookup"><span data-stu-id="95a38-165">Successful request with an **HTTP status 202** status code:</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
