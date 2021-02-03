---
title: Hämta användnings översikt för kundens prenumeration
description: Du kan använda SubscriptionUsageSummary-resursen för att få en översikt över en prenumerations användning av en viss Azure-tjänst eller resurs under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769138"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="ad58d-103">Hämta användnings översikt för kundens prenumeration</span><span class="sxs-lookup"><span data-stu-id="ad58d-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="ad58d-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="ad58d-104">**Applies to:**</span></span>

- <span data-ttu-id="ad58d-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="ad58d-105">Partner Center</span></span>
- <span data-ttu-id="ad58d-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="ad58d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ad58d-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ad58d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ad58d-108">Du kan använda **SubscriptionUsageSummary** -resursen för att få en översikt över prenumerations användning för en kund.</span><span class="sxs-lookup"><span data-stu-id="ad58d-108">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="ad58d-109">Den här resursen representerar prenumerations användnings översikten för en viss Azure-tjänst eller resurs under den aktuella fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="ad58d-109">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad58d-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ad58d-110">Prerequisites</span></span>

- <span data-ttu-id="ad58d-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ad58d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ad58d-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ad58d-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ad58d-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ad58d-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ad58d-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="ad58d-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ad58d-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="ad58d-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ad58d-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="ad58d-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ad58d-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="ad58d-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ad58d-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ad58d-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ad58d-119">Ett prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="ad58d-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="ad58d-120">C\#</span><span class="sxs-lookup"><span data-stu-id="ad58d-120">C\#</span></span>

<span data-ttu-id="ad58d-121">Så här hämtar du en prenumerations användnings översikt för en kunds prenumeration:</span><span class="sxs-lookup"><span data-stu-id="ad58d-121">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="ad58d-122">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="ad58d-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="ad58d-123">Anropa sedan egenskapen Subscriptions och egenskapen **UsageSummary** .</span><span class="sxs-lookup"><span data-stu-id="ad58d-123">Then call the Subscriptions property, as well as **UsageSummary** property.</span></span> <span data-ttu-id="ad58d-124">Slutför genom att anropa metoderna Get () eller GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="ad58d-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="ad58d-125">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="ad58d-125">For an example, see the following:</span></span>

- <span data-ttu-id="ad58d-126">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ad58d-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ad58d-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="ad58d-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="ad58d-128">Klass: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="ad58d-128">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="ad58d-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ad58d-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ad58d-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="ad58d-130">Request syntax</span></span>

| <span data-ttu-id="ad58d-131">Metod</span><span class="sxs-lookup"><span data-stu-id="ad58d-131">Method</span></span>  | <span data-ttu-id="ad58d-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ad58d-132">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad58d-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="ad58d-133">**GET**</span></span> | <span data-ttu-id="ad58d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="ad58d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="ad58d-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="ad58d-135">URI parameters</span></span>

<span data-ttu-id="ad58d-136">Den här tabellen innehåller de frågeparametrar som krävs för att hämta kundens beräknade användnings information.</span><span class="sxs-lookup"><span data-stu-id="ad58d-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="ad58d-137">Namn</span><span class="sxs-lookup"><span data-stu-id="ad58d-137">Name</span></span>                   | <span data-ttu-id="ad58d-138">Typ</span><span class="sxs-lookup"><span data-stu-id="ad58d-138">Type</span></span>     | <span data-ttu-id="ad58d-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ad58d-139">Required</span></span> | <span data-ttu-id="ad58d-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ad58d-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="ad58d-141">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="ad58d-141">**customer-tenant-id**</span></span> | <span data-ttu-id="ad58d-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="ad58d-142">**guid**</span></span> | <span data-ttu-id="ad58d-143">Y</span><span class="sxs-lookup"><span data-stu-id="ad58d-143">Y</span></span>        | <span data-ttu-id="ad58d-144">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="ad58d-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="ad58d-145">**prenumerations-ID**</span><span class="sxs-lookup"><span data-stu-id="ad58d-145">**subscription-id**</span></span>    | <span data-ttu-id="ad58d-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="ad58d-146">**guid**</span></span> | <span data-ttu-id="ad58d-147">Y</span><span class="sxs-lookup"><span data-stu-id="ad58d-147">Y</span></span>        | <span data-ttu-id="ad58d-148">Ett GUID som motsvarar identifieraren för en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="ad58d-148">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="ad58d-149">För en Azure-plan är detta ID för motsvarande Partner Center [prenumerations resurs](subscription-resources.md#subscription), som representerar Azure-planen.</span><span class="sxs-lookup"><span data-stu-id="ad58d-149">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="ad58d-150">*För prenumerations resurser i Azure plan anger du **plan-ID** som **prenumerations-ID** i den här vägen.*</span><span class="sxs-lookup"><span data-stu-id="ad58d-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ad58d-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ad58d-151">Request headers</span></span>

<span data-ttu-id="ad58d-152">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ad58d-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ad58d-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ad58d-153">Request body</span></span>

<span data-ttu-id="ad58d-154">Inga.</span><span class="sxs-lookup"><span data-stu-id="ad58d-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ad58d-155">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ad58d-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="ad58d-156">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ad58d-156">REST response</span></span>

<span data-ttu-id="ad58d-157">Om det lyckas returnerar den här metoden en **SubscriptionUsageSummary** -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="ad58d-157">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ad58d-158">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ad58d-158">Response success and error codes</span></span>

<span data-ttu-id="ad58d-159">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="ad58d-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ad58d-160">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ad58d-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="ad58d-161">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ad58d-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="ad58d-162">Svars exempel för Microsoft Azure (MS-AZR-0145P)-prenumerationer</span><span class="sxs-lookup"><span data-stu-id="ad58d-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="ad58d-163">I det här exemplet har kunden köpt ett **145P Azure PayG** -erbjudande.</span><span class="sxs-lookup"><span data-stu-id="ad58d-163">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="ad58d-164">*För kunder med Microsoft Azure-prenumerationer (MS-AZR-0145P) sker ingen ändring i API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="ad58d-164">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="ad58d-165">Exempel på REST-svar för Azure-prenumeration</span><span class="sxs-lookup"><span data-stu-id="ad58d-165">REST response example for Azure plan</span></span>

<span data-ttu-id="ad58d-166">I det här exemplet har kunden köpt en Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="ad58d-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="ad58d-167">*För kunder med Azure-planer finns följande ändringar i API-svaret:*</span><span class="sxs-lookup"><span data-stu-id="ad58d-167">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="ad58d-168">**currencyLocale** ersätts med **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="ad58d-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="ad58d-169">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="ad58d-169">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
