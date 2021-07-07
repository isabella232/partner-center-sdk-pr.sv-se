---
title: Hämta tillgängligheten efter ID
description: Hämtar tillgängligheten för den angivna produkten och SKU:n med hjälp av ett tillgänglighets-ID.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c31bc12d8d484cc8042f36aa865145600d9e6738
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760206"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="ad297-103">Hämta tillgängligheten efter ID</span><span class="sxs-lookup"><span data-stu-id="ad297-103">Get the availability by ID</span></span>

<span data-ttu-id="ad297-104">Hämtar tillgängligheten för den angivna produkten och SKU:n med hjälp av ett tillgänglighets-ID.</span><span class="sxs-lookup"><span data-stu-id="ad297-104">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad297-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ad297-105">Prerequisites</span></span>

- <span data-ttu-id="ad297-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ad297-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ad297-107">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ad297-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ad297-108">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="ad297-108">A product ID.</span></span>

- <span data-ttu-id="ad297-109">Ett SKU-ID.</span><span class="sxs-lookup"><span data-stu-id="ad297-109">A SKU ID.</span></span>

- <span data-ttu-id="ad297-110">Ett tillgänglighets-ID.</span><span class="sxs-lookup"><span data-stu-id="ad297-110">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="ad297-111">C\#</span><span class="sxs-lookup"><span data-stu-id="ad297-111">C\#</span></span>

<span data-ttu-id="ad297-112">Om du vill [](product-resources.md#availability)ha information om en specifik tillgänglighet börjar du med att följa stegen i Hämta en [SKU](get-a-sku-by-id.md) efter ID för att hämta gränssnittet för en [specifik SKU:ns](product-resources.md#sku) åtgärder.</span><span class="sxs-lookup"><span data-stu-id="ad297-112">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="ad297-113">Från det resulterande gränssnittet väljer du **egenskapen Availabilities (Tillgänglighet)** för att hämta ett gränssnitt med tillgängliga åtgärder för Tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="ad297-113">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="ad297-114">Därefter skickar du tillgänglighets-ID:t till **metoden ById()** för att hämta åtgärderna för den specifika tillgängligheten och anropar **sedan Get()** eller **GetAsync()** för att hämta tillgänglighetsinformationen.</span><span class="sxs-lookup"><span data-stu-id="ad297-114">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="ad297-115">Java</span><span class="sxs-lookup"><span data-stu-id="ad297-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="ad297-116">Om du vill [](product-resources.md#availability)ha information om en specifik tillgänglighet börjar du med att följa stegen i Hämta en [SKU](get-a-sku-by-id.md) efter ID för att hämta gränssnittet för en [specifik SKU:ns](product-resources.md#sku) åtgärder.</span><span class="sxs-lookup"><span data-stu-id="ad297-116">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="ad297-117">Från det resulterande gränssnittet väljer du funktionen **getAvailabilities** för att hämta ett gränssnitt med tillgängliga åtgärder för tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="ad297-117">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="ad297-118">Därefter skickar du tillgänglighets-ID:t till **funktionen byId()** för att hämta åtgärderna för den specifika tillgängligheten och anropar **sedan funktionen get()** för att hämta tillgänglighetsinformationen.</span><span class="sxs-lookup"><span data-stu-id="ad297-118">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="ad297-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad297-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="ad297-120">Om du vill [](product-resources.md#availability)ha information om en specifik tillgänglighet kör du [**parametrarna Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) och **availabilityId,** **CountryCode,** **ProductId** och **SkuId** för att hämta tillgänglighetsinformationen.</span><span class="sxs-lookup"><span data-stu-id="ad297-120">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="ad297-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ad297-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ad297-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ad297-122">Request syntax</span></span>

| <span data-ttu-id="ad297-123">Metod</span><span class="sxs-lookup"><span data-stu-id="ad297-123">Method</span></span>  | <span data-ttu-id="ad297-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ad297-124">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad297-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="ad297-125">**GET**</span></span> | <span data-ttu-id="ad297-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ad297-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="ad297-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ad297-127">URI parameter</span></span>

<span data-ttu-id="ad297-128">Använd följande sökväg och frågeparametrar för att få en specifik tillgänglighet med hjälp av ett tillgänglighets-ID.</span><span class="sxs-lookup"><span data-stu-id="ad297-128">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="ad297-129">Namn</span><span class="sxs-lookup"><span data-stu-id="ad297-129">Name</span></span>                   | <span data-ttu-id="ad297-130">Typ</span><span class="sxs-lookup"><span data-stu-id="ad297-130">Type</span></span>     | <span data-ttu-id="ad297-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ad297-131">Required</span></span> | <span data-ttu-id="ad297-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ad297-132">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="ad297-133">produkt-id</span><span class="sxs-lookup"><span data-stu-id="ad297-133">product-id</span></span>             | <span data-ttu-id="ad297-134">sträng</span><span class="sxs-lookup"><span data-stu-id="ad297-134">string</span></span>   | <span data-ttu-id="ad297-135">Ja</span><span class="sxs-lookup"><span data-stu-id="ad297-135">Yes</span></span>      | <span data-ttu-id="ad297-136">En GUID-formaterad sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="ad297-136">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="ad297-137">sku-id</span><span class="sxs-lookup"><span data-stu-id="ad297-137">sku-id</span></span>                 | <span data-ttu-id="ad297-138">sträng</span><span class="sxs-lookup"><span data-stu-id="ad297-138">string</span></span>   | <span data-ttu-id="ad297-139">Ja</span><span class="sxs-lookup"><span data-stu-id="ad297-139">Yes</span></span>      | <span data-ttu-id="ad297-140">En GUID-formaterad sträng som identifierar SKU:n.</span><span class="sxs-lookup"><span data-stu-id="ad297-140">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="ad297-141">tillgänglighets-id</span><span class="sxs-lookup"><span data-stu-id="ad297-141">availability-id</span></span>        | <span data-ttu-id="ad297-142">sträng</span><span class="sxs-lookup"><span data-stu-id="ad297-142">string</span></span>   | <span data-ttu-id="ad297-143">Ja</span><span class="sxs-lookup"><span data-stu-id="ad297-143">Yes</span></span>      | <span data-ttu-id="ad297-144">En GUID-formaterad sträng som identifierar tillgängligheten.</span><span class="sxs-lookup"><span data-stu-id="ad297-144">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="ad297-145">landskod</span><span class="sxs-lookup"><span data-stu-id="ad297-145">country-code</span></span>           | <span data-ttu-id="ad297-146">sträng</span><span class="sxs-lookup"><span data-stu-id="ad297-146">string</span></span>   | <span data-ttu-id="ad297-147">Ja</span><span class="sxs-lookup"><span data-stu-id="ad297-147">Yes</span></span>      | <span data-ttu-id="ad297-148">Ett lands-/regions-ID.</span><span class="sxs-lookup"><span data-stu-id="ad297-148">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="ad297-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ad297-149">Request headers</span></span>

<span data-ttu-id="ad297-150">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ad297-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ad297-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ad297-151">Request body</span></span>

<span data-ttu-id="ad297-152">Inga.</span><span class="sxs-lookup"><span data-stu-id="ad297-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ad297-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ad297-153">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ad297-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ad297-154">REST response</span></span>

<span data-ttu-id="ad297-155">Om det lyckas innehåller svarstexten en [tillgänglighetsresurs.](product-resources.md#availability)</span><span class="sxs-lookup"><span data-stu-id="ad297-155">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ad297-156">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ad297-156">Response success and error codes</span></span>

<span data-ttu-id="ad297-157">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ad297-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ad297-158">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ad297-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ad297-159">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ad297-159">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="ad297-160">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="ad297-160">This method returns the following error codes:</span></span>

| <span data-ttu-id="ad297-161">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="ad297-161">HTTP Status Code</span></span>     | <span data-ttu-id="ad297-162">Felkod</span><span class="sxs-lookup"><span data-stu-id="ad297-162">Error code</span></span>   | <span data-ttu-id="ad297-163">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ad297-163">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad297-164">404</span><span class="sxs-lookup"><span data-stu-id="ad297-164">404</span></span>                  | <span data-ttu-id="ad297-165">400013</span><span class="sxs-lookup"><span data-stu-id="ad297-165">400013</span></span>       | <span data-ttu-id="ad297-166">Det gick inte att hitta produkten.</span><span class="sxs-lookup"><span data-stu-id="ad297-166">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="ad297-167">404</span><span class="sxs-lookup"><span data-stu-id="ad297-167">404</span></span>                  | <span data-ttu-id="ad297-168">400018</span><span class="sxs-lookup"><span data-stu-id="ad297-168">400018</span></span>       | <span data-ttu-id="ad297-169">SKU hittades inte.</span><span class="sxs-lookup"><span data-stu-id="ad297-169">SKU was not found.</span></span>                                                                                        |
| <span data-ttu-id="ad297-170">404</span><span class="sxs-lookup"><span data-stu-id="ad297-170">404</span></span>                  | <span data-ttu-id="ad297-171">400019</span><span class="sxs-lookup"><span data-stu-id="ad297-171">400019</span></span>       | <span data-ttu-id="ad297-172">Det går inte att hitta tillgängligheten.</span><span class="sxs-lookup"><span data-stu-id="ad297-172">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="ad297-173">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ad297-173">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
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
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
