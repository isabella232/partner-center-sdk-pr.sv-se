---
title: Inaktivera en prenumeration
description: 'Pausar en prenumerations resurs som matchar kund-och prenumerations-ID: t på grund av bedrägerier eller utebliven betalning. På instrument panelen för partner Center kan du utföra den här åtgärden genom att först välja en kund.'
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f351c87efe2bdc810a66c64a9d01b7d376f8a6e3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769597"
---
# <a name="suspend-a-subscription"></a><span data-ttu-id="80692-103">Inaktivera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="80692-103">Suspend a subscription</span></span>

<span data-ttu-id="80692-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="80692-104">**Applies To**</span></span>

- <span data-ttu-id="80692-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="80692-105">Partner Center</span></span>
- <span data-ttu-id="80692-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="80692-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="80692-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="80692-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="80692-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="80692-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="80692-109">Pausar en [prenumerations](subscription-resources.md) resurs som matchar kund-och prenumerations-ID: t på grund av bedrägerier eller utebliven betalning.</span><span class="sxs-lookup"><span data-stu-id="80692-109">Suspends a [Subscription](subscription-resources.md) resource that matches the customer and subscription ID due to fraud or non-payment.</span></span>

<span data-ttu-id="80692-110">På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="80692-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="80692-111">Välj sedan den prenumeration i fråga som du vill byta namn på.</span><span class="sxs-lookup"><span data-stu-id="80692-111">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="80692-112">Slutför genom att välja knappen **inaktiverat** och sedan **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="80692-112">To finish, choose the **Suspended** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80692-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="80692-113">Prerequisites</span></span>

- <span data-ttu-id="80692-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="80692-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80692-115">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="80692-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="80692-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80692-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80692-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="80692-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80692-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="80692-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80692-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="80692-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80692-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="80692-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80692-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80692-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="80692-122">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="80692-122">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="80692-123">C\#</span><span class="sxs-lookup"><span data-stu-id="80692-123">C\#</span></span>

<span data-ttu-id="80692-124">Om du vill inaktivera en kunds prenumeration måste du först [Hämta prenumerationen](get-a-subscription-by-id.md)och sedan ändra prenumerationens [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) egenskap.</span><span class="sxs-lookup"><span data-stu-id="80692-124">To suspend a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="80692-125">Information om **status** koder finns i [SubscriptionStatus Enumeration/dotNet/API/Microsoft. Store. Partnercenter. Models. Subscriptions. SubscriptionStatus).</span><span class="sxs-lookup"><span data-stu-id="80692-125">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="80692-126">När ändringen har gjorts använder du din **IAggregatePartner. Customers** -samling och anropar metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="80692-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="80692-127">Anropa sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="80692-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="80692-128">Sedan avslutar du genom att anropa **patch-metoden ()** .</span><span class="sxs-lookup"><span data-stu-id="80692-128">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Suspended
   });
```

<span data-ttu-id="80692-129">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80692-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80692-130">**Projekt**: PartnerSDK. FeatureSample- **klass**: UpdateSubscription.CS</span><span class="sxs-lookup"><span data-stu-id="80692-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="80692-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="80692-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80692-132">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="80692-132">Request syntax</span></span>

| <span data-ttu-id="80692-133">Metod</span><span class="sxs-lookup"><span data-stu-id="80692-133">Method</span></span>    | <span data-ttu-id="80692-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="80692-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80692-135">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="80692-135">**PATCH**</span></span> | <span data-ttu-id="80692-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="80692-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="80692-137">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="80692-137">URI parameter</span></span>

<span data-ttu-id="80692-138">Den här tabellen visar den obligatoriska Frågeparametern för att pausa prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="80692-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="80692-139">Namn</span><span class="sxs-lookup"><span data-stu-id="80692-139">Name</span></span>                    | <span data-ttu-id="80692-140">Typ</span><span class="sxs-lookup"><span data-stu-id="80692-140">Type</span></span>     | <span data-ttu-id="80692-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="80692-141">Required</span></span> | <span data-ttu-id="80692-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="80692-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="80692-143">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="80692-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="80692-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="80692-144">**guid**</span></span> | <span data-ttu-id="80692-145">Y</span><span class="sxs-lookup"><span data-stu-id="80692-145">Y</span></span>        | <span data-ttu-id="80692-146">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="80692-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="80692-147">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="80692-147">**id-for-subscription**</span></span> | <span data-ttu-id="80692-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="80692-148">**guid**</span></span> | <span data-ttu-id="80692-149">Y</span><span class="sxs-lookup"><span data-stu-id="80692-149">Y</span></span>        | <span data-ttu-id="80692-150">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="80692-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80692-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="80692-151">Request headers</span></span>

<span data-ttu-id="80692-152">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="80692-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80692-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="80692-153">Request body</span></span>

<span data-ttu-id="80692-154">En fullständig **prenumerations** resurs krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="80692-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="80692-155">Se till att **status** egenskapen har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="80692-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="80692-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="80692-156">Request example</span></span>

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
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
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

## <a name="rest-response"></a><span data-ttu-id="80692-157">REST-svar</span><span class="sxs-lookup"><span data-stu-id="80692-157">REST response</span></span>

<span data-ttu-id="80692-158">Om det lyckas returnerar den här metoden uppdaterade [prenumerations](subscription-resources.md) resurs egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="80692-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80692-159">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="80692-159">Response success and error codes</span></span>

<span data-ttu-id="80692-160">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="80692-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80692-161">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="80692-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80692-162">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="80692-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80692-163">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="80692-163">Response example</span></span>

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
    "Status": "suspended",
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
