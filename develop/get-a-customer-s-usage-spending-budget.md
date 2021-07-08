---
title: Hämta en kunds utgiftsbudget för användning
description: Du kan använda en utgiftsbudget (objektet SpendingBudget) för att uppdatera en sammanfattning av kundanvändning (resursen CustomerUsageSummary).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b55f59fff7e5d7865811ecab3e901848126d31f7
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874881"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="157f3-103">Hämta en kunds utgiftsbudget för användning</span><span class="sxs-lookup"><span data-stu-id="157f3-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="157f3-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="157f3-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="157f3-105">Du kan uppdatera utgiftsbudgeten **(objektet SpendingBudget)** i sammanfattningen för [kundanvändning (resursen **CustomerUsageSummary).**](customer-usage-resources.md#customerusagesummary)</span><span class="sxs-lookup"><span data-stu-id="157f3-105">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="157f3-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="157f3-106">Prerequisites</span></span>

- <span data-ttu-id="157f3-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="157f3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="157f3-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="157f3-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="157f3-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="157f3-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="157f3-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="157f3-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="157f3-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="157f3-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="157f3-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="157f3-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="157f3-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="157f3-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="157f3-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="157f3-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="157f3-115">C\#</span><span class="sxs-lookup"><span data-stu-id="157f3-115">C\#</span></span>

<span data-ttu-id="157f3-116">Så här uppdaterar du en kunds användningsbudget:</span><span class="sxs-lookup"><span data-stu-id="157f3-116">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="157f3-117">Skapa ett nytt [**SpendingBudget-objekt**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) med det uppdaterade beloppet.</span><span class="sxs-lookup"><span data-stu-id="157f3-117">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="157f3-118">Använd [**samlingen IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) för att anropa [**Metoden ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med den angivna kundens identifierare.</span><span class="sxs-lookup"><span data-stu-id="157f3-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="157f3-119">Anropa [**metoden Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) för att hämta kundens användningsbudget.</span><span class="sxs-lookup"><span data-stu-id="157f3-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="157f3-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="157f3-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="157f3-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="157f3-121">Request syntax</span></span>

| <span data-ttu-id="157f3-122">Metod</span><span class="sxs-lookup"><span data-stu-id="157f3-122">Method</span></span>    | <span data-ttu-id="157f3-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="157f3-123">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="157f3-124">**Få**</span><span class="sxs-lookup"><span data-stu-id="157f3-124">**GET**</span></span> | <span data-ttu-id="157f3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="157f3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="157f3-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="157f3-126">URI parameter</span></span>

<span data-ttu-id="157f3-127">Använd följande frågeparameter för att uppdatera faktureringsprofilen.</span><span class="sxs-lookup"><span data-stu-id="157f3-127">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="157f3-128">Namn</span><span class="sxs-lookup"><span data-stu-id="157f3-128">Name</span></span>                   | <span data-ttu-id="157f3-129">Typ</span><span class="sxs-lookup"><span data-stu-id="157f3-129">Type</span></span>     | <span data-ttu-id="157f3-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="157f3-130">Required</span></span> | <span data-ttu-id="157f3-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="157f3-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="157f3-132">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="157f3-132">**customer-tenant-id**</span></span> | <span data-ttu-id="157f3-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="157f3-133">**guid**</span></span> | <span data-ttu-id="157f3-134">Y</span><span class="sxs-lookup"><span data-stu-id="157f3-134">Y</span></span>        | <span data-ttu-id="157f3-135">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="157f3-135">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="157f3-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="157f3-136">Request headers</span></span>

<span data-ttu-id="157f3-137">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="157f3-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="157f3-138">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="157f3-138">Request body</span></span>

<span data-ttu-id="157f3-139">Den fullständiga resursen.</span><span class="sxs-lookup"><span data-stu-id="157f3-139">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="157f3-140">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="157f3-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="157f3-141">REST-svar</span><span class="sxs-lookup"><span data-stu-id="157f3-141">REST response</span></span>

<span data-ttu-id="157f3-142">Om det lyckas returnerar den här metoden en användares utgiftsbudget med det uppdaterade beloppet.</span><span class="sxs-lookup"><span data-stu-id="157f3-142">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="157f3-143">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="157f3-143">Response success and error codes</span></span>

<span data-ttu-id="157f3-144">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="157f3-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="157f3-145">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="157f3-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="157f3-146">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="157f3-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="157f3-147">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="157f3-147">Response example</span></span>

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
