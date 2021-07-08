---
title: Hämta en produkt efter ID
description: Hämtar den angivna produktresursen med hjälp av ett produkt-ID.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 769a4307dc3cebdc7ebbdcf51d9f2b67a9f4b7c2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874031"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="5c1fc-103">Hämta en produkt efter ID</span><span class="sxs-lookup"><span data-stu-id="5c1fc-103">Get a product by ID</span></span>

<span data-ttu-id="5c1fc-104">Hämtar den angivna produktresursen med hjälp av ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-104">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c1fc-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="5c1fc-105">Prerequisites</span></span>

- <span data-ttu-id="5c1fc-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5c1fc-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5c1fc-107">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5c1fc-108">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-108">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="5c1fc-109">C\#</span><span class="sxs-lookup"><span data-stu-id="5c1fc-109">C\#</span></span>

<span data-ttu-id="5c1fc-110">Om du vill hitta en specifik produkt efter ID använder du **samlingen IAggregatePartner.Products,** väljer land med hjälp av **metoden ByCountry()** och anropar **sedan metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="5c1fc-110">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="5c1fc-111">Anropa slutligen metoden **Get()** eller **GetAsync()** för att returnera produkten.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-111">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="5c1fc-112">Java</span><span class="sxs-lookup"><span data-stu-id="5c1fc-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="5c1fc-113">Om du vill hitta en specifik produkt efter ID använder du funktionen **IAggregatePartner.getProducts,** väljer land med hjälp av funktionen **byCountry()** och anropar **sedan funktionen byId().**</span><span class="sxs-lookup"><span data-stu-id="5c1fc-113">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="5c1fc-114">Anropa slutligen funktionen **get()** för att returnera produkten.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-114">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="5c1fc-115">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c1fc-115">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="5c1fc-116">Om du vill hitta en specifik produkt efter ID kör du kommandot [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) och anger **parametern ProductId.**</span><span class="sxs-lookup"><span data-stu-id="5c1fc-116">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="5c1fc-117">Parametern **CountryCode** är alternativ. Om den inte anges används det land som är associerat med återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-117">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="5c1fc-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="5c1fc-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5c1fc-119">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="5c1fc-119">Request syntax</span></span>

| <span data-ttu-id="5c1fc-120">Metod</span><span class="sxs-lookup"><span data-stu-id="5c1fc-120">Method</span></span>  | <span data-ttu-id="5c1fc-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="5c1fc-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="5c1fc-122">**Få**</span><span class="sxs-lookup"><span data-stu-id="5c1fc-122">**GET**</span></span> | <span data-ttu-id="5c1fc-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5c1fc-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="5c1fc-124">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="5c1fc-124">URI parameter</span></span>

<span data-ttu-id="5c1fc-125">Använd följande sökvägsparametrar för att hämta den angivna produkten.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="5c1fc-126">Namn</span><span class="sxs-lookup"><span data-stu-id="5c1fc-126">Name</span></span>                   | <span data-ttu-id="5c1fc-127">Typ</span><span class="sxs-lookup"><span data-stu-id="5c1fc-127">Type</span></span>     | <span data-ttu-id="5c1fc-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="5c1fc-128">Required</span></span> | <span data-ttu-id="5c1fc-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5c1fc-129">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="5c1fc-130">produkt-id</span><span class="sxs-lookup"><span data-stu-id="5c1fc-130">product-id</span></span>             | <span data-ttu-id="5c1fc-131">sträng</span><span class="sxs-lookup"><span data-stu-id="5c1fc-131">string</span></span>   | <span data-ttu-id="5c1fc-132">Ja</span><span class="sxs-lookup"><span data-stu-id="5c1fc-132">Yes</span></span>      | <span data-ttu-id="5c1fc-133">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-133">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="5c1fc-134">land</span><span class="sxs-lookup"><span data-stu-id="5c1fc-134">country</span></span>                | <span data-ttu-id="5c1fc-135">sträng</span><span class="sxs-lookup"><span data-stu-id="5c1fc-135">string</span></span>   | <span data-ttu-id="5c1fc-136">Ja</span><span class="sxs-lookup"><span data-stu-id="5c1fc-136">Yes</span></span>      | <span data-ttu-id="5c1fc-137">Ett lands-/regions-ID.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="5c1fc-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="5c1fc-138">Request headers</span></span>

<span data-ttu-id="5c1fc-139">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5c1fc-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5c1fc-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="5c1fc-140">Request body</span></span>

<span data-ttu-id="5c1fc-141">Inga.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5c1fc-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="5c1fc-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="5c1fc-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="5c1fc-143">REST response</span></span>

<span data-ttu-id="5c1fc-144">Om det lyckas innehåller svarstexten en [produktresurs.](product-resources.md#product)</span><span class="sxs-lookup"><span data-stu-id="5c1fc-144">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5c1fc-145">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="5c1fc-145">Response success and error codes</span></span>

<span data-ttu-id="5c1fc-146">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5c1fc-147">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5c1fc-148">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5c1fc-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="5c1fc-149">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="5c1fc-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="5c1fc-150">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="5c1fc-150">HTTP Status Code</span></span>     | <span data-ttu-id="5c1fc-151">Felkod</span><span class="sxs-lookup"><span data-stu-id="5c1fc-151">Error code</span></span>   | <span data-ttu-id="5c1fc-152">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5c1fc-152">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="5c1fc-153">404</span><span class="sxs-lookup"><span data-stu-id="5c1fc-153">404</span></span>                  | <span data-ttu-id="5c1fc-154">400013</span><span class="sxs-lookup"><span data-stu-id="5c1fc-154">400013</span></span>       | <span data-ttu-id="5c1fc-155">Det gick inte att hitta produkten.</span><span class="sxs-lookup"><span data-stu-id="5c1fc-155">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="5c1fc-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="5c1fc-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
