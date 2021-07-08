---
title: Hämta prenumerationsanalys via sökfråga
description: Så här hämtar du information om prenumerationsanalys filtrerad efter en sökfråga.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548744"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="6f4f3-103">Hämta information om prenumerationsanalys filtrerad efter en sökfråga</span><span class="sxs-lookup"><span data-stu-id="6f4f3-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="6f4f3-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6f4f3-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6f4f3-105">Så här hämtar du prenumerationsanalysinformation för dina kunder filtrerade efter en sökfråga.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-105">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f4f3-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6f4f3-106">Prerequisites</span></span>

- <span data-ttu-id="6f4f3-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6f4f3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6f4f3-108">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="6f4f3-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6f4f3-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6f4f3-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="6f4f3-110">Request syntax</span></span>

| <span data-ttu-id="6f4f3-111">Metod</span><span class="sxs-lookup"><span data-stu-id="6f4f3-111">Method</span></span> | <span data-ttu-id="6f4f3-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6f4f3-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="6f4f3-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="6f4f3-113">**GET**</span></span> | <span data-ttu-id="6f4f3-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span><span class="sxs-lookup"><span data-stu-id="6f4f3-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="6f4f3-115">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="6f4f3-115">URI parameters</span></span>

<span data-ttu-id="6f4f3-116">Använd följande obligatoriska sökvägsparameter för att identifiera din organisation och filtrera sökningen.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-116">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="6f4f3-117">Namn</span><span class="sxs-lookup"><span data-stu-id="6f4f3-117">Name</span></span> | <span data-ttu-id="6f4f3-118">Typ</span><span class="sxs-lookup"><span data-stu-id="6f4f3-118">Type</span></span> | <span data-ttu-id="6f4f3-119">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6f4f3-119">Required</span></span> | <span data-ttu-id="6f4f3-120">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6f4f3-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="6f4f3-121">filter_string</span><span class="sxs-lookup"><span data-stu-id="6f4f3-121">filter_string</span></span> | <span data-ttu-id="6f4f3-122">sträng</span><span class="sxs-lookup"><span data-stu-id="6f4f3-122">string</span></span> | <span data-ttu-id="6f4f3-123">Ja</span><span class="sxs-lookup"><span data-stu-id="6f4f3-123">Yes</span></span> | <span data-ttu-id="6f4f3-124">Filtret som ska tillämpas på prenumerationsanalysen.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-124">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="6f4f3-125">Se avsnitten Filtersyntax och Filterfält för syntax, fält och operatorer som ska användas i den här parametern.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-125">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="6f4f3-126">Filtersyntax</span><span class="sxs-lookup"><span data-stu-id="6f4f3-126">Filter syntax</span></span>

<span data-ttu-id="6f4f3-127">Filterparametern måste bestå av en serie kombinationer av fält, värde och operator.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-127">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="6f4f3-128">Flera kombinationer kan kombineras med operatorerna **`and`** **`or`** eller .</span><span class="sxs-lookup"><span data-stu-id="6f4f3-128">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="6f4f3-129">Ett okodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="6f4f3-129">An unencoded example looks like this:</span></span>

- <span data-ttu-id="6f4f3-130">Sträng: `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-130">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="6f4f3-131">Boolean: `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-131">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="6f4f3-132">Innehåller `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-132">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="6f4f3-133">Filterfält</span><span class="sxs-lookup"><span data-stu-id="6f4f3-133">Filter fields</span></span>

<span data-ttu-id="6f4f3-134">Filterparametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-134">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="6f4f3-135">Varje -instruktion innehåller ett fält och värde som är associerade med **`eq`** **`ne`** operatorerna eller .</span><span class="sxs-lookup"><span data-stu-id="6f4f3-135">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="6f4f3-136">Vissa fält stöder också **`contains`** operatorerna **`gt`** , , , och **`lt`** **`ge`** **`le`** .</span><span class="sxs-lookup"><span data-stu-id="6f4f3-136">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="6f4f3-137">Instruktioner kan kombineras med **`and`** operatorerna **`or`** eller .</span><span class="sxs-lookup"><span data-stu-id="6f4f3-137">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="6f4f3-138">Följande är exempel på filtersträngar:</span><span class="sxs-lookup"><span data-stu-id="6f4f3-138">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="6f4f3-139">I följande tabell visas en lista över de fält som stöds och stödoperatorer för filterparametern.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-139">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="6f4f3-140">Strängvärden måste omges av enkla citattecken.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-140">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="6f4f3-141">Parameter</span><span class="sxs-lookup"><span data-stu-id="6f4f3-141">Parameter</span></span> | <span data-ttu-id="6f4f3-142">Operatorer som stöds</span><span class="sxs-lookup"><span data-stu-id="6f4f3-142">Supported operators</span></span> | <span data-ttu-id="6f4f3-143">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6f4f3-143">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="6f4f3-144">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="6f4f3-144">autoRenewEnabled</span></span> | <span data-ttu-id="6f4f3-145">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-145">`eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-146">Ett värde som anger om prenumerationen förnyas automatiskt.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-146">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="6f4f3-147">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-147">commitmentEndDate</span></span> | <span data-ttu-id="6f4f3-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="6f4f3-149">Det datum då prenumerationen upphör.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-149">The date the subscription ends.</span></span> |
| <span data-ttu-id="6f4f3-150">creationDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-150">creationDate</span></span> | <span data-ttu-id="6f4f3-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="6f4f3-152">Det datum då prenumerationen skapades.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-152">The date the subscription was created.</span></span> |
| <span data-ttu-id="6f4f3-153">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-153">currentStateEndDate</span></span> | <span data-ttu-id="6f4f3-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="6f4f3-155">Det datum då prenumerationens aktuella status ändras.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-155">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="6f4f3-156">customerMarket</span><span class="sxs-lookup"><span data-stu-id="6f4f3-156">customerMarket</span></span> | <span data-ttu-id="6f4f3-157">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-157">`eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-158">Land/region som kunden gör affärer i.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-158">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="6f4f3-159">customerName</span><span class="sxs-lookup"><span data-stu-id="6f4f3-159">customerName</span></span> | `contains` | <span data-ttu-id="6f4f3-160">Namnet på kunden.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-160">The name of the customer.</span></span> |
| <span data-ttu-id="6f4f3-161">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="6f4f3-161">customerTenantId</span></span> | <span data-ttu-id="6f4f3-162">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-162">`eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-163">En GUID-formaterad sträng som identifierar kundens klientorganisation.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-163">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="6f4f3-164">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-164">deprovisionedDate</span></span> | <span data-ttu-id="6f4f3-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="6f4f3-166">Det datum då prenumerationen avetableades.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-166">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="6f4f3-167">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-167">The default value is null.</span></span> |
| <span data-ttu-id="6f4f3-168">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-168">effectiveStartDate</span></span> | <span data-ttu-id="6f4f3-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="6f4f3-170">Det datum då prenumerationen startar.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-170">The date the subscription starts.</span></span> |
| <span data-ttu-id="6f4f3-171">friendlyName</span><span class="sxs-lookup"><span data-stu-id="6f4f3-171">friendlyName</span></span> | `contains` | <span data-ttu-id="6f4f3-172">Namnet på prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-172">The name of the subscription.</span></span> |
| <span data-ttu-id="6f4f3-173">id</span><span class="sxs-lookup"><span data-stu-id="6f4f3-173">id</span></span> | <span data-ttu-id="6f4f3-174">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-174">`eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-175">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="6f4f3-176">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-176">lastRenewalDate</span></span> | <span data-ttu-id="6f4f3-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="6f4f3-178">Det datum då prenumerationen senast förnyades.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-178">The date that the subscription was last renewed.</span></span> <span data-ttu-id="6f4f3-179">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-179">The default value is null.</span></span> |
| <span data-ttu-id="6f4f3-180">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-180">lastUsageDate</span></span> | <span data-ttu-id="6f4f3-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="6f4f3-182">Det datum då prenumerationen senast användes.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-182">The date that the subscription was last used.</span></span> <span data-ttu-id="6f4f3-183">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-183">The default value is null.</span></span> |
| <span data-ttu-id="6f4f3-184">partnerId</span><span class="sxs-lookup"><span data-stu-id="6f4f3-184">partnerId</span></span> | <span data-ttu-id="6f4f3-185">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-185">`eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-186">MPN-ID: t.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-186">The MPN ID.</span></span> <span data-ttu-id="6f4f3-187">För en direktåterförsäljare är det här värdet PARTNERns MPN-ID.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-187">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="6f4f3-188">För en indirekt återförsäljare blir det här värdet MPN-ID:t för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-188">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="6f4f3-189">partnerName</span><span class="sxs-lookup"><span data-stu-id="6f4f3-189">partnerName</span></span> | <span data-ttu-id="6f4f3-190">sträng</span><span class="sxs-lookup"><span data-stu-id="6f4f3-190">string</span></span> | <span data-ttu-id="6f4f3-191">Namnet på den partner som prenumerationen köptes för</span><span class="sxs-lookup"><span data-stu-id="6f4f3-191">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="6f4f3-192">Productname</span><span class="sxs-lookup"><span data-stu-id="6f4f3-192">productName</span></span> | <span data-ttu-id="6f4f3-193">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-193">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-194">Namnet på produkten.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-194">The name of the product.</span></span> |
| <span data-ttu-id="6f4f3-195">providerName</span><span class="sxs-lookup"><span data-stu-id="6f4f3-195">providerName</span></span> | <span data-ttu-id="6f4f3-196">sträng</span><span class="sxs-lookup"><span data-stu-id="6f4f3-196">string</span></span> | <span data-ttu-id="6f4f3-197">När prenumerationstransaktionen är för den indirekta återförsäljaren är providernamnet den indirekta leverantör som köpte prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-197">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="6f4f3-198">status</span><span class="sxs-lookup"><span data-stu-id="6f4f3-198">status</span></span> | <span data-ttu-id="6f4f3-199">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-199">`eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-200">Prenumerationsstatus.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-200">The subscription status.</span></span> <span data-ttu-id="6f4f3-201">Värden som stöds är: "ACTIVE", "SUSPENDED" eller "DEPROVISIONED".</span><span class="sxs-lookup"><span data-stu-id="6f4f3-201">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="6f4f3-202">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="6f4f3-202">subscriptionType</span></span> | <span data-ttu-id="6f4f3-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-203">`eq`, `ne`</span></span> | <span data-ttu-id="6f4f3-204">Prenumerationstyp.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-204">The subscription type.</span></span> <span data-ttu-id="6f4f3-205">**Obs!** Det här fältet är case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-205">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="6f4f3-206">Värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="6f4f3-206">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="6f4f3-207">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-207">trialStartDate</span></span> | <span data-ttu-id="6f4f3-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="6f4f3-209">Det datum då utvärderingsperioden för prenumerationen startade.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-209">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="6f4f3-210">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-210">The default value is null.</span></span> |
| <span data-ttu-id="6f4f3-211">trialToDateConversionDate</span><span class="sxs-lookup"><span data-stu-id="6f4f3-211">trialToPaidConversionDate</span></span> | <span data-ttu-id="6f4f3-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="6f4f3-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="6f4f3-213">Det datum då prenumerationen konverteras från utvärderingsversion till betald.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-213">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="6f4f3-214">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-214">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6f4f3-215">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6f4f3-215">Request headers</span></span>

<span data-ttu-id="6f4f3-216">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6f4f3-216">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6f4f3-217">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6f4f3-217">Request body</span></span>

<span data-ttu-id="6f4f3-218">Inga.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-218">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6f4f3-219">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6f4f3-219">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="6f4f3-220">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6f4f3-220">REST response</span></span>

<span data-ttu-id="6f4f3-221">Om det lyckas innehåller svarstexten en samling [prenumerationsresurser](partner-center-analytics-resources.md#subscription-resource) som uppfyller filtervillkoren.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-221">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6f4f3-222">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6f4f3-222">Response success and error codes</span></span>

<span data-ttu-id="6f4f3-223">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-223">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6f4f3-224">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6f4f3-224">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6f4f3-225">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6f4f3-225">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6f4f3-226">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6f4f3-226">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a><span data-ttu-id="6f4f3-227">Se även</span><span class="sxs-lookup"><span data-stu-id="6f4f3-227">See also</span></span>

- [<span data-ttu-id="6f4f3-228">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="6f4f3-228">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
