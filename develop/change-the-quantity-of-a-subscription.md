---
title: Ändra kvantiteten för en prenumeration
description: 'Lär dig hur du använder API: er för partner Center för att ändra antalet licenser för en kund prenumeration. Du kan också göra detta på instrument panelen för partner Center.'
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770071"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="a7b3a-104">Ändra antalet licenser i en kund prenumeration</span><span class="sxs-lookup"><span data-stu-id="a7b3a-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="a7b3a-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="a7b3a-105">**Applies to:**</span></span>

- <span data-ttu-id="a7b3a-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a7b3a-106">Partner Center</span></span>
- <span data-ttu-id="a7b3a-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a7b3a-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a7b3a-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="a7b3a-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a7b3a-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a7b3a-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a7b3a-110">Uppdaterar en [prenumeration](subscription-resources.md) för att öka eller minska antalet licenser.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-110">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="a7b3a-111">På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="a7b3a-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="a7b3a-112">Välj sedan den prenumeration i fråga som du vill byta namn på.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="a7b3a-113">Slutför genom att ändra värdet i fältet **kvantitet** och sedan **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="a7b3a-113">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7b3a-114">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a7b3a-114">Prerequisites</span></span>

- <span data-ttu-id="a7b3a-115">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a7b3a-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a7b3a-116">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a7b3a-117">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a7b3a-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a7b3a-118">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a7b3a-119">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a7b3a-120">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a7b3a-121">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="a7b3a-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a7b3a-122">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a7b3a-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a7b3a-123">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="a7b3a-124">C\#</span><span class="sxs-lookup"><span data-stu-id="a7b3a-124">C\#</span></span>

<span data-ttu-id="a7b3a-125">Om du vill ändra antalet för en kund prenumeration ska du först [Hämta prenumerationen](get-a-subscription-by-id.md)och sedan ändra prenumerationens egenskap för [**kvantitet**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) .</span><span class="sxs-lookup"><span data-stu-id="a7b3a-125">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="a7b3a-126">När ändringen har gjorts använder du din **IAggregatePartner. Customers** -samling och anropar metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="a7b3a-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="a7b3a-127">Anropa sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="a7b3a-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="a7b3a-128">Sedan avslutar du genom att anropa **patch-metoden ()** .</span><span class="sxs-lookup"><span data-stu-id="a7b3a-128">Then, finish by calling the **Patch()** method.</span></span>

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

<span data-ttu-id="a7b3a-129">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a7b3a-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a7b3a-130">**Projekt**: PartnerSDK. FeatureSample- **klass**: UpdateSubscription.CS</span><span class="sxs-lookup"><span data-stu-id="a7b3a-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a7b3a-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a7b3a-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a7b3a-132">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="a7b3a-132">Request syntax</span></span>

| <span data-ttu-id="a7b3a-133">Metod</span><span class="sxs-lookup"><span data-stu-id="a7b3a-133">Method</span></span>    | <span data-ttu-id="a7b3a-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a7b3a-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a7b3a-135">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="a7b3a-135">**PATCH**</span></span> | <span data-ttu-id="a7b3a-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a7b3a-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a7b3a-137">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="a7b3a-137">URI parameter</span></span>

<span data-ttu-id="a7b3a-138">Den här tabellen visar den obligatoriska Frågeparametern för att ändra antalet för prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-138">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="a7b3a-139">Namn</span><span class="sxs-lookup"><span data-stu-id="a7b3a-139">Name</span></span>                    | <span data-ttu-id="a7b3a-140">Typ</span><span class="sxs-lookup"><span data-stu-id="a7b3a-140">Type</span></span>     | <span data-ttu-id="a7b3a-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a7b3a-141">Required</span></span> | <span data-ttu-id="a7b3a-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a7b3a-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="a7b3a-143">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="a7b3a-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="a7b3a-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="a7b3a-144">**guid**</span></span> | <span data-ttu-id="a7b3a-145">Y</span><span class="sxs-lookup"><span data-stu-id="a7b3a-145">Y</span></span>        | <span data-ttu-id="a7b3a-146">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="a7b3a-147">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="a7b3a-147">**id-for-subscription**</span></span> | <span data-ttu-id="a7b3a-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="a7b3a-148">**guid**</span></span> | <span data-ttu-id="a7b3a-149">Y</span><span class="sxs-lookup"><span data-stu-id="a7b3a-149">Y</span></span>        | <span data-ttu-id="a7b3a-150">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a7b3a-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a7b3a-151">Request headers</span></span>

<span data-ttu-id="a7b3a-152">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a7b3a-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a7b3a-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a7b3a-153">Request body</span></span>

<span data-ttu-id="a7b3a-154">En fullständig **prenumerations** resurs krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="a7b3a-155">Se till att egenskapen **kvantitet** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-155">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="a7b3a-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a7b3a-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a7b3a-157">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a7b3a-157">REST response</span></span>

<span data-ttu-id="a7b3a-158">Om det lyckas returnerar den här metoden en status kod för **http-status 200** och uppdaterade [prenumerations resurs](subscription-resources.md)  egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-158">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a7b3a-159">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a7b3a-159">Response success and error codes</span></span>

<span data-ttu-id="a7b3a-160">Varje svar returnerar en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-160">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a7b3a-161">Använd ett verktyg för nätverks spårning för att läsa status koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-161">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="a7b3a-162">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a7b3a-162">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="a7b3a-163">När korrigerings åtgärden tar längre tid än den förväntade tiden skickar Partner Center en **http-status 202-** status kod och ett plats huvud som pekar på varifrån prenumerationen ska hämtas.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-163">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="a7b3a-164">Du kan fråga prenumerationen med jämna mellanrum för att övervaka ändringar av status och antal.</span><span class="sxs-lookup"><span data-stu-id="a7b3a-164">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="a7b3a-165">Svars exempel</span><span class="sxs-lookup"><span data-stu-id="a7b3a-165">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="a7b3a-166">Svars exempel 1</span><span class="sxs-lookup"><span data-stu-id="a7b3a-166">Response example 1</span></span>

<span data-ttu-id="a7b3a-167">Lyckad begäran med **http-status 200** status kod:</span><span class="sxs-lookup"><span data-stu-id="a7b3a-167">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="a7b3a-168">Svars exempel 2</span><span class="sxs-lookup"><span data-stu-id="a7b3a-168">Response example 2</span></span>

<span data-ttu-id="a7b3a-169">Lyckad begäran med **http-status 202** status kod:</span><span class="sxs-lookup"><span data-stu-id="a7b3a-169">Successful request with an **HTTP status 202** status code:</span></span>

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
