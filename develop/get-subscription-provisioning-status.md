---
title: Hämta status för prenumerationsetablering
description: Så här hämtar du prenumerationens etablerings status för en kund prenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38544aa380ba0a6a8804ae45f7d8ae7cb431d3ba
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769843"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="ecb1a-103">Hämta status för prenumerationsetablering</span><span class="sxs-lookup"><span data-stu-id="ecb1a-103">Get subscription provisioning status</span></span>

<span data-ttu-id="ecb1a-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="ecb1a-104">**Applies To**</span></span>

- <span data-ttu-id="ecb1a-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="ecb1a-105">Partner Center</span></span>
- <span data-ttu-id="ecb1a-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="ecb1a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ecb1a-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="ecb1a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ecb1a-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ecb1a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ecb1a-109">Så här hämtar du prenumerationens etablerings status för en kund prenumeration.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-109">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecb1a-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ecb1a-110">Prerequisites</span></span>

- <span data-ttu-id="ecb1a-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ecb1a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ecb1a-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ecb1a-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ecb1a-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ecb1a-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ecb1a-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ecb1a-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ecb1a-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="ecb1a-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ecb1a-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ecb1a-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ecb1a-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-119">A subscription identifier.</span></span>

- <span data-ttu-id="ecb1a-120">Delegerade administratörs behörigheter för prenumerationen krävs för att utföra den här åtgärden.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-120">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="ecb1a-121">C\#</span><span class="sxs-lookup"><span data-stu-id="ecb1a-121">C\#</span></span>

<span data-ttu-id="ecb1a-122">Börja med att använda metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att identifiera kunden för att få etablerings statusen för en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-122">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ecb1a-123">Hämta sedan ett gränssnitt till prenumerations åtgärder genom att anropa metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID: t.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-123">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="ecb1a-124">Använd sedan egenskapen [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) för att hämta ett gränssnitt till etablerings status åtgärderna för den aktuella prenumerationen och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) för att hämta [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) -objektet.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-124">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="ecb1a-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ecb1a-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ecb1a-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="ecb1a-126">Request syntax</span></span>

| <span data-ttu-id="ecb1a-127">Metod</span><span class="sxs-lookup"><span data-stu-id="ecb1a-127">Method</span></span>  | <span data-ttu-id="ecb1a-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ecb1a-128">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ecb1a-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="ecb1a-129">**GET**</span></span> | <span data-ttu-id="ecb1a-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/provisioningstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="ecb1a-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="ecb1a-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="ecb1a-131">URI parameters</span></span>

<span data-ttu-id="ecb1a-132">Använd följande Sök vägs parametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="ecb1a-133">Namn</span><span class="sxs-lookup"><span data-stu-id="ecb1a-133">Name</span></span>            | <span data-ttu-id="ecb1a-134">Typ</span><span class="sxs-lookup"><span data-stu-id="ecb1a-134">Type</span></span>   | <span data-ttu-id="ecb1a-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ecb1a-135">Required</span></span> | <span data-ttu-id="ecb1a-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ecb1a-136">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="ecb1a-137">kund-ID</span><span class="sxs-lookup"><span data-stu-id="ecb1a-137">customer-id</span></span>     | <span data-ttu-id="ecb1a-138">sträng</span><span class="sxs-lookup"><span data-stu-id="ecb1a-138">string</span></span> | <span data-ttu-id="ecb1a-139">Yes</span><span class="sxs-lookup"><span data-stu-id="ecb1a-139">Yes</span></span>      | <span data-ttu-id="ecb1a-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-140">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="ecb1a-141">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="ecb1a-141">subscription-id</span></span> | <span data-ttu-id="ecb1a-142">sträng</span><span class="sxs-lookup"><span data-stu-id="ecb1a-142">string</span></span> | <span data-ttu-id="ecb1a-143">Yes</span><span class="sxs-lookup"><span data-stu-id="ecb1a-143">Yes</span></span>      | <span data-ttu-id="ecb1a-144">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-144">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ecb1a-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ecb1a-145">Request headers</span></span>

<span data-ttu-id="ecb1a-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ecb1a-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ecb1a-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ecb1a-147">Request body</span></span>

<span data-ttu-id="ecb1a-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ecb1a-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ecb1a-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ecb1a-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ecb1a-150">REST response</span></span>

<span data-ttu-id="ecb1a-151">Om det lyckas innehåller svars texten en [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) -resurs.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-151">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ecb1a-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ecb1a-152">Response success and error codes</span></span>

<span data-ttu-id="ecb1a-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ecb1a-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ecb1a-155">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ecb1a-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ecb1a-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ecb1a-156">Response example</span></span>

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

## <a name="remarks"></a><span data-ttu-id="ecb1a-157">Kommentarer</span><span class="sxs-lookup"><span data-stu-id="ecb1a-157">Remarks</span></span>

- <span data-ttu-id="ecb1a-158">Under en licens ändrings tilldelning anges status fältet i [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) till "väntar".</span><span class="sxs-lookup"><span data-stu-id="ecb1a-158">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="ecb1a-159">Fältet status uppdateras var femtonde minut.</span><span class="sxs-lookup"><span data-stu-id="ecb1a-159">The status field is updated every fifteen minutes.</span></span>
