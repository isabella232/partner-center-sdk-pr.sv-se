---
title: Uppdatera en kunds förbruknings utgifts budget
description: Uppdatera utgifts budgeten som har allokerats för kundens användning.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 839305fb8fad3ce2442ab93e1d8a4a170b4d41c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769759"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="dae89-103">Uppdatera en kunds förbruknings utgifts budget</span><span class="sxs-lookup"><span data-stu-id="dae89-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="dae89-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="dae89-104">**Applies To**</span></span>

- <span data-ttu-id="dae89-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="dae89-105">Partner Center</span></span>
- <span data-ttu-id="dae89-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="dae89-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="dae89-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="dae89-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="dae89-108">Uppdatera [utgifts budgeten](customer-usage-resources.md#customerusagesummary) som har allokerats för kundens användning.</span><span class="sxs-lookup"><span data-stu-id="dae89-108">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dae89-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="dae89-109">Prerequisites</span></span>

- <span data-ttu-id="dae89-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dae89-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dae89-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="dae89-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="dae89-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dae89-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="dae89-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="dae89-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="dae89-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="dae89-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="dae89-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="dae89-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="dae89-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="dae89-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="dae89-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dae89-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="dae89-118">C\#</span><span class="sxs-lookup"><span data-stu-id="dae89-118">C\#</span></span>

<span data-ttu-id="dae89-119">Om du vill uppdatera en kunds förbruknings utgifts budget måste du först skapa ett nytt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) -objekt med den uppdaterade mängden.</span><span class="sxs-lookup"><span data-stu-id="dae89-119">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="dae89-120">Använd sedan [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) -samlingen och anropa [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) -metoden med det angivna kund-ID: t.</span><span class="sxs-lookup"><span data-stu-id="dae89-120">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="dae89-121">Öppna sedan egenskapen [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) och skicka den uppdaterade användnings budgeten till [**patch ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) eller [**PatchAsync ()-**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) metoden.</span><span class="sxs-lookup"><span data-stu-id="dae89-121">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="dae89-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="dae89-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dae89-123">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="dae89-123">Request syntax</span></span>

| <span data-ttu-id="dae89-124">Metod</span><span class="sxs-lookup"><span data-stu-id="dae89-124">Method</span></span>    | <span data-ttu-id="dae89-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="dae89-125">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dae89-126">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="dae89-126">**PATCH**</span></span> | <span data-ttu-id="dae89-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagebudget http/1.1</span><span class="sxs-lookup"><span data-stu-id="dae89-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="dae89-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="dae89-128">URI parameter</span></span>

<span data-ttu-id="dae89-129">Använd följande frågeparameter för att uppdatera fakturerings profilen.</span><span class="sxs-lookup"><span data-stu-id="dae89-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="dae89-130">Namn</span><span class="sxs-lookup"><span data-stu-id="dae89-130">Name</span></span>                   | <span data-ttu-id="dae89-131">Typ</span><span class="sxs-lookup"><span data-stu-id="dae89-131">Type</span></span>     | <span data-ttu-id="dae89-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="dae89-132">Required</span></span> | <span data-ttu-id="dae89-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="dae89-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dae89-134">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="dae89-134">**customer-tenant-id**</span></span> | <span data-ttu-id="dae89-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="dae89-135">**guid**</span></span> | <span data-ttu-id="dae89-136">Y</span><span class="sxs-lookup"><span data-stu-id="dae89-136">Y</span></span>        | <span data-ttu-id="dae89-137">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="dae89-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dae89-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="dae89-138">Request headers</span></span>

<span data-ttu-id="dae89-139">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dae89-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dae89-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="dae89-140">Request body</span></span>

<span data-ttu-id="dae89-141">Den fullständiga resursen.</span><span class="sxs-lookup"><span data-stu-id="dae89-141">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="dae89-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="dae89-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="dae89-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="dae89-143">REST response</span></span>

<span data-ttu-id="dae89-144">Om det lyckas returnerar den här metoden en användares utgifts budget med den uppdaterade mängden.</span><span class="sxs-lookup"><span data-stu-id="dae89-144">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dae89-145">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="dae89-145">Response success and error codes</span></span>

<span data-ttu-id="dae89-146">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="dae89-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dae89-147">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="dae89-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dae89-148">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dae89-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dae89-149">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="dae89-149">Response example</span></span>

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
