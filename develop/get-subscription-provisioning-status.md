---
title: Hämta status för prenumerationsetablering
description: Så här hämtar du prenumerationens etableringsstatus för en kundprenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8797fa494cd77f11a1179d6406ca021f0d7788c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548710"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="1a2b4-103">Hämta status för prenumerationsetablering</span><span class="sxs-lookup"><span data-stu-id="1a2b4-103">Get subscription provisioning status</span></span>

<span data-ttu-id="1a2b4-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1a2b4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1a2b4-105">Så här hämtar du prenumerationens etableringsstatus för en kundprenumeration.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-105">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a2b4-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1a2b4-106">Prerequisites</span></span>

- <span data-ttu-id="1a2b4-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1a2b4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1a2b4-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1a2b4-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a2b4-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1a2b4-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1a2b4-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1a2b4-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1a2b4-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="1a2b4-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1a2b4-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="1a2b4-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1a2b4-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a2b4-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1a2b4-115">En prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-115">A subscription identifier.</span></span>

- <span data-ttu-id="1a2b4-116">Delegerade administratörsbehörigheter för prenumerationen krävs för att utföra den här åtgärden.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-116">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="1a2b4-117">C\#</span><span class="sxs-lookup"><span data-stu-id="1a2b4-117">C\#</span></span>

<span data-ttu-id="1a2b4-118">Om du vill hämta etableringsstatusen för en prenumeration börjar du med att använda metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-118">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="1a2b4-119">Hämta sedan ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID:t.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="1a2b4-120">Använd sedan egenskapen [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) för att hämta ett gränssnitt till den aktuella prenumerationens etableringsstatusåtgärder och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) för att hämta [**objektet SubscriptionProvisioningStatus.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus)</span><span class="sxs-lookup"><span data-stu-id="1a2b4-120">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="1a2b4-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1a2b4-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1a2b4-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="1a2b4-122">Request syntax</span></span>

| <span data-ttu-id="1a2b4-123">Metod</span><span class="sxs-lookup"><span data-stu-id="1a2b4-123">Method</span></span>  | <span data-ttu-id="1a2b4-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1a2b4-124">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1a2b4-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="1a2b4-125">**GET**</span></span> | <span data-ttu-id="1a2b4-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1a2b4-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="1a2b4-127">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="1a2b4-127">URI parameters</span></span>

<span data-ttu-id="1a2b4-128">Använd följande sökvägsparametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-128">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="1a2b4-129">Namn</span><span class="sxs-lookup"><span data-stu-id="1a2b4-129">Name</span></span>            | <span data-ttu-id="1a2b4-130">Typ</span><span class="sxs-lookup"><span data-stu-id="1a2b4-130">Type</span></span>   | <span data-ttu-id="1a2b4-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1a2b4-131">Required</span></span> | <span data-ttu-id="1a2b4-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1a2b4-132">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="1a2b4-133">kund-id</span><span class="sxs-lookup"><span data-stu-id="1a2b4-133">customer-id</span></span>     | <span data-ttu-id="1a2b4-134">sträng</span><span class="sxs-lookup"><span data-stu-id="1a2b4-134">string</span></span> | <span data-ttu-id="1a2b4-135">Ja</span><span class="sxs-lookup"><span data-stu-id="1a2b4-135">Yes</span></span>      | <span data-ttu-id="1a2b4-136">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-136">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="1a2b4-137">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="1a2b4-137">subscription-id</span></span> | <span data-ttu-id="1a2b4-138">sträng</span><span class="sxs-lookup"><span data-stu-id="1a2b4-138">string</span></span> | <span data-ttu-id="1a2b4-139">Ja</span><span class="sxs-lookup"><span data-stu-id="1a2b4-139">Yes</span></span>      | <span data-ttu-id="1a2b4-140">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-140">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1a2b4-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1a2b4-141">Request headers</span></span>

<span data-ttu-id="1a2b4-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1a2b4-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1a2b4-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1a2b4-143">Request body</span></span>

<span data-ttu-id="1a2b4-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1a2b4-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1a2b4-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1a2b4-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1a2b4-146">REST response</span></span>

<span data-ttu-id="1a2b4-147">Om det lyckas innehåller svarstexten en [SubscriptionProvisioningStatus-resurs.](subscription-resources.md#subscriptionprovisioningstatus)</span><span class="sxs-lookup"><span data-stu-id="1a2b4-147">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1a2b4-148">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1a2b4-148">Response success and error codes</span></span>

<span data-ttu-id="1a2b4-149">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1a2b4-150">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1a2b4-151">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1a2b4-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1a2b4-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1a2b4-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a><span data-ttu-id="1a2b4-153">Kommentarer</span><span class="sxs-lookup"><span data-stu-id="1a2b4-153">Remarks</span></span>

- <span data-ttu-id="1a2b4-154">Under en licensändringstilldelning anges statusfältet [i SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) till "väntande".</span><span class="sxs-lookup"><span data-stu-id="1a2b4-154">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="1a2b4-155">Statusfältet uppdateras var 15:e minut.</span><span class="sxs-lookup"><span data-stu-id="1a2b4-155">The status field is updated every 15 minutes.</span></span>
