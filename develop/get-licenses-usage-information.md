---
title: Hämta information om licensanvändning
description: Så här hämtar du licens användnings information på arbets belastnings nivå för Office och Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769429"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="b853b-103">Hämta information om licensanvändning</span><span class="sxs-lookup"><span data-stu-id="b853b-103">Get licenses usage information</span></span>

<span data-ttu-id="b853b-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="b853b-104">**Applies To**</span></span>

- <span data-ttu-id="b853b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b853b-105">Partner Center</span></span>

<span data-ttu-id="b853b-106">Så här hämtar du licens användnings information på arbets belastnings nivå för Office och Dynamics.</span><span class="sxs-lookup"><span data-stu-id="b853b-106">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b853b-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b853b-107">Prerequisites</span></span>

<span data-ttu-id="b853b-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b853b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b853b-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b853b-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b853b-110">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b853b-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b853b-111">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b853b-111">Request syntax</span></span>

| <span data-ttu-id="b853b-112">Metod</span><span class="sxs-lookup"><span data-stu-id="b853b-112">Method</span></span>  | <span data-ttu-id="b853b-113">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b853b-113">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="b853b-114">**TA**</span><span class="sxs-lookup"><span data-stu-id="b853b-114">**GET**</span></span> | <span data-ttu-id="b853b-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Usage/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="b853b-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b853b-116">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b853b-116">Request headers</span></span>

<span data-ttu-id="b853b-117">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b853b-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="b853b-118">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b853b-118">URI parameters</span></span>

| <span data-ttu-id="b853b-119">Parameter</span><span class="sxs-lookup"><span data-stu-id="b853b-119">Parameter</span></span>         | <span data-ttu-id="b853b-120">Typ</span><span class="sxs-lookup"><span data-stu-id="b853b-120">Type</span></span>     | <span data-ttu-id="b853b-121">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b853b-121">Description</span></span> | <span data-ttu-id="b853b-122">Krävs</span><span class="sxs-lookup"><span data-stu-id="b853b-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="b853b-123">top</span><span class="sxs-lookup"><span data-stu-id="b853b-123">top</span></span>               | <span data-ttu-id="b853b-124">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-124">string</span></span>   | <span data-ttu-id="b853b-125">Det antal rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="b853b-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="b853b-126">Det maximala värdet och standardvärdet om det inte anges är 10000.</span><span class="sxs-lookup"><span data-stu-id="b853b-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="b853b-127">Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="b853b-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="b853b-128">No</span><span class="sxs-lookup"><span data-stu-id="b853b-128">No</span></span> |
| <span data-ttu-id="b853b-129">hoppa över</span><span class="sxs-lookup"><span data-stu-id="b853b-129">skip</span></span>              | <span data-ttu-id="b853b-130">int</span><span class="sxs-lookup"><span data-stu-id="b853b-130">int</span></span>      | <span data-ttu-id="b853b-131">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="b853b-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="b853b-132">Använd den här parametern för att växla mellan stora data mängder.</span><span class="sxs-lookup"><span data-stu-id="b853b-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="b853b-133">Till exempel Top = 10000 och Skip = 0 hämtar de första 10000 raderna med data, Top = 10000 och Skip = 10000 hämtar nästa 10000 rader med data och så vidare.</span><span class="sxs-lookup"><span data-stu-id="b853b-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="b853b-134">No</span><span class="sxs-lookup"><span data-stu-id="b853b-134">No</span></span> |
| <span data-ttu-id="b853b-135">filter</span><span class="sxs-lookup"><span data-stu-id="b853b-135">filter</span></span>            | <span data-ttu-id="b853b-136">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-136">string</span></span>   | <span data-ttu-id="b853b-137">*Filter* parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="b853b-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="b853b-138">Varje instruktion innehåller ett fält och ett värde som är associerat **`eq`** med **`ne`** operatorerna or och som kan kombineras med hjälp av **`and`** eller **`or`** .</span><span class="sxs-lookup"><span data-stu-id="b853b-138">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="b853b-139">Här följer några exempel på *filter* parametrar:</span><span class="sxs-lookup"><span data-stu-id="b853b-139">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="b853b-140">*filter = workloadCode EQ ' SFB '*</span><span class="sxs-lookup"><span data-stu-id="b853b-140">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="b853b-141">*filter = workloadCode EQ ' SFB '* eller (*kanal EQ åter försäljare*)</span><span class="sxs-lookup"><span data-stu-id="b853b-141">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="b853b-142">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="b853b-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="b853b-143">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="b853b-143">**workloadCode**</span></span><br/><span data-ttu-id="b853b-144">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="b853b-144">**workloadName**</span></span><br/><span data-ttu-id="b853b-145">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="b853b-145">**serviceCode**</span></span><br/><span data-ttu-id="b853b-146">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="b853b-146">**serviceName**</span></span><br/><span data-ttu-id="b853b-147">**kanalig**</span><span class="sxs-lookup"><span data-stu-id="b853b-147">**channel**</span></span><br/><span data-ttu-id="b853b-148">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="b853b-148">**customerTenantId**</span></span><br/><span data-ttu-id="b853b-149">**customerName**</span><span class="sxs-lookup"><span data-stu-id="b853b-149">**customerName**</span></span><br/><span data-ttu-id="b853b-150">**productId**</span><span class="sxs-lookup"><span data-stu-id="b853b-150">**productId**</span></span><br/><span data-ttu-id="b853b-151">**Namn**</span><span class="sxs-lookup"><span data-stu-id="b853b-151">**productName**</span></span> | <span data-ttu-id="b853b-152">No</span><span class="sxs-lookup"><span data-stu-id="b853b-152">No</span></span> |
| <span data-ttu-id="b853b-153">groupby</span><span class="sxs-lookup"><span data-stu-id="b853b-153">groupby</span></span>           | <span data-ttu-id="b853b-154">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-154">string</span></span>   | <span data-ttu-id="b853b-155">En instruktion som endast tillämpar data agg regering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="b853b-155">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="b853b-156">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="b853b-156">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="b853b-157">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="b853b-157">**workloadCode**</span></span><br/><span data-ttu-id="b853b-158">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="b853b-158">**workloadName**</span></span><br/><span data-ttu-id="b853b-159">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="b853b-159">**serviceCode**</span></span><br/><span data-ttu-id="b853b-160">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="b853b-160">**serviceName**</span></span><br/><span data-ttu-id="b853b-161">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="b853b-161">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="b853b-162">**customerName**</span><span class="sxs-lookup"><span data-stu-id="b853b-162">**customerName**</span></span><br/><span data-ttu-id="b853b-163">**productId**</span><span class="sxs-lookup"><span data-stu-id="b853b-163">**productId**</span></span><br/><span data-ttu-id="b853b-164">**Namn**</span><span class="sxs-lookup"><span data-stu-id="b853b-164">**productName**</span></span><br/><br/><span data-ttu-id="b853b-165">De returnerade data raderna innehåller fälten som anges i *groupby* -parametern samt följande:</span><span class="sxs-lookup"><span data-stu-id="b853b-165">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="b853b-166">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="b853b-166">**licensesActive**</span></span><br/><span data-ttu-id="b853b-167">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="b853b-167">**licensesQualified**</span></span> | <span data-ttu-id="b853b-168">No</span><span class="sxs-lookup"><span data-stu-id="b853b-168">No</span></span> |
| <span data-ttu-id="b853b-169">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="b853b-169">processedDateTime</span></span> | <span data-ttu-id="b853b-170">DateTime</span><span class="sxs-lookup"><span data-stu-id="b853b-170">DateTime</span></span> | <span data-ttu-id="b853b-171">En kan ange det datum från vilket användnings data bearbetades.</span><span class="sxs-lookup"><span data-stu-id="b853b-171">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="b853b-172">Standardvärdet är det senaste datumet då data bearbetades</span><span class="sxs-lookup"><span data-stu-id="b853b-172">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="b853b-173">No</span><span class="sxs-lookup"><span data-stu-id="b853b-173">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="b853b-174">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b853b-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="b853b-175">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b853b-175">REST response</span></span>

<span data-ttu-id="b853b-176">Om det lyckas innehåller svars texten följande fält som innehåller data om licens användning.</span><span class="sxs-lookup"><span data-stu-id="b853b-176">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="b853b-177">Fält</span><span class="sxs-lookup"><span data-stu-id="b853b-177">Field</span></span>             | <span data-ttu-id="b853b-178">Typ</span><span class="sxs-lookup"><span data-stu-id="b853b-178">Type</span></span>     | <span data-ttu-id="b853b-179">Description</span><span class="sxs-lookup"><span data-stu-id="b853b-179">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="b853b-180">workloadCode</span><span class="sxs-lookup"><span data-stu-id="b853b-180">workloadCode</span></span>      | <span data-ttu-id="b853b-181">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-181">string</span></span>   | <span data-ttu-id="b853b-182">Arbets belastnings kod</span><span class="sxs-lookup"><span data-stu-id="b853b-182">Workload code</span></span>                                 |
| <span data-ttu-id="b853b-183">workloadName</span><span class="sxs-lookup"><span data-stu-id="b853b-183">workloadName</span></span>      | <span data-ttu-id="b853b-184">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-184">string</span></span>   | <span data-ttu-id="b853b-185">Arbets belastnings namn</span><span class="sxs-lookup"><span data-stu-id="b853b-185">Workload name</span></span>                                 |
| <span data-ttu-id="b853b-186">serviceCode</span><span class="sxs-lookup"><span data-stu-id="b853b-186">serviceCode</span></span>       | <span data-ttu-id="b853b-187">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-187">string</span></span>   | <span data-ttu-id="b853b-188">Service kod</span><span class="sxs-lookup"><span data-stu-id="b853b-188">Service code</span></span>                                  |
| <span data-ttu-id="b853b-189">serviceName</span><span class="sxs-lookup"><span data-stu-id="b853b-189">serviceName</span></span>       | <span data-ttu-id="b853b-190">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-190">string</span></span>   | <span data-ttu-id="b853b-191">Tjänstnamn</span><span class="sxs-lookup"><span data-stu-id="b853b-191">Service name</span></span>                                  |
| <span data-ttu-id="b853b-192">kanalig</span><span class="sxs-lookup"><span data-stu-id="b853b-192">channel</span></span>           | <span data-ttu-id="b853b-193">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-193">string</span></span>   | <span data-ttu-id="b853b-194">Kanal namn, åter försäljare</span><span class="sxs-lookup"><span data-stu-id="b853b-194">Channel name, reseller</span></span>                        |
| <span data-ttu-id="b853b-195">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="b853b-195">customerTenantId</span></span>  | <span data-ttu-id="b853b-196">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-196">string</span></span>   | <span data-ttu-id="b853b-197">Unikt ID för kunden</span><span class="sxs-lookup"><span data-stu-id="b853b-197">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="b853b-198">customerName</span><span class="sxs-lookup"><span data-stu-id="b853b-198">customerName</span></span>      | <span data-ttu-id="b853b-199">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-199">string</span></span>   | <span data-ttu-id="b853b-200">Kundnamn</span><span class="sxs-lookup"><span data-stu-id="b853b-200">Customer name</span></span>                                 |
| <span data-ttu-id="b853b-201">productId</span><span class="sxs-lookup"><span data-stu-id="b853b-201">productId</span></span>         | <span data-ttu-id="b853b-202">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-202">string</span></span>   | <span data-ttu-id="b853b-203">Unikt ID för produkten</span><span class="sxs-lookup"><span data-stu-id="b853b-203">Unique identifier for the product</span></span>             |
| <span data-ttu-id="b853b-204">Namn</span><span class="sxs-lookup"><span data-stu-id="b853b-204">productName</span></span>       | <span data-ttu-id="b853b-205">sträng</span><span class="sxs-lookup"><span data-stu-id="b853b-205">string</span></span>   | <span data-ttu-id="b853b-206">Produktnamn</span><span class="sxs-lookup"><span data-stu-id="b853b-206">Product name</span></span>                                  |
| <span data-ttu-id="b853b-207">licensesActive</span><span class="sxs-lookup"><span data-stu-id="b853b-207">licensesActive</span></span>    | <span data-ttu-id="b853b-208">long</span><span class="sxs-lookup"><span data-stu-id="b853b-208">long</span></span>     | <span data-ttu-id="b853b-209">Antal aktiva licenser per arbets belastning</span><span class="sxs-lookup"><span data-stu-id="b853b-209">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="b853b-210">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="b853b-210">licensesQualified</span></span> | <span data-ttu-id="b853b-211">long</span><span class="sxs-lookup"><span data-stu-id="b853b-211">long</span></span>     | <span data-ttu-id="b853b-212">Antal kvalificerade licenser för arbets belastningen</span><span class="sxs-lookup"><span data-stu-id="b853b-212">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="b853b-213">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="b853b-213">processedDateTime</span></span> | <span data-ttu-id="b853b-214">DateTime</span><span class="sxs-lookup"><span data-stu-id="b853b-214">DateTime</span></span> | <span data-ttu-id="b853b-215">Datum när data senast bearbetades</span><span class="sxs-lookup"><span data-stu-id="b853b-215">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b853b-216">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b853b-216">Response success and error codes</span></span>

<span data-ttu-id="b853b-217">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b853b-217">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b853b-218">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b853b-218">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b853b-219">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b853b-219">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b853b-220">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b853b-220">Response example</span></span>

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
