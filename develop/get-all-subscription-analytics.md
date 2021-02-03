---
title: Hämta all information om prenumerationsanalys
description: Hämta all information om prenumerations analys.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768754"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="41c32-103">Hämta all information om prenumerationsanalys</span><span class="sxs-lookup"><span data-stu-id="41c32-103">Get all subscription analytics information</span></span>

<span data-ttu-id="41c32-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="41c32-104">**Applies to:**</span></span>

- <span data-ttu-id="41c32-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="41c32-105">Partner Center</span></span>
- <span data-ttu-id="41c32-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="41c32-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="41c32-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="41c32-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="41c32-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="41c32-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="41c32-109">Den här artikeln beskriver hur du hämtar all information om prenumerations analys för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="41c32-109">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41c32-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="41c32-110">Prerequisites</span></span>

- <span data-ttu-id="41c32-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="41c32-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="41c32-112">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="41c32-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="41c32-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="41c32-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="41c32-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="41c32-114">Request syntax</span></span>

| <span data-ttu-id="41c32-115">Metod</span><span class="sxs-lookup"><span data-stu-id="41c32-115">Method</span></span> | <span data-ttu-id="41c32-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="41c32-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="41c32-117">**TA**</span><span class="sxs-lookup"><span data-stu-id="41c32-117">**GET**</span></span> | <span data-ttu-id="41c32-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions http/1.1</span><span class="sxs-lookup"><span data-stu-id="41c32-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="41c32-119">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="41c32-119">URI parameters</span></span>

<span data-ttu-id="41c32-120">I följande tabell visas valfria parametrar och beskrivningar:</span><span class="sxs-lookup"><span data-stu-id="41c32-120">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="41c32-121">Parameter</span><span class="sxs-lookup"><span data-stu-id="41c32-121">Parameter</span></span> | <span data-ttu-id="41c32-122">Typ</span><span class="sxs-lookup"><span data-stu-id="41c32-122">Type</span></span> |  <span data-ttu-id="41c32-123">Description</span><span class="sxs-lookup"><span data-stu-id="41c32-123">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="41c32-124">top</span><span class="sxs-lookup"><span data-stu-id="41c32-124">top</span></span> | <span data-ttu-id="41c32-125">int</span><span class="sxs-lookup"><span data-stu-id="41c32-125">int</span></span> | <span data-ttu-id="41c32-126">Det antal rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="41c32-126">The number of rows of data to return in the request.</span></span> <span data-ttu-id="41c32-127">Om värdet inte anges, är det högsta värdet och standardvärdet `10000` .</span><span class="sxs-lookup"><span data-stu-id="41c32-127">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="41c32-128">Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="41c32-128">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="41c32-129">hoppa över</span><span class="sxs-lookup"><span data-stu-id="41c32-129">skip</span></span> | <span data-ttu-id="41c32-130">int</span><span class="sxs-lookup"><span data-stu-id="41c32-130">int</span></span> | <span data-ttu-id="41c32-131">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="41c32-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="41c32-132">Använd den här parametern för att växla mellan stora data mängder.</span><span class="sxs-lookup"><span data-stu-id="41c32-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="41c32-133">Till exempel `top=10000` och `skip=0` hämtar de första 10000 raderna med data `top=10000` och `skip=10000` hämtar nästa 10000 rader med data.</span><span class="sxs-lookup"><span data-stu-id="41c32-133">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="41c32-134">filter</span><span class="sxs-lookup"><span data-stu-id="41c32-134">filter</span></span> | <span data-ttu-id="41c32-135">sträng</span><span class="sxs-lookup"><span data-stu-id="41c32-135">string</span></span> | <span data-ttu-id="41c32-136">En eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="41c32-136">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="41c32-137">Varje filter instruktion innehåller ett fält namn från svars texten och ett värde som är kopplat till **`eq`** , **`ne`** , eller för vissa fält, **`contains`** operatorn.</span><span class="sxs-lookup"><span data-stu-id="41c32-137">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="41c32-138">Instruktioner kan kombineras med hjälp av **`and`** eller **`or`** .</span><span class="sxs-lookup"><span data-stu-id="41c32-138">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="41c32-139">Sträng värden måste omges av enkla citat tecken i **filter** parametern.</span><span class="sxs-lookup"><span data-stu-id="41c32-139">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="41c32-140">I följande avsnitt finns en lista över fält som kan filtreras och de operatorer som stöds med dessa fält.</span><span class="sxs-lookup"><span data-stu-id="41c32-140">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="41c32-141">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="41c32-141">aggregationLevel</span></span> | <span data-ttu-id="41c32-142">sträng</span><span class="sxs-lookup"><span data-stu-id="41c32-142">string</span></span> | <span data-ttu-id="41c32-143">Anger det tidsintervall som aggregerade data ska hämtas från.</span><span class="sxs-lookup"><span data-stu-id="41c32-143">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="41c32-144">Kan vara en av följande strängar: **dag**, **vecka** eller **månad**.</span><span class="sxs-lookup"><span data-stu-id="41c32-144">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="41c32-145">Om värdet inte anges är standardvärdet **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="41c32-145">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="41c32-146">Den här parametern gäller endast när ett datum fält skickas som en del av **groupBy** -parametern.</span><span class="sxs-lookup"><span data-stu-id="41c32-146">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="41c32-147">groupBy</span><span class="sxs-lookup"><span data-stu-id="41c32-147">groupBy</span></span> | <span data-ttu-id="41c32-148">sträng</span><span class="sxs-lookup"><span data-stu-id="41c32-148">string</span></span> | <span data-ttu-id="41c32-149">En instruktion som endast tillämpar data agg regering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="41c32-149">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="41c32-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="41c32-150">Request headers</span></span>

<span data-ttu-id="41c32-151">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="41c32-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="41c32-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="41c32-152">Request body</span></span>

<span data-ttu-id="41c32-153">Inga.</span><span class="sxs-lookup"><span data-stu-id="41c32-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="41c32-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="41c32-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="41c32-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="41c32-155">REST response</span></span>

<span data-ttu-id="41c32-156">Om det lyckas innehåller svars texten en samling [**prenumerations**](partner-center-analytics-resources.md#subscription-resource) resurser.</span><span class="sxs-lookup"><span data-stu-id="41c32-156">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="41c32-157">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="41c32-157">Response success and error codes</span></span>

<span data-ttu-id="41c32-158">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="41c32-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="41c32-159">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="41c32-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="41c32-160">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="41c32-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="41c32-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="41c32-161">Response example</span></span>

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a><span data-ttu-id="41c32-162">Se även</span><span class="sxs-lookup"><span data-stu-id="41c32-162">See also</span></span>

- [<span data-ttu-id="41c32-163">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="41c32-163">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
