---
title: Hämta en lista över produkter (efter land)
description: Du kan använda produkt resursen för att hämta en samling produkter per kund land.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769447"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="171c0-103">Hämta en lista över produkter (efter land)</span><span class="sxs-lookup"><span data-stu-id="171c0-103">Get a list of products (by country)</span></span>

<span data-ttu-id="171c0-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="171c0-104">**Applies to:**</span></span>

- <span data-ttu-id="171c0-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="171c0-105">Partner Center</span></span>
- <span data-ttu-id="171c0-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="171c0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="171c0-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="171c0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="171c0-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="171c0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="171c0-109">Du kan använda följande metoder för att hämta en samling produkter som är tillgängliga i ett visst land.</span><span class="sxs-lookup"><span data-stu-id="171c0-109">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="171c0-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="171c0-110">Prerequisites</span></span>

- <span data-ttu-id="171c0-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="171c0-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="171c0-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="171c0-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="171c0-113">Ett land.</span><span class="sxs-lookup"><span data-stu-id="171c0-113">A country.</span></span>

## <a name="c"></a><span data-ttu-id="171c0-114">C\#</span><span class="sxs-lookup"><span data-stu-id="171c0-114">C\#</span></span>

<span data-ttu-id="171c0-115">Så här hämtar du en lista över produkter:</span><span class="sxs-lookup"><span data-stu-id="171c0-115">To get a list of products:</span></span>

1. <span data-ttu-id="171c0-116">Använd din **IAggregatePartner. Products** -samling för att välja land med hjälp av metoden **ByCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="171c0-116">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="171c0-117">Välj vyn katalog med metoden **ByTargetView ()** .</span><span class="sxs-lookup"><span data-stu-id="171c0-117">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="171c0-118">Valfritt Välj reservations omfånget med metoden **ByReservationScope ()** .</span><span class="sxs-lookup"><span data-stu-id="171c0-118">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="171c0-119">Valfritt Välj mål segmentet med metoden **ByTargetSegment ()** .</span><span class="sxs-lookup"><span data-stu-id="171c0-119">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="171c0-120">Anropa metoden **Get ()** eller **GetAsync ()** för att returnera samlingen.</span><span class="sxs-lookup"><span data-stu-id="171c0-120">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="171c0-121">Java</span><span class="sxs-lookup"><span data-stu-id="171c0-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="171c0-122">Så här hämtar du en lista över produkter:</span><span class="sxs-lookup"><span data-stu-id="171c0-122">To get a list of products:</span></span>

1. <span data-ttu-id="171c0-123">Använd funktionen **IAggregatePartner. getProducts** för att välja land med hjälp av funktionen **byCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="171c0-123">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="171c0-124">Välj vyn katalog med funktionen **byTargetView ()** .</span><span class="sxs-lookup"><span data-stu-id="171c0-124">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="171c0-125">Valfritt Välj mål segment med funktionen **byTargetSegment ()** .</span><span class="sxs-lookup"><span data-stu-id="171c0-125">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="171c0-126">Anropa funktionen **Get ()** för att returnera samlingen.</span><span class="sxs-lookup"><span data-stu-id="171c0-126">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="171c0-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="171c0-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="171c0-128">Så här hämtar du en lista över produkter:</span><span class="sxs-lookup"><span data-stu-id="171c0-128">To get a list of products:</span></span>

1. <span data-ttu-id="171c0-129">Kör kommandot [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) .</span><span class="sxs-lookup"><span data-stu-id="171c0-129">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="171c0-130">Välj katalogen genom att ange **katalog** parametern.</span><span class="sxs-lookup"><span data-stu-id="171c0-130">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="171c0-131">Valfritt Välj mål segmentet genom att ange **segment** parametern.</span><span class="sxs-lookup"><span data-stu-id="171c0-131">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="171c0-132">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="171c0-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="171c0-133">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="171c0-133">Request syntax</span></span>

| <span data-ttu-id="171c0-134">Metod</span><span class="sxs-lookup"><span data-stu-id="171c0-134">Method</span></span>  | <span data-ttu-id="171c0-135">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="171c0-135">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="171c0-136">**TA**</span><span class="sxs-lookup"><span data-stu-id="171c0-136">**GET**</span></span> | <span data-ttu-id="171c0-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products? Country = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} http/1.1</span><span class="sxs-lookup"><span data-stu-id="171c0-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="171c0-138">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="171c0-138">URI parameters</span></span>

<span data-ttu-id="171c0-139">Använd följande sökväg och frågeparametrar för att hämta en lista över produkter.</span><span class="sxs-lookup"><span data-stu-id="171c0-139">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="171c0-140">Namn</span><span class="sxs-lookup"><span data-stu-id="171c0-140">Name</span></span>                   | <span data-ttu-id="171c0-141">Typ</span><span class="sxs-lookup"><span data-stu-id="171c0-141">Type</span></span>     | <span data-ttu-id="171c0-142">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="171c0-142">Required</span></span> | <span data-ttu-id="171c0-143">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="171c0-143">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="171c0-144">land</span><span class="sxs-lookup"><span data-stu-id="171c0-144">country</span></span>                | <span data-ttu-id="171c0-145">sträng</span><span class="sxs-lookup"><span data-stu-id="171c0-145">string</span></span>   | <span data-ttu-id="171c0-146">Yes</span><span class="sxs-lookup"><span data-stu-id="171c0-146">Yes</span></span>      | <span data-ttu-id="171c0-147">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="171c0-147">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="171c0-148">targetView</span><span class="sxs-lookup"><span data-stu-id="171c0-148">targetView</span></span>             | <span data-ttu-id="171c0-149">sträng</span><span class="sxs-lookup"><span data-stu-id="171c0-149">string</span></span>   | <span data-ttu-id="171c0-150">Yes</span><span class="sxs-lookup"><span data-stu-id="171c0-150">Yes</span></span>      | <span data-ttu-id="171c0-151">Identifierar katalogens mållista.</span><span class="sxs-lookup"><span data-stu-id="171c0-151">Identifies the target view of the catalog.</span></span> <span data-ttu-id="171c0-152">De värden som stöds är:</span><span class="sxs-lookup"><span data-stu-id="171c0-152">The supported values are:</span></span> <br/><br/><span data-ttu-id="171c0-153">**Azure**, som innehåller alla Azure-objekt</span><span class="sxs-lookup"><span data-stu-id="171c0-153">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="171c0-154">**AzureReservations**, som innehåller alla Azure reservation-objekt</span><span class="sxs-lookup"><span data-stu-id="171c0-154">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="171c0-155">**AzureReservationsVM**, som innehåller alla reservations objekt för virtuella datorer (VM)</span><span class="sxs-lookup"><span data-stu-id="171c0-155">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="171c0-156">**AzureReservationsSQL**, som innehåller alla SQL reservation-objekt</span><span class="sxs-lookup"><span data-stu-id="171c0-156">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="171c0-157">**AzureReservationsCosmosDb**, som innehåller alla Cosmos-databas reservations objekt</span><span class="sxs-lookup"><span data-stu-id="171c0-157">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="171c0-158">**MicrosoftAzure**, som innehåller objekt för Microsoft Azure prenumerationer (**MS-AZR-0145P**) och Azure-planer</span><span class="sxs-lookup"><span data-stu-id="171c0-158">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="171c0-159">**OnlineServices**, som omfattar alla online tjänst objekt (inklusive kommersiella produkter från marknaden)</span><span class="sxs-lookup"><span data-stu-id="171c0-159">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="171c0-160">**Program vara**, som innehåller alla program varu objekt</span><span class="sxs-lookup"><span data-stu-id="171c0-160">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="171c0-161">**SoftwareSUSELinux**, som innehåller alla program vara SUSE Linux-objekt</span><span class="sxs-lookup"><span data-stu-id="171c0-161">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="171c0-162">**SoftwarePerpetual**, som innehåller alla objekt med beständig program vara</span><span class="sxs-lookup"><span data-stu-id="171c0-162">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="171c0-163">**SoftwareSubscriptions**, som innehåller alla program prenumerations objekt</span><span class="sxs-lookup"><span data-stu-id="171c0-163">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="171c0-164">targetSegment</span><span class="sxs-lookup"><span data-stu-id="171c0-164">targetSegment</span></span>          | <span data-ttu-id="171c0-165">sträng</span><span class="sxs-lookup"><span data-stu-id="171c0-165">string</span></span>   | <span data-ttu-id="171c0-166">No</span><span class="sxs-lookup"><span data-stu-id="171c0-166">No</span></span>       | <span data-ttu-id="171c0-167">Identifierar mål segmentet.</span><span class="sxs-lookup"><span data-stu-id="171c0-167">Identifies the target segment.</span></span> <span data-ttu-id="171c0-168">Vyn för olika mål grupper.</span><span class="sxs-lookup"><span data-stu-id="171c0-168">The view for different target audiences.</span></span> <span data-ttu-id="171c0-169">De värden som stöds är:</span><span class="sxs-lookup"><span data-stu-id="171c0-169">The supported values are:</span></span> <br/><br/><span data-ttu-id="171c0-170">**marknadsmässig**</span><span class="sxs-lookup"><span data-stu-id="171c0-170">**commercial**</span></span><br/><span data-ttu-id="171c0-171">**kontor**</span><span class="sxs-lookup"><span data-stu-id="171c0-171">**education**</span></span><br/><span data-ttu-id="171c0-172">**stat**</span><span class="sxs-lookup"><span data-stu-id="171c0-172">**government**</span></span><br/><span data-ttu-id="171c0-173">**vinstdrivande**</span><span class="sxs-lookup"><span data-stu-id="171c0-173">**nonprofit**</span></span>  |
| <span data-ttu-id="171c0-174">reservationScope</span><span class="sxs-lookup"><span data-stu-id="171c0-174">reservationScope</span></span> | <span data-ttu-id="171c0-175">sträng</span><span class="sxs-lookup"><span data-stu-id="171c0-175">string</span></span>   | <span data-ttu-id="171c0-176">No</span><span class="sxs-lookup"><span data-stu-id="171c0-176">No</span></span> | <span data-ttu-id="171c0-177">När du frågar efter en lista över produkter för Azure Reservations anger `reservationScope=AzurePlan` du för att hämta en lista över produkter som är tillämpliga på Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="171c0-177">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="171c0-178">Undanta den här parametern för att hämta en lista över produkter för Azure-reservationer som är tillämpliga på Microsoft Azure (**MS-AZR-0145P**)-prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="171c0-178">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="171c0-179">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="171c0-179">Request headers</span></span>

<span data-ttu-id="171c0-180">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="171c0-180">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="171c0-181">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="171c0-181">Request body</span></span>

<span data-ttu-id="171c0-182">Inga.</span><span class="sxs-lookup"><span data-stu-id="171c0-182">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="171c0-183">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="171c0-183">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="171c0-184">Produkter efter land</span><span class="sxs-lookup"><span data-stu-id="171c0-184">Products by country</span></span>

<span data-ttu-id="171c0-185">Följ det här exemplet för att hämta en lista över produkter efter land för Microsoft Azure (MS-AZR-0145P) prenumerationer och Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="171c0-185">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="171c0-186">Azure VM-reservationer (Azure-plan)</span><span class="sxs-lookup"><span data-stu-id="171c0-186">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="171c0-187">Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som är tillämpliga för Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="171c0-187">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="171c0-188">Azure VM-reservationer för Microsoft Azure (MS-AZR-0145P)-prenumerationer</span><span class="sxs-lookup"><span data-stu-id="171c0-188">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="171c0-189">Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som är tillämpliga på Microsoft Azure (MS-AZR-0145P)-prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="171c0-189">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="171c0-190">REST-svar</span><span class="sxs-lookup"><span data-stu-id="171c0-190">REST response</span></span>

<span data-ttu-id="171c0-191">Om det lyckas innehåller svars texten en samling [**produkt**](product-resources.md#product) resurser.</span><span class="sxs-lookup"><span data-stu-id="171c0-191">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="171c0-192">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="171c0-192">Response success and error codes</span></span>

<span data-ttu-id="171c0-193">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="171c0-193">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="171c0-194">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="171c0-194">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="171c0-195">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="171c0-195">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="171c0-196">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="171c0-196">This method returns the following error codes:</span></span>

| <span data-ttu-id="171c0-197">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="171c0-197">HTTP Status Code</span></span>     | <span data-ttu-id="171c0-198">Felkod</span><span class="sxs-lookup"><span data-stu-id="171c0-198">Error code</span></span>   | <span data-ttu-id="171c0-199">Description</span><span class="sxs-lookup"><span data-stu-id="171c0-199">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="171c0-200">403</span><span class="sxs-lookup"><span data-stu-id="171c0-200">403</span></span>                  | <span data-ttu-id="171c0-201">400030</span><span class="sxs-lookup"><span data-stu-id="171c0-201">400030</span></span>       | <span data-ttu-id="171c0-202">Åtkomst till den begärda targetSegment är inte tillåten.</span><span class="sxs-lookup"><span data-stu-id="171c0-202">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="171c0-203">403</span><span class="sxs-lookup"><span data-stu-id="171c0-203">403</span></span>                  | <span data-ttu-id="171c0-204">400036</span><span class="sxs-lookup"><span data-stu-id="171c0-204">400036</span></span>       | <span data-ttu-id="171c0-205">Åtkomst till den begärda targetView är inte tillåten.</span><span class="sxs-lookup"><span data-stu-id="171c0-205">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="171c0-206">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="171c0-206">Response example</span></span>

```http
{
    "totalCount": 19,
    "items": [
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
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
