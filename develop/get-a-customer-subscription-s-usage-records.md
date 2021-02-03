---
title: Hämta alla prenumerationsanvändningsposter för en kund
description: Du kan använda SubscriptionMonthlyUsageRecord-resurs samlingen för att hämta prenumerations användnings poster för en kund av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 765ea16ff58b462d83ae3b8764b8b34c3ef804dc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769144"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="5ee1a-103">Hämta prenumerations användnings poster för en kund</span><span class="sxs-lookup"><span data-stu-id="5ee1a-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="5ee1a-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="5ee1a-104">**Applies to:**</span></span>

- <span data-ttu-id="5ee1a-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="5ee1a-105">Partner Center</span></span>
- <span data-ttu-id="5ee1a-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="5ee1a-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5ee1a-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5ee1a-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5ee1a-108">Du kan använda **SubscriptionMonthlyUsageRecord** -resurs samlingen för att hämta prenumerations användnings poster för en kund av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-108">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="5ee1a-109">Den här resursen representerar alla prenumerationer för kunden.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-109">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="5ee1a-110">För en kund med en Azure-plan returnerar den här resursen en lista över dessa planer (inte enskilda Azure-prenumerationer).</span><span class="sxs-lookup"><span data-stu-id="5ee1a-110">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ee1a-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="5ee1a-111">Prerequisites</span></span>

- <span data-ttu-id="5ee1a-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5ee1a-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5ee1a-113">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5ee1a-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5ee1a-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5ee1a-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5ee1a-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5ee1a-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5ee1a-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="5ee1a-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5ee1a-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5ee1a-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5ee1a-120">C\#</span><span class="sxs-lookup"><span data-stu-id="5ee1a-120">C\#</span></span>

<span data-ttu-id="5ee1a-121">För att hämta prenumerations användnings poster för en kund av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden.:</span><span class="sxs-lookup"><span data-stu-id="5ee1a-121">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period.:</span></span>

1. <span data-ttu-id="5ee1a-122">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="5ee1a-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="5ee1a-123">Anropa sedan egenskapen **Subscriptions** och egenskapen **UsageRecords** .</span><span class="sxs-lookup"><span data-stu-id="5ee1a-123">Then call the **Subscriptions** property, as well as **UsageRecords** property.</span></span> <span data-ttu-id="5ee1a-124">Slutför genom att anropa metoderna Get () eller GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="5ee1a-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="5ee1a-125">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="5ee1a-125">For an example, see the following:</span></span>

- <span data-ttu-id="5ee1a-126">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5ee1a-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5ee1a-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="5ee1a-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="5ee1a-128">Klass: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="5ee1a-128">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5ee1a-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="5ee1a-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5ee1a-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="5ee1a-130">Request syntax</span></span>

| <span data-ttu-id="5ee1a-131">Metod</span><span class="sxs-lookup"><span data-stu-id="5ee1a-131">Method</span></span>  | <span data-ttu-id="5ee1a-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="5ee1a-132">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5ee1a-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="5ee1a-133">**GET**</span></span> | <span data-ttu-id="5ee1a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="5ee1a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="5ee1a-135">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="5ee1a-135">URI parameter</span></span>

<span data-ttu-id="5ee1a-136">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta kundens beräknade användnings information.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-136">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="5ee1a-137">Namn</span><span class="sxs-lookup"><span data-stu-id="5ee1a-137">Name</span></span>                   | <span data-ttu-id="5ee1a-138">Typ</span><span class="sxs-lookup"><span data-stu-id="5ee1a-138">Type</span></span>     | <span data-ttu-id="5ee1a-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="5ee1a-139">Required</span></span> | <span data-ttu-id="5ee1a-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5ee1a-140">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="5ee1a-141">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="5ee1a-141">**customer-tenant-id**</span></span> | <span data-ttu-id="5ee1a-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="5ee1a-142">**guid**</span></span> | <span data-ttu-id="5ee1a-143">Y</span><span class="sxs-lookup"><span data-stu-id="5ee1a-143">Y</span></span>        | <span data-ttu-id="5ee1a-144">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-144">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5ee1a-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="5ee1a-145">Request headers</span></span>

<span data-ttu-id="5ee1a-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5ee1a-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5ee1a-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="5ee1a-147">Request body</span></span>

<span data-ttu-id="5ee1a-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5ee1a-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="5ee1a-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="5ee1a-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="5ee1a-150">REST response</span></span>

<span data-ttu-id="5ee1a-151">Om det lyckas returnerar den här metoden en **SubscriptionMonthlyUsageRecord** -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-151">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5ee1a-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="5ee1a-152">Response success and error codes</span></span>

<span data-ttu-id="5ee1a-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5ee1a-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-154">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="5ee1a-155">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5ee1a-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="5ee1a-156">Svars exempel för Microsoft Azure (MS-AZR-0145P)-prenumerationer</span><span class="sxs-lookup"><span data-stu-id="5ee1a-156">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="5ee1a-157">I det här exemplet har kunden köpt ett **145P Azure PayG** -erbjudande.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-157">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="5ee1a-158">*För kunder med Microsoft Azure-prenumerationer (MS-AZR-0145P) sker ingen ändring i API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="5ee1a-158">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="5ee1a-159">Exempel på REST-svar för Azure-prenumeration</span><span class="sxs-lookup"><span data-stu-id="5ee1a-159">REST response example for Azure plan</span></span>

<span data-ttu-id="5ee1a-160">I det här exemplet har kunden köpt en Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="5ee1a-160">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="5ee1a-161">*För kunder med Azure-planer finns följande ändringar i API-svaret:*</span><span class="sxs-lookup"><span data-stu-id="5ee1a-161">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="5ee1a-162">**currencyLocale** ersätts med **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="5ee1a-162">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="5ee1a-163">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="5ee1a-163">**usdTotalCost** is a new field</span></span>

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
