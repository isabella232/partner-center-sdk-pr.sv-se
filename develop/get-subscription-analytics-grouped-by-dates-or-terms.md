---
title: Hämta prenumerationsanalys grupperade efter datum eller villkor
description: Så här hämtar du prenumerationsanalysinformation grupperad efter datum eller villkor.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8192a9863d53ec8697a7341cd38c69200614bd4a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548727"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="2309d-103">Hämta prenumerationsanalys grupperade efter datum eller villkor</span><span class="sxs-lookup"><span data-stu-id="2309d-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="2309d-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2309d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2309d-105">Så här hämtar du prenumerationsanalysinformation för dina kunder grupperade efter datum eller villkor.</span><span class="sxs-lookup"><span data-stu-id="2309d-105">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2309d-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2309d-106">Prerequisites</span></span>

- <span data-ttu-id="2309d-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2309d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2309d-108">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2309d-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="2309d-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2309d-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2309d-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="2309d-110">Request syntax</span></span>

| <span data-ttu-id="2309d-111">Metod</span><span class="sxs-lookup"><span data-stu-id="2309d-111">Method</span></span> | <span data-ttu-id="2309d-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2309d-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="2309d-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="2309d-113">**GET**</span></span> | <span data-ttu-id="2309d-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="2309d-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="2309d-115">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="2309d-115">URI parameters</span></span>

<span data-ttu-id="2309d-116">Använd följande obligatoriska sökvägsparametrar för att identifiera din organisation och gruppera resultaten.</span><span class="sxs-lookup"><span data-stu-id="2309d-116">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="2309d-117">Namn</span><span class="sxs-lookup"><span data-stu-id="2309d-117">Name</span></span> | <span data-ttu-id="2309d-118">Typ</span><span class="sxs-lookup"><span data-stu-id="2309d-118">Type</span></span> | <span data-ttu-id="2309d-119">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2309d-119">Required</span></span> | <span data-ttu-id="2309d-120">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2309d-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="2309d-121">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="2309d-121">groupby_queries</span></span> | <span data-ttu-id="2309d-122">par med strängar och dateTime</span><span class="sxs-lookup"><span data-stu-id="2309d-122">pairs of strings and dateTime</span></span> | <span data-ttu-id="2309d-123">Ja</span><span class="sxs-lookup"><span data-stu-id="2309d-123">Yes</span></span> | <span data-ttu-id="2309d-124">Termerna och datumen för att filtrera resultatet.</span><span class="sxs-lookup"><span data-stu-id="2309d-124">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="2309d-125">GroupBy-syntax</span><span class="sxs-lookup"><span data-stu-id="2309d-125">GroupBy syntax</span></span>

<span data-ttu-id="2309d-126">Gruppera efter parameter måste bestå av en serie kommaavgränsade fältvärden.</span><span class="sxs-lookup"><span data-stu-id="2309d-126">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="2309d-127">Ett okodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="2309d-127">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="2309d-128">I följande tabell visas en lista över de fält som stöds för gruppera efter.</span><span class="sxs-lookup"><span data-stu-id="2309d-128">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="2309d-129">Fält</span><span class="sxs-lookup"><span data-stu-id="2309d-129">Field</span></span> | <span data-ttu-id="2309d-130">Typ</span><span class="sxs-lookup"><span data-stu-id="2309d-130">Type</span></span> | <span data-ttu-id="2309d-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2309d-131">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="2309d-132">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="2309d-132">customerTenantId</span></span> | <span data-ttu-id="2309d-133">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-133">string</span></span> | <span data-ttu-id="2309d-134">En GUID-formaterad sträng som identifierar kundens klientorganisation.</span><span class="sxs-lookup"><span data-stu-id="2309d-134">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="2309d-135">customerName</span><span class="sxs-lookup"><span data-stu-id="2309d-135">customerName</span></span> | <span data-ttu-id="2309d-136">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-136">string</span></span> | <span data-ttu-id="2309d-137">Namnet på kunden.</span><span class="sxs-lookup"><span data-stu-id="2309d-137">The name of the customer.</span></span> |
| <span data-ttu-id="2309d-138">customerMarket</span><span class="sxs-lookup"><span data-stu-id="2309d-138">customerMarket</span></span> | <span data-ttu-id="2309d-139">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-139">string</span></span> | <span data-ttu-id="2309d-140">Land/region som kunden gör affärer i.</span><span class="sxs-lookup"><span data-stu-id="2309d-140">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="2309d-141">id</span><span class="sxs-lookup"><span data-stu-id="2309d-141">id</span></span> | <span data-ttu-id="2309d-142">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-142">string</span></span> | <span data-ttu-id="2309d-143">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="2309d-143">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="2309d-144">status</span><span class="sxs-lookup"><span data-stu-id="2309d-144">status</span></span> | <span data-ttu-id="2309d-145">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-145">string</span></span> | <span data-ttu-id="2309d-146">Prenumerationsstatus.</span><span class="sxs-lookup"><span data-stu-id="2309d-146">The subscription status.</span></span> <span data-ttu-id="2309d-147">Värden som stöds är: "ACTIVE", "SUSPENDED" eller "DEPROVISIONED".</span><span class="sxs-lookup"><span data-stu-id="2309d-147">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="2309d-148">Productname</span><span class="sxs-lookup"><span data-stu-id="2309d-148">productName</span></span> | <span data-ttu-id="2309d-149">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-149">string</span></span> | <span data-ttu-id="2309d-150">Namnet på produkten.</span><span class="sxs-lookup"><span data-stu-id="2309d-150">The name of the product.</span></span> |
| <span data-ttu-id="2309d-151">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="2309d-151">subscriptionType</span></span> | <span data-ttu-id="2309d-152">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-152">string</span></span> | <span data-ttu-id="2309d-153">Prenumerationstyp.</span><span class="sxs-lookup"><span data-stu-id="2309d-153">The subscription type.</span></span> <span data-ttu-id="2309d-154">Obs! Det här fältet är case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="2309d-154">Note: This field is case-sensitive.</span></span> <span data-ttu-id="2309d-155">Värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="2309d-155">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="2309d-156">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="2309d-156">autoRenewEnabled</span></span> | <span data-ttu-id="2309d-157">Boolesk</span><span class="sxs-lookup"><span data-stu-id="2309d-157">Boolean</span></span> | <span data-ttu-id="2309d-158">Ett värde som anger om prenumerationen förnyas automatiskt.</span><span class="sxs-lookup"><span data-stu-id="2309d-158">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="2309d-159">partnerId</span><span class="sxs-lookup"><span data-stu-id="2309d-159">partnerId</span></span>  | <span data-ttu-id="2309d-160">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-160">string</span></span> | <span data-ttu-id="2309d-161">MPN-ID: t.</span><span class="sxs-lookup"><span data-stu-id="2309d-161">The MPN ID.</span></span> <span data-ttu-id="2309d-162">För en direktåterförsäljare är den här parametern MPN-ID för partnern.</span><span class="sxs-lookup"><span data-stu-id="2309d-162">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="2309d-163">För en indirekt återförsäljare är den här parametern MPN-ID:t för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="2309d-163">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="2309d-164">friendlyName</span><span class="sxs-lookup"><span data-stu-id="2309d-164">friendlyName</span></span> | <span data-ttu-id="2309d-165">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-165">string</span></span> | <span data-ttu-id="2309d-166">Namnet på prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="2309d-166">The name of the subscription.</span></span> |
| <span data-ttu-id="2309d-167">partnerName</span><span class="sxs-lookup"><span data-stu-id="2309d-167">partnerName</span></span> | <span data-ttu-id="2309d-168">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-168">string</span></span> | <span data-ttu-id="2309d-169">Namnet på den partner som prenumerationen köptes för</span><span class="sxs-lookup"><span data-stu-id="2309d-169">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="2309d-170">providerName</span><span class="sxs-lookup"><span data-stu-id="2309d-170">providerName</span></span> | <span data-ttu-id="2309d-171">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-171">string</span></span> | <span data-ttu-id="2309d-172">När prenumerationstransaktionen är för den indirekta återförsäljaren är providernamnet den indirekta leverantör som köpte prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="2309d-172">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="2309d-173">creationDate</span><span class="sxs-lookup"><span data-stu-id="2309d-173">creationDate</span></span> | <span data-ttu-id="2309d-174">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-174">string in UTC date time format</span></span> | <span data-ttu-id="2309d-175">Det datum då prenumerationen skapades.</span><span class="sxs-lookup"><span data-stu-id="2309d-175">The date the subscription was created.</span></span> |
| <span data-ttu-id="2309d-176">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="2309d-176">effectiveStartDate</span></span> | <span data-ttu-id="2309d-177">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-177">string in UTC date time format</span></span> | <span data-ttu-id="2309d-178">Det datum då prenumerationen startar.</span><span class="sxs-lookup"><span data-stu-id="2309d-178">The date the subscription starts.</span></span> |
| <span data-ttu-id="2309d-179">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="2309d-179">commitmentEndDate</span></span> | <span data-ttu-id="2309d-180">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-180">string in UTC date time format</span></span> | <span data-ttu-id="2309d-181">Det datum då prenumerationen upphör.</span><span class="sxs-lookup"><span data-stu-id="2309d-181">The date the subscription ends.</span></span> |
| <span data-ttu-id="2309d-182">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="2309d-182">currentStateEndDate</span></span> | <span data-ttu-id="2309d-183">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-183">string in UTC date time format</span></span> | <span data-ttu-id="2309d-184">Det datum då prenumerationens aktuella status ändras.</span><span class="sxs-lookup"><span data-stu-id="2309d-184">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="2309d-185">trialToDateConversionDate</span><span class="sxs-lookup"><span data-stu-id="2309d-185">trialToPaidConversionDate</span></span> | <span data-ttu-id="2309d-186">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-186">string in UTC date time format</span></span> | <span data-ttu-id="2309d-187">Det datum då prenumerationen konverteras från utvärderingsversion till betald.</span><span class="sxs-lookup"><span data-stu-id="2309d-187">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="2309d-188">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="2309d-188">The default value is null.</span></span> |
| <span data-ttu-id="2309d-189">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="2309d-189">trialStartDate</span></span> | <span data-ttu-id="2309d-190">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-190">string in UTC date time format</span></span> | <span data-ttu-id="2309d-191">Det datum då utvärderingsperioden för prenumerationen startade.</span><span class="sxs-lookup"><span data-stu-id="2309d-191">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="2309d-192">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="2309d-192">The default value is null.</span></span> |
| <span data-ttu-id="2309d-193">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="2309d-193">lastUsageDate</span></span> | <span data-ttu-id="2309d-194">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-194">string in UTC date time format</span></span> | <span data-ttu-id="2309d-195">Det datum då prenumerationen senast användes.</span><span class="sxs-lookup"><span data-stu-id="2309d-195">The date that the subscription was last used.</span></span> <span data-ttu-id="2309d-196">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="2309d-196">The default value is null.</span></span> |
| <span data-ttu-id="2309d-197">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="2309d-197">deprovisionedDate</span></span> | <span data-ttu-id="2309d-198">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-198">string in UTC date time format</span></span> | <span data-ttu-id="2309d-199">Det datum då prenumerationen avetableades.</span><span class="sxs-lookup"><span data-stu-id="2309d-199">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="2309d-200">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="2309d-200">The default value is null.</span></span> |
| <span data-ttu-id="2309d-201">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="2309d-201">lastRenewalDate</span></span> | <span data-ttu-id="2309d-202">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="2309d-202">string in UTC date time format</span></span> | <span data-ttu-id="2309d-203">Det datum då prenumerationen senast förnyades.</span><span class="sxs-lookup"><span data-stu-id="2309d-203">The date that the subscription was last renewed.</span></span> <span data-ttu-id="2309d-204">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="2309d-204">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="2309d-205">Filterfält</span><span class="sxs-lookup"><span data-stu-id="2309d-205">Filter fields</span></span>

<span data-ttu-id="2309d-206">I följande tabell visas valfria filterfält och deras beskrivningar:</span><span class="sxs-lookup"><span data-stu-id="2309d-206">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="2309d-207">Fält</span><span class="sxs-lookup"><span data-stu-id="2309d-207">Field</span></span> | <span data-ttu-id="2309d-208">Typ</span><span class="sxs-lookup"><span data-stu-id="2309d-208">Type</span></span> |  <span data-ttu-id="2309d-209">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2309d-209">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="2309d-210">top</span><span class="sxs-lookup"><span data-stu-id="2309d-210">top</span></span> | <span data-ttu-id="2309d-211">int</span><span class="sxs-lookup"><span data-stu-id="2309d-211">int</span></span> | <span data-ttu-id="2309d-212">Antalet rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="2309d-212">The number of rows of data to return in the request.</span></span> <span data-ttu-id="2309d-213">Om värdet inte anges är det högsta värdet och standardvärdet 10000.</span><span class="sxs-lookup"><span data-stu-id="2309d-213">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="2309d-214">Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="2309d-214">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="2309d-215">hoppa över</span><span class="sxs-lookup"><span data-stu-id="2309d-215">skip</span></span> | <span data-ttu-id="2309d-216">int</span><span class="sxs-lookup"><span data-stu-id="2309d-216">int</span></span> | <span data-ttu-id="2309d-217">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="2309d-217">The number of rows to skip in the query.</span></span> <span data-ttu-id="2309d-218">Använd den här parametern för att bläddra igenom stora datamängder.</span><span class="sxs-lookup"><span data-stu-id="2309d-218">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="2309d-219">Till exempel hämtar top=10000 och skip=0 de första 10 000 raderna med data, top=10000 och skip=10000 hämtar de nästa 10 000 raderna med data.</span><span class="sxs-lookup"><span data-stu-id="2309d-219">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="2309d-220">filter</span><span class="sxs-lookup"><span data-stu-id="2309d-220">filter</span></span> | <span data-ttu-id="2309d-221">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-221">string</span></span> | <span data-ttu-id="2309d-222">En eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="2309d-222">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="2309d-223">Varje filtersats innehåller ett fältnamn från svarstexten och ett värde som är associerade med **`eq`** **`ne`** operatorn , eller för vissa **`contains`** fält.</span><span class="sxs-lookup"><span data-stu-id="2309d-223">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="2309d-224">Instruktioner kan kombineras med **`and`** hjälp av eller **`or`** .</span><span class="sxs-lookup"><span data-stu-id="2309d-224">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="2309d-225">Strängvärden måste omges av enkla citattecken i filterparametern.</span><span class="sxs-lookup"><span data-stu-id="2309d-225">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="2309d-226">I följande avsnitt finns en lista över fält som kan filtreras och de operatorer som stöds med dessa fält.</span><span class="sxs-lookup"><span data-stu-id="2309d-226">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="2309d-227">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="2309d-227">aggregationLevel</span></span> | <span data-ttu-id="2309d-228">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-228">string</span></span> | <span data-ttu-id="2309d-229">Anger det tidsperiod som aggregerade data ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="2309d-229">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="2309d-230">Kan vara någon av följande strängar: **dag,** **vecka** eller **månad.**</span><span class="sxs-lookup"><span data-stu-id="2309d-230">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="2309d-231">Om värdet inte anges är standardvärdet **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="2309d-231">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="2309d-232">**Obs!** Den här parametern gäller endast när ett datumfält skickas som en del av parametern groupBy.</span><span class="sxs-lookup"><span data-stu-id="2309d-232">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="2309d-233">groupBy</span><span class="sxs-lookup"><span data-stu-id="2309d-233">groupBy</span></span> | <span data-ttu-id="2309d-234">sträng</span><span class="sxs-lookup"><span data-stu-id="2309d-234">string</span></span> | <span data-ttu-id="2309d-235">En instruktion som endast tillämpar dataaggregering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="2309d-235">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2309d-236">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2309d-236">Request headers</span></span>

<span data-ttu-id="2309d-237">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2309d-237">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2309d-238">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2309d-238">Request body</span></span>

<span data-ttu-id="2309d-239">Inga.</span><span class="sxs-lookup"><span data-stu-id="2309d-239">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2309d-240">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2309d-240">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="2309d-241">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2309d-241">REST response</span></span>

<span data-ttu-id="2309d-242">Om det lyckas innehåller svarstexten en samling [prenumerationsresurser](partner-center-analytics-resources.md#subscription-resource) grupperade efter de angivna termerna och datumen.</span><span class="sxs-lookup"><span data-stu-id="2309d-242">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2309d-243">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2309d-243">Response success and error codes</span></span>

<span data-ttu-id="2309d-244">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="2309d-244">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2309d-245">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2309d-245">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2309d-246">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2309d-246">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2309d-247">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2309d-247">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="2309d-248">Se även</span><span class="sxs-lookup"><span data-stu-id="2309d-248">See also</span></span>

[<span data-ttu-id="2309d-249">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="2309d-249">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
