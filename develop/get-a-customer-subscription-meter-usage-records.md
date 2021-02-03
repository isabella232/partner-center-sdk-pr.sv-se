---
title: Hämta användningsdata för prenumeration efter mätare
description: Du kan använda MeterUsageRecord resurs samling för att få användnings poster för mätare för en kund för specifika Azure-tjänster eller-resurser under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769147"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="24ae7-103">Hämta användningsdata för prenumeration efter mätare</span><span class="sxs-lookup"><span data-stu-id="24ae7-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="24ae7-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="24ae7-104">**Applies to:**</span></span>

- <span data-ttu-id="24ae7-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="24ae7-105">Partner Center</span></span>
- <span data-ttu-id="24ae7-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="24ae7-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="24ae7-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="24ae7-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="24ae7-108">Du kan använda **MeterUsageRecord** resurs samling för att få användnings poster för mätare för en kund för specifika Azure-tjänster eller-resurser under den aktuella fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="24ae7-108">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="24ae7-109">Den här resurs samlingen representerar en sammanställd summa för varje mätare för den aktuella fakturerings perioden i hela Azure-planen.</span><span class="sxs-lookup"><span data-stu-id="24ae7-109">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24ae7-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="24ae7-110">Prerequisites</span></span>

- <span data-ttu-id="24ae7-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="24ae7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="24ae7-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="24ae7-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="24ae7-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="24ae7-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="24ae7-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="24ae7-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="24ae7-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="24ae7-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="24ae7-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="24ae7-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="24ae7-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="24ae7-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="24ae7-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="24ae7-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="24ae7-119">Ett prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="24ae7-119">A subscription ID</span></span>

<span data-ttu-id="24ae7-120">*Den nya vägen motsvarar `subscriptions/{subscription-id}/usagerecords/resources` , som fortsätter att fungera enbart för Microsoft Azure (MS-AZR-0145P)-prenumerationer.*</span><span class="sxs-lookup"><span data-stu-id="24ae7-120">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="24ae7-121">Den nya vägen stöder både Microsoft Azure (MS-AZR-0145P)-prenumerationer och Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="24ae7-121">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="24ae7-122">För att få den här informationen för din Azure-plan måste du växla till den nya vägen.</span><span class="sxs-lookup"><span data-stu-id="24ae7-122">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="24ae7-123">Förutom de egenskaper som anges i följande avsnitt, är svaret detsamma som den gamla vägen.</span><span class="sxs-lookup"><span data-stu-id="24ae7-123">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="24ae7-124">C\#</span><span class="sxs-lookup"><span data-stu-id="24ae7-124">C\#</span></span>

<span data-ttu-id="24ae7-125">Så här hämtar du mätar användnings poster för en kund för en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden:</span><span class="sxs-lookup"><span data-stu-id="24ae7-125">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="24ae7-126">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="24ae7-126">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="24ae7-127">Anropa egenskapen Subscriptions och **UsageRecords**, sedan egenskapen **meters** .</span><span class="sxs-lookup"><span data-stu-id="24ae7-127">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="24ae7-128">Slutför genom att anropa metoderna Get () eller GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="24ae7-128">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="24ae7-129">Ett exempel finns i följande exempel:</span><span class="sxs-lookup"><span data-stu-id="24ae7-129">For an example, see the following sample:</span></span>

- <span data-ttu-id="24ae7-130">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="24ae7-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="24ae7-131">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="24ae7-131">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="24ae7-132">Klass: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="24ae7-132">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="24ae7-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="24ae7-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="24ae7-134">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="24ae7-134">Request syntax</span></span>

| <span data-ttu-id="24ae7-135">Metod</span><span class="sxs-lookup"><span data-stu-id="24ae7-135">Method</span></span>  | <span data-ttu-id="24ae7-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="24ae7-136">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="24ae7-137">**TA**</span><span class="sxs-lookup"><span data-stu-id="24ae7-137">**GET**</span></span> | <span data-ttu-id="24ae7-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/meterusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="24ae7-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="24ae7-139">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="24ae7-139">URI parameters</span></span>

<span data-ttu-id="24ae7-140">Den här tabellen innehåller de frågeparametrar som krävs för att hämta kundens beräknade användnings information.</span><span class="sxs-lookup"><span data-stu-id="24ae7-140">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="24ae7-141">Namn</span><span class="sxs-lookup"><span data-stu-id="24ae7-141">Name</span></span>                   | <span data-ttu-id="24ae7-142">Typ</span><span class="sxs-lookup"><span data-stu-id="24ae7-142">Type</span></span>     | <span data-ttu-id="24ae7-143">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="24ae7-143">Required</span></span> | <span data-ttu-id="24ae7-144">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="24ae7-144">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="24ae7-145">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="24ae7-145">**customer-tenant-id**</span></span> | <span data-ttu-id="24ae7-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="24ae7-146">**guid**</span></span> | <span data-ttu-id="24ae7-147">Y</span><span class="sxs-lookup"><span data-stu-id="24ae7-147">Y</span></span>        | <span data-ttu-id="24ae7-148">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="24ae7-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="24ae7-149">**prenumerations-ID**</span><span class="sxs-lookup"><span data-stu-id="24ae7-149">**subscription-id**</span></span>    | <span data-ttu-id="24ae7-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="24ae7-150">**guid**</span></span> | <span data-ttu-id="24ae7-151">Y</span><span class="sxs-lookup"><span data-stu-id="24ae7-151">Y</span></span>        | <span data-ttu-id="24ae7-152">Ett GUID som motsvarar ID: t för en [prenumerations resurs](subscription-resources.md#subscription)för partner Center, som representerar en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="24ae7-152">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="24ae7-153">*För prenumerations resurser i Azure plan anger du **plan-ID** som **prenumerations-ID** i den här vägen.*</span><span class="sxs-lookup"><span data-stu-id="24ae7-153">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="24ae7-154">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="24ae7-154">Request headers</span></span>

<span data-ttu-id="24ae7-155">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="24ae7-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="24ae7-156">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="24ae7-156">Request body</span></span>

<span data-ttu-id="24ae7-157">Inga.</span><span class="sxs-lookup"><span data-stu-id="24ae7-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="24ae7-158">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="24ae7-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="24ae7-159">REST-svar</span><span class="sxs-lookup"><span data-stu-id="24ae7-159">REST response</span></span>

<span data-ttu-id="24ae7-160">Om det lyckas returnerar den här metoden **en \<MeterUsageRecord> PagedResourceCollection** -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="24ae7-160">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="24ae7-161">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="24ae7-161">Response success and error codes</span></span>

<span data-ttu-id="24ae7-162">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="24ae7-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="24ae7-163">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="24ae7-163">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="24ae7-164">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="24ae7-164">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="24ae7-165">Svars exempel för Microsoft Azure (MS-AZR-0145P)-prenumerationer</span><span class="sxs-lookup"><span data-stu-id="24ae7-165">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="24ae7-166">I det här exemplet har kunden köpt **145P Azure-PayG**.</span><span class="sxs-lookup"><span data-stu-id="24ae7-166">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="24ae7-167">*För kunder med en Microsoft Azure-prenumeration (MS-AZR-0145P) sker ingen ändring i API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="24ae7-167">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="24ae7-168">Exempel på REST-svar för Azure-prenumeration</span><span class="sxs-lookup"><span data-stu-id="24ae7-168">REST response example for Azure plan</span></span>

<span data-ttu-id="24ae7-169">I det här exemplet har kunden köpt en Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="24ae7-169">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="24ae7-170">*För kunder med Azure-planer finns följande ändringar i API-svaret:*</span><span class="sxs-lookup"><span data-stu-id="24ae7-170">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="24ae7-171">**currencyLocale** ersätts med **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="24ae7-171">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="24ae7-172">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="24ae7-172">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
