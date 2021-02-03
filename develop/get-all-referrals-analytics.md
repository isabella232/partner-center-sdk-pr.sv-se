---
title: Hämta all information om hänvisningsanalys
description: Så här hämtar du all information om referenser till analyser.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769081"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="24532-103">Hämta all information om hänvisningsanalys</span><span class="sxs-lookup"><span data-stu-id="24532-103">Get all referrals analytics information</span></span>

<span data-ttu-id="24532-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="24532-104">**Applies To**</span></span>

- <span data-ttu-id="24532-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="24532-105">Partner Center</span></span>
- <span data-ttu-id="24532-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="24532-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="24532-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="24532-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="24532-108">Så här hämtar du all referensinformations analys information för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="24532-108">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24532-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="24532-109">Prerequisites</span></span>

- <span data-ttu-id="24532-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="24532-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="24532-111">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="24532-111">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="24532-112">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="24532-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="24532-113">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="24532-113">Request syntax</span></span>

| <span data-ttu-id="24532-114">Metod</span><span class="sxs-lookup"><span data-stu-id="24532-114">Method</span></span>  | <span data-ttu-id="24532-115">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="24532-115">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="24532-116">**TA**</span><span class="sxs-lookup"><span data-stu-id="24532-116">**GET**</span></span> | <span data-ttu-id="24532-117">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Referrals http/1.1</span><span class="sxs-lookup"><span data-stu-id="24532-117">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="24532-118">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="24532-118">URI parameters</span></span>

| <span data-ttu-id="24532-119">Parameter</span><span class="sxs-lookup"><span data-stu-id="24532-119">Parameter</span></span> | <span data-ttu-id="24532-120">Typ</span><span class="sxs-lookup"><span data-stu-id="24532-120">Type</span></span> | <span data-ttu-id="24532-121">Description</span><span class="sxs-lookup"><span data-stu-id="24532-121">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="24532-122">filter</span><span class="sxs-lookup"><span data-stu-id="24532-122">filter</span></span> | <span data-ttu-id="24532-123">sträng</span><span class="sxs-lookup"><span data-stu-id="24532-123">string</span></span> | <span data-ttu-id="24532-124">Returnerar data som matchar filter villkoret.</span><span class="sxs-lookup"><span data-stu-id="24532-124">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="24532-125">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="24532-125">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="24532-126">groupby</span><span class="sxs-lookup"><span data-stu-id="24532-126">groupby</span></span> | <span data-ttu-id="24532-127">sträng</span><span class="sxs-lookup"><span data-stu-id="24532-127">string</span></span> | <span data-ttu-id="24532-128">Har stöd för både villkor och datum.</span><span class="sxs-lookup"><span data-stu-id="24532-128">Supports both terms and dates.</span></span> <span data-ttu-id="24532-129">Kort krets logik för att begränsa antalet buckets.</span><span class="sxs-lookup"><span data-stu-id="24532-129">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="24532-130">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="24532-130">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="24532-131">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="24532-131">aggregationLevel</span></span> | <span data-ttu-id="24532-132">sträng</span><span class="sxs-lookup"><span data-stu-id="24532-132">string</span></span> | <span data-ttu-id="24532-133">Parametern *aggregationLevel* kräver en *groupby*.</span><span class="sxs-lookup"><span data-stu-id="24532-133">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="24532-134">Parametern *aggregationLevel* gäller för alla datum fält som finns i *groupby*.</span><span class="sxs-lookup"><span data-stu-id="24532-134">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="24532-135">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="24532-135">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="24532-136">top</span><span class="sxs-lookup"><span data-stu-id="24532-136">top</span></span> | <span data-ttu-id="24532-137">sträng</span><span class="sxs-lookup"><span data-stu-id="24532-137">string</span></span> | <span data-ttu-id="24532-138">Sid gränsen är 10000.</span><span class="sxs-lookup"><span data-stu-id="24532-138">The page limit is 10000.</span></span> <span data-ttu-id="24532-139">Tar ett värde som är mindre än 10000.</span><span class="sxs-lookup"><span data-stu-id="24532-139">Takes any value less than 10000.</span></span></br> <span data-ttu-id="24532-140">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="24532-140">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="24532-141">hoppa över</span><span class="sxs-lookup"><span data-stu-id="24532-141">skip</span></span> | <span data-ttu-id="24532-142">sträng</span><span class="sxs-lookup"><span data-stu-id="24532-142">string</span></span> | <span data-ttu-id="24532-143">Antal rader som ska hoppas över.</span><span class="sxs-lookup"><span data-stu-id="24532-143">Number of rows to skip.</span></span></br> <span data-ttu-id="24532-144">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="24532-144">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="24532-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="24532-145">Request headers</span></span>

<span data-ttu-id="24532-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="24532-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="24532-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="24532-147">Request body</span></span>

<span data-ttu-id="24532-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="24532-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="24532-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="24532-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="24532-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="24532-150">REST response</span></span>

<span data-ttu-id="24532-151">Om det lyckas innehåller svars texten en samling av [hänvisnings](partner-center-analytics-resources.md#referrals-resource) resurser.</span><span class="sxs-lookup"><span data-stu-id="24532-151">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="24532-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="24532-152">Response success and error codes</span></span>

<span data-ttu-id="24532-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="24532-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="24532-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="24532-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="24532-155">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="24532-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="24532-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="24532-156">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="24532-157">Se även</span><span class="sxs-lookup"><span data-stu-id="24532-157">See also</span></span>

- [<span data-ttu-id="24532-158">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="24532-158">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
