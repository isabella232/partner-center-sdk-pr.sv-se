---
title: Få en användnings översikt för alla kunds prenumerationer
description: Du kan använda CustomerUsageSummary-resursen för att få en kunds användning av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769129"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="691b6-103">Få en användnings översikt för alla kunds prenumerationer</span><span class="sxs-lookup"><span data-stu-id="691b6-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="691b6-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="691b6-104">**Applies to:**</span></span>

- <span data-ttu-id="691b6-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="691b6-105">Partner Center</span></span>
- <span data-ttu-id="691b6-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="691b6-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="691b6-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="691b6-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="691b6-108">Du kan använda **CustomerUsageSummary** -resursen för att få en kunds användning av en specifik Azure-tjänst eller resurs under den aktuella fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="691b6-108">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="691b6-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="691b6-109">Prerequisites</span></span>

- <span data-ttu-id="691b6-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="691b6-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="691b6-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="691b6-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="691b6-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="691b6-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="691b6-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="691b6-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="691b6-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="691b6-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="691b6-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="691b6-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="691b6-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="691b6-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="691b6-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="691b6-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="691b6-118">C\#</span><span class="sxs-lookup"><span data-stu-id="691b6-118">C\#</span></span>

<span data-ttu-id="691b6-119">Så här hämtar du en användnings Sammanfattning för alla kund prenumerationer:</span><span class="sxs-lookup"><span data-stu-id="691b6-119">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="691b6-120">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="691b6-120">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="691b6-121">Anropa egenskapen **UsageSummary** följt av metoderna **Get ()** eller **GetAsync ()** :</span><span class="sxs-lookup"><span data-stu-id="691b6-121">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="691b6-122">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="691b6-122">For an example, see the following:</span></span>

- <span data-ttu-id="691b6-123">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="691b6-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="691b6-124">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="691b6-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="691b6-125">Klass: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="691b6-125">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="691b6-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="691b6-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="691b6-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="691b6-127">Request syntax</span></span>

| <span data-ttu-id="691b6-128">Metod</span><span class="sxs-lookup"><span data-stu-id="691b6-128">Method</span></span>  | <span data-ttu-id="691b6-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="691b6-129">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="691b6-130">**TA**</span><span class="sxs-lookup"><span data-stu-id="691b6-130">**GET**</span></span> | <span data-ttu-id="691b6-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="691b6-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="691b6-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="691b6-132">URI parameter</span></span>

<span data-ttu-id="691b6-133">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta kundens beräknade användnings information.</span><span class="sxs-lookup"><span data-stu-id="691b6-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="691b6-134">Namn</span><span class="sxs-lookup"><span data-stu-id="691b6-134">Name</span></span>                   | <span data-ttu-id="691b6-135">Typ</span><span class="sxs-lookup"><span data-stu-id="691b6-135">Type</span></span>     | <span data-ttu-id="691b6-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="691b6-136">Required</span></span> | <span data-ttu-id="691b6-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="691b6-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="691b6-138">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="691b6-138">**customer-tenant-id**</span></span> | <span data-ttu-id="691b6-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="691b6-139">**guid**</span></span> | <span data-ttu-id="691b6-140">Y</span><span class="sxs-lookup"><span data-stu-id="691b6-140">Y</span></span>        | <span data-ttu-id="691b6-141">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="691b6-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="691b6-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="691b6-142">Request headers</span></span>

<span data-ttu-id="691b6-143">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="691b6-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="691b6-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="691b6-144">Request body</span></span>

<span data-ttu-id="691b6-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="691b6-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="691b6-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="691b6-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="691b6-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="691b6-147">REST response</span></span>

<span data-ttu-id="691b6-148">Om det lyckas returnerar den här metoden en **CustomerUsageSummary** -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="691b6-148">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="691b6-149">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="691b6-149">Response success and error codes</span></span>

<span data-ttu-id="691b6-150">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="691b6-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="691b6-151">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="691b6-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="691b6-152">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="691b6-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="691b6-153">Svars exempel för Microsoft Azure-prenumeration (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="691b6-153">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="691b6-154">I det här exemplet har kunden köpt ett **145P Azure PayG** -erbjudande.</span><span class="sxs-lookup"><span data-stu-id="691b6-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="691b6-155">*För kunder med Microsoft Azure-prenumerationer (MS-AZR-0145P) sker ingen ändring i API-svaret.*</span><span class="sxs-lookup"><span data-stu-id="691b6-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="691b6-156">Svars exempel för Azure-plan</span><span class="sxs-lookup"><span data-stu-id="691b6-156">Response example for Azure plan</span></span>

<span data-ttu-id="691b6-157">I det här exemplet har kunden köpt en Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="691b6-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="691b6-158">*För kunder med Azure-planer finns följande ändringar i API-svaret:*</span><span class="sxs-lookup"><span data-stu-id="691b6-158">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="691b6-159">**currencyLocale** ersätts med **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="691b6-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="691b6-160">**usdTotalCost** är ett nytt fält</span><span class="sxs-lookup"><span data-stu-id="691b6-160">**usdTotalCost** is a new field</span></span>

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
