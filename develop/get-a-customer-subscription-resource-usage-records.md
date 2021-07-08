---
title: Hämta användningsdata för prenumeration efter resurs
description: Du kan använda resursen ResourceUsageRecord för att hämta en kunds resursanvändningsposter för specifika Azure-tjänster eller -resurser under den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50edb9de1d09363b242c080a76c683732f05a5de
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874847"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="15a69-103">Hämta användningsdata för prenumeration efter resurs</span><span class="sxs-lookup"><span data-stu-id="15a69-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="15a69-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="15a69-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="15a69-105">I den här artikeln beskrivs hur du hämtar **resursen ResourceUsageRecord.**</span><span class="sxs-lookup"><span data-stu-id="15a69-105">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="15a69-106">Den här resursen representerar en aggregerad summa för månaden för enskilda resurser som etablerats i din Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="15a69-106">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="15a69-107">Du kan använda den här resursen för att hämta en kunds resursanvändningsposter för specifika Azure-tjänster eller -resurser under den aktuella faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="15a69-107">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="15a69-108">Det här API:et returnerar data som inte var tillgängliga tidigare via Api:er för Azure-utgifter.</span><span class="sxs-lookup"><span data-stu-id="15a69-108">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="15a69-109">*Den här vägen stöder inte Microsoft Azure prenumerationer (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="15a69-109">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15a69-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="15a69-110">Prerequisites</span></span>

- <span data-ttu-id="15a69-111">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="15a69-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="15a69-112">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="15a69-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="15a69-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="15a69-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="15a69-114">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="15a69-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="15a69-115">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="15a69-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="15a69-116">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="15a69-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="15a69-117">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="15a69-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="15a69-118">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="15a69-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="15a69-119">En prenumerationsidentifierare</span><span class="sxs-lookup"><span data-stu-id="15a69-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="15a69-120">C\#</span><span class="sxs-lookup"><span data-stu-id="15a69-120">C\#</span></span>

<span data-ttu-id="15a69-121">Så här hämtar du resursanvändningsposter för en kund för en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden:</span><span class="sxs-lookup"><span data-stu-id="15a69-121">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="15a69-122">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="15a69-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="15a69-123">Anropa egenskapen Prenumerationer och **UsageRecords** och sedan **egenskapen** Resurser.</span><span class="sxs-lookup"><span data-stu-id="15a69-123">Call the Subscriptions property and **UsageRecords**, and then the **Resources** property.</span></span> <span data-ttu-id="15a69-124">Slutför genom att anropa metoderna Get() eller GetAsync().</span><span class="sxs-lookup"><span data-stu-id="15a69-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="15a69-125">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="15a69-125">For an example, see the following:</span></span>

- <span data-ttu-id="15a69-126">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="15a69-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="15a69-127">Project: **PartnerSDK.FeatureExempel**</span><span class="sxs-lookup"><span data-stu-id="15a69-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="15a69-128">Klass: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="15a69-128">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="15a69-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="15a69-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="15a69-130">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="15a69-130">Request syntax</span></span>

| <span data-ttu-id="15a69-131">Metod</span><span class="sxs-lookup"><span data-stu-id="15a69-131">Method</span></span>  | <span data-ttu-id="15a69-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="15a69-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="15a69-133">**Få**</span><span class="sxs-lookup"><span data-stu-id="15a69-133">**GET**</span></span> | <span data-ttu-id="15a69-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="15a69-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="15a69-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="15a69-135">URI parameters</span></span>

<span data-ttu-id="15a69-136">I den här tabellen visas de frågeparametrar som krävs för att hämta kundens klassificerade användningsinformation.</span><span class="sxs-lookup"><span data-stu-id="15a69-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="15a69-137">Namn</span><span class="sxs-lookup"><span data-stu-id="15a69-137">Name</span></span>                   | <span data-ttu-id="15a69-138">Typ</span><span class="sxs-lookup"><span data-stu-id="15a69-138">Type</span></span>     | <span data-ttu-id="15a69-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="15a69-139">Required</span></span> | <span data-ttu-id="15a69-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="15a69-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="15a69-141">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="15a69-141">**customer-tenant-id**</span></span> | <span data-ttu-id="15a69-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="15a69-142">**guid**</span></span> | <span data-ttu-id="15a69-143">Y</span><span class="sxs-lookup"><span data-stu-id="15a69-143">Y</span></span>        | <span data-ttu-id="15a69-144">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="15a69-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="15a69-145">**prenumerations-id**</span><span class="sxs-lookup"><span data-stu-id="15a69-145">**subscription-id**</span></span>    | <span data-ttu-id="15a69-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="15a69-146">**guid**</span></span> | <span data-ttu-id="15a69-147">Y</span><span class="sxs-lookup"><span data-stu-id="15a69-147">Y</span></span>        | <span data-ttu-id="15a69-148">Ett GUID som motsvarar identifieraren [](subscription-resources.md#subscription)för en Partner Center-prenumerationsresurs , som representerar en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="15a69-148">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="15a69-149">*För prenumerationsresurser för **Azure-prenumeration anger du plan-id som** **prenumerations-ID i** den här vägen.*</span><span class="sxs-lookup"><span data-stu-id="15a69-149">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="15a69-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="15a69-150">Request headers</span></span>

<span data-ttu-id="15a69-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="15a69-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="15a69-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="15a69-152">Request body</span></span>

<span data-ttu-id="15a69-153">Inga.</span><span class="sxs-lookup"><span data-stu-id="15a69-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="15a69-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="15a69-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="15a69-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="15a69-155">REST response</span></span>

<span data-ttu-id="15a69-156">Om det lyckas returnerar den här metoden **en PagedResourceCollection-resurs \<ResourceUsageRecord>** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="15a69-156">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="15a69-157">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="15a69-157">Response success and error codes</span></span>

<span data-ttu-id="15a69-158">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="15a69-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="15a69-159">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="15a69-159">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="15a69-160">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="15a69-160">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="15a69-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="15a69-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
