---
title: Återaktivera en inaktiverad prenumeration
description: Återaktiverar en prenumeration som tidigare har inaktiverats för utebliven betalning. På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först välja en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b6e3574119f9c645cc3f730047d2a23484ad8a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547723"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="43a27-104">Återaktivera en inaktiverad prenumeration</span><span class="sxs-lookup"><span data-stu-id="43a27-104">Reactivate a suspended subscription</span></span>

<span data-ttu-id="43a27-105">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="43a27-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="43a27-106">Återaktiverar en [prenumeration som](subscription-resources.md) tidigare har inaktiverats för utebliven betalning.</span><span class="sxs-lookup"><span data-stu-id="43a27-106">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="43a27-107">På instrumentpanelen i Partnercenter kan den här åtgärden utföras genom att först [välja en kund.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="43a27-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="43a27-108">Välj sedan den prenumeration som du vill byta namn på.</span><span class="sxs-lookup"><span data-stu-id="43a27-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="43a27-109">Slutför genom att välja **knappen Aktiv** och sedan **skicka.**</span><span class="sxs-lookup"><span data-stu-id="43a27-109">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43a27-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="43a27-110">Prerequisites</span></span>

- <span data-ttu-id="43a27-111">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="43a27-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="43a27-112">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="43a27-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="43a27-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="43a27-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="43a27-114">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="43a27-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="43a27-115">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="43a27-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="43a27-116">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="43a27-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="43a27-117">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="43a27-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="43a27-118">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="43a27-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="43a27-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="43a27-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="43a27-120">C\#</span><span class="sxs-lookup"><span data-stu-id="43a27-120">C\#</span></span>

<span data-ttu-id="43a27-121">Om du vill återaktivera en kunds prenumeration hämtar du [först prenumerationen](get-a-subscription-by-id.md)och ändrar sedan prenumerationens [**Status-egenskap.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)</span><span class="sxs-lookup"><span data-stu-id="43a27-121">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="43a27-122">Information om **statuskoder** finns i [SubscriptionStatus-uppräkning/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="43a27-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="43a27-123">När ändringen har gjorts använder du samlingen [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropar [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="43a27-123">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="43a27-124">Anropa sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="43a27-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="43a27-125">Avsluta sedan med att anropa [**metoden Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="43a27-125">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

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

<span data-ttu-id="43a27-126">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="43a27-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="43a27-127">**Project:** FunktionerExempelApplication.</span><span class="sxs-lookup"><span data-stu-id="43a27-127">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="43a27-128">**Klass:** UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="43a27-128">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="43a27-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="43a27-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="43a27-130">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="43a27-130">Request syntax</span></span>

| <span data-ttu-id="43a27-131">Metod</span><span class="sxs-lookup"><span data-stu-id="43a27-131">Method</span></span>    | <span data-ttu-id="43a27-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="43a27-132">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="43a27-133">**Patch**</span><span class="sxs-lookup"><span data-stu-id="43a27-133">**PATCH**</span></span> | <span data-ttu-id="43a27-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="43a27-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="43a27-135">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="43a27-135">URI parameter</span></span>

<span data-ttu-id="43a27-136">Den här tabellen innehåller frågeparametern som krävs för att återaktivera prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="43a27-136">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="43a27-137">Namn</span><span class="sxs-lookup"><span data-stu-id="43a27-137">Name</span></span>                    | <span data-ttu-id="43a27-138">Typ</span><span class="sxs-lookup"><span data-stu-id="43a27-138">Type</span></span>     | <span data-ttu-id="43a27-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="43a27-139">Required</span></span> | <span data-ttu-id="43a27-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="43a27-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="43a27-141">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="43a27-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="43a27-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="43a27-142">**guid**</span></span> | <span data-ttu-id="43a27-143">Y</span><span class="sxs-lookup"><span data-stu-id="43a27-143">Y</span></span>        | <span data-ttu-id="43a27-144">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="43a27-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="43a27-145">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="43a27-145">**id-for-subscription**</span></span> | <span data-ttu-id="43a27-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="43a27-146">**guid**</span></span> | <span data-ttu-id="43a27-147">Y</span><span class="sxs-lookup"><span data-stu-id="43a27-147">Y</span></span>        | <span data-ttu-id="43a27-148">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="43a27-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="43a27-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="43a27-149">Request headers</span></span>

<span data-ttu-id="43a27-150">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="43a27-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="43a27-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="43a27-151">Request body</span></span>

<span data-ttu-id="43a27-152">En fullständig **prenumerationsresurs** krävs i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="43a27-152">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="43a27-153">Kontrollera att **egenskapen Status** har uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="43a27-153">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="43a27-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="43a27-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="43a27-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="43a27-155">REST response</span></span>

<span data-ttu-id="43a27-156">Om det lyckas returnerar den här metoden [uppdaterade prenumerationsresursegenskaper](subscription-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="43a27-156">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="43a27-157">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="43a27-157">Response success and error codes</span></span>

<span data-ttu-id="43a27-158">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="43a27-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="43a27-159">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="43a27-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="43a27-160">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="43a27-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="43a27-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="43a27-161">Response example</span></span>

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
