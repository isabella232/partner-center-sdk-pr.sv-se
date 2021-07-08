---
title: Hämta användningsdata för prenumeration efter mätare
description: Du kan använda resurssamlingen MeterUsageRecord för att hämta mätaranvändningsposter för en kund för specifika Azure-tjänster eller -resurser under den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0bd6143c80059bd140a4c4332ab4ec19c54d99f1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874864"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="63f36-103">Hämta användningsdata för prenumeration efter mätare</span><span class="sxs-lookup"><span data-stu-id="63f36-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="63f36-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="63f36-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="63f36-105">Du kan använda **resurssamlingen MeterUsageRecord** för att hämta mätaranvändningsposter för en kund för specifika Azure-tjänster eller -resurser under den aktuella faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="63f36-105">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="63f36-106">Den här resurssamlingen representerar en aggregerad summa för varje mätare för den aktuella faktureringsperioden i hela din Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="63f36-106">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63f36-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="63f36-107">Prerequisites</span></span>

- <span data-ttu-id="63f36-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="63f36-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="63f36-109">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="63f36-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="63f36-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63f36-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="63f36-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="63f36-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="63f36-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="63f36-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="63f36-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="63f36-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="63f36-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="63f36-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="63f36-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63f36-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="63f36-116">Ett prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="63f36-116">A subscription ID</span></span>

<span data-ttu-id="63f36-117">*Den här nya vägen motsvarar , som fortsätter att fungera endast `subscriptions/{subscription-id}/usagerecords/resources` för Microsoft Azure prenumerationer (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="63f36-117">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="63f36-118">Den här nya vägen stöder både Microsoft Azure prenumerationer (MS-AZR-0145P) och Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="63f36-118">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="63f36-119">För att få den här informationen för din Azure-plan måste du växla till den här nya vägen.</span><span class="sxs-lookup"><span data-stu-id="63f36-119">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="63f36-120">Förutom de egenskaper som anges i följande avsnitt är svaret detsamma som den gamla vägen.</span><span class="sxs-lookup"><span data-stu-id="63f36-120">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="63f36-121">C\#</span><span class="sxs-lookup"><span data-stu-id="63f36-121">C\#</span></span>

<span data-ttu-id="63f36-122">Så här hämtar du mätaranvändningsposter för en kund för en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden:</span><span class="sxs-lookup"><span data-stu-id="63f36-122">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="63f36-123">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="63f36-123">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="63f36-124">Anropa egenskapen Subscriptions och **UsageRecords** och sedan **egenskapen Meter.**</span><span class="sxs-lookup"><span data-stu-id="63f36-124">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="63f36-125">Slutför genom att anropa metoderna Get() eller GetAsync().</span><span class="sxs-lookup"><span data-stu-id="63f36-125">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="63f36-126">Ett exempel finns i följande exempel:</span><span class="sxs-lookup"><span data-stu-id="63f36-126">For an example, see the following sample:</span></span>

- <span data-ttu-id="63f36-127">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="63f36-127">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="63f36-128">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="63f36-128">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="63f36-129">Klass: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="63f36-129">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="63f36-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="63f36-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="63f36-131">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="63f36-131">Request syntax</span></span>

| <span data-ttu-id="63f36-132">Metod</span><span class="sxs-lookup"><span data-stu-id="63f36-132">Method</span></span>  | <span data-ttu-id="63f36-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="63f36-133">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="63f36-134">**Få**</span><span class="sxs-lookup"><span data-stu-id="63f36-134">**GET**</span></span> | <span data-ttu-id="63f36-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="63f36-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="63f36-136">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="63f36-136">URI parameters</span></span>

<span data-ttu-id="63f36-137">I den här tabellen visas de frågeparametrar som krävs för att hämta kundens klassificerade användningsinformation.</span><span class="sxs-lookup"><span data-stu-id="63f36-137">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="63f36-138">Namn</span><span class="sxs-lookup"><span data-stu-id="63f36-138">Name</span></span>                   | <span data-ttu-id="63f36-139">Typ</span><span class="sxs-lookup"><span data-stu-id="63f36-139">Type</span></span>     | <span data-ttu-id="63f36-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="63f36-140">Required</span></span> | <span data-ttu-id="63f36-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="63f36-141">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="63f36-142">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="63f36-142">**customer-tenant-id**</span></span> | <span data-ttu-id="63f36-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="63f36-143">**guid**</span></span> | <span data-ttu-id="63f36-144">Y</span><span class="sxs-lookup"><span data-stu-id="63f36-144">Y</span></span>        | <span data-ttu-id="63f36-145">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="63f36-145">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="63f36-146">**prenumerations-id**</span><span class="sxs-lookup"><span data-stu-id="63f36-146">**subscription-id**</span></span>    | <span data-ttu-id="63f36-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="63f36-147">**guid**</span></span> | <span data-ttu-id="63f36-148">Y</span><span class="sxs-lookup"><span data-stu-id="63f36-148">Y</span></span>        | <span data-ttu-id="63f36-149">Ett GUID som motsvarar identifieraren [](subscription-resources.md#subscription)för en Partner Center-prenumerationsresurs , som representerar en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="63f36-149">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="63f36-150">*För prenumerationsresurser för Azure-plan anger du **plan-ID:t** som **prenumerations-ID i** den här vägen.*</span><span class="sxs-lookup"><span data-stu-id="63f36-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="63f36-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="63f36-151">Request headers</span></span>

<span data-ttu-id="63f36-152">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="63f36-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="63f36-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="63f36-153">Request body</span></span>

<span data-ttu-id="63f36-154">Inga.</span><span class="sxs-lookup"><span data-stu-id="63f36-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="63f36-155">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="63f36-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="63f36-156">REST-svar</span><span class="sxs-lookup"><span data-stu-id="63f36-156">REST response</span></span>

<span data-ttu-id="63f36-157">Om det lyckas returnerar den här metoden **en PagedResourceCollection-resurs \<MeterUsageRecord>** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="63f36-157">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="63f36-158">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="63f36-158">Response success and error codes</span></span>

<span data-ttu-id="63f36-159">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="63f36-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="63f36-160">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="63f36-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="63f36-161">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="63f36-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="63f36-162">Svarsexempel Microsoft Azure prenumerationer (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="63f36-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="63f36-163">I det här exemplet köpte kunden **145P Azure PayG**.</span><span class="sxs-lookup"><span data-stu-id="63f36-163">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="63f36-164">*För kunder med en prenumeration Microsoft Azure (MS-AZR-0145P) ändras inte API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="63f36-164">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="63f36-165">REST-svarsexempel för Azure-plan</span><span class="sxs-lookup"><span data-stu-id="63f36-165">REST response example for Azure plan</span></span>

<span data-ttu-id="63f36-166">I det här exemplet köpte kunden en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="63f36-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="63f36-167">*För kunder med Azure-planer finns följande ändringar i API-svaret:*</span><span class="sxs-lookup"><span data-stu-id="63f36-167">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="63f36-168">**currencyLocale** ersätts med **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="63f36-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="63f36-169">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="63f36-169">**usdTotalCost** is a new field</span></span>

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
