---
title: Hämta tillgänglighet efter ID
description: 'Hämtar tillgänglighet för den angivna produkten och SKU: n med hjälp av ett tillgänglighets-ID.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768760"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="fc46a-103">Hämta tillgänglighet efter ID</span><span class="sxs-lookup"><span data-stu-id="fc46a-103">Get the availability by ID</span></span>

<span data-ttu-id="fc46a-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="fc46a-104">**Applies To**</span></span>

- <span data-ttu-id="fc46a-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="fc46a-105">Partner Center</span></span>

<span data-ttu-id="fc46a-106">Hämtar tillgänglighet för den angivna produkten och SKU: n med hjälp av ett tillgänglighets-ID.</span><span class="sxs-lookup"><span data-stu-id="fc46a-106">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc46a-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="fc46a-107">Prerequisites</span></span>

- <span data-ttu-id="fc46a-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fc46a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc46a-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="fc46a-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fc46a-110">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="fc46a-110">A product ID.</span></span>

- <span data-ttu-id="fc46a-111">ETT SKU-ID.</span><span class="sxs-lookup"><span data-stu-id="fc46a-111">A SKU ID.</span></span>

- <span data-ttu-id="fc46a-112">Ett tillgänglighets-ID.</span><span class="sxs-lookup"><span data-stu-id="fc46a-112">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="fc46a-113">C\#</span><span class="sxs-lookup"><span data-stu-id="fc46a-113">C\#</span></span>

<span data-ttu-id="fc46a-114">Om du vill ha information om en speciell [tillgänglighet](product-resources.md#availability)börjar du med att följa stegen i [Hämta en SKU efter ID](get-a-sku-by-id.md) för att hämta gränssnittet för en speciell [SKU: s](product-resources.md#sku) åtgärder.</span><span class="sxs-lookup"><span data-stu-id="fc46a-114">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="fc46a-115">Från det resulterande gränssnittet väljer du egenskapen **tillgänglighet** för att hämta ett gränssnitt med tillgängliga åtgärder för tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="fc46a-115">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="fc46a-116">Därefter skickar du tillgänglighets-ID: t till metoden **ById ()** för att hämta åtgärder för den aktuella tillgängligheten och anropa sedan **Get ()** eller **GetAsync ()** för att hämta tillgänglighets information.</span><span class="sxs-lookup"><span data-stu-id="fc46a-116">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="fc46a-117">Java</span><span class="sxs-lookup"><span data-stu-id="fc46a-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="fc46a-118">Om du vill ha information om en speciell [tillgänglighet](product-resources.md#availability)börjar du med att följa stegen i [Hämta en SKU efter ID](get-a-sku-by-id.md) för att hämta gränssnittet för en speciell [SKU: s](product-resources.md#sku) åtgärder.</span><span class="sxs-lookup"><span data-stu-id="fc46a-118">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="fc46a-119">Från det resulterande gränssnittet väljer du funktionen **getAvailabilities** för att hämta ett gränssnitt med tillgängliga åtgärder för tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="fc46a-119">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="fc46a-120">Därefter skickar du tillgänglighets-ID: t till funktionen **byId ()** för att hämta åtgärder för den aktuella tillgängligheten och anropar sedan funktionen **Get ()** för att hämta tillgänglighets informationen.</span><span class="sxs-lookup"><span data-stu-id="fc46a-120">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="fc46a-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc46a-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="fc46a-122">Om du vill ha information om en speciell [tillgänglighet](product-resources.md#availability)kör du [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) och anger **parametrarna AvailabilityId**, **CountryCode**, **ProductID** och **SkuId** för att hämta tillgänglighets informationen.</span><span class="sxs-lookup"><span data-stu-id="fc46a-122">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="fc46a-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="fc46a-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc46a-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="fc46a-124">Request syntax</span></span>

| <span data-ttu-id="fc46a-125">Metod</span><span class="sxs-lookup"><span data-stu-id="fc46a-125">Method</span></span>  | <span data-ttu-id="fc46a-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="fc46a-126">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc46a-127">**TA**</span><span class="sxs-lookup"><span data-stu-id="fc46a-127">**GET**</span></span> | <span data-ttu-id="fc46a-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities/{Availability-ID}? land = {Country-Code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fc46a-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="fc46a-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="fc46a-129">URI parameter</span></span>

<span data-ttu-id="fc46a-130">Använd följande sökväg och frågeparametrar för att få en speciell tillgänglighet med hjälp av ett tillgänglighets-ID.</span><span class="sxs-lookup"><span data-stu-id="fc46a-130">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="fc46a-131">Namn</span><span class="sxs-lookup"><span data-stu-id="fc46a-131">Name</span></span>                   | <span data-ttu-id="fc46a-132">Typ</span><span class="sxs-lookup"><span data-stu-id="fc46a-132">Type</span></span>     | <span data-ttu-id="fc46a-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="fc46a-133">Required</span></span> | <span data-ttu-id="fc46a-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="fc46a-134">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="fc46a-135">produkt-ID</span><span class="sxs-lookup"><span data-stu-id="fc46a-135">product-id</span></span>             | <span data-ttu-id="fc46a-136">sträng</span><span class="sxs-lookup"><span data-stu-id="fc46a-136">string</span></span>   | <span data-ttu-id="fc46a-137">Yes</span><span class="sxs-lookup"><span data-stu-id="fc46a-137">Yes</span></span>      | <span data-ttu-id="fc46a-138">En GUID-formaterad sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="fc46a-138">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="fc46a-139">SKU-ID</span><span class="sxs-lookup"><span data-stu-id="fc46a-139">sku-id</span></span>                 | <span data-ttu-id="fc46a-140">sträng</span><span class="sxs-lookup"><span data-stu-id="fc46a-140">string</span></span>   | <span data-ttu-id="fc46a-141">Yes</span><span class="sxs-lookup"><span data-stu-id="fc46a-141">Yes</span></span>      | <span data-ttu-id="fc46a-142">En GUID-formaterad sträng som identifierar SKU: n.</span><span class="sxs-lookup"><span data-stu-id="fc46a-142">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="fc46a-143">tillgänglighets-ID</span><span class="sxs-lookup"><span data-stu-id="fc46a-143">availability-id</span></span>        | <span data-ttu-id="fc46a-144">sträng</span><span class="sxs-lookup"><span data-stu-id="fc46a-144">string</span></span>   | <span data-ttu-id="fc46a-145">Yes</span><span class="sxs-lookup"><span data-stu-id="fc46a-145">Yes</span></span>      | <span data-ttu-id="fc46a-146">En GUID-formaterad sträng som identifierar tillgängligheten.</span><span class="sxs-lookup"><span data-stu-id="fc46a-146">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="fc46a-147">landskod</span><span class="sxs-lookup"><span data-stu-id="fc46a-147">country-code</span></span>           | <span data-ttu-id="fc46a-148">sträng</span><span class="sxs-lookup"><span data-stu-id="fc46a-148">string</span></span>   | <span data-ttu-id="fc46a-149">Yes</span><span class="sxs-lookup"><span data-stu-id="fc46a-149">Yes</span></span>      | <span data-ttu-id="fc46a-150">Ett land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="fc46a-150">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="fc46a-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="fc46a-151">Request headers</span></span>

<span data-ttu-id="fc46a-152">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fc46a-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc46a-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="fc46a-153">Request body</span></span>

<span data-ttu-id="fc46a-154">Inga.</span><span class="sxs-lookup"><span data-stu-id="fc46a-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fc46a-155">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="fc46a-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fc46a-156">REST-svar</span><span class="sxs-lookup"><span data-stu-id="fc46a-156">REST response</span></span>

<span data-ttu-id="fc46a-157">Om det lyckas innehåller svars texten en [tillgänglighets](product-resources.md#availability) resurs.</span><span class="sxs-lookup"><span data-stu-id="fc46a-157">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc46a-158">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="fc46a-158">Response success and error codes</span></span>

<span data-ttu-id="fc46a-159">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="fc46a-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc46a-160">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="fc46a-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc46a-161">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fc46a-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="fc46a-162">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="fc46a-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="fc46a-163">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="fc46a-163">HTTP Status Code</span></span>     | <span data-ttu-id="fc46a-164">Felkod</span><span class="sxs-lookup"><span data-stu-id="fc46a-164">Error code</span></span>   | <span data-ttu-id="fc46a-165">Description</span><span class="sxs-lookup"><span data-stu-id="fc46a-165">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc46a-166">404</span><span class="sxs-lookup"><span data-stu-id="fc46a-166">404</span></span>                  | <span data-ttu-id="fc46a-167">400013</span><span class="sxs-lookup"><span data-stu-id="fc46a-167">400013</span></span>       | <span data-ttu-id="fc46a-168">Det gick inte att hitta produkten.</span><span class="sxs-lookup"><span data-stu-id="fc46a-168">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="fc46a-169">404</span><span class="sxs-lookup"><span data-stu-id="fc46a-169">404</span></span>                  | <span data-ttu-id="fc46a-170">400018</span><span class="sxs-lookup"><span data-stu-id="fc46a-170">400018</span></span>       | <span data-ttu-id="fc46a-171">Det gick inte att hitta SKU: n.</span><span class="sxs-lookup"><span data-stu-id="fc46a-171">Sku was not found.</span></span>                                                                                        |
| <span data-ttu-id="fc46a-172">404</span><span class="sxs-lookup"><span data-stu-id="fc46a-172">404</span></span>                  | <span data-ttu-id="fc46a-173">400019</span><span class="sxs-lookup"><span data-stu-id="fc46a-173">400019</span></span>       | <span data-ttu-id="fc46a-174">Tillgänglighet hittades inte.</span><span class="sxs-lookup"><span data-stu-id="fc46a-174">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="fc46a-175">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="fc46a-175">Response example</span></span>

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
