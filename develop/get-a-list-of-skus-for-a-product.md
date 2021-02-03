---
title: Hämta en lista över SKU:er för en produkt (efter land)
description: 'Du kan hämta och filtrera en samling SKU: er efter land för en produkt med hjälp av API: er för partner Center.'
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9d5ec9172ed92d33e6ff291eafd523cbc13bfbbd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769093"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="cbb81-103">Hämta en lista över SKU:er för en produkt (efter land)</span><span class="sxs-lookup"><span data-stu-id="cbb81-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="cbb81-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="cbb81-104">**Applies to:**</span></span>

- <span data-ttu-id="cbb81-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="cbb81-105">Partner Center</span></span>

<span data-ttu-id="cbb81-106">Du kan hämta en samling SKU: er som är tillgängliga i ett land för en speciell produkt med hjälp av API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="cbb81-106">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbb81-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cbb81-107">Prerequisites</span></span>

- <span data-ttu-id="cbb81-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cbb81-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cbb81-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cbb81-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cbb81-110">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="cbb81-110">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="cbb81-111">C\#</span><span class="sxs-lookup"><span data-stu-id="cbb81-111">C\#</span></span>

<span data-ttu-id="cbb81-112">Hämta listan över SKU: er för en produkt:</span><span class="sxs-lookup"><span data-stu-id="cbb81-112">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="cbb81-113">Hämta ett gränssnitt för en speciell produkt åtgärd genom att följa stegen i [Hämta en produkt efter ID](get-a-product-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="cbb81-113">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="cbb81-114">Från gränssnittet väljer du **SKU** -egenskapen för att få ett gränssnitt med tillgängliga åtgärder för SKU: er.</span><span class="sxs-lookup"><span data-stu-id="cbb81-114">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="cbb81-115">Anropa metoden **Get ()** eller **GetAsync ()** för att hämta en samling med tillgängliga SKU: er för produkten.</span><span class="sxs-lookup"><span data-stu-id="cbb81-115">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="cbb81-116">Valfritt Välj reservations omfånget med metoden **ByReservationScope ()** .</span><span class="sxs-lookup"><span data-stu-id="cbb81-116">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="cbb81-117">Valfritt Använd metoden **ByTargetSegment ()** för att filtrera SKU: er efter mål segment innan du anropar **Get ()** eller **GetAsync ()**.</span><span class="sxs-lookup"><span data-stu-id="cbb81-117">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

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

## <a name="java"></a><span data-ttu-id="cbb81-118">Java</span><span class="sxs-lookup"><span data-stu-id="cbb81-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="cbb81-119">Hämta listan över SKU: er för en produkt:</span><span class="sxs-lookup"><span data-stu-id="cbb81-119">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="cbb81-120">Hämta ett gränssnitt för en speciell produkt åtgärd genom att följa stegen i [Hämta en produkt efter ID](get-a-product-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="cbb81-120">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="cbb81-121">Från gränssnittet väljer du funktionen **getSkus** för att hämta ett gränssnitt med tillgängliga åtgärder för SKU: er.</span><span class="sxs-lookup"><span data-stu-id="cbb81-121">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="cbb81-122">Anropa funktionen **Get ()** för att hämta en samling med tillgängliga SKU: er för produkten.</span><span class="sxs-lookup"><span data-stu-id="cbb81-122">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="cbb81-123">Valfritt Använd funktionen **byTargetSegment ()** för att filtrera SKU: er efter mål segment innan du anropar **Get ()** -funktionen.</span><span class="sxs-lookup"><span data-stu-id="cbb81-123">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="cbb81-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbb81-124">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="cbb81-125">Hämta listan över SKU: er för en produkt:</span><span class="sxs-lookup"><span data-stu-id="cbb81-125">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="cbb81-126">Kör kommandot [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) .</span><span class="sxs-lookup"><span data-stu-id="cbb81-126">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="cbb81-127">Valfritt Ange **segment** parametern för att filtrera SKU: er efter mål segment.</span><span class="sxs-lookup"><span data-stu-id="cbb81-127">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="cbb81-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cbb81-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cbb81-129">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="cbb81-129">Request syntax</span></span>

| <span data-ttu-id="cbb81-130">Metod</span><span class="sxs-lookup"><span data-stu-id="cbb81-130">Method</span></span>  | <span data-ttu-id="cbb81-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cbb81-131">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cbb81-132">**TA**</span><span class="sxs-lookup"><span data-stu-id="cbb81-132">**GET**</span></span> | <span data-ttu-id="cbb81-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs? land = {Country-code} &targetSegment = {Target-segment} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cbb81-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="cbb81-134">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="cbb81-134">URI parameters</span></span>

<span data-ttu-id="cbb81-135">Använd följande sökväg och frågeparametrar för att hämta en lista över SKU: er för en produkt.</span><span class="sxs-lookup"><span data-stu-id="cbb81-135">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="cbb81-136">Namn</span><span class="sxs-lookup"><span data-stu-id="cbb81-136">Name</span></span>                   | <span data-ttu-id="cbb81-137">Typ</span><span class="sxs-lookup"><span data-stu-id="cbb81-137">Type</span></span>     | <span data-ttu-id="cbb81-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cbb81-138">Required</span></span> | <span data-ttu-id="cbb81-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cbb81-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="cbb81-140">produkt-ID</span><span class="sxs-lookup"><span data-stu-id="cbb81-140">product-id</span></span>             | <span data-ttu-id="cbb81-141">sträng</span><span class="sxs-lookup"><span data-stu-id="cbb81-141">string</span></span>   | <span data-ttu-id="cbb81-142">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb81-142">Yes</span></span>      | <span data-ttu-id="cbb81-143">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="cbb81-143">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="cbb81-144">landskod</span><span class="sxs-lookup"><span data-stu-id="cbb81-144">country-code</span></span>           | <span data-ttu-id="cbb81-145">sträng</span><span class="sxs-lookup"><span data-stu-id="cbb81-145">string</span></span>   | <span data-ttu-id="cbb81-146">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb81-146">Yes</span></span>      | <span data-ttu-id="cbb81-147">Ett land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="cbb81-147">A country/region ID.</span></span>                                            |
| <span data-ttu-id="cbb81-148">mål segment</span><span class="sxs-lookup"><span data-stu-id="cbb81-148">target-segment</span></span>         | <span data-ttu-id="cbb81-149">sträng</span><span class="sxs-lookup"><span data-stu-id="cbb81-149">string</span></span>   | <span data-ttu-id="cbb81-150">No</span><span class="sxs-lookup"><span data-stu-id="cbb81-150">No</span></span>       | <span data-ttu-id="cbb81-151">En sträng som identifierar det mål segment som används för filtrering.</span><span class="sxs-lookup"><span data-stu-id="cbb81-151">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="cbb81-152">reservationScope</span><span class="sxs-lookup"><span data-stu-id="cbb81-152">reservationScope</span></span> | <span data-ttu-id="cbb81-153">sträng</span><span class="sxs-lookup"><span data-stu-id="cbb81-153">string</span></span>   | <span data-ttu-id="cbb81-154">No</span><span class="sxs-lookup"><span data-stu-id="cbb81-154">No</span></span> | <span data-ttu-id="cbb81-155">När du frågar efter en lista över SKU: er för en Azure-reservations produkt anger `reservationScope=AzurePlan` du för att hämta en lista över SKU: er som är tillämpliga på AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="cbb81-155">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs which are applicable to AzurePlan.</span></span> <span data-ttu-id="cbb81-156">Undanta den här parametern för att hämta en lista över SKU: er för en Azure-reservations produkt som gäller för Microsoft Azure (MS-AZR-0145P)-prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="cbb81-156">Exclude this parameter to get a list of SKUs for an Azure Reservation products which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="cbb81-157">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cbb81-157">Request headers</span></span>

<span data-ttu-id="cbb81-158">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cbb81-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cbb81-159">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cbb81-159">Request body</span></span>

<span data-ttu-id="cbb81-160">Inga.</span><span class="sxs-lookup"><span data-stu-id="cbb81-160">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="cbb81-161">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cbb81-161">Request examples</span></span>

<span data-ttu-id="cbb81-162">Hämta en lista över SKU: er för en specifik produkt:</span><span class="sxs-lookup"><span data-stu-id="cbb81-162">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="cbb81-163">Hämta en lista över SKU: er för en Azure-reservations produkt.</span><span class="sxs-lookup"><span data-stu-id="cbb81-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="cbb81-164">Ta bara med SKU: er som är tillämpliga på Azure-planer och inte Microsoft Azure (MS-AZR-0145P)-prenumerationer:</span><span class="sxs-lookup"><span data-stu-id="cbb81-164">Only include the SKUs which are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="cbb81-165">Hämta en lista över SKU: er för en Azure-reservations produkt.</span><span class="sxs-lookup"><span data-stu-id="cbb81-165">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="cbb81-166">Inkludera endast SKU: er som är tillämpliga på Microsoft Azure (MS-AZR-0145P)-prenumerationer och inte Azure-planer:</span><span class="sxs-lookup"><span data-stu-id="cbb81-166">Only include the SKUs which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="cbb81-167">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cbb81-167">REST response</span></span>

<span data-ttu-id="cbb81-168">Om det lyckas innehåller svars texten en samling [SKU](product-resources.md#sku) -resurser.</span><span class="sxs-lookup"><span data-stu-id="cbb81-168">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cbb81-169">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cbb81-169">Response success and error codes</span></span>

<span data-ttu-id="cbb81-170">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="cbb81-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cbb81-171">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cbb81-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cbb81-172">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cbb81-172">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="cbb81-173">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="cbb81-173">This method returns the following error codes:</span></span>

| <span data-ttu-id="cbb81-174">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="cbb81-174">HTTP Status Code</span></span>     | <span data-ttu-id="cbb81-175">Felkod</span><span class="sxs-lookup"><span data-stu-id="cbb81-175">Error code</span></span>   | <span data-ttu-id="cbb81-176">Description</span><span class="sxs-lookup"><span data-stu-id="cbb81-176">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cbb81-177">403</span><span class="sxs-lookup"><span data-stu-id="cbb81-177">403</span></span>                  | <span data-ttu-id="cbb81-178">400030</span><span class="sxs-lookup"><span data-stu-id="cbb81-178">400030</span></span>       | <span data-ttu-id="cbb81-179">Åtkomst till den begärda targetSegment är inte tillåten.</span><span class="sxs-lookup"><span data-stu-id="cbb81-179">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="cbb81-180">404</span><span class="sxs-lookup"><span data-stu-id="cbb81-180">404</span></span>                  | <span data-ttu-id="cbb81-181">400013</span><span class="sxs-lookup"><span data-stu-id="cbb81-181">400013</span></span>       | <span data-ttu-id="cbb81-182">Det gick inte att hitta den överordnade produkten.</span><span class="sxs-lookup"><span data-stu-id="cbb81-182">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="cbb81-183">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cbb81-183">Response example</span></span>

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
