---
title: Aktivera säker programmodell
description: Skydda dina Partnercenter- och kontrollpanelens appar.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 19a1c39576a4f897df2d1205e3501839f6580831
ms.sourcegitcommit: e0077b2724d128ab20cb05696e5e5b1cde8e5214
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/07/2021
ms.locfileid: "113481675"
---
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="edb53-103">Aktivera Secure Application Model-ramverket</span><span class="sxs-lookup"><span data-stu-id="edb53-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="edb53-104">Microsoft introducerar ett säkert, skalbart ramverk för autentisering av molnlösningsleverantörer (CSP) och leverantörer av kontrollpaneler (CPV) via arkitekturen för Microsoft Azure Active Directory Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="edb53-104">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure Active Directory Multi-Factor Authentication (MFA) architecture.</span></span>

<span data-ttu-id="edb53-105">Du kan använda den nya modellen för att höja säkerheten för Partner Center API-integreringssamtal.</span><span class="sxs-lookup"><span data-stu-id="edb53-105">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="edb53-106">Detta hjälper alla parter (inklusive Microsoft, CSP-partner och CPV:er) att skydda sin infrastruktur och sina kunddata mot säkerhetsrisker.</span><span class="sxs-lookup"><span data-stu-id="edb53-106">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="edb53-107">Omfång</span><span class="sxs-lookup"><span data-stu-id="edb53-107">Scope</span></span>

<span data-ttu-id="edb53-108">Den här artikeln handlar om följande aktörer:</span><span class="sxs-lookup"><span data-stu-id="edb53-108">This article concerns the following actors:</span></span>

- <span data-ttu-id="edb53-109">CPV</span><span class="sxs-lookup"><span data-stu-id="edb53-109">CPVs</span></span>
  - <span data-ttu-id="edb53-110">En CPV är en oberoende programvaruleverantör som utvecklar appar som CSP-partner använder för att integrera med Partnercenter-API:er.</span><span class="sxs-lookup"><span data-stu-id="edb53-110">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="edb53-111">En CPV är inte en CSP-partner med direkt åtkomst till Partnercenter-instrumentpanelen eller -API:er.</span><span class="sxs-lookup"><span data-stu-id="edb53-111">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="edb53-112">Indirekta CSP-leverantörer och CSP-direktpartner som använder app-ID + användarautentisering och integrerar direkt med Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="edb53-112">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="edb53-113">Säkerhetskrav</span><span class="sxs-lookup"><span data-stu-id="edb53-113">Security requirements</span></span>

<span data-ttu-id="edb53-114">Mer information om säkerhetskrav finns i [Säkerhetskrav för partner.](/partner-center/partner-security-requirements)</span><span class="sxs-lookup"><span data-stu-id="edb53-114">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="edb53-115">Modell för säkra program</span><span class="sxs-lookup"><span data-stu-id="edb53-115">Secure Application Model</span></span>

<span data-ttu-id="edb53-116">Marketplace-program måste personifiera CSP-partnerbehörigheter för att anropa Microsoft-API:er.</span><span class="sxs-lookup"><span data-stu-id="edb53-116">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="edb53-117">Säkerhetsattacker mot dessa känsliga program kan leda till att kunddata kompromettens.</span><span class="sxs-lookup"><span data-stu-id="edb53-117">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="edb53-118">Om du vill ha en översikt och information om det nya autentiseringsramverket [kan du Modell för säkra program dokumentet om ramverket](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) för autentisering.</span><span class="sxs-lookup"><span data-stu-id="edb53-118">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="edb53-119">Det här dokumentet beskriver principer och metodtips för att göra marketplace-program hållbara och robusta från säkerhetskompromettering.</span><span class="sxs-lookup"><span data-stu-id="edb53-119">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="edb53-120">Exempel</span><span class="sxs-lookup"><span data-stu-id="edb53-120">Samples</span></span>

<span data-ttu-id="edb53-121">Följande översiktsdokument och exempelkod beskriver hur partner kan implementera Modell för säkra program ramverket:</span><span class="sxs-lookup"><span data-stu-id="edb53-121">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="edb53-122">Översiktsdokument för CPV</span><span class="sxs-lookup"><span data-stu-id="edb53-122">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="edb53-123">Översiktsdokument för CSP</span><span class="sxs-lookup"><span data-stu-id="edb53-123">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="edb53-124">.NET-exempel</span><span class="sxs-lookup"><span data-stu-id="edb53-124">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="edb53-125">Java-exempel</span><span class="sxs-lookup"><span data-stu-id="edb53-125">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="edb53-126">REST-instruktioner och exempel</span><span class="sxs-lookup"><span data-stu-id="edb53-126">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="edb53-127">PowerShell-instruktioner och -exempel</span><span class="sxs-lookup"><span data-stu-id="edb53-127">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="edb53-128">REST</span><span class="sxs-lookup"><span data-stu-id="edb53-128">REST</span></span>

<span data-ttu-id="edb53-129">Om du vill göra REST-anrop Modell för säkra program ramverket med exempelkod följer du dessa steg:</span><span class="sxs-lookup"><span data-stu-id="edb53-129">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="edb53-130">Skapa en webbapp</span><span class="sxs-lookup"><span data-stu-id="edb53-130">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="edb53-131">Hämta en auktoriseringskod</span><span class="sxs-lookup"><span data-stu-id="edb53-131">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="edb53-132">Hämta en uppdateringstoken</span><span class="sxs-lookup"><span data-stu-id="edb53-132">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="edb53-133">Hämta en åtkomsttoken</span><span class="sxs-lookup"><span data-stu-id="edb53-133">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="edb53-134">Gör ett Partnercenter-API-anrop</span><span class="sxs-lookup"><span data-stu-id="edb53-134">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="edb53-135">Du kan använda Partner Center PowerShell-modulen för att hämta en auktoriseringskod och en uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="edb53-135">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="edb53-136">Du kan välja det här alternativet i stället för steg 2 och 3.</span><span class="sxs-lookup"><span data-stu-id="edb53-136">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="edb53-137">Mer information finns i [PowerShell-avsnittet och i exemplen](#powershell).</span><span class="sxs-lookup"><span data-stu-id="edb53-137">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="edb53-138">Skapa en webbapp</span><span class="sxs-lookup"><span data-stu-id="edb53-138">Create a web app</span></span>

<span data-ttu-id="edb53-139">Du måste skapa och registrera en webbapp i Partnercenter innan du gör REST-anrop.</span><span class="sxs-lookup"><span data-stu-id="edb53-139">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="edb53-140">Logga in på [Azure-portalen](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="edb53-140">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="edb53-141">Skapa en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edb53-141">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="edb53-142">Ge delegerade programbehörigheter till följande *resurser, beroende på programmets krav*.</span><span class="sxs-lookup"><span data-stu-id="edb53-142">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="edb53-143">Om det behövs kan du lägga till fler delegerade behörigheter för programresurser.</span><span class="sxs-lookup"><span data-stu-id="edb53-143">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="edb53-144">**Microsoft Partner Center** (vissa klienter visar detta som **SampleBECApp**)</span><span class="sxs-lookup"><span data-stu-id="edb53-144">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="edb53-145">**Azure Management-API:er** (om du planerar att anropa Azure-API:er)</span><span class="sxs-lookup"><span data-stu-id="edb53-145">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="edb53-146">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="edb53-146">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="edb53-147">Kontrollera att appens hem-URL är inställd på en slutpunkt där en live-webbapp körs.</span><span class="sxs-lookup"><span data-stu-id="edb53-147">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="edb53-148">Den här appen måste godkänna [auktoriseringskoden från](#get-authorization-code) Azure AD-inloggningssamtalet.</span><span class="sxs-lookup"><span data-stu-id="edb53-148">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="edb53-149">I exempelkoden i följande avsnitt [körs](#get-authorization-code)till exempel webbappen på `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="edb53-149">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="edb53-150">Observera följande information från webbappens inställningar i Azure AD:</span><span class="sxs-lookup"><span data-stu-id="edb53-150">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="edb53-151">Program-ID:t</span><span class="sxs-lookup"><span data-stu-id="edb53-151">Application ID</span></span>
   - <span data-ttu-id="edb53-152">Apphemlighet</span><span class="sxs-lookup"><span data-stu-id="edb53-152">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="edb53-153">Vi rekommenderar att du [använder ett certifikat som din programhemlighet.](/azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="edb53-153">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="edb53-154">Du kan dock även skapa en programnyckel i Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="edb53-154">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="edb53-155">Exempelkoden i [följande avsnitt använder](#get-authorization-code) en programnyckel.</span><span class="sxs-lookup"><span data-stu-id="edb53-155">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="edb53-156">Hämta auktoriseringskod</span><span class="sxs-lookup"><span data-stu-id="edb53-156">Get authorization code</span></span>

<span data-ttu-id="edb53-157">Du måste få en auktoriseringskod som din webbapp kan godkänna från Azure AD-inloggningssamtalet:</span><span class="sxs-lookup"><span data-stu-id="edb53-157">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="edb53-158">Logga in på Azure AD på följande URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="edb53-158">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="edb53-159">Se till att logga in med det användarkonto som du ska göra API-anrop från i Partnercenter (till exempel en administratörsagent eller ett agentkonto för försäljning).</span><span class="sxs-lookup"><span data-stu-id="edb53-159">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="edb53-160">Ersätt **Program-ID med** ditt Azure AD-app-ID (GUID).</span><span class="sxs-lookup"><span data-stu-id="edb53-160">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="edb53-161">När du uppmanas till det loggar du in med ditt användarkonto med MFA konfigurerat.</span><span class="sxs-lookup"><span data-stu-id="edb53-161">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="edb53-162">När du uppmanas till det anger du ytterligare MFA-information (telefonnummer eller e-postadress) för att verifiera inloggningen.</span><span class="sxs-lookup"><span data-stu-id="edb53-162">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="edb53-163">När du har loggat in omdirigerar webbläsaren anropet till slutpunkten för webbappen med din auktoriseringskod.</span><span class="sxs-lookup"><span data-stu-id="edb53-163">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="edb53-164">Följande exempelkod omdirigerar till exempel till `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="edb53-164">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="edb53-165">Anropsspårning för auktoriseringskod</span><span class="sxs-lookup"><span data-stu-id="edb53-165">Authorization code call trace</span></span>

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a><span data-ttu-id="edb53-166">Hämta uppdateringstoken</span><span class="sxs-lookup"><span data-stu-id="edb53-166">Get refresh token</span></span>

<span data-ttu-id="edb53-167">Du måste sedan använda din auktoriseringskod för att hämta en uppdateringstoken:</span><span class="sxs-lookup"><span data-stu-id="edb53-167">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="edb53-168">Gör ett POST-anrop till Azure AD-inloggningsslutpunkten `https://login.microsoftonline.com/CSPTenantID/oauth2/token` med auktoriseringskoden.</span><span class="sxs-lookup"><span data-stu-id="edb53-168">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="edb53-169">Ett exempel finns i följande exempel [på anrop .](#sample-refresh-call)</span><span class="sxs-lookup"><span data-stu-id="edb53-169">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="edb53-170">Observera uppdateringstoken som returneras.</span><span class="sxs-lookup"><span data-stu-id="edb53-170">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="edb53-171">Lagra uppdateringstoken i Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="edb53-171">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="edb53-172">Mer information finns i [API Key Vault dokumentationen](/rest/api/keyvault/).</span><span class="sxs-lookup"><span data-stu-id="edb53-172">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="edb53-173">Uppdateringstoken måste [lagras som en hemlighet](/rest/api/keyvault/setsecret/setsecret) i Key Vault.</span><span class="sxs-lookup"><span data-stu-id="edb53-173">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="edb53-174">Exempel på uppdateringssamtal</span><span class="sxs-lookup"><span data-stu-id="edb53-174">Sample refresh call</span></span>

<span data-ttu-id="edb53-175">Platshållarbegäran:</span><span class="sxs-lookup"><span data-stu-id="edb53-175">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="edb53-176">Begärandetext:</span><span class="sxs-lookup"><span data-stu-id="edb53-176">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="edb53-177">Platshållarsvar:</span><span class="sxs-lookup"><span data-stu-id="edb53-177">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="edb53-178">Svarstext:</span><span class="sxs-lookup"><span data-stu-id="edb53-178">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="edb53-179">Hämta åtkomsttoken</span><span class="sxs-lookup"><span data-stu-id="edb53-179">Get access token</span></span>

<span data-ttu-id="edb53-180">Du måste hämta en åtkomsttoken innan du kan göra anrop till Partner Center-API:erna.</span><span class="sxs-lookup"><span data-stu-id="edb53-180">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="edb53-181">Du måste använda en uppdateringstoken för att hämta en åtkomsttoken eftersom åtkomsttoken vanligtvis har en mycket begränsad livslängd (till exempel mindre än en timme).</span><span class="sxs-lookup"><span data-stu-id="edb53-181">You must use a refresh token to obtain an access token because access tokens generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="edb53-182">Platshållarbegäran:</span><span class="sxs-lookup"><span data-stu-id="edb53-182">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="edb53-183">Begärandetext:</span><span class="sxs-lookup"><span data-stu-id="edb53-183">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="edb53-184">Platshållarsvar:</span><span class="sxs-lookup"><span data-stu-id="edb53-184">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="edb53-185">Svarstext:</span><span class="sxs-lookup"><span data-stu-id="edb53-185">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="edb53-186">Göra PARTNER Center API-anrop</span><span class="sxs-lookup"><span data-stu-id="edb53-186">Make Partner Center API calls</span></span>

<span data-ttu-id="edb53-187">Du måste använda din åtkomsttoken för att anropa Partner Center-API:erna.</span><span class="sxs-lookup"><span data-stu-id="edb53-187">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="edb53-188">Se följande exempel på anrop.</span><span class="sxs-lookup"><span data-stu-id="edb53-188">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="edb53-189">Exempel på partnercenter-API-anrop</span><span class="sxs-lookup"><span data-stu-id="edb53-189">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="edb53-190">PowerShell</span><span class="sxs-lookup"><span data-stu-id="edb53-190">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="edb53-191">Du kan använda [Partner Center PowerShell-modulen för att](https://www.powershellgallery.com/packages/PartnerCenter) minska den infrastruktur som krävs för att utbyta en auktoriseringskod för en åtkomsttoken.</span><span class="sxs-lookup"><span data-stu-id="edb53-191">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="edb53-192">Den här metoden är valfri för att göra [Partner Center REST-anrop](#rest).</span><span class="sxs-lookup"><span data-stu-id="edb53-192">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="edb53-193">Mer information om den här processen finns i [Dokumentationen för Secure Appmodell](/powershell/partnercenter/secure-app-model) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edb53-193">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="edb53-194">Installera PowerShell-modulerna för Azure AD och Partner Center.</span><span class="sxs-lookup"><span data-stu-id="edb53-194">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="edb53-195">Använd kommandot **[New-PartnerAccessToken för](/powershell/module/partnercenter/new-partneraccesstoken)** att utföra medgivandeprocessen och samla in nödvändig uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="edb53-195">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    $token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="edb53-196">Parametern **ServicePrincipal** används med kommandot **New-PartnerAccessToken** eftersom en Azure AD-app med en typ av **webb/API** används.</span><span class="sxs-lookup"><span data-stu-id="edb53-196">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="edb53-197">Den här typen av app kräver att en klientidentifierare och en hemlighet ingår i begäran om åtkomsttoken.</span><span class="sxs-lookup"><span data-stu-id="edb53-197">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="edb53-198">När **kommandot Get-Credential** anropas uppmanas du att ange ett användarnamn och lösenord.</span><span class="sxs-lookup"><span data-stu-id="edb53-198">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="edb53-199">Ange programidentifieraren som användarnamn.</span><span class="sxs-lookup"><span data-stu-id="edb53-199">Enter the application identifier as the username.</span></span> <span data-ttu-id="edb53-200">Ange programhemligheten som lösenord.</span><span class="sxs-lookup"><span data-stu-id="edb53-200">Enter the application secret as the password.</span></span> <span data-ttu-id="edb53-201">När kommandot **New-PartnerAccessToken** anropas uppmanas du att ange autentiseringsuppgifter igen.</span><span class="sxs-lookup"><span data-stu-id="edb53-201">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="edb53-202">Ange autentiseringsuppgifterna för det tjänstkonto som du använder.</span><span class="sxs-lookup"><span data-stu-id="edb53-202">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="edb53-203">Det här tjänstkontot ska vara ett partnerkonto med rätt behörigheter.</span><span class="sxs-lookup"><span data-stu-id="edb53-203">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="edb53-204">Kopiera värdet för uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="edb53-204">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="edb53-205">Du bör lagra värdet för uppdateringstoken i en säker lagringsplats, till exempel Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="edb53-205">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="edb53-206">Mer information om hur du använder modulen för säkra program med PowerShell finns i artikeln [multifaktorautentisering.](/powershell/partnercenter/multi-factor-auth)</span><span class="sxs-lookup"><span data-stu-id="edb53-206">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
