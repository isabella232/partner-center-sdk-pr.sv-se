---
title: Hämta alla månatliga användningsposter för en prenumeration
description: Du kan använda resurssamlingen AzureResourceMonthlyUsageRecord för att hämta en lista över tjänster i en kunds prenumeration och deras associerade klassificerade användningsinformation.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ee4bd413eec7d5a2dddbe3803df8839589ab7504
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760291"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="a49f2-103">Hämta alla månatliga användningsposter för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="a49f2-103">Get all monthly usage records for a subscription</span></span>

<span data-ttu-id="a49f2-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a49f2-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a49f2-105">Du kan använda [**resurssamlingen AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) för att hämta en lista över tjänster i en kunds prenumeration och deras associerade klassificerade användningsinformation.</span><span class="sxs-lookup"><span data-stu-id="a49f2-105">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a49f2-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a49f2-106">Prerequisites</span></span>

- <span data-ttu-id="a49f2-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a49f2-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a49f2-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a49f2-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a49f2-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a49f2-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a49f2-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a49f2-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a49f2-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="a49f2-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a49f2-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="a49f2-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a49f2-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="a49f2-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a49f2-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a49f2-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a49f2-115">En prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="a49f2-115">A subscription identifier.</span></span>

<span data-ttu-id="a49f2-116">*Det här API:et stöder Microsoft Azure prenumerationer (MS-AZR-0145P). Om du använder en Azure-plan kan du läsa [Hämta användningsdata för prenumeration per mätare i](get-a-customer-subscription-meter-usage-records.md) stället.*</span><span class="sxs-lookup"><span data-stu-id="a49f2-116">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="a49f2-117">C\#</span><span class="sxs-lookup"><span data-stu-id="a49f2-117">C\#</span></span>

<span data-ttu-id="a49f2-118">Så här hämtar du information om prenumerationens resursanvändning:</span><span class="sxs-lookup"><span data-stu-id="a49f2-118">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="a49f2-119">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="a49f2-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="a49f2-120">Anropa egenskapen **Prenumerationer** och **UsageRecords** och sedan **egenskapen** Resurser.</span><span class="sxs-lookup"><span data-stu-id="a49f2-120">Call the **Subscriptions** property, and **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="a49f2-121">Anropa metoderna **Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="a49f2-121">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="a49f2-122">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="a49f2-122">For an example, see the following:</span></span>

- <span data-ttu-id="a49f2-123">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a49f2-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a49f2-124">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="a49f2-124">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="a49f2-125">Klass: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="a49f2-125">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="a49f2-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a49f2-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a49f2-127">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="a49f2-127">Request syntax</span></span>

| <span data-ttu-id="a49f2-128">Metod</span><span class="sxs-lookup"><span data-stu-id="a49f2-128">Method</span></span>  | <span data-ttu-id="a49f2-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a49f2-129">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a49f2-130">**Få**</span><span class="sxs-lookup"><span data-stu-id="a49f2-130">**GET**</span></span> | <span data-ttu-id="a49f2-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a49f2-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a49f2-132">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="a49f2-132">URI parameters</span></span>

<span data-ttu-id="a49f2-133">I den här tabellen visas de frågeparametrar som krävs för att hämta den klassificerade användningsinformationen.</span><span class="sxs-lookup"><span data-stu-id="a49f2-133">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="a49f2-134">Namn</span><span class="sxs-lookup"><span data-stu-id="a49f2-134">Name</span></span>                    | <span data-ttu-id="a49f2-135">Typ</span><span class="sxs-lookup"><span data-stu-id="a49f2-135">Type</span></span>     | <span data-ttu-id="a49f2-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a49f2-136">Required</span></span> | <span data-ttu-id="a49f2-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a49f2-137">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="a49f2-138">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="a49f2-138">**customer-tenant-id**</span></span>  | <span data-ttu-id="a49f2-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="a49f2-139">**guid**</span></span> | <span data-ttu-id="a49f2-140">Y</span><span class="sxs-lookup"><span data-stu-id="a49f2-140">Y</span></span>        | <span data-ttu-id="a49f2-141">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="a49f2-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="a49f2-142">**prenumerations-id**</span><span class="sxs-lookup"><span data-stu-id="a49f2-142">**subscription-id**</span></span> | <span data-ttu-id="a49f2-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="a49f2-143">**guid**</span></span> | <span data-ttu-id="a49f2-144">Y</span><span class="sxs-lookup"><span data-stu-id="a49f2-144">Y</span></span>        | <span data-ttu-id="a49f2-145">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="a49f2-145">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a49f2-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a49f2-146">Request headers</span></span>

<span data-ttu-id="a49f2-147">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a49f2-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a49f2-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a49f2-148">Request body</span></span>

<span data-ttu-id="a49f2-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="a49f2-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a49f2-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a49f2-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="a49f2-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a49f2-151">REST response</span></span>

<span data-ttu-id="a49f2-152">Om det lyckas returnerar den här metoden en samling **AzureResourceMonthlyUsageRecord-resurser** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="a49f2-152">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a49f2-153">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a49f2-153">Response success and error codes</span></span>

<span data-ttu-id="a49f2-154">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="a49f2-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a49f2-155">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a49f2-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a49f2-156">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a49f2-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a49f2-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a49f2-157">Response example</span></span>

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
