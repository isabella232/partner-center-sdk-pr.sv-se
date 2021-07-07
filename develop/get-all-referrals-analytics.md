---
title: Hämta all information om hänvisningsanalys
description: Så här hämtar du all referensanalysinformation.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 7deda4098ceb9eb4e1ee75056c53c754618bf3e2
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760614"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="12509-103">Hämta all information om hänvisningsanalys</span><span class="sxs-lookup"><span data-stu-id="12509-103">Get all referrals analytics information</span></span>

<span data-ttu-id="12509-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="12509-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="12509-105">Hur du hämtar all referensanalysinformation för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="12509-105">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12509-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="12509-106">Prerequisites</span></span>

- <span data-ttu-id="12509-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="12509-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="12509-108">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="12509-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="12509-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="12509-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="12509-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="12509-110">Request syntax</span></span>

| <span data-ttu-id="12509-111">Metod</span><span class="sxs-lookup"><span data-stu-id="12509-111">Method</span></span>  | <span data-ttu-id="12509-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="12509-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="12509-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="12509-113">**GET**</span></span> | <span data-ttu-id="12509-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="12509-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="12509-115">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="12509-115">URI parameters</span></span>

| <span data-ttu-id="12509-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="12509-116">Parameter</span></span> | <span data-ttu-id="12509-117">Typ</span><span class="sxs-lookup"><span data-stu-id="12509-117">Type</span></span> | <span data-ttu-id="12509-118">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="12509-118">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="12509-119">filter</span><span class="sxs-lookup"><span data-stu-id="12509-119">filter</span></span> | <span data-ttu-id="12509-120">sträng</span><span class="sxs-lookup"><span data-stu-id="12509-120">string</span></span> | <span data-ttu-id="12509-121">Returnerar data som matchar filtervillkoret.</span><span class="sxs-lookup"><span data-stu-id="12509-121">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="12509-122">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="12509-122">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="12509-123">groupby</span><span class="sxs-lookup"><span data-stu-id="12509-123">groupby</span></span> | <span data-ttu-id="12509-124">sträng</span><span class="sxs-lookup"><span data-stu-id="12509-124">string</span></span> | <span data-ttu-id="12509-125">Stöder både termer och datum.</span><span class="sxs-lookup"><span data-stu-id="12509-125">Supports both terms and dates.</span></span> <span data-ttu-id="12509-126">Kortslutningslogik för att begränsa antalet bucketar.</span><span class="sxs-lookup"><span data-stu-id="12509-126">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="12509-127">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="12509-127">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="12509-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="12509-128">aggregationLevel</span></span> | <span data-ttu-id="12509-129">sträng</span><span class="sxs-lookup"><span data-stu-id="12509-129">string</span></span> | <span data-ttu-id="12509-130">Parametern *aggregationLevel* kräver en *groupby*.</span><span class="sxs-lookup"><span data-stu-id="12509-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="12509-131">Parametern *aggregationLevel* gäller för alla datumfält som finns i *groupby*.</span><span class="sxs-lookup"><span data-stu-id="12509-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="12509-132">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="12509-132">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="12509-133">top</span><span class="sxs-lookup"><span data-stu-id="12509-133">top</span></span> | <span data-ttu-id="12509-134">sträng</span><span class="sxs-lookup"><span data-stu-id="12509-134">string</span></span> | <span data-ttu-id="12509-135">Sidgränsen är 10 000.</span><span class="sxs-lookup"><span data-stu-id="12509-135">The page limit is 10000.</span></span> <span data-ttu-id="12509-136">Tar ett värde som är mindre än 10 000.</span><span class="sxs-lookup"><span data-stu-id="12509-136">Takes any value less than 10000.</span></span></br> <span data-ttu-id="12509-137">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="12509-137">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="12509-138">hoppa över</span><span class="sxs-lookup"><span data-stu-id="12509-138">skip</span></span> | <span data-ttu-id="12509-139">sträng</span><span class="sxs-lookup"><span data-stu-id="12509-139">string</span></span> | <span data-ttu-id="12509-140">Antal rader som ska hoppas över.</span><span class="sxs-lookup"><span data-stu-id="12509-140">Number of rows to skip.</span></span></br> <span data-ttu-id="12509-141">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="12509-141">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="12509-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="12509-142">Request headers</span></span>

<span data-ttu-id="12509-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="12509-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="12509-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="12509-144">Request body</span></span>

<span data-ttu-id="12509-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="12509-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="12509-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="12509-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="12509-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="12509-147">REST response</span></span>

<span data-ttu-id="12509-148">Om det lyckas innehåller svarstexten en samling [referensresurser.](partner-center-analytics-resources.md#referrals-resource)</span><span class="sxs-lookup"><span data-stu-id="12509-148">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="12509-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="12509-149">Response success and error codes</span></span>

<span data-ttu-id="12509-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="12509-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="12509-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="12509-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="12509-152">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="12509-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="12509-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="12509-153">Response example</span></span>

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a><span data-ttu-id="12509-154">Se även</span><span class="sxs-lookup"><span data-stu-id="12509-154">See also</span></span>

- [<span data-ttu-id="12509-155">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="12509-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
