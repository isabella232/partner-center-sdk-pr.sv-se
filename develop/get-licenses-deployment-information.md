---
title: Hämta information om licensdistribution
description: Så här hämtar du distributions information för Office-och Dynamics-licenser.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769435"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="7f71c-103">Hämta information om licensdistribution</span><span class="sxs-lookup"><span data-stu-id="7f71c-103">Get licenses deployment information</span></span>

<span data-ttu-id="7f71c-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="7f71c-104">**Applies To**</span></span>

- <span data-ttu-id="7f71c-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7f71c-105">Partner Center</span></span>

<span data-ttu-id="7f71c-106">Så här hämtar du distributions information för Office-och Dynamics-licenser.</span><span class="sxs-lookup"><span data-stu-id="7f71c-106">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f71c-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7f71c-107">Prerequisites</span></span>

<span data-ttu-id="7f71c-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7f71c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7f71c-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7f71c-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7f71c-110">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7f71c-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7f71c-111">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="7f71c-111">Request syntax</span></span>

| <span data-ttu-id="7f71c-112">Metod</span><span class="sxs-lookup"><span data-stu-id="7f71c-112">Method</span></span>  | <span data-ttu-id="7f71c-113">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7f71c-113">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7f71c-114">**TA**</span><span class="sxs-lookup"><span data-stu-id="7f71c-114">**GET**</span></span> | <span data-ttu-id="7f71c-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Deployment/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="7f71c-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7f71c-116">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7f71c-116">Request headers</span></span>

<span data-ttu-id="7f71c-117">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7f71c-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="7f71c-118">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="7f71c-118">URI parameters</span></span>

| <span data-ttu-id="7f71c-119">Parameter</span><span class="sxs-lookup"><span data-stu-id="7f71c-119">Parameter</span></span>         | <span data-ttu-id="7f71c-120">Typ</span><span class="sxs-lookup"><span data-stu-id="7f71c-120">Type</span></span>     | <span data-ttu-id="7f71c-121">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7f71c-121">Description</span></span> | <span data-ttu-id="7f71c-122">Krävs</span><span class="sxs-lookup"><span data-stu-id="7f71c-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="7f71c-123">top</span><span class="sxs-lookup"><span data-stu-id="7f71c-123">top</span></span>               | <span data-ttu-id="7f71c-124">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-124">string</span></span>   | <span data-ttu-id="7f71c-125">Det antal rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="7f71c-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="7f71c-126">Det maximala värdet och standardvärdet om det inte anges är 10000.</span><span class="sxs-lookup"><span data-stu-id="7f71c-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="7f71c-127">Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="7f71c-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="7f71c-128">No</span><span class="sxs-lookup"><span data-stu-id="7f71c-128">No</span></span> |
| <span data-ttu-id="7f71c-129">hoppa över</span><span class="sxs-lookup"><span data-stu-id="7f71c-129">skip</span></span>              | <span data-ttu-id="7f71c-130">int</span><span class="sxs-lookup"><span data-stu-id="7f71c-130">int</span></span>      | <span data-ttu-id="7f71c-131">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="7f71c-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="7f71c-132">Använd den här parametern för att växla mellan stora data mängder.</span><span class="sxs-lookup"><span data-stu-id="7f71c-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="7f71c-133">Till exempel Top = 10000 och Skip = 0 hämtar de första 10000 raderna med data, Top = 10000 och Skip = 10000 hämtar nästa 10000 rader med data och så vidare.</span><span class="sxs-lookup"><span data-stu-id="7f71c-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="7f71c-134">No</span><span class="sxs-lookup"><span data-stu-id="7f71c-134">No</span></span> |
| <span data-ttu-id="7f71c-135">filter</span><span class="sxs-lookup"><span data-stu-id="7f71c-135">filter</span></span>            | <span data-ttu-id="7f71c-136">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-136">string</span></span>   | <span data-ttu-id="7f71c-137">*Filter* parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="7f71c-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="7f71c-138">Varje instruktion innehåller ett fält och ett värde som är associerat `eq` med `ne` operatorerna or och som kan kombineras med hjälp av `and` eller `or` .</span><span class="sxs-lookup"><span data-stu-id="7f71c-138">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="7f71c-139">Här följer några exempel på *filter* parametrar:</span><span class="sxs-lookup"><span data-stu-id="7f71c-139">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="7f71c-140">*filter = serviceCode EQ ' O365 '*</span><span class="sxs-lookup"><span data-stu-id="7f71c-140">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="7f71c-141">*filter = serviceCode EQ ' O365 '* eller (*kanal EQ åter försäljare*)</span><span class="sxs-lookup"><span data-stu-id="7f71c-141">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="7f71c-142">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="7f71c-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="7f71c-143">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="7f71c-143">**serviceCode**</span></span><br/><span data-ttu-id="7f71c-144">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="7f71c-144">**serviceName**</span></span><br/><span data-ttu-id="7f71c-145">**kanalig**</span><span class="sxs-lookup"><span data-stu-id="7f71c-145">**channel**</span></span><br/><span data-ttu-id="7f71c-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="7f71c-146">**customerTenantId**</span></span><br/><span data-ttu-id="7f71c-147">**customerName**</span><span class="sxs-lookup"><span data-stu-id="7f71c-147">**customerName**</span></span><br/><span data-ttu-id="7f71c-148">**productId**</span><span class="sxs-lookup"><span data-stu-id="7f71c-148">**productId**</span></span><br/><span data-ttu-id="7f71c-149">**Namn**</span><span class="sxs-lookup"><span data-stu-id="7f71c-149">**productName**</span></span>  | <span data-ttu-id="7f71c-150">No</span><span class="sxs-lookup"><span data-stu-id="7f71c-150">No</span></span> |
| <span data-ttu-id="7f71c-151">groupby</span><span class="sxs-lookup"><span data-stu-id="7f71c-151">groupby</span></span>           | <span data-ttu-id="7f71c-152">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-152">string</span></span>   | <span data-ttu-id="7f71c-153">En instruktion som endast tillämpar data agg regering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="7f71c-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="7f71c-154">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="7f71c-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="7f71c-155">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="7f71c-155">**serviceCode**</span></span><br/><span data-ttu-id="7f71c-156">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="7f71c-156">**serviceName**</span></span><br/><span data-ttu-id="7f71c-157">**kanalig**</span><span class="sxs-lookup"><span data-stu-id="7f71c-157">**channel**</span></span><br/><span data-ttu-id="7f71c-158">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="7f71c-158">**customerTenantId**</span></span><br/><span data-ttu-id="7f71c-159">**customerName**</span><span class="sxs-lookup"><span data-stu-id="7f71c-159">**customerName**</span></span><br/><span data-ttu-id="7f71c-160">**productId**</span><span class="sxs-lookup"><span data-stu-id="7f71c-160">**productId**</span></span><br/><span data-ttu-id="7f71c-161">**Namn**</span><span class="sxs-lookup"><span data-stu-id="7f71c-161">**productName**</span></span><br/><br/> <span data-ttu-id="7f71c-162">De returnerade data raderna innehåller fälten som anges i *groupby* -parametern samt följande:</span><span class="sxs-lookup"><span data-stu-id="7f71c-162">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="7f71c-163">**licensesDeployed**</span><span class="sxs-lookup"><span data-stu-id="7f71c-163">**licensesDeployed**</span></span><br/><span data-ttu-id="7f71c-164">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="7f71c-164">**licensesSold**</span></span>  | <span data-ttu-id="7f71c-165">No</span><span class="sxs-lookup"><span data-stu-id="7f71c-165">No</span></span> |
| <span data-ttu-id="7f71c-166">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="7f71c-166">processedDateTime</span></span> | <span data-ttu-id="7f71c-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f71c-167">DateTime</span></span> | <span data-ttu-id="7f71c-168">En kan ange det datum från vilket användnings data bearbetades.</span><span class="sxs-lookup"><span data-stu-id="7f71c-168">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="7f71c-169">Standardvärdet är det senaste datumet då data bearbetades</span><span class="sxs-lookup"><span data-stu-id="7f71c-169">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="7f71c-170">No</span><span class="sxs-lookup"><span data-stu-id="7f71c-170">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="7f71c-171">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7f71c-171">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7f71c-172">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7f71c-172">REST response</span></span>

<span data-ttu-id="7f71c-173">Om det lyckas innehåller svars texten följande fält som innehåller information om de licenser som har distribuerats.</span><span class="sxs-lookup"><span data-stu-id="7f71c-173">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="7f71c-174">Fält</span><span class="sxs-lookup"><span data-stu-id="7f71c-174">Field</span></span>             | <span data-ttu-id="7f71c-175">Typ</span><span class="sxs-lookup"><span data-stu-id="7f71c-175">Type</span></span>     | <span data-ttu-id="7f71c-176">Description</span><span class="sxs-lookup"><span data-stu-id="7f71c-176">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="7f71c-177">serviceCode</span><span class="sxs-lookup"><span data-stu-id="7f71c-177">serviceCode</span></span>       | <span data-ttu-id="7f71c-178">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-178">string</span></span>   | <span data-ttu-id="7f71c-179">Service kod</span><span class="sxs-lookup"><span data-stu-id="7f71c-179">Service code</span></span>                          |
| <span data-ttu-id="7f71c-180">serviceName</span><span class="sxs-lookup"><span data-stu-id="7f71c-180">serviceName</span></span>       | <span data-ttu-id="7f71c-181">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-181">string</span></span>   | <span data-ttu-id="7f71c-182">Tjänstnamn</span><span class="sxs-lookup"><span data-stu-id="7f71c-182">Service name</span></span>                          |
| <span data-ttu-id="7f71c-183">kanalig</span><span class="sxs-lookup"><span data-stu-id="7f71c-183">channel</span></span>           | <span data-ttu-id="7f71c-184">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-184">string</span></span>   | <span data-ttu-id="7f71c-185">Kanal namn, åter försäljare</span><span class="sxs-lookup"><span data-stu-id="7f71c-185">Channel name, reseller</span></span>                |
| <span data-ttu-id="7f71c-186">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="7f71c-186">customerTenantId</span></span>  | <span data-ttu-id="7f71c-187">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-187">string</span></span>   | <span data-ttu-id="7f71c-188">Unikt ID för kunden</span><span class="sxs-lookup"><span data-stu-id="7f71c-188">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="7f71c-189">customerName</span><span class="sxs-lookup"><span data-stu-id="7f71c-189">customerName</span></span>      | <span data-ttu-id="7f71c-190">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-190">string</span></span>   | <span data-ttu-id="7f71c-191">Kundnamn</span><span class="sxs-lookup"><span data-stu-id="7f71c-191">Customer name</span></span>                         |
| <span data-ttu-id="7f71c-192">productId</span><span class="sxs-lookup"><span data-stu-id="7f71c-192">productId</span></span>         | <span data-ttu-id="7f71c-193">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-193">string</span></span>   | <span data-ttu-id="7f71c-194">Unikt ID för produkten</span><span class="sxs-lookup"><span data-stu-id="7f71c-194">Unique identifier for the product</span></span>     |
| <span data-ttu-id="7f71c-195">Namn</span><span class="sxs-lookup"><span data-stu-id="7f71c-195">productName</span></span>       | <span data-ttu-id="7f71c-196">sträng</span><span class="sxs-lookup"><span data-stu-id="7f71c-196">string</span></span>   | <span data-ttu-id="7f71c-197">Produktnamn</span><span class="sxs-lookup"><span data-stu-id="7f71c-197">Product name</span></span>                          |
| <span data-ttu-id="7f71c-198">licensesDeployed</span><span class="sxs-lookup"><span data-stu-id="7f71c-198">licensesDeployed</span></span>  | <span data-ttu-id="7f71c-199">long</span><span class="sxs-lookup"><span data-stu-id="7f71c-199">long</span></span>     | <span data-ttu-id="7f71c-200">Antal distribuerade licenser</span><span class="sxs-lookup"><span data-stu-id="7f71c-200">Number of licenses deployed</span></span>           |
| <span data-ttu-id="7f71c-201">licensesSold</span><span class="sxs-lookup"><span data-stu-id="7f71c-201">licensesSold</span></span>      | <span data-ttu-id="7f71c-202">long</span><span class="sxs-lookup"><span data-stu-id="7f71c-202">long</span></span>     | <span data-ttu-id="7f71c-203">Antal sålda licenser</span><span class="sxs-lookup"><span data-stu-id="7f71c-203">Number of licenses sold</span></span>               |
| <span data-ttu-id="7f71c-204">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="7f71c-204">processedDateTime</span></span> | <span data-ttu-id="7f71c-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f71c-205">DateTime</span></span> | <span data-ttu-id="7f71c-206">Datum när data senast bearbetades</span><span class="sxs-lookup"><span data-stu-id="7f71c-206">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7f71c-207">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7f71c-207">Response success and error codes</span></span>

<span data-ttu-id="7f71c-208">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="7f71c-208">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7f71c-209">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7f71c-209">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7f71c-210">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7f71c-210">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7f71c-211">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7f71c-211">Response example</span></span>

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
