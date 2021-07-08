---
title: Hämta en lista över produkter (efter land)
description: Du kan använda produktresursen för att hämta en samling produkter efter kundland.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1258727ecbe7c5cc332624577fa8a355e28e3717
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874218"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="06ba4-103">Hämta en lista över produkter (efter land)</span><span class="sxs-lookup"><span data-stu-id="06ba4-103">Get a list of products (by country)</span></span>

<span data-ttu-id="06ba4-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="06ba4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="06ba4-105">Du kan använda följande metoder för att hämta en samling produkter som är tillgängliga i ett visst land.</span><span class="sxs-lookup"><span data-stu-id="06ba4-105">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06ba4-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="06ba4-106">Prerequisites</span></span>

- <span data-ttu-id="06ba4-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="06ba4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="06ba4-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="06ba4-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="06ba4-109">Ett land.</span><span class="sxs-lookup"><span data-stu-id="06ba4-109">A country.</span></span>

## <a name="c"></a><span data-ttu-id="06ba4-110">C\#</span><span class="sxs-lookup"><span data-stu-id="06ba4-110">C\#</span></span>

<span data-ttu-id="06ba4-111">Så här hämtar du en lista över produkter:</span><span class="sxs-lookup"><span data-stu-id="06ba4-111">To get a list of products:</span></span>

1. <span data-ttu-id="06ba4-112">Använd din **IAggregatePartner.Products-samling** för att välja land med hjälp av **metoden ByCountry().**</span><span class="sxs-lookup"><span data-stu-id="06ba4-112">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="06ba4-113">Välj katalogvyn med hjälp av **metoden ByTargetView().**</span><span class="sxs-lookup"><span data-stu-id="06ba4-113">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="06ba4-114">(Valfritt) Välj reservationsomfånget med hjälp **av metoden ByReservationScope().**</span><span class="sxs-lookup"><span data-stu-id="06ba4-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="06ba4-115">(Valfritt) Välj målsegmentet med hjälp **av metoden ByTargetSegment().**</span><span class="sxs-lookup"><span data-stu-id="06ba4-115">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="06ba4-116">Anropa metoden **Get()** eller **GetAsync()** för att returnera samlingen.</span><span class="sxs-lookup"><span data-stu-id="06ba4-116">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

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

## <a name="java"></a><span data-ttu-id="06ba4-117">Java</span><span class="sxs-lookup"><span data-stu-id="06ba4-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="06ba4-118">Så här hämtar du en lista över produkter:</span><span class="sxs-lookup"><span data-stu-id="06ba4-118">To get a list of products:</span></span>

1. <span data-ttu-id="06ba4-119">Använd funktionen **IAggregatePartner.getProducts** för att välja land med hjälp av funktionen **byCountry().**</span><span class="sxs-lookup"><span data-stu-id="06ba4-119">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="06ba4-120">Välj katalogvyn med hjälp av **funktionen byTargetView().**</span><span class="sxs-lookup"><span data-stu-id="06ba4-120">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="06ba4-121">(Valfritt) Välj målsegmentet med hjälp **av funktionen byTargetSegment().**</span><span class="sxs-lookup"><span data-stu-id="06ba4-121">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="06ba4-122">Anropa **funktionen get()** för att returnera samlingen.</span><span class="sxs-lookup"><span data-stu-id="06ba4-122">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="06ba4-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06ba4-123">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="06ba4-124">Så här hämtar du en lista över produkter:</span><span class="sxs-lookup"><span data-stu-id="06ba4-124">To get a list of products:</span></span>

1. <span data-ttu-id="06ba4-125">Kör kommandot [**Get-PartnerProduct.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)</span><span class="sxs-lookup"><span data-stu-id="06ba4-125">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="06ba4-126">Välj katalogen genom att ange **parametern** Catalog.</span><span class="sxs-lookup"><span data-stu-id="06ba4-126">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="06ba4-127">(Valfritt) Välj målsegmentet genom att ange **parametern** Segment.</span><span class="sxs-lookup"><span data-stu-id="06ba4-127">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="06ba4-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="06ba4-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="06ba4-129">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="06ba4-129">Request syntax</span></span>

| <span data-ttu-id="06ba4-130">Metod</span><span class="sxs-lookup"><span data-stu-id="06ba4-130">Method</span></span>  | <span data-ttu-id="06ba4-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="06ba4-131">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="06ba4-132">**Få**</span><span class="sxs-lookup"><span data-stu-id="06ba4-132">**GET**</span></span> | <span data-ttu-id="06ba4-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="06ba4-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="06ba4-134">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="06ba4-134">URI parameters</span></span>

<span data-ttu-id="06ba4-135">Använd följande sökväg och frågeparametrar för att hämta en lista över produkter.</span><span class="sxs-lookup"><span data-stu-id="06ba4-135">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="06ba4-136">Namn</span><span class="sxs-lookup"><span data-stu-id="06ba4-136">Name</span></span>                   | <span data-ttu-id="06ba4-137">Typ</span><span class="sxs-lookup"><span data-stu-id="06ba4-137">Type</span></span>     | <span data-ttu-id="06ba4-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="06ba4-138">Required</span></span> | <span data-ttu-id="06ba4-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="06ba4-139">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="06ba4-140">land</span><span class="sxs-lookup"><span data-stu-id="06ba4-140">country</span></span>                | <span data-ttu-id="06ba4-141">sträng</span><span class="sxs-lookup"><span data-stu-id="06ba4-141">string</span></span>   | <span data-ttu-id="06ba4-142">Ja</span><span class="sxs-lookup"><span data-stu-id="06ba4-142">Yes</span></span>      | <span data-ttu-id="06ba4-143">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="06ba4-143">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="06ba4-144">targetView</span><span class="sxs-lookup"><span data-stu-id="06ba4-144">targetView</span></span>             | <span data-ttu-id="06ba4-145">sträng</span><span class="sxs-lookup"><span data-stu-id="06ba4-145">string</span></span>   | <span data-ttu-id="06ba4-146">Ja</span><span class="sxs-lookup"><span data-stu-id="06ba4-146">Yes</span></span>      | <span data-ttu-id="06ba4-147">Identifierar målvyn för katalogen.</span><span class="sxs-lookup"><span data-stu-id="06ba4-147">Identifies the target view of the catalog.</span></span> <span data-ttu-id="06ba4-148">Värdena som stöds är:</span><span class="sxs-lookup"><span data-stu-id="06ba4-148">The supported values are:</span></span> <br/><br/><span data-ttu-id="06ba4-149">**Azure**, som innehåller alla Azure-objekt</span><span class="sxs-lookup"><span data-stu-id="06ba4-149">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="06ba4-150">**AzureReservations**, som innehåller alla Reservationsobjekt i Azure</span><span class="sxs-lookup"><span data-stu-id="06ba4-150">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="06ba4-151">**AzureReservationsVM**, som innehåller alla reservationsobjekt för virtuella datorer (VM)</span><span class="sxs-lookup"><span data-stu-id="06ba4-151">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="06ba4-152">**AzureReservationsSQL**, som innehåller alla SQL reservationsobjekt</span><span class="sxs-lookup"><span data-stu-id="06ba4-152">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="06ba4-153">**AzureReservationsCosmosDb**, som innehåller alla reservationsobjekt för Cosmos-databasen</span><span class="sxs-lookup"><span data-stu-id="06ba4-153">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="06ba4-154">**MicrosoftAzure**, som innehåller objekt för Microsoft Azure-prenumerationer **(MS-AZR-0145P)** och Azure-planer</span><span class="sxs-lookup"><span data-stu-id="06ba4-154">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="06ba4-155">**OnlineServices**, som innehåller alla onlinetjänstobjekt (inklusive produkter från den kommersiella marknadsplatsen)</span><span class="sxs-lookup"><span data-stu-id="06ba4-155">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="06ba4-156">**Programvara**, som innehåller alla programvaruobjekt</span><span class="sxs-lookup"><span data-stu-id="06ba4-156">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="06ba4-157">**SoftwareSUSELinux**, som innehåller alla SUSE Linux-programobjekt</span><span class="sxs-lookup"><span data-stu-id="06ba4-157">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="06ba4-158">**SoftwarePerpetual**, som innehåller alla permanenta programvaruobjekt</span><span class="sxs-lookup"><span data-stu-id="06ba4-158">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="06ba4-159">**SoftwareSubscriptions**, som innehåller alla programprenumerationsobjekt</span><span class="sxs-lookup"><span data-stu-id="06ba4-159">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="06ba4-160">targetSegment</span><span class="sxs-lookup"><span data-stu-id="06ba4-160">targetSegment</span></span>          | <span data-ttu-id="06ba4-161">sträng</span><span class="sxs-lookup"><span data-stu-id="06ba4-161">string</span></span>   | <span data-ttu-id="06ba4-162">No</span><span class="sxs-lookup"><span data-stu-id="06ba4-162">No</span></span>       | <span data-ttu-id="06ba4-163">Identifierar målsegmentet.</span><span class="sxs-lookup"><span data-stu-id="06ba4-163">Identifies the target segment.</span></span> <span data-ttu-id="06ba4-164">Vyn för olika målgrupper.</span><span class="sxs-lookup"><span data-stu-id="06ba4-164">The view for different target audiences.</span></span> <span data-ttu-id="06ba4-165">Värdena som stöds är:</span><span class="sxs-lookup"><span data-stu-id="06ba4-165">The supported values are:</span></span> <br/><br/><span data-ttu-id="06ba4-166">**Kommersiella**</span><span class="sxs-lookup"><span data-stu-id="06ba4-166">**commercial**</span></span><br/><span data-ttu-id="06ba4-167">**Utbildning**</span><span class="sxs-lookup"><span data-stu-id="06ba4-167">**education**</span></span><br/><span data-ttu-id="06ba4-168">**Regeringen**</span><span class="sxs-lookup"><span data-stu-id="06ba4-168">**government**</span></span><br/><span data-ttu-id="06ba4-169">**Ideell**</span><span class="sxs-lookup"><span data-stu-id="06ba4-169">**nonprofit**</span></span>  |
| <span data-ttu-id="06ba4-170">reservationScope</span><span class="sxs-lookup"><span data-stu-id="06ba4-170">reservationScope</span></span> | <span data-ttu-id="06ba4-171">sträng</span><span class="sxs-lookup"><span data-stu-id="06ba4-171">string</span></span>   | <span data-ttu-id="06ba4-172">No</span><span class="sxs-lookup"><span data-stu-id="06ba4-172">No</span></span> | <span data-ttu-id="06ba4-173">När du frågar efter en lista över produkter för Azure-reservationer anger du för att hämta en lista över `reservationScope=AzurePlan` produkter som gäller för Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="06ba4-173">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="06ba4-174">Undanta den här parametern för att hämta en lista över produkter för Azure-reservationer, som gäller för Microsoft Azure-prenumerationer **(MS-AZR-0145P).**</span><span class="sxs-lookup"><span data-stu-id="06ba4-174">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="06ba4-175">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="06ba4-175">Request headers</span></span>

<span data-ttu-id="06ba4-176">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="06ba4-176">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="06ba4-177">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="06ba4-177">Request body</span></span>

<span data-ttu-id="06ba4-178">Inga.</span><span class="sxs-lookup"><span data-stu-id="06ba4-178">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="06ba4-179">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="06ba4-179">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="06ba4-180">Produkter efter land</span><span class="sxs-lookup"><span data-stu-id="06ba4-180">Products by country</span></span>

<span data-ttu-id="06ba4-181">Följ det här exemplet för att hämta en lista över produkter efter land Microsoft Azure prenumerationer (MS-AZR-0145P) och Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="06ba4-181">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="06ba4-182">Reservationer för virtuella Azure-datorer (Azure-plan)</span><span class="sxs-lookup"><span data-stu-id="06ba4-182">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="06ba4-183">Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som gäller för Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="06ba4-183">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="06ba4-184">Azure VM-reservationer Microsoft Azure prenumerationer (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="06ba4-184">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="06ba4-185">Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som gäller för Microsoft Azure-prenumerationer (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="06ba4-185">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="06ba4-186">REST-svar</span><span class="sxs-lookup"><span data-stu-id="06ba4-186">REST response</span></span>

<span data-ttu-id="06ba4-187">Om det lyckas innehåller svarstexten en samling [**produktresurser.**](product-resources.md#product)</span><span class="sxs-lookup"><span data-stu-id="06ba4-187">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="06ba4-188">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="06ba4-188">Response success and error codes</span></span>

<span data-ttu-id="06ba4-189">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="06ba4-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="06ba4-190">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="06ba4-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="06ba4-191">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="06ba4-191">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="06ba4-192">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="06ba4-192">This method returns the following error codes:</span></span>

| <span data-ttu-id="06ba4-193">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="06ba4-193">HTTP Status Code</span></span>     | <span data-ttu-id="06ba4-194">Felkod</span><span class="sxs-lookup"><span data-stu-id="06ba4-194">Error code</span></span>   | <span data-ttu-id="06ba4-195">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="06ba4-195">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="06ba4-196">403</span><span class="sxs-lookup"><span data-stu-id="06ba4-196">403</span></span>                  | <span data-ttu-id="06ba4-197">400030</span><span class="sxs-lookup"><span data-stu-id="06ba4-197">400030</span></span>       | <span data-ttu-id="06ba4-198">Åtkomst till det begärda targetSegment tillåts inte.</span><span class="sxs-lookup"><span data-stu-id="06ba4-198">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="06ba4-199">403</span><span class="sxs-lookup"><span data-stu-id="06ba4-199">403</span></span>                  | <span data-ttu-id="06ba4-200">400036</span><span class="sxs-lookup"><span data-stu-id="06ba4-200">400036</span></span>       | <span data-ttu-id="06ba4-201">Åtkomst till begärd targetView tillåts inte.</span><span class="sxs-lookup"><span data-stu-id="06ba4-201">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="06ba4-202">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="06ba4-202">Response example</span></span>

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
