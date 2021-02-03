---
title: Hämta en lista över tillgängliga för en SKU (efter land)
description: 'Så här hämtar du en samling tillgänglighet för den angivna produkten och SKU: n per kund land.'
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769123"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="82743-103">Hämta en lista över tillgängliga för en SKU (efter land)</span><span class="sxs-lookup"><span data-stu-id="82743-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="82743-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="82743-104">**Applies to:**</span></span>

- <span data-ttu-id="82743-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="82743-105">Partner Center</span></span>

<span data-ttu-id="82743-106">Den här artikeln beskriver hur du hämtar en samling tillgänglighet i ett visst land för en angiven produkt och SKU.</span><span class="sxs-lookup"><span data-stu-id="82743-106">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82743-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="82743-107">Prerequisites</span></span>

- <span data-ttu-id="82743-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="82743-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="82743-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="82743-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="82743-110">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="82743-110">A product identifier.</span></span>

- <span data-ttu-id="82743-111">Ett SKU-ID.</span><span class="sxs-lookup"><span data-stu-id="82743-111">A SKU identifier.</span></span>

- <span data-ttu-id="82743-112">Ett land.</span><span class="sxs-lookup"><span data-stu-id="82743-112">A country.</span></span>

## <a name="c"></a><span data-ttu-id="82743-113">C\#</span><span class="sxs-lookup"><span data-stu-id="82743-113">C\#</span></span>

<span data-ttu-id="82743-114">Hämta listan över [tillgänglighet](product-resources.md#availability) för en [SKU](product-resources.md#sku):</span><span class="sxs-lookup"><span data-stu-id="82743-114">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="82743-115">Följ stegen i [Hämta ett SKU efter ID](get-a-sku-by-id.md) för att hämta gränssnittet för en speciell SKU: s åtgärder.</span><span class="sxs-lookup"><span data-stu-id="82743-115">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="82743-116">Välj egenskapen **tillgänglighet** från SKU-gränssnittet för att hämta ett gränssnitt med åtgärder för tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="82743-116">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="82743-117">Valfritt Använd metoden **ByTargetSegment ()** för att filtrera tillgänglighet efter mål segment.</span><span class="sxs-lookup"><span data-stu-id="82743-117">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="82743-118">Anropa **Get ()** eller **GetAsync ()** för att hämta en samling av tillgänglighet för denna SKU.</span><span class="sxs-lookup"><span data-stu-id="82743-118">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a><span data-ttu-id="82743-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="82743-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="82743-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="82743-120">Request syntax</span></span>

| <span data-ttu-id="82743-121">Metod</span><span class="sxs-lookup"><span data-stu-id="82743-121">Method</span></span>  | <span data-ttu-id="82743-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="82743-122">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="82743-123">**TA**</span><span class="sxs-lookup"><span data-stu-id="82743-123">**GET**</span></span> | <span data-ttu-id="82743-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities? land = {Country-code} &targetSegment = {Target-segment} http/1.1</span><span class="sxs-lookup"><span data-stu-id="82743-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="82743-125">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="82743-125">URI parameters</span></span>

<span data-ttu-id="82743-126">Använd följande sökväg och frågeparametrar för att hämta en lista över tillgänglighet för en SKU.</span><span class="sxs-lookup"><span data-stu-id="82743-126">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="82743-127">Namn</span><span class="sxs-lookup"><span data-stu-id="82743-127">Name</span></span>                   | <span data-ttu-id="82743-128">Typ</span><span class="sxs-lookup"><span data-stu-id="82743-128">Type</span></span>     | <span data-ttu-id="82743-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="82743-129">Required</span></span> | <span data-ttu-id="82743-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="82743-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="82743-131">produkt-ID</span><span class="sxs-lookup"><span data-stu-id="82743-131">product-id</span></span>             | <span data-ttu-id="82743-132">sträng</span><span class="sxs-lookup"><span data-stu-id="82743-132">string</span></span>   | <span data-ttu-id="82743-133">Yes</span><span class="sxs-lookup"><span data-stu-id="82743-133">Yes</span></span>      | <span data-ttu-id="82743-134">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="82743-134">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="82743-135">SKU-ID</span><span class="sxs-lookup"><span data-stu-id="82743-135">sku-id</span></span>                 | <span data-ttu-id="82743-136">sträng</span><span class="sxs-lookup"><span data-stu-id="82743-136">string</span></span>   | <span data-ttu-id="82743-137">Yes</span><span class="sxs-lookup"><span data-stu-id="82743-137">Yes</span></span>      | <span data-ttu-id="82743-138">En sträng som identifierar SKU: n.</span><span class="sxs-lookup"><span data-stu-id="82743-138">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="82743-139">landskod</span><span class="sxs-lookup"><span data-stu-id="82743-139">country-code</span></span>           | <span data-ttu-id="82743-140">sträng</span><span class="sxs-lookup"><span data-stu-id="82743-140">string</span></span>   | <span data-ttu-id="82743-141">Yes</span><span class="sxs-lookup"><span data-stu-id="82743-141">Yes</span></span>      | <span data-ttu-id="82743-142">Ett land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="82743-142">A country/region ID.</span></span>                                            |
| <span data-ttu-id="82743-143">mål segment</span><span class="sxs-lookup"><span data-stu-id="82743-143">target-segment</span></span>         | <span data-ttu-id="82743-144">sträng</span><span class="sxs-lookup"><span data-stu-id="82743-144">string</span></span>   | <span data-ttu-id="82743-145">No</span><span class="sxs-lookup"><span data-stu-id="82743-145">No</span></span>       | <span data-ttu-id="82743-146">En sträng som identifierar det mål segment som används för filtrering.</span><span class="sxs-lookup"><span data-stu-id="82743-146">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="82743-147">reservationScope</span><span class="sxs-lookup"><span data-stu-id="82743-147">reservationScope</span></span> | <span data-ttu-id="82743-148">sträng</span><span class="sxs-lookup"><span data-stu-id="82743-148">string</span></span>   | <span data-ttu-id="82743-149">No</span><span class="sxs-lookup"><span data-stu-id="82743-149">No</span></span> | <span data-ttu-id="82743-150">När du frågar efter en lista över tillgänglighet för en Azure reservations-SKU, anger `reservationScope=AzurePlan` du för att hämta en lista över tillgänglighet som är tillämpliga på AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="82743-150">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities which are applicable to AzurePlan.</span></span> <span data-ttu-id="82743-151">Undanta den här parametern för att hämta en lista över tillgänglighet som är tillämpliga på Microsoft Azure (MS-AZR-0145P)-prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="82743-151">Exclude this parameter to get a list of availabilities which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="82743-152">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="82743-152">Request headers</span></span>

<span data-ttu-id="82743-153">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="82743-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="82743-154">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="82743-154">Request body</span></span>

<span data-ttu-id="82743-155">Inga.</span><span class="sxs-lookup"><span data-stu-id="82743-155">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="82743-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="82743-156">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="82743-157">Tillgänglighet för SKU efter land</span><span class="sxs-lookup"><span data-stu-id="82743-157">Availabilities for SKU by country</span></span>

<span data-ttu-id="82743-158">Följ det här exemplet för att hämta en lista över tillgänglighet för en specifik SKU efter land:</span><span class="sxs-lookup"><span data-stu-id="82743-158">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="82743-159">Tillgänglighet för VM-reservationer (Azure-plan)</span><span class="sxs-lookup"><span data-stu-id="82743-159">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="82743-160">Följ det här exemplet för att hämta en lista över tillgänglighet efter land för Azure VM reservation SKU: er.</span><span class="sxs-lookup"><span data-stu-id="82743-160">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="82743-161">Det här exemplet avser SKU: er som gäller för Azure-planer:</span><span class="sxs-lookup"><span data-stu-id="82743-161">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="82743-162">Tillgänglighet för VM-reservationer för Microsoft Azure (MS-AZR-0145P)-prenumerationer</span><span class="sxs-lookup"><span data-stu-id="82743-162">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="82743-163">Följ det här exemplet för att hämta en lista över tillgänglighet efter land för Azure VM-reservationer som är tillämpliga på Microsoft Azure (MS-AZR-0145P)-prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="82743-163">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="82743-164">REST-svar</span><span class="sxs-lookup"><span data-stu-id="82743-164">REST response</span></span>

<span data-ttu-id="82743-165">Om det lyckas innehåller svars texten en samling [**tillgänglighets**](product-resources.md#availability) resurser.</span><span class="sxs-lookup"><span data-stu-id="82743-165">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="82743-166">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="82743-166">Response success and error codes</span></span>

<span data-ttu-id="82743-167">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="82743-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="82743-168">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="82743-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="82743-169">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="82743-169">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="82743-170">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="82743-170">This method returns the following error codes:</span></span>

| <span data-ttu-id="82743-171">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="82743-171">HTTP Status Code</span></span>     | <span data-ttu-id="82743-172">Felkod</span><span class="sxs-lookup"><span data-stu-id="82743-172">Error code</span></span>   | <span data-ttu-id="82743-173">Description</span><span class="sxs-lookup"><span data-stu-id="82743-173">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="82743-174">403</span><span class="sxs-lookup"><span data-stu-id="82743-174">403</span></span>                  | <span data-ttu-id="82743-175">400030</span><span class="sxs-lookup"><span data-stu-id="82743-175">400030</span></span>       | <span data-ttu-id="82743-176">Åtkomst till den begärda **targetSegment** är inte tillåten.</span><span class="sxs-lookup"><span data-stu-id="82743-176">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="82743-177">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="82743-177">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
            "defaultCurrency": {
                "code": "USD",
                "symbol": "$"
            },
            "segment": "commercial",
            "country": "US",
            "isPurchasable": true,
            "isRenewable": false,
            "terms": [{
                "duration": "P1Y",
                "description": "1 Year Prepaid"
            }],
            "product": { ... },
            "sku": { ... },
            "links": {
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
