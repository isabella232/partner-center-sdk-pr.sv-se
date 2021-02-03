---
title: Hämta ett användarkonto efter ID
description: Hämta ett speciellt användar konto för en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a2f42001365324a65376318cb1f2d57dc123df0c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769270"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="2866d-103">Hämta ett användarkonto efter ID</span><span class="sxs-lookup"><span data-stu-id="2866d-103">Get a user account by ID</span></span>

<span data-ttu-id="2866d-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="2866d-104">**Applies To**</span></span>

- <span data-ttu-id="2866d-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2866d-105">Partner Center</span></span>

<span data-ttu-id="2866d-106">Hämta ett speciellt användar konto för en kund.</span><span class="sxs-lookup"><span data-stu-id="2866d-106">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="2866d-107">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2866d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2866d-108">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2866d-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2866d-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2866d-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2866d-110">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2866d-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2866d-111">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2866d-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2866d-112">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2866d-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2866d-113">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2866d-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2866d-114">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2866d-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2866d-115">C\#</span><span class="sxs-lookup"><span data-stu-id="2866d-115">C\#</span></span>

<span data-ttu-id="2866d-116">Om du vill hämta ett användar konto för en kund anropar du metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="2866d-116">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="2866d-117">Anropa sedan metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att hämta den aktuella användaren.</span><span class="sxs-lookup"><span data-stu-id="2866d-117">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="2866d-118">Anropa slutligen metoden [**users. get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) för att hämta användar kontot.</span><span class="sxs-lookup"><span data-stu-id="2866d-118">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="2866d-119">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2866d-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2866d-120">**Projekt**: Partner Center SDK-exempel **klass**: GetCustomerUserDetails.CS</span><span class="sxs-lookup"><span data-stu-id="2866d-120">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2866d-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2866d-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2866d-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2866d-122">Request syntax</span></span>

| <span data-ttu-id="2866d-123">Metod</span><span class="sxs-lookup"><span data-stu-id="2866d-123">Method</span></span>  | <span data-ttu-id="2866d-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2866d-124">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2866d-125">**TA**</span><span class="sxs-lookup"><span data-stu-id="2866d-125">**GET**</span></span> | <span data-ttu-id="2866d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2866d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2866d-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2866d-127">URI parameter</span></span>

<span data-ttu-id="2866d-128">Använd följande URI-parametrar för att identifiera rätt kund och användare.</span><span class="sxs-lookup"><span data-stu-id="2866d-128">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="2866d-129">Namn</span><span class="sxs-lookup"><span data-stu-id="2866d-129">Name</span></span>                   | <span data-ttu-id="2866d-130">Typ</span><span class="sxs-lookup"><span data-stu-id="2866d-130">Type</span></span>     | <span data-ttu-id="2866d-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2866d-131">Required</span></span> | <span data-ttu-id="2866d-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2866d-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2866d-133">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="2866d-133">**customer-tenant-id**</span></span> | <span data-ttu-id="2866d-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="2866d-134">**guid**</span></span> | <span data-ttu-id="2866d-135">Y</span><span class="sxs-lookup"><span data-stu-id="2866d-135">Y</span></span>        | <span data-ttu-id="2866d-136">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="2866d-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="2866d-137">**användar-ID**</span><span class="sxs-lookup"><span data-stu-id="2866d-137">**user-id**</span></span>            | <span data-ttu-id="2866d-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="2866d-138">**guid**</span></span> | <span data-ttu-id="2866d-139">Y</span><span class="sxs-lookup"><span data-stu-id="2866d-139">Y</span></span>        | <span data-ttu-id="2866d-140">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.</span><span class="sxs-lookup"><span data-stu-id="2866d-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="2866d-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2866d-141">Request headers</span></span>

<span data-ttu-id="2866d-142">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2866d-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2866d-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2866d-143">Request body</span></span>

<span data-ttu-id="2866d-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="2866d-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2866d-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2866d-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2866d-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2866d-146">REST response</span></span>

<span data-ttu-id="2866d-147">Om det lyckas returnerar den här metoden användar kontot för kunden.</span><span class="sxs-lookup"><span data-stu-id="2866d-147">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2866d-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2866d-148">Response success and error codes</span></span>

<span data-ttu-id="2866d-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2866d-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2866d-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2866d-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2866d-151">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2866d-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2866d-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2866d-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 432
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CV: uWM1EGU7+0aI2MvV.0
MS-ServerId: 020021921
Date: Wed, 21 Dec 2016 22:59:10 GMT

{
    "usageLocation": "US",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Daniel",
    "lastName": "Tsai",
    "displayName": "Daniel Tsai",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
