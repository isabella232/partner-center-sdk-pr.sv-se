---
title: Hämta en lista över SKU:er för en produkt (efter land)
description: Du kan hämta och filtrera en samling SKU:er efter land för en produkt med hjälp av Partner Center-API:erna.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 27a2391a22a9439461fb53764b87c1cafa68b875
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873895"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="0214d-103">Hämta en lista över SKU:er för en produkt (efter land)</span><span class="sxs-lookup"><span data-stu-id="0214d-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="0214d-104">Du kan hämta en samling SKU:er som är tillgängliga i ett land för en specifik produkt med hjälp av Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="0214d-104">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0214d-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="0214d-105">Prerequisites</span></span>

- <span data-ttu-id="0214d-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0214d-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0214d-107">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="0214d-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0214d-108">En produktidentifierare.</span><span class="sxs-lookup"><span data-stu-id="0214d-108">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="0214d-109">C\#</span><span class="sxs-lookup"><span data-stu-id="0214d-109">C\#</span></span>

<span data-ttu-id="0214d-110">Så här hämtar du listan över SKU:er för en produkt:</span><span class="sxs-lookup"><span data-stu-id="0214d-110">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="0214d-111">Hämta ett gränssnitt för en specifik produkts åtgärder genom att följa stegen i [Hämta en produkt efter ID.](get-a-product-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="0214d-111">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="0214d-112">Från gränssnittet väljer du egenskapen **SKU:er** för att hämta ett gränssnitt med tillgängliga åtgärder för SKU:er.</span><span class="sxs-lookup"><span data-stu-id="0214d-112">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="0214d-113">Anropa metoden **Get()** eller **GetAsync()** för att hämta en samling tillgängliga SKU:er för produkten.</span><span class="sxs-lookup"><span data-stu-id="0214d-113">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="0214d-114">(Valfritt) Välj reservationsomfånget med hjälp **av metoden ByReservationScope().**</span><span class="sxs-lookup"><span data-stu-id="0214d-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="0214d-115">(Valfritt) Använd metoden **ByTargetSegment()** för att filtrera SKU:erna efter målsegment innan du anropar **Get()** **eller GetAsync()**.</span><span class="sxs-lookup"><span data-stu-id="0214d-115">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="0214d-116">Java</span><span class="sxs-lookup"><span data-stu-id="0214d-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="0214d-117">Så här hämtar du listan över SKU:er för en produkt:</span><span class="sxs-lookup"><span data-stu-id="0214d-117">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="0214d-118">Hämta ett gränssnitt för en specifik produkts åtgärder genom att följa stegen i [Hämta en produkt efter ID.](get-a-product-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="0214d-118">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="0214d-119">Från gränssnittet väljer du funktionen **getSkus för att hämta** ett gränssnitt med tillgängliga åtgärder för SKU:er.</span><span class="sxs-lookup"><span data-stu-id="0214d-119">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="0214d-120">Anropa **funktionen get()** för att hämta en samling tillgängliga SKU:er för produkten.</span><span class="sxs-lookup"><span data-stu-id="0214d-120">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="0214d-121">(Valfritt) Använd funktionen **byTargetSegment()** för att filtrera SKU:er efter målsegment innan du anropar **funktionen get().**</span><span class="sxs-lookup"><span data-stu-id="0214d-121">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a><span data-ttu-id="0214d-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0214d-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="0214d-123">Så här hämtar du listan över SKU:er för en produkt:</span><span class="sxs-lookup"><span data-stu-id="0214d-123">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="0214d-124">Kör kommandot [**Get-PartnerProductSku.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md)</span><span class="sxs-lookup"><span data-stu-id="0214d-124">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="0214d-125">(Valfritt) Ange **parametern Segment** för att filtrera SKU:erna efter målsegment.</span><span class="sxs-lookup"><span data-stu-id="0214d-125">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="0214d-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="0214d-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0214d-127">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="0214d-127">Request syntax</span></span>

| <span data-ttu-id="0214d-128">Metod</span><span class="sxs-lookup"><span data-stu-id="0214d-128">Method</span></span>  | <span data-ttu-id="0214d-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="0214d-129">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0214d-130">**Få**</span><span class="sxs-lookup"><span data-stu-id="0214d-130">**GET**</span></span> | <span data-ttu-id="0214d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0214d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="0214d-132">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="0214d-132">URI parameters</span></span>

<span data-ttu-id="0214d-133">Använd följande sökväg och frågeparametrar för att hämta en lista över SKU:er för en produkt.</span><span class="sxs-lookup"><span data-stu-id="0214d-133">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="0214d-134">Namn</span><span class="sxs-lookup"><span data-stu-id="0214d-134">Name</span></span>                   | <span data-ttu-id="0214d-135">Typ</span><span class="sxs-lookup"><span data-stu-id="0214d-135">Type</span></span>     | <span data-ttu-id="0214d-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="0214d-136">Required</span></span> | <span data-ttu-id="0214d-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0214d-137">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="0214d-138">produkt-id</span><span class="sxs-lookup"><span data-stu-id="0214d-138">product-id</span></span>             | <span data-ttu-id="0214d-139">sträng</span><span class="sxs-lookup"><span data-stu-id="0214d-139">string</span></span>   | <span data-ttu-id="0214d-140">Ja</span><span class="sxs-lookup"><span data-stu-id="0214d-140">Yes</span></span>      | <span data-ttu-id="0214d-141">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="0214d-141">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="0214d-142">landskod</span><span class="sxs-lookup"><span data-stu-id="0214d-142">country-code</span></span>           | <span data-ttu-id="0214d-143">sträng</span><span class="sxs-lookup"><span data-stu-id="0214d-143">string</span></span>   | <span data-ttu-id="0214d-144">Ja</span><span class="sxs-lookup"><span data-stu-id="0214d-144">Yes</span></span>      | <span data-ttu-id="0214d-145">Ett lands-/regions-ID.</span><span class="sxs-lookup"><span data-stu-id="0214d-145">A country/region ID.</span></span>                                            |
| <span data-ttu-id="0214d-146">målsegment</span><span class="sxs-lookup"><span data-stu-id="0214d-146">target-segment</span></span>         | <span data-ttu-id="0214d-147">sträng</span><span class="sxs-lookup"><span data-stu-id="0214d-147">string</span></span>   | <span data-ttu-id="0214d-148">No</span><span class="sxs-lookup"><span data-stu-id="0214d-148">No</span></span>       | <span data-ttu-id="0214d-149">En sträng som identifierar målsegmentet som används för filtrering.</span><span class="sxs-lookup"><span data-stu-id="0214d-149">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="0214d-150">reservationScope</span><span class="sxs-lookup"><span data-stu-id="0214d-150">reservationScope</span></span> | <span data-ttu-id="0214d-151">sträng</span><span class="sxs-lookup"><span data-stu-id="0214d-151">string</span></span>   | <span data-ttu-id="0214d-152">No</span><span class="sxs-lookup"><span data-stu-id="0214d-152">No</span></span> | <span data-ttu-id="0214d-153">När du frågar efter en lista över SKU:er för en Azure-reservationsprodukt anger du för att hämta en lista över `reservationScope=AzurePlan` SKU:er som gäller för AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="0214d-153">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs that are applicable to AzurePlan.</span></span> <span data-ttu-id="0214d-154">Undanta den här parametern för att hämta en lista över SKU:er för Azure-reservationsprodukter som gäller för Microsoft Azure-prenumerationer (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="0214d-154">Exclude this parameter to get a list of SKUs for Azure Reservation products that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="0214d-155">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="0214d-155">Request headers</span></span>

<span data-ttu-id="0214d-156">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0214d-156">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0214d-157">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="0214d-157">Request body</span></span>

<span data-ttu-id="0214d-158">Inga.</span><span class="sxs-lookup"><span data-stu-id="0214d-158">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="0214d-159">Begärandeexempel</span><span class="sxs-lookup"><span data-stu-id="0214d-159">Request examples</span></span>

<span data-ttu-id="0214d-160">Hämta en lista över SKU:er för en viss produkt:</span><span class="sxs-lookup"><span data-stu-id="0214d-160">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="0214d-161">Hämta en lista över SKU:er för en Azure-reservationsprodukt.</span><span class="sxs-lookup"><span data-stu-id="0214d-161">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="0214d-162">Inkludera endast de SKU:er som gäller för Azure-planer och inte Microsoft Azure prenumerationer (MS-AZR-0145P):</span><span class="sxs-lookup"><span data-stu-id="0214d-162">Only include the SKUs that are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="0214d-163">Hämta en lista över SKU:er för en Azure-reservationsprodukt.</span><span class="sxs-lookup"><span data-stu-id="0214d-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="0214d-164">Inkludera endast de SKU:er som gäller Microsoft Azure prenumerationer (MS-AZR-0145P) och inte Azure-planer:</span><span class="sxs-lookup"><span data-stu-id="0214d-164">Only include the SKUs that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="0214d-165">REST-svar</span><span class="sxs-lookup"><span data-stu-id="0214d-165">REST response</span></span>

<span data-ttu-id="0214d-166">Om det lyckas innehåller svarstexten en samling [SKU-resurser.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="0214d-166">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0214d-167">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="0214d-167">Response success and error codes</span></span>

<span data-ttu-id="0214d-168">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="0214d-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0214d-169">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="0214d-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0214d-170">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0214d-170">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="0214d-171">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="0214d-171">This method returns the following error codes:</span></span>

| <span data-ttu-id="0214d-172">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="0214d-172">HTTP Status Code</span></span>     | <span data-ttu-id="0214d-173">Felkod</span><span class="sxs-lookup"><span data-stu-id="0214d-173">Error code</span></span>   | <span data-ttu-id="0214d-174">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0214d-174">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0214d-175">403</span><span class="sxs-lookup"><span data-stu-id="0214d-175">403</span></span>                  | <span data-ttu-id="0214d-176">400030</span><span class="sxs-lookup"><span data-stu-id="0214d-176">400030</span></span>       | <span data-ttu-id="0214d-177">Åtkomst till det begärda targetSegment tillåts inte.</span><span class="sxs-lookup"><span data-stu-id="0214d-177">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="0214d-178">404</span><span class="sxs-lookup"><span data-stu-id="0214d-178">404</span></span>                  | <span data-ttu-id="0214d-179">400013</span><span class="sxs-lookup"><span data-stu-id="0214d-179">400013</span></span>       | <span data-ttu-id="0214d-180">Den överordnade produkten hittades inte.</span><span class="sxs-lookup"><span data-stu-id="0214d-180">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="0214d-181">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="0214d-181">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
