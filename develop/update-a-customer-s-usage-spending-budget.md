---
title: Uppdatera en kunds utgiftsbudget för användning
description: Uppdatera utgiftsbudgeten som allokerats för en kunds användning.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 043bd442266d081105e5e8767b6d597e89fc9e8b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529723"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="b3510-103">Uppdatera en kunds utgiftsbudget för användning</span><span class="sxs-lookup"><span data-stu-id="b3510-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="b3510-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b3510-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b3510-105">Uppdatera [utgiftsbudgeten som](customer-usage-resources.md#customerusagesummary) allokerats för en kunds användning.</span><span class="sxs-lookup"><span data-stu-id="b3510-105">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3510-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b3510-106">Prerequisites</span></span>

- <span data-ttu-id="b3510-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b3510-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b3510-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b3510-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b3510-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3510-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b3510-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b3510-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b3510-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="b3510-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b3510-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="b3510-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b3510-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="b3510-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b3510-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3510-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b3510-115">C\#</span><span class="sxs-lookup"><span data-stu-id="b3510-115">C\#</span></span>

<span data-ttu-id="b3510-116">Om du vill uppdatera en kunds användningsbudget skapar du först ett nytt [**SpendingBudget-objekt**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) med det uppdaterade beloppet.</span><span class="sxs-lookup"><span data-stu-id="b3510-116">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="b3510-117">Använd sedan [**samlingen IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) och anropa [**ById()-metoden**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med den angivna kundens ID.</span><span class="sxs-lookup"><span data-stu-id="b3510-117">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="b3510-118">Gå sedan till [**egenskapen UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) och skicka den uppdaterade användningsbudgeten till metoden [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) [**eller PatchAsync().**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync)</span><span class="sxs-lookup"><span data-stu-id="b3510-118">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```

## <a name="rest-request"></a><span data-ttu-id="b3510-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b3510-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b3510-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b3510-120">Request syntax</span></span>

| <span data-ttu-id="b3510-121">Metod</span><span class="sxs-lookup"><span data-stu-id="b3510-121">Method</span></span>    | <span data-ttu-id="b3510-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b3510-122">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3510-123">**Patch**</span><span class="sxs-lookup"><span data-stu-id="b3510-123">**PATCH**</span></span> | <span data-ttu-id="b3510-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b3510-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b3510-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="b3510-125">URI parameter</span></span>

<span data-ttu-id="b3510-126">Använd följande frågeparameter för att uppdatera faktureringsprofilen.</span><span class="sxs-lookup"><span data-stu-id="b3510-126">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="b3510-127">Namn</span><span class="sxs-lookup"><span data-stu-id="b3510-127">Name</span></span>                   | <span data-ttu-id="b3510-128">Typ</span><span class="sxs-lookup"><span data-stu-id="b3510-128">Type</span></span>     | <span data-ttu-id="b3510-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b3510-129">Required</span></span> | <span data-ttu-id="b3510-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b3510-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3510-131">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="b3510-131">**customer-tenant-id**</span></span> | <span data-ttu-id="b3510-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="b3510-132">**guid**</span></span> | <span data-ttu-id="b3510-133">Y</span><span class="sxs-lookup"><span data-stu-id="b3510-133">Y</span></span>        | <span data-ttu-id="b3510-134">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="b3510-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b3510-135">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b3510-135">Request headers</span></span>

<span data-ttu-id="b3510-136">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b3510-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b3510-137">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b3510-137">Request body</span></span>

<span data-ttu-id="b3510-138">Den fullständiga resursen.</span><span class="sxs-lookup"><span data-stu-id="b3510-138">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="b3510-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b3510-139">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```

## <a name="rest-response"></a><span data-ttu-id="b3510-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b3510-140">REST response</span></span>

<span data-ttu-id="b3510-141">Om det lyckas returnerar den här metoden en användares utgiftsbudget med det uppdaterade beloppet.</span><span class="sxs-lookup"><span data-stu-id="b3510-141">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b3510-142">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b3510-142">Response success and error codes</span></span>

<span data-ttu-id="b3510-143">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b3510-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b3510-144">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b3510-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b3510-145">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b3510-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b3510-146">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b3510-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"PATCH",
            "headers":[]
        }
    }
}
```
