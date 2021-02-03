---
title: Hämta en lista över alla användarkonton för en kund
description: Så här hämtar du en lista över alla användar konton som tillhör en av dina kunder.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f2b1bcf9926e02232b6e2cc68b71e992b015324
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769333"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="49238-103">Hämta en lista över alla användarkonton för en kund</span><span class="sxs-lookup"><span data-stu-id="49238-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="49238-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="49238-104">**Applies to:**</span></span>

- <span data-ttu-id="49238-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="49238-105">Partner Center</span></span>

<span data-ttu-id="49238-106">Den här artikeln beskriver hur du hämtar en lista över alla användar konton som tillhör en av dina kunder.</span><span class="sxs-lookup"><span data-stu-id="49238-106">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="49238-107">Information om hur du söker efter ett enskilt användar konto efter ID finns i [Hämta ett användar konto efter ID](get-a-user-account-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="49238-107">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49238-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="49238-108">Prerequisites</span></span>

- <span data-ttu-id="49238-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="49238-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="49238-110">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="49238-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="49238-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="49238-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="49238-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="49238-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="49238-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="49238-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="49238-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="49238-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="49238-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="49238-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="49238-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="49238-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="49238-117">C\#</span><span class="sxs-lookup"><span data-stu-id="49238-117">C\#</span></span>

<span data-ttu-id="49238-118">Hämta samlingen med alla användar konton för en angiven kund:</span><span class="sxs-lookup"><span data-stu-id="49238-118">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="49238-119">Anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det angivna kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="49238-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="49238-120">Anropa [**users. get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) -metoden för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="49238-120">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="49238-121">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="49238-121">For an example, see the following:</span></span>

- <span data-ttu-id="49238-122">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="49238-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="49238-123">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="49238-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="49238-124">Klass: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="49238-124">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="49238-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="49238-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="49238-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="49238-126">Request syntax</span></span>

| <span data-ttu-id="49238-127">Metod</span><span class="sxs-lookup"><span data-stu-id="49238-127">Method</span></span>  | <span data-ttu-id="49238-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="49238-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="49238-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="49238-129">**GET**</span></span> | <span data-ttu-id="49238-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="49238-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="49238-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="49238-131">URI parameter</span></span>

<span data-ttu-id="49238-132">Använd följande URI-parameter för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="49238-132">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="49238-133">Namn</span><span class="sxs-lookup"><span data-stu-id="49238-133">Name</span></span>                   | <span data-ttu-id="49238-134">Typ</span><span class="sxs-lookup"><span data-stu-id="49238-134">Type</span></span>     | <span data-ttu-id="49238-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="49238-135">Required</span></span> | <span data-ttu-id="49238-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="49238-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="49238-137">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="49238-137">**customer-tenant-id**</span></span> | <span data-ttu-id="49238-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="49238-138">**guid**</span></span> | <span data-ttu-id="49238-139">Y</span><span class="sxs-lookup"><span data-stu-id="49238-139">Y</span></span>        | <span data-ttu-id="49238-140">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="49238-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="49238-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="49238-141">Request headers</span></span>

<span data-ttu-id="49238-142">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="49238-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="49238-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="49238-143">Request body</span></span>

<span data-ttu-id="49238-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="49238-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="49238-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="49238-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="49238-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="49238-146">REST response</span></span>

<span data-ttu-id="49238-147">Om det lyckas returnerar den här metoden en samling användar konton för en kund.</span><span class="sxs-lookup"><span data-stu-id="49238-147">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="49238-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="49238-148">Response success and error codes</span></span>

<span data-ttu-id="49238-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="49238-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="49238-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="49238-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="49238-151">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="49238-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="49238-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="49238-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1030
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CV: 6zmKqrSFB0+t7m3y.0
MS-ServerId: 101112616
Date: Wed, 21 Dec 2016 21:13:24 GMT

 {
    "totalCount": 2,
    "items": [{
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
        }, {
            "id": "6e668259-1f09-479d-bcb8-d9b03e826b8d",
            "userPrincipalName": "admin@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "DT Demo CSP Customer 005",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/6e668259-1f09-479d-bcb8-d9b03e826b8d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
