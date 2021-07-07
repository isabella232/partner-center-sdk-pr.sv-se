---
title: Hämta en SKU efter ID
description: Hämtar en SKU för den angivna produkten med det angivna SKU-ID:t.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9516a87a438a0a84a6f6069c1f9b2a2e97e90fba
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873861"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="daffd-103">Hämta en SKU efter ID</span><span class="sxs-lookup"><span data-stu-id="daffd-103">Get a SKU by ID</span></span>

<span data-ttu-id="daffd-104">Hämtar en SKU för den angivna produkten med det angivna SKU-ID:t.</span><span class="sxs-lookup"><span data-stu-id="daffd-104">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daffd-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="daffd-105">Prerequisites</span></span>

- <span data-ttu-id="daffd-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="daffd-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="daffd-107">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="daffd-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="daffd-108">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="daffd-108">A product ID.</span></span>

- <span data-ttu-id="daffd-109">Ett SKU-ID.</span><span class="sxs-lookup"><span data-stu-id="daffd-109">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="daffd-110">C\#</span><span class="sxs-lookup"><span data-stu-id="daffd-110">C\#</span></span>

<span data-ttu-id="daffd-111">Börja med att följa stegen i Hämta en produkt efter [ID](get-a-product-by-id.md) för att hämta gränssnittet för en specifik produkts åtgärder för att hämta information om en specifik SKU.</span><span class="sxs-lookup"><span data-stu-id="daffd-111">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="daffd-112">Från det resulterande gränssnittet väljer du egenskapen **SKU:er** för att hämta ett gränssnitt med tillgängliga åtgärder för SKU:er.</span><span class="sxs-lookup"><span data-stu-id="daffd-112">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="daffd-113">Skicka SKU-ID:t till **metoden ById()** och anropa **Get()** eller **GetAsync()** för att hämta SKU-informationen.</span><span class="sxs-lookup"><span data-stu-id="daffd-113">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="daffd-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="daffd-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="daffd-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="daffd-115">Request syntax</span></span>

| <span data-ttu-id="daffd-116">Metod</span><span class="sxs-lookup"><span data-stu-id="daffd-116">Method</span></span>  | <span data-ttu-id="daffd-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="daffd-117">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="daffd-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="daffd-118">**GET**</span></span> | <span data-ttu-id="daffd-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="daffd-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="daffd-120">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="daffd-120">URI parameter</span></span>

<span data-ttu-id="daffd-121">Använd följande sökväg och frågeparametrar för att hämta en SKU för den angivna produkten med hjälp av det angivna SKU-ID:t.</span><span class="sxs-lookup"><span data-stu-id="daffd-121">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="daffd-122">Namn</span><span class="sxs-lookup"><span data-stu-id="daffd-122">Name</span></span>                   | <span data-ttu-id="daffd-123">Typ</span><span class="sxs-lookup"><span data-stu-id="daffd-123">Type</span></span>     | <span data-ttu-id="daffd-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="daffd-124">Required</span></span> | <span data-ttu-id="daffd-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="daffd-125">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="daffd-126">produkt-id</span><span class="sxs-lookup"><span data-stu-id="daffd-126">product-id</span></span>             | <span data-ttu-id="daffd-127">sträng</span><span class="sxs-lookup"><span data-stu-id="daffd-127">string</span></span>   | <span data-ttu-id="daffd-128">Ja</span><span class="sxs-lookup"><span data-stu-id="daffd-128">Yes</span></span>      | <span data-ttu-id="daffd-129">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="daffd-129">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="daffd-130">sku-id</span><span class="sxs-lookup"><span data-stu-id="daffd-130">sku-id</span></span>                 | <span data-ttu-id="daffd-131">sträng</span><span class="sxs-lookup"><span data-stu-id="daffd-131">string</span></span>   | <span data-ttu-id="daffd-132">Ja</span><span class="sxs-lookup"><span data-stu-id="daffd-132">Yes</span></span>      | <span data-ttu-id="daffd-133">En sträng som identifierar SKU:n.</span><span class="sxs-lookup"><span data-stu-id="daffd-133">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="daffd-134">landskod</span><span class="sxs-lookup"><span data-stu-id="daffd-134">country-code</span></span>           | <span data-ttu-id="daffd-135">sträng</span><span class="sxs-lookup"><span data-stu-id="daffd-135">string</span></span>   | <span data-ttu-id="daffd-136">Ja</span><span class="sxs-lookup"><span data-stu-id="daffd-136">Yes</span></span>      | <span data-ttu-id="daffd-137">Ett lands-/regions-ID.</span><span class="sxs-lookup"><span data-stu-id="daffd-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="daffd-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="daffd-138">Request headers</span></span>

<span data-ttu-id="daffd-139">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="daffd-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="daffd-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="daffd-140">Request body</span></span>

<span data-ttu-id="daffd-141">Inga.</span><span class="sxs-lookup"><span data-stu-id="daffd-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="daffd-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="daffd-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="daffd-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="daffd-143">REST response</span></span>

<span data-ttu-id="daffd-144">Om det lyckas innehåller svarstexten en [SKU-resurs.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="daffd-144">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="daffd-145">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="daffd-145">Response success and error codes</span></span>

<span data-ttu-id="daffd-146">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="daffd-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="daffd-147">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="daffd-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="daffd-148">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="daffd-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="daffd-149">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="daffd-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="daffd-150">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="daffd-150">HTTP Status Code</span></span>     | <span data-ttu-id="daffd-151">Felkod</span><span class="sxs-lookup"><span data-stu-id="daffd-151">Error code</span></span>   | <span data-ttu-id="daffd-152">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="daffd-152">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="daffd-153">404</span><span class="sxs-lookup"><span data-stu-id="daffd-153">404</span></span>                  | <span data-ttu-id="daffd-154">400013</span><span class="sxs-lookup"><span data-stu-id="daffd-154">400013</span></span>       | <span data-ttu-id="daffd-155">Det gick inte att hitta produkten.</span><span class="sxs-lookup"><span data-stu-id="daffd-155">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="daffd-156">404</span><span class="sxs-lookup"><span data-stu-id="daffd-156">404</span></span>                  | <span data-ttu-id="daffd-157">400018</span><span class="sxs-lookup"><span data-stu-id="daffd-157">400018</span></span>       | <span data-ttu-id="daffd-158">Det gick inte att hitta SKU:n.</span><span class="sxs-lookup"><span data-stu-id="daffd-158">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="daffd-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="daffd-159">Response example</span></span>

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
