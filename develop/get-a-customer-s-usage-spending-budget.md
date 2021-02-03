---
title: Hämta en kunds förbruknings utgifts budget
description: Du kan använda en utgifts budget (SpendingBudget-objektet) för att uppdatera en kund användnings Sammanfattning (CustomerUsageSummary-resursen).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8be9ceaab6b7546de8eacba1e52e8766719e5125
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769345"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="518cf-103">Hämta en kunds förbruknings utgifts budget</span><span class="sxs-lookup"><span data-stu-id="518cf-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="518cf-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="518cf-104">**Applies to:**</span></span>

- <span data-ttu-id="518cf-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="518cf-105">Partner Center</span></span>
- <span data-ttu-id="518cf-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="518cf-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="518cf-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="518cf-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="518cf-108">Du kan uppdatera utgifts budgeten ( **SpendingBudget** -objektet) i [Översikt över kund användning ( **CustomerUsageSummary** -resursen)](customer-usage-resources.md#customerusagesummary).</span><span class="sxs-lookup"><span data-stu-id="518cf-108">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="518cf-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="518cf-109">Prerequisites</span></span>

- <span data-ttu-id="518cf-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="518cf-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="518cf-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="518cf-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="518cf-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="518cf-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="518cf-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="518cf-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="518cf-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="518cf-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="518cf-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="518cf-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="518cf-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="518cf-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="518cf-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="518cf-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="518cf-118">C\#</span><span class="sxs-lookup"><span data-stu-id="518cf-118">C\#</span></span>

<span data-ttu-id="518cf-119">Så här uppdaterar du en kunds förbruknings utgifts budget:</span><span class="sxs-lookup"><span data-stu-id="518cf-119">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="518cf-120">Skapa ett nytt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) -objekt med det uppdaterade beloppet.</span><span class="sxs-lookup"><span data-stu-id="518cf-120">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="518cf-121">Använd [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) -samlingen för att anropa metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med den angivna kundens ID.</span><span class="sxs-lookup"><span data-stu-id="518cf-121">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="518cf-122">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) -metoden för att hämta kundens användnings budget.</span><span class="sxs-lookup"><span data-stu-id="518cf-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest-request"></a><span data-ttu-id="518cf-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="518cf-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="518cf-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="518cf-124">Request syntax</span></span>

| <span data-ttu-id="518cf-125">Metod</span><span class="sxs-lookup"><span data-stu-id="518cf-125">Method</span></span>    | <span data-ttu-id="518cf-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="518cf-126">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="518cf-127">**TA**</span><span class="sxs-lookup"><span data-stu-id="518cf-127">**GET**</span></span> | <span data-ttu-id="518cf-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagebudget http/1.1</span><span class="sxs-lookup"><span data-stu-id="518cf-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="518cf-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="518cf-129">URI parameter</span></span>

<span data-ttu-id="518cf-130">Använd följande frågeparameter för att uppdatera fakturerings profilen.</span><span class="sxs-lookup"><span data-stu-id="518cf-130">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="518cf-131">Namn</span><span class="sxs-lookup"><span data-stu-id="518cf-131">Name</span></span>                   | <span data-ttu-id="518cf-132">Typ</span><span class="sxs-lookup"><span data-stu-id="518cf-132">Type</span></span>     | <span data-ttu-id="518cf-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="518cf-133">Required</span></span> | <span data-ttu-id="518cf-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="518cf-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="518cf-135">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="518cf-135">**customer-tenant-id**</span></span> | <span data-ttu-id="518cf-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="518cf-136">**guid**</span></span> | <span data-ttu-id="518cf-137">Y</span><span class="sxs-lookup"><span data-stu-id="518cf-137">Y</span></span>        | <span data-ttu-id="518cf-138">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="518cf-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="518cf-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="518cf-139">Request headers</span></span>

<span data-ttu-id="518cf-140">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="518cf-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="518cf-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="518cf-141">Request body</span></span>

<span data-ttu-id="518cf-142">Den fullständiga resursen.</span><span class="sxs-lookup"><span data-stu-id="518cf-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="518cf-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="518cf-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="518cf-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="518cf-144">REST response</span></span>

<span data-ttu-id="518cf-145">Om det lyckas returnerar den här metoden en användares utgifts budget med den uppdaterade mängden.</span><span class="sxs-lookup"><span data-stu-id="518cf-145">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="518cf-146">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="518cf-146">Response success and error codes</span></span>

<span data-ttu-id="518cf-147">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="518cf-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="518cf-148">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="518cf-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="518cf-149">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="518cf-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="518cf-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="518cf-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

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
            "method":"GET",
            "headers":[]
        }
    }
}
```
