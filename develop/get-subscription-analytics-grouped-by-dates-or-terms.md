---
title: Hämta prenumerations analys grupperat efter datum eller villkor
description: Hur du hämtar information om prenumerations analys grupperat efter datum eller villkor.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769051"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="d7cd2-103">Hämta prenumerations analys grupperat efter datum eller villkor</span><span class="sxs-lookup"><span data-stu-id="d7cd2-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="d7cd2-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="d7cd2-104">**Applies To**</span></span>

- <span data-ttu-id="d7cd2-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d7cd2-105">Partner Center</span></span>
- <span data-ttu-id="d7cd2-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d7cd2-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d7cd2-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="d7cd2-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d7cd2-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d7cd2-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d7cd2-109">Hur du hämtar information om prenumerations analys för dina kunder grupperade efter datum eller villkor.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-109">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7cd2-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d7cd2-110">Prerequisites</span></span>

- <span data-ttu-id="d7cd2-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d7cd2-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d7cd2-112">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d7cd2-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d7cd2-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d7cd2-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d7cd2-114">Request syntax</span></span>

| <span data-ttu-id="d7cd2-115">Metod</span><span class="sxs-lookup"><span data-stu-id="d7cd2-115">Method</span></span> | <span data-ttu-id="d7cd2-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d7cd2-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="d7cd2-117">**TA**</span><span class="sxs-lookup"><span data-stu-id="d7cd2-117">**GET**</span></span> | <span data-ttu-id="d7cd2-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? groupby = {groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="d7cd2-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="d7cd2-119">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="d7cd2-119">URI parameters</span></span>

<span data-ttu-id="d7cd2-120">Använd följande obligatoriska Sök vägs parametrar för att identifiera din organisation och gruppera resultatet.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-120">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="d7cd2-121">Namn</span><span class="sxs-lookup"><span data-stu-id="d7cd2-121">Name</span></span> | <span data-ttu-id="d7cd2-122">Typ</span><span class="sxs-lookup"><span data-stu-id="d7cd2-122">Type</span></span> | <span data-ttu-id="d7cd2-123">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d7cd2-123">Required</span></span> | <span data-ttu-id="d7cd2-124">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d7cd2-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="d7cd2-125">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="d7cd2-125">groupby_queries</span></span> | <span data-ttu-id="d7cd2-126">par med strängar och dateTime</span><span class="sxs-lookup"><span data-stu-id="d7cd2-126">pairs of strings and dateTime</span></span> | <span data-ttu-id="d7cd2-127">Yes</span><span class="sxs-lookup"><span data-stu-id="d7cd2-127">Yes</span></span> | <span data-ttu-id="d7cd2-128">Villkoren och datumen för att filtrera resultatet.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-128">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="d7cd2-129">GroupBy-syntax</span><span class="sxs-lookup"><span data-stu-id="d7cd2-129">GroupBy syntax</span></span>

<span data-ttu-id="d7cd2-130">Group by-parametern måste bestå av en serie kommaavgränsade fält värden.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-130">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="d7cd2-131">Ett avkodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="d7cd2-131">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="d7cd2-132">I följande tabell visas en lista över de fält som stöds för Group by.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-132">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="d7cd2-133">Fält</span><span class="sxs-lookup"><span data-stu-id="d7cd2-133">Field</span></span> | <span data-ttu-id="d7cd2-134">Typ</span><span class="sxs-lookup"><span data-stu-id="d7cd2-134">Type</span></span> | <span data-ttu-id="d7cd2-135">Description</span><span class="sxs-lookup"><span data-stu-id="d7cd2-135">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="d7cd2-136">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="d7cd2-136">customerTenantId</span></span> | <span data-ttu-id="d7cd2-137">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-137">string</span></span> | <span data-ttu-id="d7cd2-138">En GUID-formaterad sträng som identifierar kundens klient organisation.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-138">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="d7cd2-139">customerName</span><span class="sxs-lookup"><span data-stu-id="d7cd2-139">customerName</span></span> | <span data-ttu-id="d7cd2-140">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-140">string</span></span> | <span data-ttu-id="d7cd2-141">Namnet på kunden.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-141">The name of the customer.</span></span> |
| <span data-ttu-id="d7cd2-142">customerMarket</span><span class="sxs-lookup"><span data-stu-id="d7cd2-142">customerMarket</span></span> | <span data-ttu-id="d7cd2-143">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-143">string</span></span> | <span data-ttu-id="d7cd2-144">Landet/regionen som kunden gör affärer med.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-144">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="d7cd2-145">id</span><span class="sxs-lookup"><span data-stu-id="d7cd2-145">id</span></span> | <span data-ttu-id="d7cd2-146">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-146">string</span></span> | <span data-ttu-id="d7cd2-147">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-147">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="d7cd2-148">status</span><span class="sxs-lookup"><span data-stu-id="d7cd2-148">status</span></span> | <span data-ttu-id="d7cd2-149">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-149">string</span></span> | <span data-ttu-id="d7cd2-150">Prenumerationens status.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-150">The subscription status.</span></span> <span data-ttu-id="d7cd2-151">De värden som stöds är: "aktiv", "inaktive rad" eller "deetablerat".</span><span class="sxs-lookup"><span data-stu-id="d7cd2-151">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="d7cd2-152">Namn</span><span class="sxs-lookup"><span data-stu-id="d7cd2-152">productName</span></span> | <span data-ttu-id="d7cd2-153">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-153">string</span></span> | <span data-ttu-id="d7cd2-154">Produktens namn.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-154">The name of the product.</span></span> |
| <span data-ttu-id="d7cd2-155">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="d7cd2-155">subscriptionType</span></span> | <span data-ttu-id="d7cd2-156">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-156">string</span></span> | <span data-ttu-id="d7cd2-157">Prenumerations typ.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-157">The subscription type.</span></span> <span data-ttu-id="d7cd2-158">Obs! det här fältet är Skift läges känsligt.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-158">Note: This field is case sensitive.</span></span> <span data-ttu-id="d7cd2-159">De värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="d7cd2-159">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="d7cd2-160">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="d7cd2-160">autoRenewEnabled</span></span> | <span data-ttu-id="d7cd2-161">Boolesk</span><span class="sxs-lookup"><span data-stu-id="d7cd2-161">Boolean</span></span> | <span data-ttu-id="d7cd2-162">Ett värde som anger om prenumerationen förnyas automatiskt.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-162">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="d7cd2-163">Partner</span><span class="sxs-lookup"><span data-stu-id="d7cd2-163">partnerId</span></span>  | <span data-ttu-id="d7cd2-164">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-164">string</span></span> | <span data-ttu-id="d7cd2-165">MPN-ID.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-165">The MPN ID.</span></span> <span data-ttu-id="d7cd2-166">För en direkt åter försäljare är den här parametern MPN-ID för partnern.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-166">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="d7cd2-167">För en indirekt åter försäljare är den här parametern MPN-ID: t för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-167">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="d7cd2-168">friendlyName</span><span class="sxs-lookup"><span data-stu-id="d7cd2-168">friendlyName</span></span> | <span data-ttu-id="d7cd2-169">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-169">string</span></span> | <span data-ttu-id="d7cd2-170">Namnet på prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-170">The name of the subscription.</span></span> |
| <span data-ttu-id="d7cd2-171">partnerName</span><span class="sxs-lookup"><span data-stu-id="d7cd2-171">partnerName</span></span> | <span data-ttu-id="d7cd2-172">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-172">string</span></span> | <span data-ttu-id="d7cd2-173">Namnet på partnern som prenumerationen köptes för</span><span class="sxs-lookup"><span data-stu-id="d7cd2-173">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="d7cd2-174">providerName</span><span class="sxs-lookup"><span data-stu-id="d7cd2-174">providerName</span></span> | <span data-ttu-id="d7cd2-175">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-175">string</span></span> | <span data-ttu-id="d7cd2-176">När prenumerations transaktionen är för den indirekta åter försäljaren är Providerns namn den indirekta providern som köpte prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-176">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="d7cd2-177">creationDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-177">creationDate</span></span> | <span data-ttu-id="d7cd2-178">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-178">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-179">Det datum då prenumerationen skapades.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-179">The date the subscription was created.</span></span> |
| <span data-ttu-id="d7cd2-180">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-180">effectiveStartDate</span></span> | <span data-ttu-id="d7cd2-181">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-181">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-182">Det datum då prenumerationen startar.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-182">The date the subscription starts.</span></span> |
| <span data-ttu-id="d7cd2-183">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-183">commitmentEndDate</span></span> | <span data-ttu-id="d7cd2-184">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-184">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-185">Det datum då prenumerationen slutar.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-185">The date the subscription ends.</span></span> |
| <span data-ttu-id="d7cd2-186">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-186">currentStateEndDate</span></span> | <span data-ttu-id="d7cd2-187">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-187">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-188">Det datum då prenumerationens aktuella status kommer att ändras.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-188">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="d7cd2-189">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-189">trialToPaidConversionDate</span></span> | <span data-ttu-id="d7cd2-190">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-190">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-191">Det datum då prenumerationen konverteras från utvärderings versionen till betald.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-191">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="d7cd2-192">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-192">The default value is null.</span></span> |
| <span data-ttu-id="d7cd2-193">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-193">trialStartDate</span></span> | <span data-ttu-id="d7cd2-194">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-194">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-195">Det datum då utvärderings perioden för prenumerationen startades.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-195">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="d7cd2-196">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-196">The default value is null.</span></span> |
| <span data-ttu-id="d7cd2-197">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-197">lastUsageDate</span></span> | <span data-ttu-id="d7cd2-198">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-198">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-199">Det datum då prenumerationen senast användes.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-199">The date that the subscription was last used.</span></span> <span data-ttu-id="d7cd2-200">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-200">The default value is null.</span></span> |
| <span data-ttu-id="d7cd2-201">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-201">deprovisionedDate</span></span> | <span data-ttu-id="d7cd2-202">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-202">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-203">Det datum då prenumerationen avetablerades.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-203">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="d7cd2-204">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-204">The default value is null.</span></span> |
| <span data-ttu-id="d7cd2-205">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="d7cd2-205">lastRenewalDate</span></span> | <span data-ttu-id="d7cd2-206">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="d7cd2-206">string in UTC date time format</span></span> | <span data-ttu-id="d7cd2-207">Det datum då prenumerationen senast förnyades.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-207">The date that the subscription was last renewed.</span></span> <span data-ttu-id="d7cd2-208">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-208">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="d7cd2-209">Filter fält</span><span class="sxs-lookup"><span data-stu-id="d7cd2-209">Filter fields</span></span>

<span data-ttu-id="d7cd2-210">I följande tabell visas valfria filter fält och deras beskrivningar:</span><span class="sxs-lookup"><span data-stu-id="d7cd2-210">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="d7cd2-211">Fält</span><span class="sxs-lookup"><span data-stu-id="d7cd2-211">Field</span></span> | <span data-ttu-id="d7cd2-212">Typ</span><span class="sxs-lookup"><span data-stu-id="d7cd2-212">Type</span></span> |  <span data-ttu-id="d7cd2-213">Description</span><span class="sxs-lookup"><span data-stu-id="d7cd2-213">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="d7cd2-214">top</span><span class="sxs-lookup"><span data-stu-id="d7cd2-214">top</span></span> | <span data-ttu-id="d7cd2-215">int</span><span class="sxs-lookup"><span data-stu-id="d7cd2-215">int</span></span> | <span data-ttu-id="d7cd2-216">Det antal rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-216">The number of rows of data to return in the request.</span></span> <span data-ttu-id="d7cd2-217">Om värdet inte anges är det högsta värdet och standardvärdet 10000.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-217">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="d7cd2-218">Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-218">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="d7cd2-219">hoppa över</span><span class="sxs-lookup"><span data-stu-id="d7cd2-219">skip</span></span> | <span data-ttu-id="d7cd2-220">int</span><span class="sxs-lookup"><span data-stu-id="d7cd2-220">int</span></span> | <span data-ttu-id="d7cd2-221">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-221">The number of rows to skip in the query.</span></span> <span data-ttu-id="d7cd2-222">Använd den här parametern för att växla mellan stora data mängder.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-222">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="d7cd2-223">Till exempel Top = 10000 och Skip = 0 hämtar de första 10000 raderna med data, Top = 10000 och Skip = 10000 hämtar nästa 10000 rader med data.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-223">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="d7cd2-224">filter</span><span class="sxs-lookup"><span data-stu-id="d7cd2-224">filter</span></span> | <span data-ttu-id="d7cd2-225">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-225">string</span></span> | <span data-ttu-id="d7cd2-226">En eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-226">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="d7cd2-227">Varje filter instruktion innehåller ett fält namn från svars texten och ett värde som är kopplat till **`eq`** , **`ne`** , eller för vissa fält, **`contains`** operatorn.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-227">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="d7cd2-228">Instruktioner kan kombineras med hjälp av **`and`** eller **`or`** .</span><span class="sxs-lookup"><span data-stu-id="d7cd2-228">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="d7cd2-229">Sträng värden måste omges av enkla citat tecken i filter parametern.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-229">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="d7cd2-230">I följande avsnitt finns en lista över fält som kan filtreras och de operatorer som stöds med dessa fält.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-230">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="d7cd2-231">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="d7cd2-231">aggregationLevel</span></span> | <span data-ttu-id="d7cd2-232">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-232">string</span></span> | <span data-ttu-id="d7cd2-233">Anger det tidsintervall som aggregerade data ska hämtas från.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-233">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="d7cd2-234">Kan vara en av följande strängar: **dag**, **vecka** eller **månad**.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-234">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="d7cd2-235">Om värdet inte anges är standardvärdet **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-235">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="d7cd2-236">**Obs!** den här parametern gäller endast när ett datum fält skickas som en del av parametern groupBy.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-236">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="d7cd2-237">groupBy</span><span class="sxs-lookup"><span data-stu-id="d7cd2-237">groupBy</span></span> | <span data-ttu-id="d7cd2-238">sträng</span><span class="sxs-lookup"><span data-stu-id="d7cd2-238">string</span></span> | <span data-ttu-id="d7cd2-239">En instruktion som endast tillämpar data agg regering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-239">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d7cd2-240">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d7cd2-240">Request headers</span></span>

<span data-ttu-id="d7cd2-241">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d7cd2-241">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d7cd2-242">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d7cd2-242">Request body</span></span>

<span data-ttu-id="d7cd2-243">Inga.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-243">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d7cd2-244">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d7cd2-244">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="d7cd2-245">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d7cd2-245">REST response</span></span>

<span data-ttu-id="d7cd2-246">Om det lyckas innehåller svars texten en samling [prenumerations](partner-center-analytics-resources.md#subscription-resource) resurser grupperade enligt de angivna villkoren och datumen.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-246">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d7cd2-247">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d7cd2-247">Response success and error codes</span></span>

<span data-ttu-id="d7cd2-248">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-248">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d7cd2-249">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d7cd2-249">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d7cd2-250">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d7cd2-250">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d7cd2-251">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d7cd2-251">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a><span data-ttu-id="d7cd2-252">Se även</span><span class="sxs-lookup"><span data-stu-id="d7cd2-252">See also</span></span>

[<span data-ttu-id="d7cd2-253">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="d7cd2-253">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
