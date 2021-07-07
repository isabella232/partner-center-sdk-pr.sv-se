---
title: Uppdatera smeknamnet för en prenumeration
description: Uppdaterar det egna namnet eller smeknamnet för en kunds prenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 195a85fcf29b3e4c9fe0e578d4d8cb80ca068c40
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530012"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="95692-103">Uppdatera smeknamnet för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="95692-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="95692-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="95692-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="95692-105">Uppdaterar det egna namnet eller smeknamnet för en kunds [prenumeration](subscription-resources.md).</span><span class="sxs-lookup"><span data-stu-id="95692-105">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="95692-106">Det här namnet visas i Partnercenter för att hjälpa till att särskilja prenumerationerna i kundens konto.</span><span class="sxs-lookup"><span data-stu-id="95692-106">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="95692-107">På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först [välja en kund.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="95692-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="95692-108">Välj sedan den prenumeration som du vill byta namn på.</span><span class="sxs-lookup"><span data-stu-id="95692-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="95692-109">Avsluta genom att ändra namnet i fältet **Smeknamn för prenumeration** och välj sedan **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="95692-109">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95692-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="95692-110">Prerequisites</span></span>

- <span data-ttu-id="95692-111">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="95692-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95692-112">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="95692-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="95692-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95692-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="95692-114">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="95692-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="95692-115">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="95692-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="95692-116">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="95692-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="95692-117">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="95692-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="95692-118">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95692-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="95692-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="95692-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="95692-120">C\#</span><span class="sxs-lookup"><span data-stu-id="95692-120">C\#</span></span>

<span data-ttu-id="95692-121">Om du vill uppdatera smeknamnet för en kunds prenumeration hämtar du först prenumerationen [och](get-a-subscription-by-id.md)ändrar sedan prenumerationens [**FriendlyName-egenskap.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname)</span><span class="sxs-lookup"><span data-stu-id="95692-121">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="95692-122">När ändringen har gjorts använder du samlingen [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropar [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="95692-122">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="95692-123">Anropa sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="95692-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="95692-124">Avsluta sedan med att anropa [**metoden Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="95692-124">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="95692-125">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="95692-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="95692-126">**Project:** PartnerSDK.FeatureSamples-klass: UpdateSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="95692-126">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="95692-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="95692-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95692-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="95692-128">Request syntax</span></span>

| <span data-ttu-id="95692-129">Metod</span><span class="sxs-lookup"><span data-stu-id="95692-129">Method</span></span>    | <span data-ttu-id="95692-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="95692-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95692-131">**Patch**</span><span class="sxs-lookup"><span data-stu-id="95692-131">**PATCH**</span></span> | <span data-ttu-id="95692-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="95692-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="95692-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="95692-133">URI parameter</span></span>

<span data-ttu-id="95692-134">I den här tabellen visas frågeparametern som krävs för att uppdatera prenumerationens smeknamn.</span><span class="sxs-lookup"><span data-stu-id="95692-134">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="95692-135">Namn</span><span class="sxs-lookup"><span data-stu-id="95692-135">Name</span></span>                    | <span data-ttu-id="95692-136">Typ</span><span class="sxs-lookup"><span data-stu-id="95692-136">Type</span></span>     | <span data-ttu-id="95692-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="95692-137">Required</span></span> | <span data-ttu-id="95692-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="95692-138">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="95692-139">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="95692-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="95692-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="95692-140">**guid**</span></span> | <span data-ttu-id="95692-141">Y</span><span class="sxs-lookup"><span data-stu-id="95692-141">Y</span></span>        | <span data-ttu-id="95692-142">Kundens **klientorganisations-ID** (ett GUID).</span><span class="sxs-lookup"><span data-stu-id="95692-142">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="95692-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="95692-143">**id-for-subscription**</span></span> | <span data-ttu-id="95692-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="95692-144">**guid**</span></span> | <span data-ttu-id="95692-145">Y</span><span class="sxs-lookup"><span data-stu-id="95692-145">Y</span></span>        | <span data-ttu-id="95692-146">Prenumerations-ID :t (ett GUID).</span><span class="sxs-lookup"><span data-stu-id="95692-146">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="95692-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="95692-147">Request headers</span></span>

<span data-ttu-id="95692-148">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="95692-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95692-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="95692-149">Request body</span></span>

<span data-ttu-id="95692-150">En fullständig **prenumerationsresurs** krävs i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="95692-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="95692-151">Kontrollera att **egenskapen FriendlyName** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="95692-151">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="95692-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="95692-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="95692-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="95692-153">REST response</span></span>

<span data-ttu-id="95692-154">Om det lyckas returnerar den här metoden uppdaterade [prenumerationsresursegenskaper](subscription-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="95692-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95692-155">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="95692-155">Response success and error codes</span></span>

<span data-ttu-id="95692-156">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="95692-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95692-157">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="95692-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="95692-158">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="95692-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="95692-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="95692-159">Response example</span></span>

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
