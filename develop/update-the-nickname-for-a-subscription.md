---
title: Uppdatera smeknamnet för en prenumeration
description: Uppdaterar det egna namnet eller smek namnet för en kunds prenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 57a9fec4b69d4a64128425ea58b4bb84d0d7dd54
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769645"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="a28d8-103">Uppdatera smeknamnet för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="a28d8-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="a28d8-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="a28d8-104">**Applies To**</span></span>

- <span data-ttu-id="a28d8-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a28d8-105">Partner Center</span></span>
- <span data-ttu-id="a28d8-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a28d8-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a28d8-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="a28d8-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a28d8-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a28d8-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a28d8-109">Uppdaterar det egna namnet eller smek namnet för en kunds [prenumeration](subscription-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a28d8-109">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="a28d8-110">Det här namnet visas i Partner Center för att hjälpa till att skilja prenumerationerna på kundens konto.</span><span class="sxs-lookup"><span data-stu-id="a28d8-110">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="a28d8-111">På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="a28d8-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="a28d8-112">Välj sedan den prenumeration i fråga som du vill byta namn på.</span><span class="sxs-lookup"><span data-stu-id="a28d8-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="a28d8-113">Slutför genom att ändra namnet i fältet för **prenumerationens smek** namn och välj sedan **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="a28d8-113">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a28d8-114">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a28d8-114">Prerequisites</span></span>

- <span data-ttu-id="a28d8-115">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a28d8-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a28d8-116">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a28d8-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a28d8-117">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a28d8-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a28d8-118">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="a28d8-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a28d8-119">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="a28d8-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a28d8-120">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="a28d8-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a28d8-121">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="a28d8-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a28d8-122">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a28d8-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a28d8-123">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="a28d8-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="a28d8-124">C\#</span><span class="sxs-lookup"><span data-stu-id="a28d8-124">C\#</span></span>

<span data-ttu-id="a28d8-125">Om du vill uppdatera smek namnet för en kunds prenumeration börjar du med att [Hämta prenumerationen](get-a-subscription-by-id.md)och ändrar sedan prenumerationens egenskap [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) .</span><span class="sxs-lookup"><span data-stu-id="a28d8-125">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="a28d8-126">När ändringen har gjorts använder du din [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling och anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="a28d8-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="a28d8-127">Anropa sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="a28d8-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="a28d8-128">Sedan avslutar du genom att anropa [**patch-metoden ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) .</span><span class="sxs-lookup"><span data-stu-id="a28d8-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="a28d8-129">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a28d8-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a28d8-130">**Projekt**: PartnerSDK. FeatureSamples- **klass**: UpdateSubscription.CS</span><span class="sxs-lookup"><span data-stu-id="a28d8-130">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a28d8-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a28d8-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a28d8-132">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="a28d8-132">Request syntax</span></span>

| <span data-ttu-id="a28d8-133">Metod</span><span class="sxs-lookup"><span data-stu-id="a28d8-133">Method</span></span>    | <span data-ttu-id="a28d8-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a28d8-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a28d8-135">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="a28d8-135">**PATCH**</span></span> | <span data-ttu-id="a28d8-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a28d8-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a28d8-137">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="a28d8-137">URI parameter</span></span>

<span data-ttu-id="a28d8-138">Den här tabellen innehåller den obligatoriska Frågeparametern för att uppdatera prenumerationens smek namn.</span><span class="sxs-lookup"><span data-stu-id="a28d8-138">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="a28d8-139">Namn</span><span class="sxs-lookup"><span data-stu-id="a28d8-139">Name</span></span>                    | <span data-ttu-id="a28d8-140">Typ</span><span class="sxs-lookup"><span data-stu-id="a28d8-140">Type</span></span>     | <span data-ttu-id="a28d8-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a28d8-141">Required</span></span> | <span data-ttu-id="a28d8-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a28d8-142">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="a28d8-143">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="a28d8-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="a28d8-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="a28d8-144">**guid**</span></span> | <span data-ttu-id="a28d8-145">Y</span><span class="sxs-lookup"><span data-stu-id="a28d8-145">Y</span></span>        | <span data-ttu-id="a28d8-146">**Customer-Tenant-ID** (ett GUID).</span><span class="sxs-lookup"><span data-stu-id="a28d8-146">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="a28d8-147">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="a28d8-147">**id-for-subscription**</span></span> | <span data-ttu-id="a28d8-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="a28d8-148">**guid**</span></span> | <span data-ttu-id="a28d8-149">Y</span><span class="sxs-lookup"><span data-stu-id="a28d8-149">Y</span></span>        | <span data-ttu-id="a28d8-150">Prenumerations-ID (ett GUID).</span><span class="sxs-lookup"><span data-stu-id="a28d8-150">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="a28d8-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a28d8-151">Request headers</span></span>

<span data-ttu-id="a28d8-152">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a28d8-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a28d8-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a28d8-153">Request body</span></span>

<span data-ttu-id="a28d8-154">En fullständig **prenumerations** resurs krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="a28d8-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="a28d8-155">Se till att egenskapen **FriendlyName** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="a28d8-155">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="a28d8-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a28d8-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
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
    OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="a28d8-157">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a28d8-157">REST response</span></span>

<span data-ttu-id="a28d8-158">Om det lyckas returnerar den här metoden uppdaterade [prenumerations](subscription-resources.md) resurs egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="a28d8-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a28d8-159">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a28d8-159">Response success and error codes</span></span>

<span data-ttu-id="a28d8-160">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="a28d8-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a28d8-161">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a28d8-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a28d8-162">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a28d8-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a28d8-163">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a28d8-163">Response example</span></span>

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
    "Id": "<subscriptionID>",
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
