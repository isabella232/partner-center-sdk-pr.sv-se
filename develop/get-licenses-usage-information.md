---
title: Hämta information om licensanvändning
description: Så här hämtar du användningsinformation om licenser på arbetsbelastningsnivå för Office och Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445991"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="226e5-103">Hämta information om licensanvändning</span><span class="sxs-lookup"><span data-stu-id="226e5-103">Get licenses usage information</span></span>

<span data-ttu-id="226e5-104">Så här hämtar du användningsinformation om licenser på arbetsbelastningsnivå för Office och Dynamics.</span><span class="sxs-lookup"><span data-stu-id="226e5-104">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="226e5-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="226e5-105">Prerequisites</span></span>

<span data-ttu-id="226e5-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="226e5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="226e5-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="226e5-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="226e5-108">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="226e5-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="226e5-109">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="226e5-109">Request syntax</span></span>

| <span data-ttu-id="226e5-110">Metod</span><span class="sxs-lookup"><span data-stu-id="226e5-110">Method</span></span>  | <span data-ttu-id="226e5-111">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="226e5-111">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="226e5-112">**Få**</span><span class="sxs-lookup"><span data-stu-id="226e5-112">**GET**</span></span> | <span data-ttu-id="226e5-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="226e5-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="226e5-114">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="226e5-114">Request headers</span></span>

<span data-ttu-id="226e5-115">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="226e5-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="226e5-116">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="226e5-116">URI parameters</span></span>

| <span data-ttu-id="226e5-117">Parameter</span><span class="sxs-lookup"><span data-stu-id="226e5-117">Parameter</span></span>         | <span data-ttu-id="226e5-118">Typ</span><span class="sxs-lookup"><span data-stu-id="226e5-118">Type</span></span>     | <span data-ttu-id="226e5-119">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="226e5-119">Description</span></span> | <span data-ttu-id="226e5-120">Krävs</span><span class="sxs-lookup"><span data-stu-id="226e5-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="226e5-121">top</span><span class="sxs-lookup"><span data-stu-id="226e5-121">top</span></span>               | <span data-ttu-id="226e5-122">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-122">string</span></span>   | <span data-ttu-id="226e5-123">Antalet rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="226e5-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="226e5-124">Det högsta värdet och standardvärdet om inget värde anges är 10000.</span><span class="sxs-lookup"><span data-stu-id="226e5-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="226e5-125">Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="226e5-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="226e5-126">Inga</span><span class="sxs-lookup"><span data-stu-id="226e5-126">No</span></span> |
| <span data-ttu-id="226e5-127">hoppa över</span><span class="sxs-lookup"><span data-stu-id="226e5-127">skip</span></span>              | <span data-ttu-id="226e5-128">int</span><span class="sxs-lookup"><span data-stu-id="226e5-128">int</span></span>      | <span data-ttu-id="226e5-129">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="226e5-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="226e5-130">Använd den här parametern för att bläddra igenom stora datamängder.</span><span class="sxs-lookup"><span data-stu-id="226e5-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="226e5-131">Till exempel hämtar top=10000 och skip=0 de första 10 000 raderna med data, top=10000 och skip=10000 hämtar de nästa 10 000 raderna med data och så vidare.</span><span class="sxs-lookup"><span data-stu-id="226e5-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="226e5-132">Inga</span><span class="sxs-lookup"><span data-stu-id="226e5-132">No</span></span> |
| <span data-ttu-id="226e5-133">filter</span><span class="sxs-lookup"><span data-stu-id="226e5-133">filter</span></span>            | <span data-ttu-id="226e5-134">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-134">string</span></span>   | <span data-ttu-id="226e5-135">*Filterparametern* för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="226e5-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="226e5-136">Varje -instruktion innehåller ett fält och värde som är associerade med **`eq`** **`ne`** operatorerna eller , och -instruktioner kan kombineras med hjälp av **`and`** eller **`or`** .</span><span class="sxs-lookup"><span data-stu-id="226e5-136">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="226e5-137">Här är några exempel *på filterparametrar:*</span><span class="sxs-lookup"><span data-stu-id="226e5-137">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="226e5-138">*filter=workloadCode eq 'SFB'*</span><span class="sxs-lookup"><span data-stu-id="226e5-138">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="226e5-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="226e5-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="226e5-140">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="226e5-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="226e5-141">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="226e5-141">**workloadCode**</span></span><br/><span data-ttu-id="226e5-142">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="226e5-142">**workloadName**</span></span><br/><span data-ttu-id="226e5-143">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="226e5-143">**serviceCode**</span></span><br/><span data-ttu-id="226e5-144">**Tjänstnamn**</span><span class="sxs-lookup"><span data-stu-id="226e5-144">**serviceName**</span></span><br/><span data-ttu-id="226e5-145">**Kanal**</span><span class="sxs-lookup"><span data-stu-id="226e5-145">**channel**</span></span><br/><span data-ttu-id="226e5-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="226e5-146">**customerTenantId**</span></span><br/><span data-ttu-id="226e5-147">**customerName**</span><span class="sxs-lookup"><span data-stu-id="226e5-147">**customerName**</span></span><br/><span data-ttu-id="226e5-148">**Produktionen**</span><span class="sxs-lookup"><span data-stu-id="226e5-148">**productId**</span></span><br/><span data-ttu-id="226e5-149">**Productname**</span><span class="sxs-lookup"><span data-stu-id="226e5-149">**productName**</span></span> | <span data-ttu-id="226e5-150">Inga</span><span class="sxs-lookup"><span data-stu-id="226e5-150">No</span></span> |
| <span data-ttu-id="226e5-151">groupby</span><span class="sxs-lookup"><span data-stu-id="226e5-151">groupby</span></span>           | <span data-ttu-id="226e5-152">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-152">string</span></span>   | <span data-ttu-id="226e5-153">En instruktion som endast tillämpar dataaggregering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="226e5-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="226e5-154">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="226e5-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="226e5-155">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="226e5-155">**workloadCode**</span></span><br/><span data-ttu-id="226e5-156">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="226e5-156">**workloadName**</span></span><br/><span data-ttu-id="226e5-157">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="226e5-157">**serviceCode**</span></span><br/><span data-ttu-id="226e5-158">**Tjänstnamn**</span><span class="sxs-lookup"><span data-stu-id="226e5-158">**serviceName**</span></span><br/><span data-ttu-id="226e5-159">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="226e5-159">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="226e5-160">**customerName**</span><span class="sxs-lookup"><span data-stu-id="226e5-160">**customerName**</span></span><br/><span data-ttu-id="226e5-161">**Produktionen**</span><span class="sxs-lookup"><span data-stu-id="226e5-161">**productId**</span></span><br/><span data-ttu-id="226e5-162">**Productname**</span><span class="sxs-lookup"><span data-stu-id="226e5-162">**productName**</span></span><br/><br/><span data-ttu-id="226e5-163">De returnerade dataraderna innehåller de fält som anges i *parametern groupby* och följande:</span><span class="sxs-lookup"><span data-stu-id="226e5-163">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="226e5-164">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="226e5-164">**licensesActive**</span></span><br/><span data-ttu-id="226e5-165">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="226e5-165">**licensesQualified**</span></span> | <span data-ttu-id="226e5-166">Inga</span><span class="sxs-lookup"><span data-stu-id="226e5-166">No</span></span> |
| <span data-ttu-id="226e5-167">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="226e5-167">processedDateTime</span></span> | <span data-ttu-id="226e5-168">DateTime</span><span class="sxs-lookup"><span data-stu-id="226e5-168">DateTime</span></span> | <span data-ttu-id="226e5-169">Du kan ange det datum då användningsdata bearbetades.</span><span class="sxs-lookup"><span data-stu-id="226e5-169">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="226e5-170">Standardvärdet är det senaste datumet då data bearbetades</span><span class="sxs-lookup"><span data-stu-id="226e5-170">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="226e5-171">Inga</span><span class="sxs-lookup"><span data-stu-id="226e5-171">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="226e5-172">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="226e5-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="226e5-173">REST-svar</span><span class="sxs-lookup"><span data-stu-id="226e5-173">REST response</span></span>

<span data-ttu-id="226e5-174">Om det lyckas innehåller svarstexten följande fält som innehåller data om licensanvändningen.</span><span class="sxs-lookup"><span data-stu-id="226e5-174">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="226e5-175">Fält</span><span class="sxs-lookup"><span data-stu-id="226e5-175">Field</span></span>             | <span data-ttu-id="226e5-176">Typ</span><span class="sxs-lookup"><span data-stu-id="226e5-176">Type</span></span>     | <span data-ttu-id="226e5-177">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="226e5-177">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="226e5-178">workloadCode</span><span class="sxs-lookup"><span data-stu-id="226e5-178">workloadCode</span></span>      | <span data-ttu-id="226e5-179">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-179">string</span></span>   | <span data-ttu-id="226e5-180">Arbetsbelastningskod</span><span class="sxs-lookup"><span data-stu-id="226e5-180">Workload code</span></span>                                 |
| <span data-ttu-id="226e5-181">workloadName</span><span class="sxs-lookup"><span data-stu-id="226e5-181">workloadName</span></span>      | <span data-ttu-id="226e5-182">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-182">string</span></span>   | <span data-ttu-id="226e5-183">Namn på arbetsbelastning</span><span class="sxs-lookup"><span data-stu-id="226e5-183">Workload name</span></span>                                 |
| <span data-ttu-id="226e5-184">serviceCode</span><span class="sxs-lookup"><span data-stu-id="226e5-184">serviceCode</span></span>       | <span data-ttu-id="226e5-185">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-185">string</span></span>   | <span data-ttu-id="226e5-186">Tjänstkod</span><span class="sxs-lookup"><span data-stu-id="226e5-186">Service code</span></span>                                  |
| <span data-ttu-id="226e5-187">Tjänstnamn</span><span class="sxs-lookup"><span data-stu-id="226e5-187">serviceName</span></span>       | <span data-ttu-id="226e5-188">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-188">string</span></span>   | <span data-ttu-id="226e5-189">Tjänstnamn</span><span class="sxs-lookup"><span data-stu-id="226e5-189">Service name</span></span>                                  |
| <span data-ttu-id="226e5-190">Kanal</span><span class="sxs-lookup"><span data-stu-id="226e5-190">channel</span></span>           | <span data-ttu-id="226e5-191">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-191">string</span></span>   | <span data-ttu-id="226e5-192">Kanalnamn, återförsäljare</span><span class="sxs-lookup"><span data-stu-id="226e5-192">Channel name, reseller</span></span>                        |
| <span data-ttu-id="226e5-193">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="226e5-193">customerTenantId</span></span>  | <span data-ttu-id="226e5-194">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-194">string</span></span>   | <span data-ttu-id="226e5-195">Unik identifierare för kunden</span><span class="sxs-lookup"><span data-stu-id="226e5-195">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="226e5-196">customerName</span><span class="sxs-lookup"><span data-stu-id="226e5-196">customerName</span></span>      | <span data-ttu-id="226e5-197">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-197">string</span></span>   | <span data-ttu-id="226e5-198">Kundnamn</span><span class="sxs-lookup"><span data-stu-id="226e5-198">Customer name</span></span>                                 |
| <span data-ttu-id="226e5-199">productId</span><span class="sxs-lookup"><span data-stu-id="226e5-199">productId</span></span>         | <span data-ttu-id="226e5-200">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-200">string</span></span>   | <span data-ttu-id="226e5-201">Unik identifierare för produkten</span><span class="sxs-lookup"><span data-stu-id="226e5-201">Unique identifier for the product</span></span>             |
| <span data-ttu-id="226e5-202">Productname</span><span class="sxs-lookup"><span data-stu-id="226e5-202">productName</span></span>       | <span data-ttu-id="226e5-203">sträng</span><span class="sxs-lookup"><span data-stu-id="226e5-203">string</span></span>   | <span data-ttu-id="226e5-204">Produktnamn</span><span class="sxs-lookup"><span data-stu-id="226e5-204">Product name</span></span>                                  |
| <span data-ttu-id="226e5-205">licensesActive</span><span class="sxs-lookup"><span data-stu-id="226e5-205">licensesActive</span></span>    | <span data-ttu-id="226e5-206">long</span><span class="sxs-lookup"><span data-stu-id="226e5-206">long</span></span>     | <span data-ttu-id="226e5-207">Antal aktiva licenser per arbetsbelastning</span><span class="sxs-lookup"><span data-stu-id="226e5-207">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="226e5-208">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="226e5-208">licensesQualified</span></span> | <span data-ttu-id="226e5-209">long</span><span class="sxs-lookup"><span data-stu-id="226e5-209">long</span></span>     | <span data-ttu-id="226e5-210">Antal kvalificerade licenser för arbetsbelastningen</span><span class="sxs-lookup"><span data-stu-id="226e5-210">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="226e5-211">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="226e5-211">processedDateTime</span></span> | <span data-ttu-id="226e5-212">DateTime</span><span class="sxs-lookup"><span data-stu-id="226e5-212">DateTime</span></span> | <span data-ttu-id="226e5-213">Datum då data senast bearbetades</span><span class="sxs-lookup"><span data-stu-id="226e5-213">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="226e5-214">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="226e5-214">Response success and error codes</span></span>

<span data-ttu-id="226e5-215">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="226e5-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="226e5-216">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="226e5-216">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="226e5-217">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="226e5-217">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="226e5-218">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="226e5-218">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
