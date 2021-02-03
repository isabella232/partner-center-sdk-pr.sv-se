---
title: Hämta en SKU efter ID
description: Hämtar en SKU för den angivna produkten med angivet SKU-ID.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 54ef72413d2d2b9e7154e82e4bbdd7427a79a2dd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769090"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="321db-103">Hämta en SKU efter ID</span><span class="sxs-lookup"><span data-stu-id="321db-103">Get a SKU by ID</span></span>

<span data-ttu-id="321db-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="321db-104">**Applies To**</span></span>

- <span data-ttu-id="321db-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="321db-105">Partner Center</span></span>

<span data-ttu-id="321db-106">Hämtar en SKU för den angivna produkten med angivet SKU-ID.</span><span class="sxs-lookup"><span data-stu-id="321db-106">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="321db-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="321db-107">Prerequisites</span></span>

- <span data-ttu-id="321db-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="321db-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="321db-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="321db-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="321db-110">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="321db-110">A product ID.</span></span>

- <span data-ttu-id="321db-111">ETT SKU-ID.</span><span class="sxs-lookup"><span data-stu-id="321db-111">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="321db-112">C\#</span><span class="sxs-lookup"><span data-stu-id="321db-112">C\#</span></span>

<span data-ttu-id="321db-113">Om du vill hämta information om en angiven SKU börjar du med att följa stegen i [Hämta en produkt efter ID](get-a-product-by-id.md) för att hämta gränssnittet för en speciell produkts drift.</span><span class="sxs-lookup"><span data-stu-id="321db-113">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="321db-114">Från det resulterande gränssnittet väljer du egenskapen **SKU: er** för att hämta ett gränssnitt med tillgängliga åtgärder för SKU: er.</span><span class="sxs-lookup"><span data-stu-id="321db-114">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="321db-115">Skicka SKU-ID: t till metoden **ById ()** och anropa **Get ()** eller **GetAsync ()** för att hämta SKU-informationen.</span><span class="sxs-lookup"><span data-stu-id="321db-115">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="321db-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="321db-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="321db-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="321db-117">Request syntax</span></span>

| <span data-ttu-id="321db-118">Metod</span><span class="sxs-lookup"><span data-stu-id="321db-118">Method</span></span>  | <span data-ttu-id="321db-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="321db-119">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="321db-120">**TA**</span><span class="sxs-lookup"><span data-stu-id="321db-120">**GET**</span></span> | <span data-ttu-id="321db-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}? land = {Country-Code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="321db-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="321db-122">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="321db-122">URI parameter</span></span>

<span data-ttu-id="321db-123">Använd följande sökväg och frågeparametrar för att hämta en SKU för den angivna produkten med det angivna SKU-ID: t.</span><span class="sxs-lookup"><span data-stu-id="321db-123">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="321db-124">Namn</span><span class="sxs-lookup"><span data-stu-id="321db-124">Name</span></span>                   | <span data-ttu-id="321db-125">Typ</span><span class="sxs-lookup"><span data-stu-id="321db-125">Type</span></span>     | <span data-ttu-id="321db-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="321db-126">Required</span></span> | <span data-ttu-id="321db-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="321db-127">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="321db-128">produkt-ID</span><span class="sxs-lookup"><span data-stu-id="321db-128">product-id</span></span>             | <span data-ttu-id="321db-129">sträng</span><span class="sxs-lookup"><span data-stu-id="321db-129">string</span></span>   | <span data-ttu-id="321db-130">Yes</span><span class="sxs-lookup"><span data-stu-id="321db-130">Yes</span></span>      | <span data-ttu-id="321db-131">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="321db-131">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="321db-132">SKU-ID</span><span class="sxs-lookup"><span data-stu-id="321db-132">sku-id</span></span>                 | <span data-ttu-id="321db-133">sträng</span><span class="sxs-lookup"><span data-stu-id="321db-133">string</span></span>   | <span data-ttu-id="321db-134">Yes</span><span class="sxs-lookup"><span data-stu-id="321db-134">Yes</span></span>      | <span data-ttu-id="321db-135">En sträng som identifierar SKU: n.</span><span class="sxs-lookup"><span data-stu-id="321db-135">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="321db-136">landskod</span><span class="sxs-lookup"><span data-stu-id="321db-136">country-code</span></span>           | <span data-ttu-id="321db-137">sträng</span><span class="sxs-lookup"><span data-stu-id="321db-137">string</span></span>   | <span data-ttu-id="321db-138">Yes</span><span class="sxs-lookup"><span data-stu-id="321db-138">Yes</span></span>      | <span data-ttu-id="321db-139">Ett land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="321db-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="321db-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="321db-140">Request headers</span></span>

<span data-ttu-id="321db-141">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="321db-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="321db-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="321db-142">Request body</span></span>

<span data-ttu-id="321db-143">Inga.</span><span class="sxs-lookup"><span data-stu-id="321db-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="321db-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="321db-144">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="321db-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="321db-145">REST response</span></span>

<span data-ttu-id="321db-146">Om det lyckas innehåller svars texten en [SKU](product-resources.md#sku) -resurs.</span><span class="sxs-lookup"><span data-stu-id="321db-146">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="321db-147">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="321db-147">Response success and error codes</span></span>

<span data-ttu-id="321db-148">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="321db-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="321db-149">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="321db-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="321db-150">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="321db-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="321db-151">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="321db-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="321db-152">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="321db-152">HTTP Status Code</span></span>     | <span data-ttu-id="321db-153">Felkod</span><span class="sxs-lookup"><span data-stu-id="321db-153">Error code</span></span>   | <span data-ttu-id="321db-154">Description</span><span class="sxs-lookup"><span data-stu-id="321db-154">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="321db-155">404</span><span class="sxs-lookup"><span data-stu-id="321db-155">404</span></span>                  | <span data-ttu-id="321db-156">400013</span><span class="sxs-lookup"><span data-stu-id="321db-156">400013</span></span>       | <span data-ttu-id="321db-157">Det gick inte att hitta produkten.</span><span class="sxs-lookup"><span data-stu-id="321db-157">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="321db-158">404</span><span class="sxs-lookup"><span data-stu-id="321db-158">404</span></span>                  | <span data-ttu-id="321db-159">400018</span><span class="sxs-lookup"><span data-stu-id="321db-159">400018</span></span>       | <span data-ttu-id="321db-160">Det gick inte att hitta SKU: n.</span><span class="sxs-lookup"><span data-stu-id="321db-160">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="321db-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="321db-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
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
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```
