---
title: Hämta användningssammanfattning för kundens prenumeration
description: Du kan använda resursen SubscriptionUsageSummary för att hämta en prenumerationsanvändningssammanfattning för en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 362e72e1b54a62a114564d4dc48a082bcdeea012
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874677"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="6db6b-103">Hämta användningssammanfattning för kundens prenumeration</span><span class="sxs-lookup"><span data-stu-id="6db6b-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="6db6b-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6db6b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6db6b-105">Du kan använda resursen **SubscriptionUsageSummary för** att hämta en sammanfattning av prenumerationsanvändningen för en kund.</span><span class="sxs-lookup"><span data-stu-id="6db6b-105">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="6db6b-106">Den här resursen representerar prenumerationsanvändningssammanfattningen för en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="6db6b-106">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6db6b-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6db6b-107">Prerequisites</span></span>

- <span data-ttu-id="6db6b-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6db6b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6db6b-109">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6db6b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6db6b-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6db6b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6db6b-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6db6b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6db6b-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="6db6b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6db6b-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="6db6b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6db6b-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="6db6b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6db6b-115">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6db6b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6db6b-116">En prenumerationsidentifierare</span><span class="sxs-lookup"><span data-stu-id="6db6b-116">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="6db6b-117">C\#</span><span class="sxs-lookup"><span data-stu-id="6db6b-117">C\#</span></span>

<span data-ttu-id="6db6b-118">Så här hämtar du en prenumerationsanvändningssammanfattning för en kunds prenumeration:</span><span class="sxs-lookup"><span data-stu-id="6db6b-118">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="6db6b-119">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="6db6b-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="6db6b-120">Anropa sedan egenskapen Prenumerationer och **egenskapen UsageSummary.**</span><span class="sxs-lookup"><span data-stu-id="6db6b-120">Then call the Subscriptions property and the **UsageSummary** property.</span></span> <span data-ttu-id="6db6b-121">Slutför genom att anropa metoderna Get() eller GetAsync().</span><span class="sxs-lookup"><span data-stu-id="6db6b-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="6db6b-122">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="6db6b-122">For an example, see the following:</span></span>

- <span data-ttu-id="6db6b-123">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6db6b-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6db6b-124">Project: **PartnerSDK.FeatureExempel**</span><span class="sxs-lookup"><span data-stu-id="6db6b-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="6db6b-125">Klass: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="6db6b-125">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6db6b-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6db6b-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6db6b-127">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="6db6b-127">Request syntax</span></span>

| <span data-ttu-id="6db6b-128">Metod</span><span class="sxs-lookup"><span data-stu-id="6db6b-128">Method</span></span>  | <span data-ttu-id="6db6b-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6db6b-129">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6db6b-130">**Få**</span><span class="sxs-lookup"><span data-stu-id="6db6b-130">**GET**</span></span> | <span data-ttu-id="6db6b-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6db6b-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6db6b-132">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="6db6b-132">URI parameters</span></span>

<span data-ttu-id="6db6b-133">I den här tabellen visas de frågeparametrar som krävs för att hämta kundens klassificerade användningsinformation.</span><span class="sxs-lookup"><span data-stu-id="6db6b-133">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="6db6b-134">Namn</span><span class="sxs-lookup"><span data-stu-id="6db6b-134">Name</span></span>                   | <span data-ttu-id="6db6b-135">Typ</span><span class="sxs-lookup"><span data-stu-id="6db6b-135">Type</span></span>     | <span data-ttu-id="6db6b-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6db6b-136">Required</span></span> | <span data-ttu-id="6db6b-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6db6b-137">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="6db6b-138">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="6db6b-138">**customer-tenant-id**</span></span> | <span data-ttu-id="6db6b-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="6db6b-139">**guid**</span></span> | <span data-ttu-id="6db6b-140">Y</span><span class="sxs-lookup"><span data-stu-id="6db6b-140">Y</span></span>        | <span data-ttu-id="6db6b-141">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="6db6b-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="6db6b-142">**prenumerations-id**</span><span class="sxs-lookup"><span data-stu-id="6db6b-142">**subscription-id**</span></span>    | <span data-ttu-id="6db6b-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="6db6b-143">**guid**</span></span> | <span data-ttu-id="6db6b-144">Y</span><span class="sxs-lookup"><span data-stu-id="6db6b-144">Y</span></span>        | <span data-ttu-id="6db6b-145">Ett GUID som motsvarar identifieraren för en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="6db6b-145">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="6db6b-146">För en Azure-plan är detta identifieraren för motsvarande Partner [Center-prenumerationsresurs](subscription-resources.md#subscription), som representerar Azure-planen.</span><span class="sxs-lookup"><span data-stu-id="6db6b-146">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="6db6b-147">*För prenumerationsresurser för Azure-plan anger du **plan-ID:t** som **prenumerations-ID i** den här vägen.*</span><span class="sxs-lookup"><span data-stu-id="6db6b-147">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6db6b-148">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6db6b-148">Request headers</span></span>

<span data-ttu-id="6db6b-149">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6db6b-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6db6b-150">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6db6b-150">Request body</span></span>

<span data-ttu-id="6db6b-151">Inga.</span><span class="sxs-lookup"><span data-stu-id="6db6b-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6db6b-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6db6b-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="6db6b-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6db6b-153">REST response</span></span>

<span data-ttu-id="6db6b-154">Om det lyckas returnerar den här metoden **en SubscriptionUsageSummary-resurs** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="6db6b-154">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6db6b-155">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6db6b-155">Response success and error codes</span></span>

<span data-ttu-id="6db6b-156">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="6db6b-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6db6b-157">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6db6b-157">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="6db6b-158">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6db6b-158">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="6db6b-159">Svarsexempel Microsoft Azure prenumerationer (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="6db6b-159">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="6db6b-160">I det här exemplet köpte kunden ett **145P Azure PayG-erbjudande.**</span><span class="sxs-lookup"><span data-stu-id="6db6b-160">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="6db6b-161">*För kunder med Microsoft Azure prenumerationer (MS-AZR-0145P) ändras inte API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="6db6b-161">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="6db6b-162">REST-svarsexempel för Azure-plan</span><span class="sxs-lookup"><span data-stu-id="6db6b-162">REST response example for Azure plan</span></span>

<span data-ttu-id="6db6b-163">I det här exemplet köpte kunden en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="6db6b-163">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="6db6b-164">*För kunder med Azure-planer finns följande API-svarsändringar:*</span><span class="sxs-lookup"><span data-stu-id="6db6b-164">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="6db6b-165">**currencyLocale** ersätts med **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="6db6b-165">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="6db6b-166">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="6db6b-166">**usdTotalCost** is a new field</span></span>

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
