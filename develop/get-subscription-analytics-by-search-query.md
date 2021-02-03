---
title: Hämta prenumerations analys per Sök fråga
description: Hämta information om prenumerations analys som filtrerats av en Sök fråga.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769054"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="567bb-103">Hämta information om prenumerationsanalys filtrerad efter en sökfråga</span><span class="sxs-lookup"><span data-stu-id="567bb-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="567bb-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="567bb-104">**Applies To**</span></span>

- <span data-ttu-id="567bb-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="567bb-105">Partner Center</span></span>
- <span data-ttu-id="567bb-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="567bb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="567bb-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="567bb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="567bb-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="567bb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="567bb-109">Hämta information om prenumerations analys för dina kunder filtrerat efter en Sök fråga.</span><span class="sxs-lookup"><span data-stu-id="567bb-109">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="567bb-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="567bb-110">Prerequisites</span></span>

- <span data-ttu-id="567bb-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="567bb-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="567bb-112">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="567bb-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="567bb-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="567bb-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="567bb-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="567bb-114">Request syntax</span></span>

| <span data-ttu-id="567bb-115">Metod</span><span class="sxs-lookup"><span data-stu-id="567bb-115">Method</span></span> | <span data-ttu-id="567bb-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="567bb-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="567bb-117">**TA**</span><span class="sxs-lookup"><span data-stu-id="567bb-117">**GET**</span></span> | <span data-ttu-id="567bb-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? filter = {filter_string}</span><span class="sxs-lookup"><span data-stu-id="567bb-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="567bb-119">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="567bb-119">URI parameters</span></span>

<span data-ttu-id="567bb-120">Använd följande obligatoriska Sök vägs parameter för att identifiera din organisation och filtrera sökningen.</span><span class="sxs-lookup"><span data-stu-id="567bb-120">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="567bb-121">Namn</span><span class="sxs-lookup"><span data-stu-id="567bb-121">Name</span></span> | <span data-ttu-id="567bb-122">Typ</span><span class="sxs-lookup"><span data-stu-id="567bb-122">Type</span></span> | <span data-ttu-id="567bb-123">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="567bb-123">Required</span></span> | <span data-ttu-id="567bb-124">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="567bb-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="567bb-125">filter_string</span><span class="sxs-lookup"><span data-stu-id="567bb-125">filter_string</span></span> | <span data-ttu-id="567bb-126">sträng</span><span class="sxs-lookup"><span data-stu-id="567bb-126">string</span></span> | <span data-ttu-id="567bb-127">Yes</span><span class="sxs-lookup"><span data-stu-id="567bb-127">Yes</span></span> | <span data-ttu-id="567bb-128">Filtret som ska användas för prenumerations analysen.</span><span class="sxs-lookup"><span data-stu-id="567bb-128">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="567bb-129">Se avsnitten filtrera syntax och filter fält för syntax, fält och operatorer som ska användas i den här parametern.</span><span class="sxs-lookup"><span data-stu-id="567bb-129">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="567bb-130">Filter-syntax</span><span class="sxs-lookup"><span data-stu-id="567bb-130">Filter syntax</span></span>

<span data-ttu-id="567bb-131">Filter parametern måste bestå av en serie av kombinationer av fält, värde och operatorer.</span><span class="sxs-lookup"><span data-stu-id="567bb-131">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="567bb-132">Flera kombinationer kan kombineras med hjälp av **`and`** eller- **`or`** operatorer.</span><span class="sxs-lookup"><span data-stu-id="567bb-132">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="567bb-133">Ett avkodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="567bb-133">An unencoded example looks like this:</span></span>

- <span data-ttu-id="567bb-134">Nollängd `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="567bb-134">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="567bb-135">Booleskt `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="567bb-135">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="567bb-136">Ingår `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="567bb-136">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="567bb-137">Filter fält</span><span class="sxs-lookup"><span data-stu-id="567bb-137">Filter fields</span></span>

<span data-ttu-id="567bb-138">Filter parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="567bb-138">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="567bb-139">Varje instruktion innehåller ett fält och ett värde som är associerat **`eq`** med **`ne`** operatorerna eller.</span><span class="sxs-lookup"><span data-stu-id="567bb-139">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="567bb-140">Vissa fält har även stöd **`contains`** för **`gt`** operatorerna,,, **`lt`** **`ge`** och **`le`** .</span><span class="sxs-lookup"><span data-stu-id="567bb-140">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="567bb-141">Instruktioner kan kombineras med hjälp av **`and`** eller- **`or`** operatorer.</span><span class="sxs-lookup"><span data-stu-id="567bb-141">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="567bb-142">Följande är exempel på filter strängar:</span><span class="sxs-lookup"><span data-stu-id="567bb-142">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="567bb-143">I följande tabell visas en lista över de fält och support operatörer som stöds för filter parametern.</span><span class="sxs-lookup"><span data-stu-id="567bb-143">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="567bb-144">Sträng värden måste omges av enkla citat tecken.</span><span class="sxs-lookup"><span data-stu-id="567bb-144">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="567bb-145">Parameter</span><span class="sxs-lookup"><span data-stu-id="567bb-145">Parameter</span></span> | <span data-ttu-id="567bb-146">Operatorer som stöds</span><span class="sxs-lookup"><span data-stu-id="567bb-146">Supported operators</span></span> | <span data-ttu-id="567bb-147">Description</span><span class="sxs-lookup"><span data-stu-id="567bb-147">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="567bb-148">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="567bb-148">autoRenewEnabled</span></span> | <span data-ttu-id="567bb-149">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-149">`eq`, `ne`</span></span> | <span data-ttu-id="567bb-150">Ett värde som anger om prenumerationen förnyas automatiskt.</span><span class="sxs-lookup"><span data-stu-id="567bb-150">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="567bb-151">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="567bb-151">commitmentEndDate</span></span> | <span data-ttu-id="567bb-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="567bb-153">Det datum då prenumerationen slutar.</span><span class="sxs-lookup"><span data-stu-id="567bb-153">The date the subscription ends.</span></span> |
| <span data-ttu-id="567bb-154">creationDate</span><span class="sxs-lookup"><span data-stu-id="567bb-154">creationDate</span></span> | <span data-ttu-id="567bb-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="567bb-156">Det datum då prenumerationen skapades.</span><span class="sxs-lookup"><span data-stu-id="567bb-156">The date the subscription was created.</span></span> |
| <span data-ttu-id="567bb-157">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="567bb-157">currentStateEndDate</span></span> | <span data-ttu-id="567bb-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="567bb-159">Det datum då prenumerationens aktuella status kommer att ändras.</span><span class="sxs-lookup"><span data-stu-id="567bb-159">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="567bb-160">customerMarket</span><span class="sxs-lookup"><span data-stu-id="567bb-160">customerMarket</span></span> | <span data-ttu-id="567bb-161">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-161">`eq`, `ne`</span></span> | <span data-ttu-id="567bb-162">Landet/regionen som kunden gör affärer med.</span><span class="sxs-lookup"><span data-stu-id="567bb-162">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="567bb-163">customerName</span><span class="sxs-lookup"><span data-stu-id="567bb-163">customerName</span></span> | `contains` | <span data-ttu-id="567bb-164">Namnet på kunden.</span><span class="sxs-lookup"><span data-stu-id="567bb-164">The name of the customer.</span></span> |
| <span data-ttu-id="567bb-165">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="567bb-165">customerTenantId</span></span> | <span data-ttu-id="567bb-166">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-166">`eq`, `ne`</span></span> | <span data-ttu-id="567bb-167">En GUID-formaterad sträng som identifierar kundens klient organisation.</span><span class="sxs-lookup"><span data-stu-id="567bb-167">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="567bb-168">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="567bb-168">deprovisionedDate</span></span> | <span data-ttu-id="567bb-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="567bb-170">Det datum då prenumerationen avetablerades.</span><span class="sxs-lookup"><span data-stu-id="567bb-170">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="567bb-171">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="567bb-171">The default value is null.</span></span> |
| <span data-ttu-id="567bb-172">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="567bb-172">effectiveStartDate</span></span> | <span data-ttu-id="567bb-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="567bb-174">Det datum då prenumerationen startar.</span><span class="sxs-lookup"><span data-stu-id="567bb-174">The date the subscription starts.</span></span> |
| <span data-ttu-id="567bb-175">friendlyName</span><span class="sxs-lookup"><span data-stu-id="567bb-175">friendlyName</span></span> | `contains` | <span data-ttu-id="567bb-176">Namnet på prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="567bb-176">The name of the subscription.</span></span> |
| <span data-ttu-id="567bb-177">id</span><span class="sxs-lookup"><span data-stu-id="567bb-177">id</span></span> | <span data-ttu-id="567bb-178">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-178">`eq`, `ne`</span></span> | <span data-ttu-id="567bb-179">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="567bb-179">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="567bb-180">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="567bb-180">lastRenewalDate</span></span> | <span data-ttu-id="567bb-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="567bb-182">Det datum då prenumerationen senast förnyades.</span><span class="sxs-lookup"><span data-stu-id="567bb-182">The date that the subscription was last renewed.</span></span> <span data-ttu-id="567bb-183">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="567bb-183">The default value is null.</span></span> |
| <span data-ttu-id="567bb-184">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="567bb-184">lastUsageDate</span></span> | <span data-ttu-id="567bb-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="567bb-186">Det datum då prenumerationen senast användes.</span><span class="sxs-lookup"><span data-stu-id="567bb-186">The date that the subscription was last used.</span></span> <span data-ttu-id="567bb-187">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="567bb-187">The default value is null.</span></span> |
| <span data-ttu-id="567bb-188">Partner</span><span class="sxs-lookup"><span data-stu-id="567bb-188">partnerId</span></span> | <span data-ttu-id="567bb-189">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-189">`eq`, `ne`</span></span> | <span data-ttu-id="567bb-190">MPN-ID.</span><span class="sxs-lookup"><span data-stu-id="567bb-190">The MPN ID.</span></span> <span data-ttu-id="567bb-191">För en direkt åter försäljare är det här värdet MPN-ID för partnern.</span><span class="sxs-lookup"><span data-stu-id="567bb-191">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="567bb-192">För en indirekt åter försäljare är det här värdet MPN-ID: t för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="567bb-192">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="567bb-193">partnerName</span><span class="sxs-lookup"><span data-stu-id="567bb-193">partnerName</span></span> | <span data-ttu-id="567bb-194">sträng</span><span class="sxs-lookup"><span data-stu-id="567bb-194">string</span></span> | <span data-ttu-id="567bb-195">Namnet på partnern som prenumerationen köptes för</span><span class="sxs-lookup"><span data-stu-id="567bb-195">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="567bb-196">Namn</span><span class="sxs-lookup"><span data-stu-id="567bb-196">productName</span></span> | <span data-ttu-id="567bb-197">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-197">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="567bb-198">Produktens namn.</span><span class="sxs-lookup"><span data-stu-id="567bb-198">The name of the product.</span></span> |
| <span data-ttu-id="567bb-199">providerName</span><span class="sxs-lookup"><span data-stu-id="567bb-199">providerName</span></span> | <span data-ttu-id="567bb-200">sträng</span><span class="sxs-lookup"><span data-stu-id="567bb-200">string</span></span> | <span data-ttu-id="567bb-201">När prenumerations transaktionen är för den indirekta åter försäljaren är Providerns namn den indirekta providern som köpte prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="567bb-201">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="567bb-202">status</span><span class="sxs-lookup"><span data-stu-id="567bb-202">status</span></span> | <span data-ttu-id="567bb-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-203">`eq`, `ne`</span></span> | <span data-ttu-id="567bb-204">Prenumerationens status.</span><span class="sxs-lookup"><span data-stu-id="567bb-204">The subscription status.</span></span> <span data-ttu-id="567bb-205">De värden som stöds är: "aktiv", "inaktive rad" eller "deetablerat".</span><span class="sxs-lookup"><span data-stu-id="567bb-205">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="567bb-206">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="567bb-206">subscriptionType</span></span> | <span data-ttu-id="567bb-207">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="567bb-207">`eq`, `ne`</span></span> | <span data-ttu-id="567bb-208">Prenumerations typ.</span><span class="sxs-lookup"><span data-stu-id="567bb-208">The subscription type.</span></span> <span data-ttu-id="567bb-209">**Obs!** det här fältet är Skift läges känsligt.</span><span class="sxs-lookup"><span data-stu-id="567bb-209">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="567bb-210">De värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="567bb-210">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="567bb-211">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="567bb-211">trialStartDate</span></span> | <span data-ttu-id="567bb-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="567bb-213">Det datum då utvärderings perioden för prenumerationen startades.</span><span class="sxs-lookup"><span data-stu-id="567bb-213">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="567bb-214">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="567bb-214">The default value is null.</span></span> |
| <span data-ttu-id="567bb-215">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="567bb-215">trialToPaidConversionDate</span></span> | <span data-ttu-id="567bb-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="567bb-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="567bb-217">Det datum då prenumerationen konverteras från utvärderings versionen till betald.</span><span class="sxs-lookup"><span data-stu-id="567bb-217">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="567bb-218">Standardvärdet är null.</span><span class="sxs-lookup"><span data-stu-id="567bb-218">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="567bb-219">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="567bb-219">Request headers</span></span>

<span data-ttu-id="567bb-220">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="567bb-220">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="567bb-221">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="567bb-221">Request body</span></span>

<span data-ttu-id="567bb-222">Inga.</span><span class="sxs-lookup"><span data-stu-id="567bb-222">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="567bb-223">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="567bb-223">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="567bb-224">REST-svar</span><span class="sxs-lookup"><span data-stu-id="567bb-224">REST response</span></span>

<span data-ttu-id="567bb-225">Om det lyckas innehåller svars texten en samling [prenumerations](partner-center-analytics-resources.md#subscription-resource) resurser som uppfyller filter kriterierna.</span><span class="sxs-lookup"><span data-stu-id="567bb-225">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="567bb-226">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="567bb-226">Response success and error codes</span></span>

<span data-ttu-id="567bb-227">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="567bb-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="567bb-228">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="567bb-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="567bb-229">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="567bb-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="567bb-230">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="567bb-230">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="567bb-231">Se även</span><span class="sxs-lookup"><span data-stu-id="567bb-231">See also</span></span>

- [<span data-ttu-id="567bb-232">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="567bb-232">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
