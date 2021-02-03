---
title: Hämta en produkt efter ID
description: Hämtar den angivna produkt resursen med ett produkt-ID.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769033"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="6c032-103">Hämta en produkt efter ID</span><span class="sxs-lookup"><span data-stu-id="6c032-103">Get a product by ID</span></span>

<span data-ttu-id="6c032-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="6c032-104">**Applies To**</span></span>

- <span data-ttu-id="6c032-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="6c032-105">Partner Center</span></span>

<span data-ttu-id="6c032-106">Hämtar den angivna produkt resursen med ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="6c032-106">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c032-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6c032-107">Prerequisites</span></span>

- <span data-ttu-id="6c032-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6c032-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6c032-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6c032-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6c032-110">Ett produkt-ID.</span><span class="sxs-lookup"><span data-stu-id="6c032-110">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="6c032-111">C\#</span><span class="sxs-lookup"><span data-stu-id="6c032-111">C\#</span></span>

<span data-ttu-id="6c032-112">Om du vill hitta en speciell produkt med ID använder du din **IAggregatePartner. Products** -samling, väljer land med hjälp av metoden **ByCountry ()** och anropar sedan metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="6c032-112">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="6c032-113">Anropa slutligen metoden **Get ()** eller **GetAsync ()** för att returnera produkten.</span><span class="sxs-lookup"><span data-stu-id="6c032-113">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="6c032-114">Java</span><span class="sxs-lookup"><span data-stu-id="6c032-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="6c032-115">Om du vill hitta en speciell produkt efter ID använder du funktionen **IAggregatePartner. getProducts** , väljer land med funktionen **byCountry ()** och anropar sedan funktionen **byId ()** .</span><span class="sxs-lookup"><span data-stu-id="6c032-115">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="6c032-116">Slutligen anropar du funktionen **Get ()** för att returnera produkten.</span><span class="sxs-lookup"><span data-stu-id="6c032-116">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="6c032-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c032-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="6c032-118">Om du vill hitta en speciell produkt efter ID kör du kommandot [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) och anger parametern **ProductID** .</span><span class="sxs-lookup"><span data-stu-id="6c032-118">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="6c032-119">**CountryCode** -parametern är alternativ, om den inte anges, kommer det land som är associerat med åter försäljaren att användas.</span><span class="sxs-lookup"><span data-stu-id="6c032-119">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="6c032-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6c032-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6c032-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="6c032-121">Request syntax</span></span>

| <span data-ttu-id="6c032-122">Metod</span><span class="sxs-lookup"><span data-stu-id="6c032-122">Method</span></span>  | <span data-ttu-id="6c032-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6c032-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c032-124">**TA**</span><span class="sxs-lookup"><span data-stu-id="6c032-124">**GET**</span></span> | <span data-ttu-id="6c032-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}? land = {Country} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6c032-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="6c032-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="6c032-126">URI parameter</span></span>

<span data-ttu-id="6c032-127">Använd följande Sök vägs parametrar för att hämta den angivna produkten.</span><span class="sxs-lookup"><span data-stu-id="6c032-127">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="6c032-128">Namn</span><span class="sxs-lookup"><span data-stu-id="6c032-128">Name</span></span>                   | <span data-ttu-id="6c032-129">Typ</span><span class="sxs-lookup"><span data-stu-id="6c032-129">Type</span></span>     | <span data-ttu-id="6c032-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6c032-130">Required</span></span> | <span data-ttu-id="6c032-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6c032-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="6c032-132">produkt-ID</span><span class="sxs-lookup"><span data-stu-id="6c032-132">product-id</span></span>             | <span data-ttu-id="6c032-133">sträng</span><span class="sxs-lookup"><span data-stu-id="6c032-133">string</span></span>   | <span data-ttu-id="6c032-134">Yes</span><span class="sxs-lookup"><span data-stu-id="6c032-134">Yes</span></span>      | <span data-ttu-id="6c032-135">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="6c032-135">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="6c032-136">land</span><span class="sxs-lookup"><span data-stu-id="6c032-136">country</span></span>                | <span data-ttu-id="6c032-137">sträng</span><span class="sxs-lookup"><span data-stu-id="6c032-137">string</span></span>   | <span data-ttu-id="6c032-138">Yes</span><span class="sxs-lookup"><span data-stu-id="6c032-138">Yes</span></span>      | <span data-ttu-id="6c032-139">Ett land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="6c032-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="6c032-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6c032-140">Request headers</span></span>

<span data-ttu-id="6c032-141">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6c032-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6c032-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6c032-142">Request body</span></span>

<span data-ttu-id="6c032-143">Inga.</span><span class="sxs-lookup"><span data-stu-id="6c032-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6c032-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6c032-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="6c032-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6c032-145">REST response</span></span>

<span data-ttu-id="6c032-146">Om det lyckas innehåller svars texten en [produkt](product-resources.md#product) resurs.</span><span class="sxs-lookup"><span data-stu-id="6c032-146">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6c032-147">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6c032-147">Response success and error codes</span></span>

<span data-ttu-id="6c032-148">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="6c032-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6c032-149">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6c032-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6c032-150">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6c032-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="6c032-151">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="6c032-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="6c032-152">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="6c032-152">HTTP Status Code</span></span>     | <span data-ttu-id="6c032-153">Felkod</span><span class="sxs-lookup"><span data-stu-id="6c032-153">Error code</span></span>   | <span data-ttu-id="6c032-154">Description</span><span class="sxs-lookup"><span data-stu-id="6c032-154">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="6c032-155">404</span><span class="sxs-lookup"><span data-stu-id="6c032-155">404</span></span>                  | <span data-ttu-id="6c032-156">400013</span><span class="sxs-lookup"><span data-stu-id="6c032-156">400013</span></span>       | <span data-ttu-id="6c032-157">Det gick inte att hitta produkten.</span><span class="sxs-lookup"><span data-stu-id="6c032-157">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="6c032-158">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6c032-158">Response example</span></span>

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
