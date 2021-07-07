---
title: Skapa indirekt återförsäljare i sandbox-miljö
description: Innehåller information för indirekta sandbox-leverantörer om hur du aktiverar testning från slutet till slut med hjälp av API:er.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973442"
---
# <a name="create-indirect-reseller-in-sandbox"></a><span data-ttu-id="bd6eb-103">Skapa indirekt återförsäljare i sandbox-miljö</span><span class="sxs-lookup"><span data-stu-id="bd6eb-103">Create Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="bd6eb-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="bd6eb-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="bd6eb-105">Det här dokumentet visar hur du skapar indirekta sandbox-providers och aktiverar testning från slutet till slut med hjälp av API:er.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-105">This document shows how to create Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd6eb-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="bd6eb-106">Prerequisites</span></span>

- <span data-ttu-id="bd6eb-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bd6eb-107">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bd6eb-108">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="csp-indirect-provider"></a><span data-ttu-id="bd6eb-109">CSP Indirect Provider</span><span class="sxs-lookup"><span data-stu-id="bd6eb-109">CSP Indirect Provider</span></span>

| <span data-ttu-id="bd6eb-110">Produktionsfunktioner</span><span class="sxs-lookup"><span data-stu-id="bd6eb-110">Production capabilities</span></span>             | <span data-ttu-id="bd6eb-111">Sandbox-funktioner</span><span class="sxs-lookup"><span data-stu-id="bd6eb-111">Sandbox capabilities</span></span>                            |
|-------------------------------------|-------------------------------------------------|
| <span data-ttu-id="bd6eb-112">Säljer via den indirekta återförsäljaren till slutanvändaren</span><span class="sxs-lookup"><span data-stu-id="bd6eb-112">Sells through the indirect reseller to the end customer</span></span> | <span data-ttu-id="bd6eb-113">Stöds</span><span class="sxs-lookup"><span data-stu-id="bd6eb-113">Supported</span></span> |
| <span data-ttu-id="bd6eb-114">Äger all försäljning, fakturering, etablering och hantering/support</span><span class="sxs-lookup"><span data-stu-id="bd6eb-114">Owns all sales, billing, provisioning, and management/support</span></span> | <span data-ttu-id="bd6eb-115">Stöds</span><span class="sxs-lookup"><span data-stu-id="bd6eb-115">Supported</span></span> |
| <span data-ttu-id="bd6eb-116">Begära ett samarbete med återförsäljarna</span><span class="sxs-lookup"><span data-stu-id="bd6eb-116">Request a partnership with the resellers</span></span> | <span data-ttu-id="bd6eb-117">Stöds</span><span class="sxs-lookup"><span data-stu-id="bd6eb-117">Supported</span></span> |
| <span data-ttu-id="bd6eb-118">Visa kunder efter återförsäljare</span><span class="sxs-lookup"><span data-stu-id="bd6eb-118">View customers by Reseller</span></span> | <span data-ttu-id="bd6eb-119">Stöds</span><span class="sxs-lookup"><span data-stu-id="bd6eb-119">Supported</span></span> |
| <span data-ttu-id="bd6eb-120">Lägga till nya kunder efter återförsäljare</span><span class="sxs-lookup"><span data-stu-id="bd6eb-120">Add new customers by resellers</span></span> | <span data-ttu-id="bd6eb-121">Stöds</span><span class="sxs-lookup"><span data-stu-id="bd6eb-121">Supported</span></span> |
| <span data-ttu-id="bd6eb-122">Bjud in kunder</span><span class="sxs-lookup"><span data-stu-id="bd6eb-122">Invite customers</span></span> | <span data-ttu-id="bd6eb-123">Begäran om kundrelationer stöds inte i sandbox-miljön</span><span class="sxs-lookup"><span data-stu-id="bd6eb-123">Customer relationship request not supported in Sandbox</span></span> |
| <span data-ttu-id="bd6eb-124">Indirekt sandbox-provider kan välja Sandbox IR (MPN ID) som LEVERANTÖR när transaktionen placeras</span><span class="sxs-lookup"><span data-stu-id="bd6eb-124">Sandbox Indirect Provider can select Sandbox IR (MPN ID) as the POR while placing the transaction</span></span> | <span data-ttu-id="bd6eb-125">Stöds</span><span class="sxs-lookup"><span data-stu-id="bd6eb-125">Supported</span></span> |
| <span data-ttu-id="bd6eb-126">Stöds inte i produktion</span><span class="sxs-lookup"><span data-stu-id="bd6eb-126">Not supported in production</span></span> | <span data-ttu-id="bd6eb-127">Sandbox Indirect Provider kan skapa indirekt Sandbox-återförsäljare</span><span class="sxs-lookup"><span data-stu-id="bd6eb-127">Sandbox Indirect Provider can create Sandbox Indirect Reseller</span></span> |
| <span data-ttu-id="bd6eb-128">MPN-ID för sandbox-miljö ska anges. Produktens MPN-ID fungerar inte</span><span class="sxs-lookup"><span data-stu-id="bd6eb-128">Sandbox MPN ID should be entered, the product MPN ID will not work</span></span> | <span data-ttu-id="bd6eb-129">Stöds inte i produktion</span><span class="sxs-lookup"><span data-stu-id="bd6eb-129">Not supported in production</span></span> |
| <span data-ttu-id="bd6eb-130">Stöds inte i produktion</span><span class="sxs-lookup"><span data-stu-id="bd6eb-130">Not supported in production</span></span> | <span data-ttu-id="bd6eb-131">Sandbox Indirect Provider kan ta bort Sandbox Indirect Reseller</span><span class="sxs-lookup"><span data-stu-id="bd6eb-131">Sandbox Indirect Provider can delete Sandbox Indirect Reseller</span></span> |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a><span data-ttu-id="bd6eb-132">Sandbox Indirect Provider – Skapa indirekt Sandbox-återförsäljare</span><span class="sxs-lookup"><span data-stu-id="bd6eb-132">Sandbox Indirect Provider – Create Sandbox Indirect Reseller</span></span>

<span data-ttu-id="bd6eb-133">Den här funktionen är bara tillgänglig i sandbox-miljön och ger indirekta sandbox-leverantörer möjlighet att skapa indirekta sandbox-återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-133">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="bd6eb-134">Gräns på fem indirekta sandbox-återförsäljare som tillåts per indirekt sandbox-provider</span><span class="sxs-lookup"><span data-stu-id="bd6eb-134">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider</span></span>
2. <span data-ttu-id="bd6eb-135">Indirekta sandbox-leverantörer kan skapa kunder med `associatedPartnerId` sandbox-återförsäljare</span><span class="sxs-lookup"><span data-stu-id="bd6eb-135">Sandbox Indirect Providers can create customers with `associatedPartnerId` of Sandbox Indirect Reseller</span></span>
3. <span data-ttu-id="bd6eb-136">Ange [MPN-ID för](/partner-center/mpn-create-a-partner-center-account) en viss region när du skapar en indirekt Sandbox-återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-136">Enter the [MPN](/partner-center/mpn-create-a-partner-center-account) ID of a specific region while creating a Sandbox Indirect Reseller.</span></span> <span data-ttu-id="bd6eb-137">Flera indirekta sandbox-återförsäljare kan skapas med samma MPN-ID för sandbox-miljö.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-137">Multiple Sandbox Indirect Resellers can be created with the same Sandbox MPN ID.</span></span>
4. <span data-ttu-id="bd6eb-138">Endast 75 kunder tillåts per indirekt sandbox-provider</span><span class="sxs-lookup"><span data-stu-id="bd6eb-138">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="sandbox-indirect-resellers--view-customers"></a><span data-ttu-id="bd6eb-139">Sandbox Indirect Resellers – Visa kunder</span><span class="sxs-lookup"><span data-stu-id="bd6eb-139">Sandbox Indirect Resellers – View customers</span></span>

1. <span data-ttu-id="bd6eb-140">Sandbox Indirect Resellers kan visa listan över sandbox-kunder av sandbox-leverantörer.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-140">Sandbox Indirect Resellers can view the list of sandbox customers by Sandbox Indirect providers.</span></span>
2. <span data-ttu-id="bd6eb-141">Indirekta sandbox-återförsäljare kan hantera kundkontot med hjälp av delegerade administratörsbehörigheter.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-141">Sandbox Indirect Resellers can manage the customer account by using delegated administrator permissions.</span></span>

## <a name="create-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="bd6eb-142">Skapa indirekt sandbox-återförsäljare via API</span><span class="sxs-lookup"><span data-stu-id="bd6eb-142">Create Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="bd6eb-143">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="bd6eb-143">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="bd6eb-144">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="bd6eb-144">Request syntax</span></span>

| <span data-ttu-id="bd6eb-145">**Metod**</span><span class="sxs-lookup"><span data-stu-id="bd6eb-145">**Method**</span></span> | <span data-ttu-id="bd6eb-146">**URI för förfrågan**</span><span class="sxs-lookup"><span data-stu-id="bd6eb-146">**Request URI**</span></span>                                                        |
|------------|------------------------------------------------------------------------|
| <span data-ttu-id="bd6eb-147">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="bd6eb-147">**POST**</span></span>   | <span data-ttu-id="bd6eb-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span><span class="sxs-lookup"><span data-stu-id="bd6eb-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="bd6eb-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="bd6eb-149">Request headers</span></span>

- <span data-ttu-id="bd6eb-150">Det här API:et är idempotent (det ger inte ett annat resultat om du anropar det flera gånger).</span><span class="sxs-lookup"><span data-stu-id="bd6eb-150">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>
- <span data-ttu-id="bd6eb-151">Ett begärande-ID och korrelations-ID krävs.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-151">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="bd6eb-152">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bd6eb-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="bd6eb-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="bd6eb-153">Request body</span></span>

<span data-ttu-id="bd6eb-154">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-154">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="bd6eb-155">Egenskap</span><span class="sxs-lookup"><span data-stu-id="bd6eb-155">Property</span></span>             | <span data-ttu-id="bd6eb-156">Typ</span><span class="sxs-lookup"><span data-stu-id="bd6eb-156">Type</span></span>           | <span data-ttu-id="bd6eb-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="bd6eb-157">Description</span></span>                                      |
|----------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="bd6eb-158">mpnId</span><span class="sxs-lookup"><span data-stu-id="bd6eb-158">mpnId</span></span>                | <span data-ttu-id="bd6eb-159">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-159">string</span></span>         | <span data-ttu-id="bd6eb-160">MPN-ID för IR i en viss region</span><span class="sxs-lookup"><span data-stu-id="bd6eb-160">The MPN ID for the IR in specific region</span></span>         |
| <span data-ttu-id="bd6eb-161">tenant</span><span class="sxs-lookup"><span data-stu-id="bd6eb-161">tenant</span></span>               | <span data-ttu-id="bd6eb-162">&lt;Ordlistesträng, sträng&gt;</span><span class="sxs-lookup"><span data-stu-id="bd6eb-162">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="bd6eb-163">Samling grundläggande information som definierar ett konto som ska skapas</span><span class="sxs-lookup"><span data-stu-id="bd6eb-163">Collection of basic information that defines an account to be created</span></span> |
| <span data-ttu-id="bd6eb-164">legalBusinessProfile</span><span class="sxs-lookup"><span data-stu-id="bd6eb-164">legalBusinessProfile</span></span> | <span data-ttu-id="bd6eb-165">&lt;Ordlistesträng, sträng&gt;</span><span class="sxs-lookup"><span data-stu-id="bd6eb-165">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="bd6eb-166">Insamling av information som representerar den juridiska enheten, till exempel kontakt, adress och namn</span><span class="sxs-lookup"><span data-stu-id="bd6eb-166">Collection of information that represents the legal business entity such as contact, address, and name</span></span> |
| <span data-ttu-id="bd6eb-167">organizationProfileLanguage</span><span class="sxs-lookup"><span data-stu-id="bd6eb-167">organizationProfileLanguage</span></span> | <span data-ttu-id="bd6eb-168">&lt;Ordlistesträng, sträng&gt;</span><span class="sxs-lookup"><span data-stu-id="bd6eb-168">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="bd6eb-169">Organisationsspråksidentifieraren</span><span class="sxs-lookup"><span data-stu-id="bd6eb-169">The organization language identifier</span></span> |

<span data-ttu-id="bd6eb-170">I den här tabellen beskrivs de nödvändiga egenskaperna i **klientattributet.**</span><span class="sxs-lookup"><span data-stu-id="bd6eb-170">This table describes the required properties in the **tenant** attribute.</span></span>

| <span data-ttu-id="bd6eb-171">Egenskap</span><span class="sxs-lookup"><span data-stu-id="bd6eb-171">Property</span></span>           | <span data-ttu-id="bd6eb-172">Typ</span><span class="sxs-lookup"><span data-stu-id="bd6eb-172">Type</span></span>           | <span data-ttu-id="bd6eb-173">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="bd6eb-173">Description</span></span>                         |
|--------------------|----------------|-------------------------------------|
| <span data-ttu-id="bd6eb-174">domainPrefix</span><span class="sxs-lookup"><span data-stu-id="bd6eb-174">domainPrefix</span></span>       | <span data-ttu-id="bd6eb-175">Sträng; Unik</span><span class="sxs-lookup"><span data-stu-id="bd6eb-175">String; unique</span></span> | <span data-ttu-id="bd6eb-176">Domän för klientkontot</span><span class="sxs-lookup"><span data-stu-id="bd6eb-176">Domain for the tenant account</span></span>       |
| <span data-ttu-id="bd6eb-177">name</span><span class="sxs-lookup"><span data-stu-id="bd6eb-177">name</span></span>               | <span data-ttu-id="bd6eb-178">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-178">string</span></span>         | <span data-ttu-id="bd6eb-179">Eget namn på klientorganisationen</span><span class="sxs-lookup"><span data-stu-id="bd6eb-179">Friendly name of the tenant</span></span>         |
| <span data-ttu-id="bd6eb-180">displayName</span><span class="sxs-lookup"><span data-stu-id="bd6eb-180">displayName</span></span>        | <span data-ttu-id="bd6eb-181">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-181">string</span></span>         | <span data-ttu-id="bd6eb-182">Visningsnamn för kontot</span><span class="sxs-lookup"><span data-stu-id="bd6eb-182">Display name for the account</span></span>        |
| <span data-ttu-id="bd6eb-183">adminUserName</span><span class="sxs-lookup"><span data-stu-id="bd6eb-183">adminUserName</span></span>      | <span data-ttu-id="bd6eb-184">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-184">string</span></span>         | <span data-ttu-id="bd6eb-185">Användarnamn för kontot för inloggning</span><span class="sxs-lookup"><span data-stu-id="bd6eb-185">User name for the account for login</span></span> |
| <span data-ttu-id="bd6eb-186">adminfirstname</span><span class="sxs-lookup"><span data-stu-id="bd6eb-186">adminfirstname</span></span>     | <span data-ttu-id="bd6eb-187">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-187">string</span></span>         | <span data-ttu-id="bd6eb-188">Förnamn för administratörsanvändaren</span><span class="sxs-lookup"><span data-stu-id="bd6eb-188">First Name for the admin user</span></span>       |
| <span data-ttu-id="bd6eb-189">adminlastname</span><span class="sxs-lookup"><span data-stu-id="bd6eb-189">adminlastname</span></span>      | <span data-ttu-id="bd6eb-190">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-190">string</span></span>         | <span data-ttu-id="bd6eb-191">Efternamn för administratörsanvändaren</span><span class="sxs-lookup"><span data-stu-id="bd6eb-191">Last Name for the admin user</span></span>        |
| <span data-ttu-id="bd6eb-192">adminAlernateEmail</span><span class="sxs-lookup"><span data-stu-id="bd6eb-192">adminAlernateEmail</span></span> | <span data-ttu-id="bd6eb-193">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-193">string</span></span>         | <span data-ttu-id="bd6eb-194">e-post för administratörsanvändaren</span><span class="sxs-lookup"><span data-stu-id="bd6eb-194">email for the admin user</span></span>            |
| <span data-ttu-id="bd6eb-195">land</span><span class="sxs-lookup"><span data-stu-id="bd6eb-195">country</span></span>            | <span data-ttu-id="bd6eb-196">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-196">string</span></span>         | <span data-ttu-id="bd6eb-197">Land för kontot</span><span class="sxs-lookup"><span data-stu-id="bd6eb-197">Country of the account</span></span>              |
| <span data-ttu-id="bd6eb-198">Kultur</span><span class="sxs-lookup"><span data-stu-id="bd6eb-198">culture</span></span>            | <span data-ttu-id="bd6eb-199">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-199">string</span></span>         | <span data-ttu-id="bd6eb-200">Språkpreferens för konto</span><span class="sxs-lookup"><span data-stu-id="bd6eb-200">Language preference for account</span></span>     |

<span data-ttu-id="bd6eb-201">I den här tabellen beskrivs de obligatoriska egenskaperna i **attributet legalBusinessProfile.**</span><span class="sxs-lookup"><span data-stu-id="bd6eb-201">This table describes the required properties in the **legalBusinessProfile** attribute.</span></span>

| <span data-ttu-id="bd6eb-202">Egenskap</span><span class="sxs-lookup"><span data-stu-id="bd6eb-202">Property</span></span>       | <span data-ttu-id="bd6eb-203">Typ</span><span class="sxs-lookup"><span data-stu-id="bd6eb-203">Type</span></span>                             | <span data-ttu-id="bd6eb-204">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="bd6eb-204">Description</span></span>                          |
|----------------|----------------------------------|--------------------------------------|
| <span data-ttu-id="bd6eb-205">companyName</span><span class="sxs-lookup"><span data-stu-id="bd6eb-205">companyName</span></span>    | <span data-ttu-id="bd6eb-206">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-206">string</span></span>                           | <span data-ttu-id="bd6eb-207">Företagsnamn för juridisk person</span><span class="sxs-lookup"><span data-stu-id="bd6eb-207">Company name for legal entity</span></span>        |
| <span data-ttu-id="bd6eb-208">adress</span><span class="sxs-lookup"><span data-stu-id="bd6eb-208">address</span></span>        | <span data-ttu-id="bd6eb-209">&lt;Ordlistesträng, sträng&gt;</span><span class="sxs-lookup"><span data-stu-id="bd6eb-209">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="bd6eb-210">Adress för den juridiska personens plats</span><span class="sxs-lookup"><span data-stu-id="bd6eb-210">Address of the legal entity location</span></span> |
| <span data-ttu-id="bd6eb-211">primaryContact</span><span class="sxs-lookup"><span data-stu-id="bd6eb-211">primaryContact</span></span> | <span data-ttu-id="bd6eb-212">&lt;Ordlistesträng, sträng&gt;</span><span class="sxs-lookup"><span data-stu-id="bd6eb-212">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="bd6eb-213">Kontaktuppgifter för företaget</span><span class="sxs-lookup"><span data-stu-id="bd6eb-213">Contact details of the company</span></span>       |
| <span data-ttu-id="bd6eb-214">Kultur</span><span class="sxs-lookup"><span data-stu-id="bd6eb-214">culture</span></span>        | <span data-ttu-id="bd6eb-215">sträng</span><span class="sxs-lookup"><span data-stu-id="bd6eb-215">string</span></span>                           | <span data-ttu-id="bd6eb-216">Språk som företaget föredrar</span><span class="sxs-lookup"><span data-stu-id="bd6eb-216">Language preferred by the company</span></span>    |

### <a name="request-example"></a><span data-ttu-id="bd6eb-217">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="bd6eb-217">Request Example</span></span>

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a><span data-ttu-id="bd6eb-218">REST-svar</span><span class="sxs-lookup"><span data-stu-id="bd6eb-218">REST response</span></span>

<span data-ttu-id="bd6eb-219">Om det lyckas returnerar den här metoden den ifyllda Sandbox IR-resursen i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="bd6eb-219">If successful, this method returns the populated Sandbox IR resource in the response body.</span></span>

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
