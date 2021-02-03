---
title: Hämta användningsdata för prenumeration efter resurs
description: Du kan använda ResourceUsageRecord-resursen för att hämta en kunds resurs användnings poster för specifika Azure-tjänster eller resurser under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769141"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="67f16-103">Hämta användningsdata för prenumeration efter resurs</span><span class="sxs-lookup"><span data-stu-id="67f16-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="67f16-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="67f16-104">**Applies to:**</span></span>

- <span data-ttu-id="67f16-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="67f16-105">Partner Center</span></span>
- <span data-ttu-id="67f16-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="67f16-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="67f16-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="67f16-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="67f16-108">Den här artikeln beskriver hur du hämtar **ResourceUsageRecord** -resursen.</span><span class="sxs-lookup"><span data-stu-id="67f16-108">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="67f16-109">Den här resursen representerar en sammanställd total summa för månaden för enskilda resurser som har skapats i din Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="67f16-109">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="67f16-110">Du kan använda den här resursen för att hämta en kunds resurs användnings poster för specifika Azure-tjänster eller resurser under den aktuella fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="67f16-110">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="67f16-111">Detta API returnerar data som inte var tillgängliga tidigare via API: er för Azure-utgifter.</span><span class="sxs-lookup"><span data-stu-id="67f16-111">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="67f16-112">*Den här vägen stöder inte Microsoft Azure-prenumerationer (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="67f16-112">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67f16-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="67f16-113">Prerequisites</span></span>

- <span data-ttu-id="67f16-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="67f16-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="67f16-115">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="67f16-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="67f16-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="67f16-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="67f16-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="67f16-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="67f16-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="67f16-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="67f16-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="67f16-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="67f16-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="67f16-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="67f16-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="67f16-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="67f16-122">Ett prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="67f16-122">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="67f16-123">C\#</span><span class="sxs-lookup"><span data-stu-id="67f16-123">C\#</span></span>

<span data-ttu-id="67f16-124">Så här hämtar du resurs användnings poster för en kund för en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden:</span><span class="sxs-lookup"><span data-stu-id="67f16-124">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="67f16-125">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="67f16-125">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="67f16-126">Anropa egenskapen Subscriptions, och **UsageRecords**, sedan egenskapen **Resources** .</span><span class="sxs-lookup"><span data-stu-id="67f16-126">Call the Subscriptions property, as well as **UsageRecords**, then the **Resources** property.</span></span> <span data-ttu-id="67f16-127">Slutför genom att anropa metoderna Get () eller GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="67f16-127">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="67f16-128">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="67f16-128">For an example, see the following:</span></span>

- <span data-ttu-id="67f16-129">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="67f16-129">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="67f16-130">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="67f16-130">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="67f16-131">Klass: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="67f16-131">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="67f16-132">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="67f16-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="67f16-133">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="67f16-133">Request syntax</span></span>

| <span data-ttu-id="67f16-134">Metod</span><span class="sxs-lookup"><span data-stu-id="67f16-134">Method</span></span>  | <span data-ttu-id="67f16-135">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="67f16-135">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="67f16-136">**TA**</span><span class="sxs-lookup"><span data-stu-id="67f16-136">**GET**</span></span> | <span data-ttu-id="67f16-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/resourceusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="67f16-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="67f16-138">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="67f16-138">URI parameters</span></span>

<span data-ttu-id="67f16-139">Den här tabellen innehåller de frågeparametrar som krävs för att hämta kundens beräknade användnings information.</span><span class="sxs-lookup"><span data-stu-id="67f16-139">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="67f16-140">Namn</span><span class="sxs-lookup"><span data-stu-id="67f16-140">Name</span></span>                   | <span data-ttu-id="67f16-141">Typ</span><span class="sxs-lookup"><span data-stu-id="67f16-141">Type</span></span>     | <span data-ttu-id="67f16-142">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="67f16-142">Required</span></span> | <span data-ttu-id="67f16-143">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="67f16-143">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="67f16-144">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="67f16-144">**customer-tenant-id**</span></span> | <span data-ttu-id="67f16-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="67f16-145">**guid**</span></span> | <span data-ttu-id="67f16-146">Y</span><span class="sxs-lookup"><span data-stu-id="67f16-146">Y</span></span>        | <span data-ttu-id="67f16-147">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="67f16-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="67f16-148">**prenumerations-ID**</span><span class="sxs-lookup"><span data-stu-id="67f16-148">**subscription-id**</span></span>    | <span data-ttu-id="67f16-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="67f16-149">**guid**</span></span> | <span data-ttu-id="67f16-150">Y</span><span class="sxs-lookup"><span data-stu-id="67f16-150">Y</span></span>        | <span data-ttu-id="67f16-151">Ett GUID som motsvarar ID: t för en [prenumerations resurs](subscription-resources.md#subscription)för partner Center, som representerar en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="67f16-151">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="67f16-152">*För prenumerations resurser i Azure plan anger du **plan-ID** som **prenumerations-ID** i den här vägen.*</span><span class="sxs-lookup"><span data-stu-id="67f16-152">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="67f16-153">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="67f16-153">Request headers</span></span>

<span data-ttu-id="67f16-154">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="67f16-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="67f16-155">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="67f16-155">Request body</span></span>

<span data-ttu-id="67f16-156">Inga.</span><span class="sxs-lookup"><span data-stu-id="67f16-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="67f16-157">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="67f16-157">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="67f16-158">REST-svar</span><span class="sxs-lookup"><span data-stu-id="67f16-158">REST response</span></span>

<span data-ttu-id="67f16-159">Om det lyckas returnerar den här metoden **en \<ResourceUsageRecord> PagedResourceCollection** -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="67f16-159">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="67f16-160">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="67f16-160">Response success and error codes</span></span>

<span data-ttu-id="67f16-161">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="67f16-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="67f16-162">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="67f16-162">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="67f16-163">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="67f16-163">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="67f16-164">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="67f16-164">Response example</span></span>

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
