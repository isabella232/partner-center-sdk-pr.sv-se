---
title: Hämta en lista över tillgängliga för en SKU (efter land)
description: Så här hämtar du en samling tillgänglighet för den angivna produkten och SKU:n efter kundland.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b29c005e74ad8a4da547a888b78e4599e74ebd02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874541"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="963d6-103">Hämta en lista över tillgängliga för en SKU (efter land)</span><span class="sxs-lookup"><span data-stu-id="963d6-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="963d6-104">Den här artikeln beskriver hur du hämtar en samling tillgänglighet i ett visst land för en angiven produkt och SKU.</span><span class="sxs-lookup"><span data-stu-id="963d6-104">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="963d6-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="963d6-105">Prerequisites</span></span>

- <span data-ttu-id="963d6-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="963d6-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="963d6-107">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="963d6-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="963d6-108">En produktidentifierare.</span><span class="sxs-lookup"><span data-stu-id="963d6-108">A product identifier.</span></span>

- <span data-ttu-id="963d6-109">En SKU-identifierare.</span><span class="sxs-lookup"><span data-stu-id="963d6-109">A SKU identifier.</span></span>

- <span data-ttu-id="963d6-110">Ett land.</span><span class="sxs-lookup"><span data-stu-id="963d6-110">A country.</span></span>

## <a name="c"></a><span data-ttu-id="963d6-111">C\#</span><span class="sxs-lookup"><span data-stu-id="963d6-111">C\#</span></span>

<span data-ttu-id="963d6-112">Hämta listan över [tillgänglighet för en](product-resources.md#availability) [SKU:](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="963d6-112">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="963d6-113">Följ stegen i Hämta [en SKU efter ID för](get-a-sku-by-id.md) att hämta gränssnittet för en specifik SKU:s åtgärder.</span><span class="sxs-lookup"><span data-stu-id="963d6-113">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="963d6-114">Från SKU-gränssnittet väljer du **egenskapen Availabilities** (Tillgänglighet) för att hämta ett gränssnitt med åtgärderna för tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="963d6-114">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="963d6-115">(Valfritt) Använd metoden **ByTargetSegment()** för att filtrera tillgängligheten efter målsegment.</span><span class="sxs-lookup"><span data-stu-id="963d6-115">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="963d6-116">Anropa **Get()** eller **GetAsync()** för att hämta en samling tillgänglighet för denna SKU.</span><span class="sxs-lookup"><span data-stu-id="963d6-116">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="963d6-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="963d6-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="963d6-118">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="963d6-118">Request syntax</span></span>

| <span data-ttu-id="963d6-119">Metod</span><span class="sxs-lookup"><span data-stu-id="963d6-119">Method</span></span>  | <span data-ttu-id="963d6-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="963d6-120">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="963d6-121">**Få**</span><span class="sxs-lookup"><span data-stu-id="963d6-121">**GET**</span></span> | <span data-ttu-id="963d6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="963d6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="963d6-123">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="963d6-123">URI parameters</span></span>

<span data-ttu-id="963d6-124">Använd följande sökväg och frågeparametrar för att hämta en lista över tillgänglighet för en SKU.</span><span class="sxs-lookup"><span data-stu-id="963d6-124">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="963d6-125">Namn</span><span class="sxs-lookup"><span data-stu-id="963d6-125">Name</span></span>                   | <span data-ttu-id="963d6-126">Typ</span><span class="sxs-lookup"><span data-stu-id="963d6-126">Type</span></span>     | <span data-ttu-id="963d6-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="963d6-127">Required</span></span> | <span data-ttu-id="963d6-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="963d6-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="963d6-129">produkt-id</span><span class="sxs-lookup"><span data-stu-id="963d6-129">product-id</span></span>             | <span data-ttu-id="963d6-130">sträng</span><span class="sxs-lookup"><span data-stu-id="963d6-130">string</span></span>   | <span data-ttu-id="963d6-131">Ja</span><span class="sxs-lookup"><span data-stu-id="963d6-131">Yes</span></span>      | <span data-ttu-id="963d6-132">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="963d6-132">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="963d6-133">sku-id</span><span class="sxs-lookup"><span data-stu-id="963d6-133">sku-id</span></span>                 | <span data-ttu-id="963d6-134">sträng</span><span class="sxs-lookup"><span data-stu-id="963d6-134">string</span></span>   | <span data-ttu-id="963d6-135">Ja</span><span class="sxs-lookup"><span data-stu-id="963d6-135">Yes</span></span>      | <span data-ttu-id="963d6-136">En sträng som identifierar SKU:n.</span><span class="sxs-lookup"><span data-stu-id="963d6-136">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="963d6-137">landskod</span><span class="sxs-lookup"><span data-stu-id="963d6-137">country-code</span></span>           | <span data-ttu-id="963d6-138">sträng</span><span class="sxs-lookup"><span data-stu-id="963d6-138">string</span></span>   | <span data-ttu-id="963d6-139">Ja</span><span class="sxs-lookup"><span data-stu-id="963d6-139">Yes</span></span>      | <span data-ttu-id="963d6-140">Ett lands-/regions-ID.</span><span class="sxs-lookup"><span data-stu-id="963d6-140">A country/region ID.</span></span>                                            |
| <span data-ttu-id="963d6-141">målsegment</span><span class="sxs-lookup"><span data-stu-id="963d6-141">target-segment</span></span>         | <span data-ttu-id="963d6-142">sträng</span><span class="sxs-lookup"><span data-stu-id="963d6-142">string</span></span>   | <span data-ttu-id="963d6-143">No</span><span class="sxs-lookup"><span data-stu-id="963d6-143">No</span></span>       | <span data-ttu-id="963d6-144">En sträng som identifierar målsegmentet som används för filtrering.</span><span class="sxs-lookup"><span data-stu-id="963d6-144">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="963d6-145">reservationScope</span><span class="sxs-lookup"><span data-stu-id="963d6-145">reservationScope</span></span> | <span data-ttu-id="963d6-146">sträng</span><span class="sxs-lookup"><span data-stu-id="963d6-146">string</span></span>   | <span data-ttu-id="963d6-147">No</span><span class="sxs-lookup"><span data-stu-id="963d6-147">No</span></span> | <span data-ttu-id="963d6-148">När du frågar efter en lista över tillgänglighet för en Azure-reservations-SKU anger du för att hämta en lista över tillgänglighet som `reservationScope=AzurePlan` gäller för AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="963d6-148">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities that are applicable to AzurePlan.</span></span> <span data-ttu-id="963d6-149">Undanta den här parametern för att hämta en lista över tillgänglighet som gäller för Microsoft Azure-prenumerationer (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="963d6-149">Exclude this parameter to get a list of availabilities that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="963d6-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="963d6-150">Request headers</span></span>

<span data-ttu-id="963d6-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="963d6-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="963d6-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="963d6-152">Request body</span></span>

<span data-ttu-id="963d6-153">Inga.</span><span class="sxs-lookup"><span data-stu-id="963d6-153">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="963d6-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="963d6-154">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="963d6-155">Tillgänglighet för SKU efter land</span><span class="sxs-lookup"><span data-stu-id="963d6-155">Availabilities for SKU by country</span></span>

<span data-ttu-id="963d6-156">Följ det här exemplet för att hämta en lista över tillgänglighet för en viss SKU efter land:</span><span class="sxs-lookup"><span data-stu-id="963d6-156">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="963d6-157">Tillgänglighet för VM-reservationer (Azure-plan)</span><span class="sxs-lookup"><span data-stu-id="963d6-157">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="963d6-158">Följ det här exemplet för att hämta en lista över tillgänglighet per land för AZURE VM-reservations-SKU:er.</span><span class="sxs-lookup"><span data-stu-id="963d6-158">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="963d6-159">Det här exemplet är för SKU:er som gäller för Azure-planer:</span><span class="sxs-lookup"><span data-stu-id="963d6-159">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="963d6-160">Tillgänglighet för VM-reservationer för Microsoft Azure prenumerationer (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="963d6-160">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="963d6-161">Följ det här exemplet för att hämta en lista över tillgänglighet per land för Azure VM-reservationer som gäller för Microsoft Azure-prenumerationer (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="963d6-161">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="963d6-162">REST-svar</span><span class="sxs-lookup"><span data-stu-id="963d6-162">REST response</span></span>

<span data-ttu-id="963d6-163">Om det lyckas innehåller svarstexten en samling [**tillgänglighetsresurser.**](product-resources.md#availability)</span><span class="sxs-lookup"><span data-stu-id="963d6-163">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="963d6-164">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="963d6-164">Response success and error codes</span></span>

<span data-ttu-id="963d6-165">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="963d6-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="963d6-166">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="963d6-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="963d6-167">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="963d6-167">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="963d6-168">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="963d6-168">This method returns the following error codes:</span></span>

| <span data-ttu-id="963d6-169">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="963d6-169">HTTP Status Code</span></span>     | <span data-ttu-id="963d6-170">Felkod</span><span class="sxs-lookup"><span data-stu-id="963d6-170">Error code</span></span>   | <span data-ttu-id="963d6-171">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="963d6-171">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="963d6-172">403</span><span class="sxs-lookup"><span data-stu-id="963d6-172">403</span></span>                  | <span data-ttu-id="963d6-173">400030</span><span class="sxs-lookup"><span data-stu-id="963d6-173">400030</span></span>       | <span data-ttu-id="963d6-174">Åtkomst till det begärda **targetSegment** tillåts inte.</span><span class="sxs-lookup"><span data-stu-id="963d6-174">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="963d6-175">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="963d6-175">Response example</span></span>

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
