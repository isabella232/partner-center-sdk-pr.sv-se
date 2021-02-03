---
title: Återaktivera en inaktiverad prenumeration
description: Återaktiverar en prenumeration som tidigare har avbrutits för inbetalning. På instrument panelen för partner Center kan du utföra den här åtgärden genom att först välja en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17c63e9c6d4c9e111bfea28e97319696534fa122
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769615"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="2869c-103">Återaktivera en inaktiverad prenumeration</span><span class="sxs-lookup"><span data-stu-id="2869c-103">Reactivate a suspended subscription</span></span>

<span data-ttu-id="2869c-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="2869c-104">**Applies To**</span></span>

- <span data-ttu-id="2869c-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2869c-105">Partner Center</span></span>
- <span data-ttu-id="2869c-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="2869c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2869c-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="2869c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2869c-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2869c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2869c-109">Återaktiverar en [prenumeration](subscription-resources.md) som tidigare har avbrutits för inbetalning.</span><span class="sxs-lookup"><span data-stu-id="2869c-109">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="2869c-110">På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="2869c-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="2869c-111">Välj sedan den prenumeration i fråga som du vill byta namn på.</span><span class="sxs-lookup"><span data-stu-id="2869c-111">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="2869c-112">Slutför genom att välja knappen **aktiv** och sedan **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="2869c-112">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2869c-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2869c-113">Prerequisites</span></span>

- <span data-ttu-id="2869c-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2869c-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2869c-115">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2869c-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2869c-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2869c-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2869c-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2869c-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2869c-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2869c-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2869c-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2869c-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2869c-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2869c-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2869c-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2869c-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2869c-122">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="2869c-122">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="2869c-123">C\#</span><span class="sxs-lookup"><span data-stu-id="2869c-123">C\#</span></span>

<span data-ttu-id="2869c-124">Om du vill återaktivera en kunds prenumeration måste du först [Hämta prenumerationen](get-a-subscription-by-id.md)och sedan ändra prenumerationens [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) egenskap.</span><span class="sxs-lookup"><span data-stu-id="2869c-124">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="2869c-125">Information om **status** koder finns i [SubscriptionStatus Enumeration/dotNet/API/Microsoft. Store. Partnercenter. Models. Subscriptions. SubscriptionStatus).</span><span class="sxs-lookup"><span data-stu-id="2869c-125">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="2869c-126">När ändringen har gjorts använder du din [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling och anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="2869c-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="2869c-127">Anropa sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="2869c-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="2869c-128">Sedan avslutar du genom att anropa [**patch-metoden ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) .</span><span class="sxs-lookup"><span data-stu-id="2869c-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

<span data-ttu-id="2869c-129">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2869c-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2869c-130">**Projekt**: FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="2869c-130">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="2869c-131">**Klass**: UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="2869c-131">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="2869c-132">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2869c-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2869c-133">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2869c-133">Request syntax</span></span>

| <span data-ttu-id="2869c-134">Metod</span><span class="sxs-lookup"><span data-stu-id="2869c-134">Method</span></span>    | <span data-ttu-id="2869c-135">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2869c-135">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2869c-136">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="2869c-136">**PATCH**</span></span> | <span data-ttu-id="2869c-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2869c-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2869c-138">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2869c-138">URI parameter</span></span>

<span data-ttu-id="2869c-139">Den här tabellen visar den obligatoriska Frågeparametern för att återaktivera prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="2869c-139">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="2869c-140">Namn</span><span class="sxs-lookup"><span data-stu-id="2869c-140">Name</span></span>                    | <span data-ttu-id="2869c-141">Typ</span><span class="sxs-lookup"><span data-stu-id="2869c-141">Type</span></span>     | <span data-ttu-id="2869c-142">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2869c-142">Required</span></span> | <span data-ttu-id="2869c-143">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2869c-143">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="2869c-144">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="2869c-144">**customer-tenant-id**</span></span>  | <span data-ttu-id="2869c-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="2869c-145">**guid**</span></span> | <span data-ttu-id="2869c-146">Y</span><span class="sxs-lookup"><span data-stu-id="2869c-146">Y</span></span>        | <span data-ttu-id="2869c-147">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="2869c-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="2869c-148">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="2869c-148">**id-for-subscription**</span></span> | <span data-ttu-id="2869c-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="2869c-149">**guid**</span></span> | <span data-ttu-id="2869c-150">Y</span><span class="sxs-lookup"><span data-stu-id="2869c-150">Y</span></span>        | <span data-ttu-id="2869c-151">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="2869c-151">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2869c-152">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2869c-152">Request headers</span></span>

<span data-ttu-id="2869c-153">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2869c-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2869c-154">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2869c-154">Request body</span></span>

<span data-ttu-id="2869c-155">En fullständig **prenumerations** resurs krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="2869c-155">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="2869c-156">Se till att **status** egenskapen har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="2869c-156">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="2869c-157">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2869c-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2869c-158">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2869c-158">REST response</span></span>

<span data-ttu-id="2869c-159">Om det lyckas returnerar den här metoden uppdaterade [prenumerations](subscription-resources.md) resurs egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="2869c-159">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2869c-160">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2869c-160">Response success and error codes</span></span>

<span data-ttu-id="2869c-161">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2869c-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2869c-162">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2869c-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2869c-163">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2869c-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2869c-164">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2869c-164">Response example</span></span>

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
