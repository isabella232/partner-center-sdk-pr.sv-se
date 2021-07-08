---
title: Hämta en lista över alla användarkonton för en kund
description: Hur du hämtar en lista över alla användarkonton som tillhör en av dina kunder.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f3d5fcc610eae8c1bff056c1e4a9e7a74093c87d
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874575"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="ed495-103">Hämta en lista över alla användarkonton för en kund</span><span class="sxs-lookup"><span data-stu-id="ed495-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="ed495-104">Den här artikeln beskriver hur du hämtar en lista över alla användarkonton som tillhör en av dina kunder.</span><span class="sxs-lookup"><span data-stu-id="ed495-104">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="ed495-105">Information om hur du söker efter ett användarkonto efter ID finns [i Hämta ett användarkonto efter ID.](get-a-user-account-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="ed495-105">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed495-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ed495-106">Prerequisites</span></span>

- <span data-ttu-id="ed495-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ed495-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ed495-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ed495-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ed495-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ed495-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ed495-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ed495-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ed495-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="ed495-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ed495-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="ed495-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ed495-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="ed495-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ed495-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ed495-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ed495-115">C\#</span><span class="sxs-lookup"><span data-stu-id="ed495-115">C\#</span></span>

<span data-ttu-id="ed495-116">Så här hämtar du samlingen med alla användarkonton för en angiven kund:</span><span class="sxs-lookup"><span data-stu-id="ed495-116">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="ed495-117">Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det angivna kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="ed495-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="ed495-118">Anropa metoden [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="ed495-118">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="ed495-119">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="ed495-119">For an example, see the following:</span></span>

- <span data-ttu-id="ed495-120">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ed495-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ed495-121">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="ed495-121">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="ed495-122">Klass: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="ed495-122">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="ed495-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ed495-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ed495-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ed495-124">Request syntax</span></span>

| <span data-ttu-id="ed495-125">Metod</span><span class="sxs-lookup"><span data-stu-id="ed495-125">Method</span></span>  | <span data-ttu-id="ed495-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ed495-126">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="ed495-127">**Få**</span><span class="sxs-lookup"><span data-stu-id="ed495-127">**GET**</span></span> | <span data-ttu-id="ed495-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ed495-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="ed495-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ed495-129">URI parameter</span></span>

<span data-ttu-id="ed495-130">Använd följande URI-parameter för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="ed495-130">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="ed495-131">Namn</span><span class="sxs-lookup"><span data-stu-id="ed495-131">Name</span></span>                   | <span data-ttu-id="ed495-132">Typ</span><span class="sxs-lookup"><span data-stu-id="ed495-132">Type</span></span>     | <span data-ttu-id="ed495-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ed495-133">Required</span></span> | <span data-ttu-id="ed495-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ed495-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ed495-135">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="ed495-135">**customer-tenant-id**</span></span> | <span data-ttu-id="ed495-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="ed495-136">**guid**</span></span> | <span data-ttu-id="ed495-137">Y</span><span class="sxs-lookup"><span data-stu-id="ed495-137">Y</span></span>        | <span data-ttu-id="ed495-138">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="ed495-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ed495-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ed495-139">Request headers</span></span>

<span data-ttu-id="ed495-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ed495-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ed495-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ed495-141">Request body</span></span>

<span data-ttu-id="ed495-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="ed495-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ed495-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ed495-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ed495-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ed495-144">REST response</span></span>

<span data-ttu-id="ed495-145">Om det lyckas returnerar den här metoden en samling användarkonton för en kund.</span><span class="sxs-lookup"><span data-stu-id="ed495-145">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ed495-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ed495-146">Response success and error codes</span></span>

<span data-ttu-id="ed495-147">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ed495-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ed495-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ed495-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ed495-149">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ed495-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ed495-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ed495-150">Response example</span></span>

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
