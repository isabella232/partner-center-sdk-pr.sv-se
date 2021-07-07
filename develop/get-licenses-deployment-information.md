---
title: Hämta information om licensdistribution
description: Så här hämtar du distributionsinformation för Office- och Dynamics-licenser.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9eb0dc655affb2216b11635e58e00ed6464d6792
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445671"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="09ec5-103">Hämta information om licensdistribution</span><span class="sxs-lookup"><span data-stu-id="09ec5-103">Get licenses deployment information</span></span>

<span data-ttu-id="09ec5-104">Så här hämtar du distributionsinformation för Office- och Dynamics-licenser.</span><span class="sxs-lookup"><span data-stu-id="09ec5-104">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09ec5-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="09ec5-105">Prerequisites</span></span>

<span data-ttu-id="09ec5-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="09ec5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="09ec5-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="09ec5-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="09ec5-108">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="09ec5-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="09ec5-109">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="09ec5-109">Request syntax</span></span>

| <span data-ttu-id="09ec5-110">Metod</span><span class="sxs-lookup"><span data-stu-id="09ec5-110">Method</span></span>  | <span data-ttu-id="09ec5-111">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="09ec5-111">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="09ec5-112">**Få**</span><span class="sxs-lookup"><span data-stu-id="09ec5-112">**GET**</span></span> | <span data-ttu-id="09ec5-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="09ec5-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="09ec5-114">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="09ec5-114">Request headers</span></span>

<span data-ttu-id="09ec5-115">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="09ec5-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="09ec5-116">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="09ec5-116">URI parameters</span></span>

| <span data-ttu-id="09ec5-117">Parameter</span><span class="sxs-lookup"><span data-stu-id="09ec5-117">Parameter</span></span>         | <span data-ttu-id="09ec5-118">Typ</span><span class="sxs-lookup"><span data-stu-id="09ec5-118">Type</span></span>     | <span data-ttu-id="09ec5-119">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="09ec5-119">Description</span></span> | <span data-ttu-id="09ec5-120">Krävs</span><span class="sxs-lookup"><span data-stu-id="09ec5-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="09ec5-121">top</span><span class="sxs-lookup"><span data-stu-id="09ec5-121">top</span></span>               | <span data-ttu-id="09ec5-122">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-122">string</span></span>   | <span data-ttu-id="09ec5-123">Antalet rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="09ec5-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="09ec5-124">Det högsta värdet och standardvärdet om inget värde anges är 10000.</span><span class="sxs-lookup"><span data-stu-id="09ec5-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="09ec5-125">Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="09ec5-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="09ec5-126">Inga</span><span class="sxs-lookup"><span data-stu-id="09ec5-126">No</span></span> |
| <span data-ttu-id="09ec5-127">hoppa över</span><span class="sxs-lookup"><span data-stu-id="09ec5-127">skip</span></span>              | <span data-ttu-id="09ec5-128">int</span><span class="sxs-lookup"><span data-stu-id="09ec5-128">int</span></span>      | <span data-ttu-id="09ec5-129">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="09ec5-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="09ec5-130">Använd den här parametern för att bläddra igenom stora datamängder.</span><span class="sxs-lookup"><span data-stu-id="09ec5-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="09ec5-131">Till exempel hämtar top=10000 och skip=0 de första 10 000 raderna med data, top=10000 och skip=10000 hämtar de nästa 10 000 raderna med data och så vidare.</span><span class="sxs-lookup"><span data-stu-id="09ec5-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="09ec5-132">Inga</span><span class="sxs-lookup"><span data-stu-id="09ec5-132">No</span></span> |
| <span data-ttu-id="09ec5-133">filter</span><span class="sxs-lookup"><span data-stu-id="09ec5-133">filter</span></span>            | <span data-ttu-id="09ec5-134">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-134">string</span></span>   | <span data-ttu-id="09ec5-135">*Filterparametern* för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="09ec5-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="09ec5-136">Varje -instruktion innehåller ett fält och värde som är associerade med `eq` `ne` operatorerna eller , och -instruktioner kan kombineras med hjälp av `and` eller `or` .</span><span class="sxs-lookup"><span data-stu-id="09ec5-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="09ec5-137">Här är några exempel *på filterparametrar:*</span><span class="sxs-lookup"><span data-stu-id="09ec5-137">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="09ec5-138">*filter=serviceCode eq 'O365'*</span><span class="sxs-lookup"><span data-stu-id="09ec5-138">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="09ec5-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="09ec5-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="09ec5-140">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="09ec5-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="09ec5-141">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="09ec5-141">**serviceCode**</span></span><br/><span data-ttu-id="09ec5-142">**Tjänstnamn**</span><span class="sxs-lookup"><span data-stu-id="09ec5-142">**serviceName**</span></span><br/><span data-ttu-id="09ec5-143">**Kanal**</span><span class="sxs-lookup"><span data-stu-id="09ec5-143">**channel**</span></span><br/><span data-ttu-id="09ec5-144">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="09ec5-144">**customerTenantId**</span></span><br/><span data-ttu-id="09ec5-145">**customerName**</span><span class="sxs-lookup"><span data-stu-id="09ec5-145">**customerName**</span></span><br/><span data-ttu-id="09ec5-146">**Produktionen**</span><span class="sxs-lookup"><span data-stu-id="09ec5-146">**productId**</span></span><br/><span data-ttu-id="09ec5-147">**Productname**</span><span class="sxs-lookup"><span data-stu-id="09ec5-147">**productName**</span></span>  | <span data-ttu-id="09ec5-148">Inga</span><span class="sxs-lookup"><span data-stu-id="09ec5-148">No</span></span> |
| <span data-ttu-id="09ec5-149">groupby</span><span class="sxs-lookup"><span data-stu-id="09ec5-149">groupby</span></span>           | <span data-ttu-id="09ec5-150">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-150">string</span></span>   | <span data-ttu-id="09ec5-151">En instruktion som endast tillämpar dataaggregering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="09ec5-151">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="09ec5-152">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="09ec5-152">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="09ec5-153">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="09ec5-153">**serviceCode**</span></span><br/><span data-ttu-id="09ec5-154">**Tjänstnamn**</span><span class="sxs-lookup"><span data-stu-id="09ec5-154">**serviceName**</span></span><br/><span data-ttu-id="09ec5-155">**Kanal**</span><span class="sxs-lookup"><span data-stu-id="09ec5-155">**channel**</span></span><br/><span data-ttu-id="09ec5-156">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="09ec5-156">**customerTenantId**</span></span><br/><span data-ttu-id="09ec5-157">**customerName**</span><span class="sxs-lookup"><span data-stu-id="09ec5-157">**customerName**</span></span><br/><span data-ttu-id="09ec5-158">**Produktionen**</span><span class="sxs-lookup"><span data-stu-id="09ec5-158">**productId**</span></span><br/><span data-ttu-id="09ec5-159">**Productname**</span><span class="sxs-lookup"><span data-stu-id="09ec5-159">**productName**</span></span><br/><br/> <span data-ttu-id="09ec5-160">De returnerade dataraderna innehåller de fält som anges i *parametern groupby* och följande:</span><span class="sxs-lookup"><span data-stu-id="09ec5-160">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="09ec5-161">**licensesDeployed**</span><span class="sxs-lookup"><span data-stu-id="09ec5-161">**licensesDeployed**</span></span><br/><span data-ttu-id="09ec5-162">**licenserSåld**</span><span class="sxs-lookup"><span data-stu-id="09ec5-162">**licensesSold**</span></span>  | <span data-ttu-id="09ec5-163">Inga</span><span class="sxs-lookup"><span data-stu-id="09ec5-163">No</span></span> |
| <span data-ttu-id="09ec5-164">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="09ec5-164">processedDateTime</span></span> | <span data-ttu-id="09ec5-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="09ec5-165">DateTime</span></span> | <span data-ttu-id="09ec5-166">Du kan ange det datum då användningsdata bearbetades.</span><span class="sxs-lookup"><span data-stu-id="09ec5-166">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="09ec5-167">Standardvärdet är det senaste datumet då data bearbetades</span><span class="sxs-lookup"><span data-stu-id="09ec5-167">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="09ec5-168">Inga</span><span class="sxs-lookup"><span data-stu-id="09ec5-168">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="09ec5-169">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="09ec5-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="09ec5-170">REST-svar</span><span class="sxs-lookup"><span data-stu-id="09ec5-170">REST response</span></span>

<span data-ttu-id="09ec5-171">Om det lyckas innehåller svarstexten följande fält som innehåller data om de distribuerade licenserna.</span><span class="sxs-lookup"><span data-stu-id="09ec5-171">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="09ec5-172">Fält</span><span class="sxs-lookup"><span data-stu-id="09ec5-172">Field</span></span>             | <span data-ttu-id="09ec5-173">Typ</span><span class="sxs-lookup"><span data-stu-id="09ec5-173">Type</span></span>     | <span data-ttu-id="09ec5-174">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="09ec5-174">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="09ec5-175">serviceCode</span><span class="sxs-lookup"><span data-stu-id="09ec5-175">serviceCode</span></span>       | <span data-ttu-id="09ec5-176">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-176">string</span></span>   | <span data-ttu-id="09ec5-177">Tjänstkod</span><span class="sxs-lookup"><span data-stu-id="09ec5-177">Service code</span></span>                          |
| <span data-ttu-id="09ec5-178">Tjänstnamn</span><span class="sxs-lookup"><span data-stu-id="09ec5-178">serviceName</span></span>       | <span data-ttu-id="09ec5-179">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-179">string</span></span>   | <span data-ttu-id="09ec5-180">Tjänstnamn</span><span class="sxs-lookup"><span data-stu-id="09ec5-180">Service name</span></span>                          |
| <span data-ttu-id="09ec5-181">Kanal</span><span class="sxs-lookup"><span data-stu-id="09ec5-181">channel</span></span>           | <span data-ttu-id="09ec5-182">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-182">string</span></span>   | <span data-ttu-id="09ec5-183">Kanalnamn, återförsäljare</span><span class="sxs-lookup"><span data-stu-id="09ec5-183">Channel name, reseller</span></span>                |
| <span data-ttu-id="09ec5-184">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="09ec5-184">customerTenantId</span></span>  | <span data-ttu-id="09ec5-185">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-185">string</span></span>   | <span data-ttu-id="09ec5-186">Unik identifierare för kunden</span><span class="sxs-lookup"><span data-stu-id="09ec5-186">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="09ec5-187">customerName</span><span class="sxs-lookup"><span data-stu-id="09ec5-187">customerName</span></span>      | <span data-ttu-id="09ec5-188">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-188">string</span></span>   | <span data-ttu-id="09ec5-189">Kundnamn</span><span class="sxs-lookup"><span data-stu-id="09ec5-189">Customer name</span></span>                         |
| <span data-ttu-id="09ec5-190">productId</span><span class="sxs-lookup"><span data-stu-id="09ec5-190">productId</span></span>         | <span data-ttu-id="09ec5-191">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-191">string</span></span>   | <span data-ttu-id="09ec5-192">Unik identifierare för produkten</span><span class="sxs-lookup"><span data-stu-id="09ec5-192">Unique identifier for the product</span></span>     |
| <span data-ttu-id="09ec5-193">Productname</span><span class="sxs-lookup"><span data-stu-id="09ec5-193">productName</span></span>       | <span data-ttu-id="09ec5-194">sträng</span><span class="sxs-lookup"><span data-stu-id="09ec5-194">string</span></span>   | <span data-ttu-id="09ec5-195">Produktnamn</span><span class="sxs-lookup"><span data-stu-id="09ec5-195">Product name</span></span>                          |
| <span data-ttu-id="09ec5-196">licensesDeployed</span><span class="sxs-lookup"><span data-stu-id="09ec5-196">licensesDeployed</span></span>  | <span data-ttu-id="09ec5-197">long</span><span class="sxs-lookup"><span data-stu-id="09ec5-197">long</span></span>     | <span data-ttu-id="09ec5-198">Antal distribuerade licenser</span><span class="sxs-lookup"><span data-stu-id="09ec5-198">Number of licenses deployed</span></span>           |
| <span data-ttu-id="09ec5-199">licenserSåld</span><span class="sxs-lookup"><span data-stu-id="09ec5-199">licensesSold</span></span>      | <span data-ttu-id="09ec5-200">long</span><span class="sxs-lookup"><span data-stu-id="09ec5-200">long</span></span>     | <span data-ttu-id="09ec5-201">Antal sålda licenser</span><span class="sxs-lookup"><span data-stu-id="09ec5-201">Number of licenses sold</span></span>               |
| <span data-ttu-id="09ec5-202">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="09ec5-202">processedDateTime</span></span> | <span data-ttu-id="09ec5-203">DateTime</span><span class="sxs-lookup"><span data-stu-id="09ec5-203">DateTime</span></span> | <span data-ttu-id="09ec5-204">Datum då data senast bearbetades</span><span class="sxs-lookup"><span data-stu-id="09ec5-204">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="09ec5-205">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="09ec5-205">Response success and error codes</span></span>

<span data-ttu-id="09ec5-206">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="09ec5-206">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="09ec5-207">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="09ec5-207">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="09ec5-208">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="09ec5-208">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="09ec5-209">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="09ec5-209">Response example</span></span>

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
