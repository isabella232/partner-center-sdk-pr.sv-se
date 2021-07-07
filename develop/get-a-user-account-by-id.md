---
title: Hämta ett användarkonto efter ID
description: Hämta ett specifikt användarkonto för en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a7cac98a8081a8557dcadfb0724f5497be7d14c
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760274"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="6401f-103">Hämta ett användarkonto efter ID</span><span class="sxs-lookup"><span data-stu-id="6401f-103">Get a user account by ID</span></span>

<span data-ttu-id="6401f-104">Hämta ett specifikt användarkonto för en kund.</span><span class="sxs-lookup"><span data-stu-id="6401f-104">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="6401f-105">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6401f-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6401f-106">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6401f-106">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6401f-107">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6401f-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6401f-108">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6401f-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6401f-109">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="6401f-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6401f-110">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="6401f-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6401f-111">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="6401f-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6401f-112">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6401f-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6401f-113">C\#</span><span class="sxs-lookup"><span data-stu-id="6401f-113">C\#</span></span>

<span data-ttu-id="6401f-114">Om du vill hämta ett användarkonto för en kund anropar du [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="6401f-114">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="6401f-115">Anropa sedan metoden [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att hämta den specifika användaren.</span><span class="sxs-lookup"><span data-stu-id="6401f-115">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="6401f-116">Anropa slutligen metoden [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) för att hämta användarkontot.</span><span class="sxs-lookup"><span data-stu-id="6401f-116">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="6401f-117">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6401f-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6401f-118">**Project:** Partnercenter-SDK **Samples-klass:** GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="6401f-118">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6401f-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6401f-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6401f-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="6401f-120">Request syntax</span></span>

| <span data-ttu-id="6401f-121">Metod</span><span class="sxs-lookup"><span data-stu-id="6401f-121">Method</span></span>  | <span data-ttu-id="6401f-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6401f-122">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6401f-123">**Få**</span><span class="sxs-lookup"><span data-stu-id="6401f-123">**GET**</span></span> | <span data-ttu-id="6401f-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6401f-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6401f-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="6401f-125">URI parameter</span></span>

<span data-ttu-id="6401f-126">Använd följande URI-parametrar för att identifiera rätt kund och användare.</span><span class="sxs-lookup"><span data-stu-id="6401f-126">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="6401f-127">Namn</span><span class="sxs-lookup"><span data-stu-id="6401f-127">Name</span></span>                   | <span data-ttu-id="6401f-128">Typ</span><span class="sxs-lookup"><span data-stu-id="6401f-128">Type</span></span>     | <span data-ttu-id="6401f-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6401f-129">Required</span></span> | <span data-ttu-id="6401f-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6401f-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6401f-131">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="6401f-131">**customer-tenant-id**</span></span> | <span data-ttu-id="6401f-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="6401f-132">**guid**</span></span> | <span data-ttu-id="6401f-133">Y</span><span class="sxs-lookup"><span data-stu-id="6401f-133">Y</span></span>        | <span data-ttu-id="6401f-134">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="6401f-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="6401f-135">**användar-id**</span><span class="sxs-lookup"><span data-stu-id="6401f-135">**user-id**</span></span>            | <span data-ttu-id="6401f-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="6401f-136">**guid**</span></span> | <span data-ttu-id="6401f-137">Y</span><span class="sxs-lookup"><span data-stu-id="6401f-137">Y</span></span>        | <span data-ttu-id="6401f-138">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.</span><span class="sxs-lookup"><span data-stu-id="6401f-138">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="6401f-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6401f-139">Request headers</span></span>

<span data-ttu-id="6401f-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6401f-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6401f-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6401f-141">Request body</span></span>

<span data-ttu-id="6401f-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="6401f-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6401f-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6401f-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6401f-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6401f-144">REST response</span></span>

<span data-ttu-id="6401f-145">Om det lyckas returnerar den här metoden användarkontot för kunden.</span><span class="sxs-lookup"><span data-stu-id="6401f-145">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6401f-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6401f-146">Response success and error codes</span></span>

<span data-ttu-id="6401f-147">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="6401f-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6401f-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6401f-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6401f-149">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6401f-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6401f-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6401f-150">Response example</span></span>

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
