---
title: Hämta alla prenumerationsanvändningsposter för en kund
description: Du kan använda resurssamlingen SubscriptionMonthlyUsageRecord för att hämta prenumerationsanvändningsposter för en kund för en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 976abd86f34c1c27184f277ffc89fbc65f16bb37
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874694"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="7bf5e-103">Hämta prenumerationsanvändningsposter för en kund</span><span class="sxs-lookup"><span data-stu-id="7bf5e-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="7bf5e-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7bf5e-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7bf5e-105">Du kan använda **resurssamlingen SubscriptionMonthlyUsageRecord** för att hämta prenumerationsanvändningsposter för en kund för en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-105">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="7bf5e-106">Den här resursen representerar alla prenumerationer för kunden.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-106">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="7bf5e-107">För en kund med en Azure-plan returnerar den här resursen en lista över dessa planer (inte enskilda Azure-prenumerationer).</span><span class="sxs-lookup"><span data-stu-id="7bf5e-107">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bf5e-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7bf5e-108">Prerequisites</span></span>

- <span data-ttu-id="7bf5e-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7bf5e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7bf5e-110">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7bf5e-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7bf5e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7bf5e-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="7bf5e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7bf5e-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7bf5e-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7bf5e-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7bf5e-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7bf5e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7bf5e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7bf5e-117">C\#</span></span>

<span data-ttu-id="7bf5e-118">Hämta användningsposter för prenumerationer för en kund för en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden genom att göra följande:</span><span class="sxs-lookup"><span data-stu-id="7bf5e-118">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period, do the following steps:</span></span>

1. <span data-ttu-id="7bf5e-119">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="7bf5e-120">Anropa sedan egenskapen **Prenumerationer** och **egenskapen UsageRecords.**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-120">Then call the **Subscriptions** property and the **UsageRecords** property.</span></span> <span data-ttu-id="7bf5e-121">Slutför genom att anropa metoderna Get() eller GetAsync().</span><span class="sxs-lookup"><span data-stu-id="7bf5e-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="7bf5e-122">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="7bf5e-122">For an example, see the following:</span></span>

- <span data-ttu-id="7bf5e-123">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7bf5e-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7bf5e-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="7bf5e-125">Klass: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-125">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7bf5e-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7bf5e-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7bf5e-127">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="7bf5e-127">Request syntax</span></span>

| <span data-ttu-id="7bf5e-128">Metod</span><span class="sxs-lookup"><span data-stu-id="7bf5e-128">Method</span></span>  | <span data-ttu-id="7bf5e-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7bf5e-129">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7bf5e-130">**Få**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-130">**GET**</span></span> | <span data-ttu-id="7bf5e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7bf5e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="7bf5e-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="7bf5e-132">URI parameter</span></span>

<span data-ttu-id="7bf5e-133">I den här tabellen visas den frågeparameter som krävs för att hämta kundens klassificerade användningsinformation.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="7bf5e-134">Namn</span><span class="sxs-lookup"><span data-stu-id="7bf5e-134">Name</span></span>                   | <span data-ttu-id="7bf5e-135">Typ</span><span class="sxs-lookup"><span data-stu-id="7bf5e-135">Type</span></span>     | <span data-ttu-id="7bf5e-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7bf5e-136">Required</span></span> | <span data-ttu-id="7bf5e-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7bf5e-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="7bf5e-138">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-138">**customer-tenant-id**</span></span> | <span data-ttu-id="7bf5e-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-139">**guid**</span></span> | <span data-ttu-id="7bf5e-140">Y</span><span class="sxs-lookup"><span data-stu-id="7bf5e-140">Y</span></span>        | <span data-ttu-id="7bf5e-141">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7bf5e-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7bf5e-142">Request headers</span></span>

<span data-ttu-id="7bf5e-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7bf5e-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7bf5e-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7bf5e-144">Request body</span></span>

<span data-ttu-id="7bf5e-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7bf5e-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7bf5e-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="7bf5e-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7bf5e-147">REST response</span></span>

<span data-ttu-id="7bf5e-148">Om det lyckas returnerar den här metoden **en SubscriptionMonthlyUsageRecord-resurs** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-148">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7bf5e-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7bf5e-149">Response success and error codes</span></span>

<span data-ttu-id="7bf5e-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7bf5e-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="7bf5e-152">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7bf5e-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="7bf5e-153">Svarsexempel Microsoft Azure prenumerationer (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="7bf5e-153">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="7bf5e-154">I det här exemplet köpte kunden ett **145P Azure PayG-erbjudande.**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="7bf5e-155">*För kunder med Microsoft Azure prenumerationer (MS-AZR-0145P) ändras inte API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="7bf5e-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="7bf5e-156">REST-svarsexempel för Azure-plan</span><span class="sxs-lookup"><span data-stu-id="7bf5e-156">REST response example for Azure plan</span></span>

<span data-ttu-id="7bf5e-157">I det här exemplet köpte kunden en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="7bf5e-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="7bf5e-158">*För kunder med Azure-planer finns följande ändringar i API-svaret:*</span><span class="sxs-lookup"><span data-stu-id="7bf5e-158">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="7bf5e-159">**currencyLocale** ersätts med **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="7bf5e-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="7bf5e-160">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="7bf5e-160">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 2,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-7d58-6654-69fa-0797198155d3",
            "id": "11111111-7d58-6654-69fa-0797198155d3",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        },
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "id": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
