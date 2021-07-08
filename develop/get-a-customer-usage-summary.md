---
title: Hämta en användningssammanfattning för alla en kunds prenumerationer
description: Du kan använda resursen CustomerUsageSummary för att få en kunds användning av en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88c69637c94b9263ede6924cf2dd09513aa00f70
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874626"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="16aef-103">Hämta en användningssammanfattning för alla en kunds prenumerationer</span><span class="sxs-lookup"><span data-stu-id="16aef-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="16aef-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="16aef-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="16aef-105">Du kan använda **resursen CustomerUsageSummary** för att få en kunds användning av en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="16aef-105">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16aef-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="16aef-106">Prerequisites</span></span>

- <span data-ttu-id="16aef-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="16aef-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="16aef-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="16aef-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="16aef-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16aef-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="16aef-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="16aef-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="16aef-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="16aef-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="16aef-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="16aef-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="16aef-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="16aef-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="16aef-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16aef-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="16aef-115">C\#</span><span class="sxs-lookup"><span data-stu-id="16aef-115">C\#</span></span>

<span data-ttu-id="16aef-116">Så här hämtar du en användningssammanfattning för alla en kunds prenumerationer:</span><span class="sxs-lookup"><span data-stu-id="16aef-116">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="16aef-117">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="16aef-117">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="16aef-118">Anropa egenskapen **UsageSummary** följt av metoderna **Get()** eller **GetAsync():**</span><span class="sxs-lookup"><span data-stu-id="16aef-118">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="16aef-119">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="16aef-119">For an example, see the following:</span></span>

- <span data-ttu-id="16aef-120">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="16aef-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="16aef-121">Project: **PartnerSDK.FeatureExempel**</span><span class="sxs-lookup"><span data-stu-id="16aef-121">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="16aef-122">Klass: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="16aef-122">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="16aef-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="16aef-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="16aef-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="16aef-124">Request syntax</span></span>

| <span data-ttu-id="16aef-125">Metod</span><span class="sxs-lookup"><span data-stu-id="16aef-125">Method</span></span>  | <span data-ttu-id="16aef-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="16aef-126">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="16aef-127">**Få**</span><span class="sxs-lookup"><span data-stu-id="16aef-127">**GET**</span></span> | <span data-ttu-id="16aef-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="16aef-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="16aef-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="16aef-129">URI parameter</span></span>

<span data-ttu-id="16aef-130">Den här tabellen innehåller frågeparametern som krävs för att hämta kundens klassificerade användningsinformation.</span><span class="sxs-lookup"><span data-stu-id="16aef-130">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="16aef-131">Namn</span><span class="sxs-lookup"><span data-stu-id="16aef-131">Name</span></span>                   | <span data-ttu-id="16aef-132">Typ</span><span class="sxs-lookup"><span data-stu-id="16aef-132">Type</span></span>     | <span data-ttu-id="16aef-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="16aef-133">Required</span></span> | <span data-ttu-id="16aef-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="16aef-134">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="16aef-135">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="16aef-135">**customer-tenant-id**</span></span> | <span data-ttu-id="16aef-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="16aef-136">**guid**</span></span> | <span data-ttu-id="16aef-137">Y</span><span class="sxs-lookup"><span data-stu-id="16aef-137">Y</span></span>        | <span data-ttu-id="16aef-138">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="16aef-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="16aef-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="16aef-139">Request headers</span></span>

<span data-ttu-id="16aef-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="16aef-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="16aef-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="16aef-141">Request body</span></span>

<span data-ttu-id="16aef-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="16aef-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="16aef-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="16aef-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="16aef-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="16aef-144">REST response</span></span>

<span data-ttu-id="16aef-145">Om det lyckas returnerar den här metoden **en CustomerUsageSummary-resurs** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="16aef-145">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="16aef-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="16aef-146">Response success and error codes</span></span>

<span data-ttu-id="16aef-147">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="16aef-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="16aef-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="16aef-148">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="16aef-149">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="16aef-149">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="16aef-150">Exempel på svar Microsoft Azure prenumeration (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="16aef-150">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="16aef-151">I det här exemplet köpte kunden ett **145P Azure PayG-erbjudande.**</span><span class="sxs-lookup"><span data-stu-id="16aef-151">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="16aef-152">*För kunder med Microsoft Azure prenumerationer (MS-AZR-0145P) ändras inte API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="16aef-152">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="16aef-153">Svarsexempel för Azure-plan</span><span class="sxs-lookup"><span data-stu-id="16aef-153">Response example for Azure plan</span></span>

<span data-ttu-id="16aef-154">I det här exemplet köpte kunden en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="16aef-154">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="16aef-155">*För kunder med Azure-planer finns följande ändringar i API-svaret:*</span><span class="sxs-lookup"><span data-stu-id="16aef-155">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="16aef-156">**currencyLocale** ersätts med **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="16aef-156">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="16aef-157">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="16aef-157">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
