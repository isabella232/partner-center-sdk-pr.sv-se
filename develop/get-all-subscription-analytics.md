---
title: Hämta all information om prenumerationsanalys
description: Så här hämtar du all prenumerationsanalysinformation.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760257"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="e3687-103">Hämta all information om prenumerationsanalys</span><span class="sxs-lookup"><span data-stu-id="e3687-103">Get all subscription analytics information</span></span>

<span data-ttu-id="e3687-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e3687-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e3687-105">Den här artikeln beskriver hur du hämtar all prenumerationsanalysinformation för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="e3687-105">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3687-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e3687-106">Prerequisites</span></span>

- <span data-ttu-id="e3687-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e3687-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e3687-108">Det här scenariot stöder autentisering endast med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e3687-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e3687-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e3687-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e3687-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="e3687-110">Request syntax</span></span>

| <span data-ttu-id="e3687-111">Metod</span><span class="sxs-lookup"><span data-stu-id="e3687-111">Method</span></span> | <span data-ttu-id="e3687-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e3687-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="e3687-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="e3687-113">**GET**</span></span> | <span data-ttu-id="e3687-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e3687-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="e3687-115">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="e3687-115">URI parameters</span></span>

<span data-ttu-id="e3687-116">I följande tabell visas valfria parametrar och deras beskrivningar:</span><span class="sxs-lookup"><span data-stu-id="e3687-116">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="e3687-117">Parameter</span><span class="sxs-lookup"><span data-stu-id="e3687-117">Parameter</span></span> | <span data-ttu-id="e3687-118">Typ</span><span class="sxs-lookup"><span data-stu-id="e3687-118">Type</span></span> |  <span data-ttu-id="e3687-119">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e3687-119">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="e3687-120">top</span><span class="sxs-lookup"><span data-stu-id="e3687-120">top</span></span> | <span data-ttu-id="e3687-121">int</span><span class="sxs-lookup"><span data-stu-id="e3687-121">int</span></span> | <span data-ttu-id="e3687-122">Antalet rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="e3687-122">The number of rows of data to return in the request.</span></span> <span data-ttu-id="e3687-123">Om värdet inte anges är det högsta värdet och standardvärdet `10000` .</span><span class="sxs-lookup"><span data-stu-id="e3687-123">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="e3687-124">Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa datasida.</span><span class="sxs-lookup"><span data-stu-id="e3687-124">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="e3687-125">hoppa över</span><span class="sxs-lookup"><span data-stu-id="e3687-125">skip</span></span> | <span data-ttu-id="e3687-126">int</span><span class="sxs-lookup"><span data-stu-id="e3687-126">int</span></span> | <span data-ttu-id="e3687-127">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="e3687-127">The number of rows to skip in the query.</span></span> <span data-ttu-id="e3687-128">Använd den här parametern för att bläddra igenom stora datamängder.</span><span class="sxs-lookup"><span data-stu-id="e3687-128">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="e3687-129">Till exempel `top=10000` hämtar och de första 10 000 raderna med data och hämtar de kommande `skip=0` `top=10000` `skip=10000` 10 000 raderna med data.</span><span class="sxs-lookup"><span data-stu-id="e3687-129">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="e3687-130">filter</span><span class="sxs-lookup"><span data-stu-id="e3687-130">filter</span></span> | <span data-ttu-id="e3687-131">sträng</span><span class="sxs-lookup"><span data-stu-id="e3687-131">string</span></span> | <span data-ttu-id="e3687-132">En eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="e3687-132">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="e3687-133">Varje filtersats innehåller ett fältnamn från svarstexten och ett värde som är associerat med **`eq`** **`ne`** operatorn , eller för vissa **`contains`** fält.</span><span class="sxs-lookup"><span data-stu-id="e3687-133">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="e3687-134">Instruktioner kan kombineras med **`and`** hjälp av eller **`or`** .</span><span class="sxs-lookup"><span data-stu-id="e3687-134">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="e3687-135">Strängvärden måste omges av enkla citattecken i **filterparametern.**</span><span class="sxs-lookup"><span data-stu-id="e3687-135">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="e3687-136">Se följande avsnitt för en lista över fält som kan filtreras och de operatorer som stöds med dessa fält.</span><span class="sxs-lookup"><span data-stu-id="e3687-136">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="e3687-137">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="e3687-137">aggregationLevel</span></span> | <span data-ttu-id="e3687-138">sträng</span><span class="sxs-lookup"><span data-stu-id="e3687-138">string</span></span> | <span data-ttu-id="e3687-139">Anger det tidsperiod som aggregerade data ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="e3687-139">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="e3687-140">Kan vara någon av följande strängar: **dag,** **vecka** eller **månad**.</span><span class="sxs-lookup"><span data-stu-id="e3687-140">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="e3687-141">Om värdet inte anges är standardvärdet **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="e3687-141">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="e3687-142">Den här parametern gäller endast när ett datumfält skickas som en del av **parametern groupBy.**</span><span class="sxs-lookup"><span data-stu-id="e3687-142">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="e3687-143">groupBy</span><span class="sxs-lookup"><span data-stu-id="e3687-143">groupBy</span></span> | <span data-ttu-id="e3687-144">sträng</span><span class="sxs-lookup"><span data-stu-id="e3687-144">string</span></span> | <span data-ttu-id="e3687-145">En instruktion som endast tillämpar dataaggregering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="e3687-145">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e3687-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e3687-146">Request headers</span></span>

<span data-ttu-id="e3687-147">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e3687-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e3687-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e3687-148">Request body</span></span>

<span data-ttu-id="e3687-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="e3687-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e3687-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e3687-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="e3687-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e3687-151">REST response</span></span>

<span data-ttu-id="e3687-152">Om det lyckas innehåller svarstexten en samling [**prenumerationsresurser.**](partner-center-analytics-resources.md#subscription-resource)</span><span class="sxs-lookup"><span data-stu-id="e3687-152">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e3687-153">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e3687-153">Response success and error codes</span></span>

<span data-ttu-id="e3687-154">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e3687-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e3687-155">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e3687-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e3687-156">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e3687-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e3687-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e3687-157">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="e3687-158">Se även</span><span class="sxs-lookup"><span data-stu-id="e3687-158">See also</span></span>

- [<span data-ttu-id="e3687-159">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="e3687-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
