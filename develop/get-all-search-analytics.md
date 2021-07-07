---
title: Hämta all information om sökanalys
description: Hur du hämtar all sökanalysinformation.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e789a013b01fb63a38c72f4fe94864ecf21f7e4b
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760172"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="3aea1-103">Hämta all information om sökanalys</span><span class="sxs-lookup"><span data-stu-id="3aea1-103">Get all search analytics information</span></span>

<span data-ttu-id="3aea1-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3aea1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3aea1-105">Hur du hämtar all sökanalysinformation för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="3aea1-105">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3aea1-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3aea1-106">Prerequisites</span></span>

- <span data-ttu-id="3aea1-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3aea1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3aea1-108">Det här scenariot stöder autentisering endast med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3aea1-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3aea1-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3aea1-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3aea1-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="3aea1-110">Request syntax</span></span>

| <span data-ttu-id="3aea1-111">Metod</span><span class="sxs-lookup"><span data-stu-id="3aea1-111">Method</span></span>  | <span data-ttu-id="3aea1-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3aea1-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="3aea1-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="3aea1-113">**GET**</span></span> | <span data-ttu-id="3aea1-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3aea1-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3aea1-115">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="3aea1-115">URI parameters</span></span>

|    <span data-ttu-id="3aea1-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aea1-116">Parameter</span></span>     |  <span data-ttu-id="3aea1-117">Typ</span><span class="sxs-lookup"><span data-stu-id="3aea1-117">Type</span></span>  |                                                                                                                   <span data-ttu-id="3aea1-118">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3aea1-118">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="3aea1-119">filter</span><span class="sxs-lookup"><span data-stu-id="3aea1-119">filter</span></span>      | <span data-ttu-id="3aea1-120">sträng</span><span class="sxs-lookup"><span data-stu-id="3aea1-120">string</span></span> |                                                                     <span data-ttu-id="3aea1-121">Returnerar data som matchar filtervillkoret.</span><span class="sxs-lookup"><span data-stu-id="3aea1-121">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="3aea1-122">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="3aea1-122">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="3aea1-123">groupby</span><span class="sxs-lookup"><span data-stu-id="3aea1-123">groupby</span></span>      | <span data-ttu-id="3aea1-124">sträng</span><span class="sxs-lookup"><span data-stu-id="3aea1-124">string</span></span> |                                         <span data-ttu-id="3aea1-125">Stöder både termer och datum.</span><span class="sxs-lookup"><span data-stu-id="3aea1-125">Supports both terms and dates.</span></span> <span data-ttu-id="3aea1-126">Kortslutningslogik för att begränsa antalet buckets.</span><span class="sxs-lookup"><span data-stu-id="3aea1-126">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="3aea1-127">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="3aea1-127">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="3aea1-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="3aea1-128">aggregationLevel</span></span> | <span data-ttu-id="3aea1-129">sträng</span><span class="sxs-lookup"><span data-stu-id="3aea1-129">string</span></span> | <span data-ttu-id="3aea1-130">Parametern *aggregationLevel* kräver en *groupby*.</span><span class="sxs-lookup"><span data-stu-id="3aea1-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="3aea1-131">Parametern *aggregationLevel* gäller för alla datumfält som finns i *groupby*.</span><span class="sxs-lookup"><span data-stu-id="3aea1-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="3aea1-132">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="3aea1-132">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="3aea1-133">top</span><span class="sxs-lookup"><span data-stu-id="3aea1-133">top</span></span>        | <span data-ttu-id="3aea1-134">sträng</span><span class="sxs-lookup"><span data-stu-id="3aea1-134">string</span></span> |                                                                     <span data-ttu-id="3aea1-135">Sidgränsen är 10 000.</span><span class="sxs-lookup"><span data-stu-id="3aea1-135">The page limit is 10000.</span></span> <span data-ttu-id="3aea1-136">Tar ett värde som är mindre än 10 000.</span><span class="sxs-lookup"><span data-stu-id="3aea1-136">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="3aea1-137">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="3aea1-137">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="3aea1-138">hoppa över</span><span class="sxs-lookup"><span data-stu-id="3aea1-138">skip</span></span>       | <span data-ttu-id="3aea1-139">sträng</span><span class="sxs-lookup"><span data-stu-id="3aea1-139">string</span></span> |                                                                                  <span data-ttu-id="3aea1-140">Antal rader som ska hoppas över.</span><span class="sxs-lookup"><span data-stu-id="3aea1-140">Number of rows to skip.</span></span> </br> <span data-ttu-id="3aea1-141">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="3aea1-141">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="3aea1-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3aea1-142">Request headers</span></span>

<span data-ttu-id="3aea1-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3aea1-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3aea1-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3aea1-144">Request body</span></span>

<span data-ttu-id="3aea1-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="3aea1-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3aea1-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3aea1-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="3aea1-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3aea1-147">REST response</span></span>

<span data-ttu-id="3aea1-148">Om det lyckas innehåller svarstexten en samling [sökresurser.](partner-center-analytics-resources.md#search-resource)</span><span class="sxs-lookup"><span data-stu-id="3aea1-148">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3aea1-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3aea1-149">Response success and error codes</span></span>

<span data-ttu-id="3aea1-150">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="3aea1-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3aea1-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3aea1-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3aea1-152">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3aea1-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3aea1-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3aea1-153">Response example</span></span>

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a><span data-ttu-id="3aea1-154">Se även</span><span class="sxs-lookup"><span data-stu-id="3aea1-154">See also</span></span>

- [<span data-ttu-id="3aea1-155">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="3aea1-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
