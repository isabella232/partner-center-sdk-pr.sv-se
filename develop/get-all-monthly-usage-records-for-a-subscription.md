---
title: Hämta alla månatliga användnings poster för en prenumeration.
description: Du kan använda AzureResourceMonthlyUsageRecord-resurs samlingen för att hämta en lista över tjänster i en kunds prenumeration och deras associerade användnings information.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1dd09d4976c9626e088cda02ce36669dd7121a99
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769735"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="d3ac3-103">Hämta alla månatliga användnings poster för en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-103">Get all monthly usage records for a subscription.</span></span>

<span data-ttu-id="d3ac3-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-104">**Applies to:**</span></span>

- <span data-ttu-id="d3ac3-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d3ac3-105">Partner Center</span></span>
- <span data-ttu-id="d3ac3-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="d3ac3-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d3ac3-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d3ac3-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d3ac3-108">Du kan använda [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) -resurs samlingen för att hämta en lista över tjänster i en kunds prenumeration och deras associerade användnings information.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-108">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3ac3-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d3ac3-109">Prerequisites</span></span>

- <span data-ttu-id="d3ac3-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d3ac3-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d3ac3-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d3ac3-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d3ac3-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d3ac3-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d3ac3-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d3ac3-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d3ac3-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="d3ac3-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d3ac3-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d3ac3-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d3ac3-118">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-118">A subscription identifier.</span></span>

<span data-ttu-id="d3ac3-119">*Detta API stöder bara Microsoft Azure (MS-AZR-0145P)-prenumerationer. Om du använder en Azure-plan läser du i stället [Hämta användnings data för prenumeration efter mätare](get-a-customer-subscription-meter-usage-records.md) .*</span><span class="sxs-lookup"><span data-stu-id="d3ac3-119">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="d3ac3-120">C\#</span><span class="sxs-lookup"><span data-stu-id="d3ac3-120">C\#</span></span>

<span data-ttu-id="d3ac3-121">Så här hämtar du en prenumerations resursanvändnings information:</span><span class="sxs-lookup"><span data-stu-id="d3ac3-121">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="d3ac3-122">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="d3ac3-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="d3ac3-123">Anropa egenskapen **Subscriptions** , och **UsageRecords**, sedan egenskapen **Resources** .</span><span class="sxs-lookup"><span data-stu-id="d3ac3-123">Call the **Subscriptions** property, as well as **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="d3ac3-124">Anropa metoderna **Get ()** eller **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="d3ac3-124">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="d3ac3-125">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="d3ac3-125">For an example, see the following:</span></span>

- <span data-ttu-id="d3ac3-126">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d3ac3-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d3ac3-127">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="d3ac3-128">Klass: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-128">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d3ac3-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d3ac3-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d3ac3-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d3ac3-130">Request syntax</span></span>

| <span data-ttu-id="d3ac3-131">Metod</span><span class="sxs-lookup"><span data-stu-id="d3ac3-131">Method</span></span>  | <span data-ttu-id="d3ac3-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d3ac3-132">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d3ac3-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-133">**GET**</span></span> | <span data-ttu-id="d3ac3-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/usagerecords/Resources http/1.1</span><span class="sxs-lookup"><span data-stu-id="d3ac3-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="d3ac3-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="d3ac3-135">URI parameters</span></span>

<span data-ttu-id="d3ac3-136">Den här tabellen innehåller de frågeparametrar som krävs för att hämta information om den angivna användningen.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-136">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="d3ac3-137">Namn</span><span class="sxs-lookup"><span data-stu-id="d3ac3-137">Name</span></span>                    | <span data-ttu-id="d3ac3-138">Typ</span><span class="sxs-lookup"><span data-stu-id="d3ac3-138">Type</span></span>     | <span data-ttu-id="d3ac3-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d3ac3-139">Required</span></span> | <span data-ttu-id="d3ac3-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d3ac3-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="d3ac3-141">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="d3ac3-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-142">**guid**</span></span> | <span data-ttu-id="d3ac3-143">Y</span><span class="sxs-lookup"><span data-stu-id="d3ac3-143">Y</span></span>        | <span data-ttu-id="d3ac3-144">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="d3ac3-145">**prenumerations-ID**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-145">**subscription-id**</span></span> | <span data-ttu-id="d3ac3-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="d3ac3-146">**guid**</span></span> | <span data-ttu-id="d3ac3-147">Y</span><span class="sxs-lookup"><span data-stu-id="d3ac3-147">Y</span></span>        | <span data-ttu-id="d3ac3-148">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d3ac3-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d3ac3-149">Request headers</span></span>

<span data-ttu-id="d3ac3-150">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d3ac3-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d3ac3-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d3ac3-151">Request body</span></span>

<span data-ttu-id="d3ac3-152">Inga.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d3ac3-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d3ac3-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="d3ac3-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d3ac3-154">REST response</span></span>

<span data-ttu-id="d3ac3-155">Om det lyckas returnerar den här metoden en samling **AzureResourceMonthlyUsageRecord** -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-155">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d3ac3-156">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d3ac3-156">Response success and error codes</span></span>

<span data-ttu-id="d3ac3-157">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d3ac3-158">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d3ac3-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d3ac3-159">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d3ac3-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d3ac3-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d3ac3-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
