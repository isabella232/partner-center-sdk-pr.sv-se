---
title: Hämta all information om sökanalys
description: Hämta all Sök analys information.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768757"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="ce7f7-103">Hämta all information om sökanalys</span><span class="sxs-lookup"><span data-stu-id="ce7f7-103">Get all search analytics information</span></span>

<span data-ttu-id="ce7f7-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="ce7f7-104">**Applies To**</span></span>

- <span data-ttu-id="ce7f7-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="ce7f7-105">Partner Center</span></span>
- <span data-ttu-id="ce7f7-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="ce7f7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ce7f7-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="ce7f7-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ce7f7-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ce7f7-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ce7f7-109">Så här hämtar du all Sök analys information för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-109">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce7f7-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ce7f7-110">Prerequisites</span></span>

- <span data-ttu-id="ce7f7-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ce7f7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ce7f7-112">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ce7f7-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ce7f7-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ce7f7-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="ce7f7-114">Request syntax</span></span>

| <span data-ttu-id="ce7f7-115">Metod</span><span class="sxs-lookup"><span data-stu-id="ce7f7-115">Method</span></span>  | <span data-ttu-id="ce7f7-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ce7f7-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="ce7f7-117">**TA**</span><span class="sxs-lookup"><span data-stu-id="ce7f7-117">**GET**</span></span> | <span data-ttu-id="ce7f7-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/search http/1.1</span><span class="sxs-lookup"><span data-stu-id="ce7f7-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="ce7f7-119">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="ce7f7-119">URI parameters</span></span>

|    <span data-ttu-id="ce7f7-120">Parameter</span><span class="sxs-lookup"><span data-stu-id="ce7f7-120">Parameter</span></span>     |  <span data-ttu-id="ce7f7-121">Typ</span><span class="sxs-lookup"><span data-stu-id="ce7f7-121">Type</span></span>  |                                                                                                                   <span data-ttu-id="ce7f7-122">Description</span><span class="sxs-lookup"><span data-stu-id="ce7f7-122">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="ce7f7-123">filter</span><span class="sxs-lookup"><span data-stu-id="ce7f7-123">filter</span></span>      | <span data-ttu-id="ce7f7-124">sträng</span><span class="sxs-lookup"><span data-stu-id="ce7f7-124">string</span></span> |                                                                     <span data-ttu-id="ce7f7-125">Returnerar data som matchar filter villkoret.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-125">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="ce7f7-126">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="ce7f7-126">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="ce7f7-127">groupby</span><span class="sxs-lookup"><span data-stu-id="ce7f7-127">groupby</span></span>      | <span data-ttu-id="ce7f7-128">sträng</span><span class="sxs-lookup"><span data-stu-id="ce7f7-128">string</span></span> |                                         <span data-ttu-id="ce7f7-129">Har stöd för både villkor och datum.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-129">Supports both terms and dates.</span></span> <span data-ttu-id="ce7f7-130">Kort krets logik för att begränsa antalet buckets.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-130">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="ce7f7-131">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="ce7f7-131">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="ce7f7-132">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="ce7f7-132">aggregationLevel</span></span> | <span data-ttu-id="ce7f7-133">sträng</span><span class="sxs-lookup"><span data-stu-id="ce7f7-133">string</span></span> | <span data-ttu-id="ce7f7-134">Parametern *aggregationLevel* kräver en *groupby*.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-134">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="ce7f7-135">Parametern *aggregationLevel* gäller för alla datum fält som finns i *groupby*.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-135">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="ce7f7-136">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="ce7f7-136">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="ce7f7-137">top</span><span class="sxs-lookup"><span data-stu-id="ce7f7-137">top</span></span>        | <span data-ttu-id="ce7f7-138">sträng</span><span class="sxs-lookup"><span data-stu-id="ce7f7-138">string</span></span> |                                                                     <span data-ttu-id="ce7f7-139">Sid gränsen är 10000.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-139">The page limit is 10000.</span></span> <span data-ttu-id="ce7f7-140">Tar ett värde som är mindre än 10000.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-140">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="ce7f7-141">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="ce7f7-141">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="ce7f7-142">hoppa över</span><span class="sxs-lookup"><span data-stu-id="ce7f7-142">skip</span></span>       | <span data-ttu-id="ce7f7-143">sträng</span><span class="sxs-lookup"><span data-stu-id="ce7f7-143">string</span></span> |                                                                                  <span data-ttu-id="ce7f7-144">Antal rader som ska hoppas över.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-144">Number of rows to skip.</span></span> </br> <span data-ttu-id="ce7f7-145">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="ce7f7-145">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="ce7f7-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ce7f7-146">Request headers</span></span>

<span data-ttu-id="ce7f7-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ce7f7-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ce7f7-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ce7f7-148">Request body</span></span>

<span data-ttu-id="ce7f7-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ce7f7-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ce7f7-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="ce7f7-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ce7f7-151">REST response</span></span>

<span data-ttu-id="ce7f7-152">Om det lyckas innehåller svars texten en samling [Sök](partner-center-analytics-resources.md#search-resource) resurser.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-152">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ce7f7-153">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ce7f7-153">Response success and error codes</span></span>

<span data-ttu-id="ce7f7-154">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ce7f7-155">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ce7f7-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ce7f7-156">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ce7f7-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ce7f7-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ce7f7-157">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ce7f7-158">Se även</span><span class="sxs-lookup"><span data-stu-id="ce7f7-158">See also</span></span>

- [<span data-ttu-id="ce7f7-159">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="ce7f7-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
