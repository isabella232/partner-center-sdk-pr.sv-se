---
title: Aktivera säker programmodell
description: Skydda dina partner Center-och kontroll panel appar.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3e153e1e7d4e38580d8cb39a3996e56365ff5fbe
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769303"
---
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="c6a6b-103">Aktivera Secure Application Model-ramverket</span><span class="sxs-lookup"><span data-stu-id="c6a6b-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="c6a6b-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="c6a6b-104">**Applies to:**</span></span>

- <span data-ttu-id="c6a6b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="c6a6b-105">Partner Center</span></span>

<span data-ttu-id="c6a6b-106">Microsoft presenterar ett säkert, skalbart ramverk för att autentisera leverantörer av moln lösnings leverantörer och kontroll panels leverantörer (CPV) via Microsoft Azure Multi-Factor Authentication (MFA)-arkitekturen.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-106">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>

<span data-ttu-id="c6a6b-107">Du kan använda den nya modellen för att öka säkerheten för API-integrerings anrop i Partner Center.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-107">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="c6a6b-108">Detta gör att alla parter (inklusive Microsoft, CSP-partner och CPVs) kan skydda sin infrastruktur och kund information från säkerhets risker.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-108">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="c6a6b-109">Omfång</span><span class="sxs-lookup"><span data-stu-id="c6a6b-109">Scope</span></span>

<span data-ttu-id="c6a6b-110">Den här artikeln gäller följande aktörer:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-110">This article concerns the following actors:</span></span>

- <span data-ttu-id="c6a6b-111">CPV</span><span class="sxs-lookup"><span data-stu-id="c6a6b-111">CPVs</span></span>
  - <span data-ttu-id="c6a6b-112">En CPV är en oberoende programvaruleverantör som utvecklar appar som CSP-partner använder för att integrera med Partnercenter-API:er.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-112">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="c6a6b-113">En CPV är inte en CSP-partner med direkt åtkomst till Partnercenter-instrumentpanelen eller -API:er.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-113">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="c6a6b-114">CSP-indirekta providers och CSP Direct-partners som använder app-ID + användarautentisering och som integreras direkt med API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-114">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="c6a6b-115">Säkerhetskrav</span><span class="sxs-lookup"><span data-stu-id="c6a6b-115">Security requirements</span></span>

<span data-ttu-id="c6a6b-116">Mer information om säkerhets krav finns i [säkerhets krav för partner](/partner-center/partner-security-requirements).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-116">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="c6a6b-117">Säker program modell</span><span class="sxs-lookup"><span data-stu-id="c6a6b-117">Secure Application Model</span></span>

<span data-ttu-id="c6a6b-118">Marketplace-program måste personifiera CSP-partnerns behörigheter för att anropa Microsoft API: er.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-118">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="c6a6b-119">Säkerhets attacker på dessa känsliga program kan leda till att kunddata komprometteras.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-119">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="c6a6b-120">Om du vill ha en översikt och information om det nya Authentication Framework laddar du ned dokumentet för [säker program modell ramverk](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) .</span><span class="sxs-lookup"><span data-stu-id="c6a6b-120">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="c6a6b-121">Det här dokumentet beskriver principer och bästa praxis för att göra Marketplace-program hållbara och robusta mot säkerhets kompromisser.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-121">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="c6a6b-122">Exempel</span><span class="sxs-lookup"><span data-stu-id="c6a6b-122">Samples</span></span>

<span data-ttu-id="c6a6b-123">Följande översikts dokument och exempel kod beskriver hur partner kan implementera säkra program modell ramverk:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-123">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="c6a6b-124">Översikts dokument för CPV</span><span class="sxs-lookup"><span data-stu-id="c6a6b-124">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="c6a6b-125">Översikts dokument för CSP</span><span class="sxs-lookup"><span data-stu-id="c6a6b-125">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="c6a6b-126">.NET-exempel</span><span class="sxs-lookup"><span data-stu-id="c6a6b-126">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="c6a6b-127">Java-exempel</span><span class="sxs-lookup"><span data-stu-id="c6a6b-127">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="c6a6b-128">REST-instruktioner och exempel</span><span class="sxs-lookup"><span data-stu-id="c6a6b-128">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="c6a6b-129">PowerShell-instruktioner och exempel</span><span class="sxs-lookup"><span data-stu-id="c6a6b-129">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="c6a6b-130">REST</span><span class="sxs-lookup"><span data-stu-id="c6a6b-130">REST</span></span>

<span data-ttu-id="c6a6b-131">Följ dessa steg om du vill göra REST-anrop med den säkra program modell ramverket med exempel kod:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-131">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="c6a6b-132">Skapa en webbapp</span><span class="sxs-lookup"><span data-stu-id="c6a6b-132">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="c6a6b-133">Hämta en auktoriseringskod</span><span class="sxs-lookup"><span data-stu-id="c6a6b-133">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="c6a6b-134">Hämta en uppdateringstoken</span><span class="sxs-lookup"><span data-stu-id="c6a6b-134">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="c6a6b-135">Hämta en åtkomsttoken</span><span class="sxs-lookup"><span data-stu-id="c6a6b-135">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="c6a6b-136">Gör ett Partnercenter-API-anrop</span><span class="sxs-lookup"><span data-stu-id="c6a6b-136">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="c6a6b-137">Du kan använda Partner Center PowerShell-modulen för att hämta en auktoriseringskod och en uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-137">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="c6a6b-138">Du kan välja det här alternativet i stället för steg 2 och 3.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-138">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="c6a6b-139">Mer information finns i PowerShell- [avsnittet och exempel](#powershell).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-139">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="c6a6b-140">Skapa en webbapp</span><span class="sxs-lookup"><span data-stu-id="c6a6b-140">Create a web app</span></span>

<span data-ttu-id="c6a6b-141">Du måste skapa och registrera en webbapp i Partner Center innan du kan göra REST-anrop.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-141">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="c6a6b-142">Logga in på [Azure-portalen](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-142">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c6a6b-143">Skapa en Azure Active Directory-app (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-143">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="c6a6b-144">Ge delegerade program behörigheter till följande resurser, *beroende på programmets krav*.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-144">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="c6a6b-145">Om det behövs kan du lägga till fler delegerade behörigheter för program resurser.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-145">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="c6a6b-146">**Microsoft Partner Center** (vissa klienter visar detta som **SampleBECApp**)</span><span class="sxs-lookup"><span data-stu-id="c6a6b-146">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="c6a6b-147">**API: er för Azure-hantering** (om du planerar att anropa Azure API: er)</span><span class="sxs-lookup"><span data-stu-id="c6a6b-147">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="c6a6b-148">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="c6a6b-148">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="c6a6b-149">Kontrol lera att appens hem-URL är inställd på en slut punkt där en Live-webbapp körs.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-149">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="c6a6b-150">Den här appen måste acceptera [auktoriseringskod](#get-authorization-code) från inloggnings anropet för Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-150">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="c6a6b-151">I exempel koden i [följande avsnitt](#get-authorization-code)körs webb programmet på `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="c6a6b-151">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="c6a6b-152">Observera följande information från webbappens inställningar i Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-152">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="c6a6b-153">Program-ID</span><span class="sxs-lookup"><span data-stu-id="c6a6b-153">Application ID</span></span>
   - <span data-ttu-id="c6a6b-154">Apphemlighet</span><span class="sxs-lookup"><span data-stu-id="c6a6b-154">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="c6a6b-155">Vi rekommenderar att du [använder ett certifikat som program hemlighet](/azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-155">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="c6a6b-156">Men du kan också skapa en program nyckel i Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-156">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="c6a6b-157">Exempel koden i [följande avsnitt](#get-authorization-code) använder en program nyckel.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-157">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="c6a6b-158">Hämta auktoriseringskod</span><span class="sxs-lookup"><span data-stu-id="c6a6b-158">Get authorization code</span></span>

<span data-ttu-id="c6a6b-159">Du måste hämta en auktoriseringskod för att din webbapp ska accepteras från Azure AD-inloggnings anropet:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-159">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="c6a6b-160">Logga in på Azure AD på följande URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="c6a6b-160">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="c6a6b-161">Var noga med att logga in med det användar konto som du ska använda för API-anrop i Partner Center (till exempel en administratörs agent eller ett försäljnings agent konto).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-161">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="c6a6b-162">Ersätt **program-ID** med ditt Azure AD App-ID (GUID).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-162">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="c6a6b-163">När du uppmanas till det loggar du in med ditt användar konto med MFA konfigurerat.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-163">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="c6a6b-164">När du uppmanas till det anger du ytterligare MFA-information (telefonnummer eller e-postadress) för att verifiera din inloggning.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-164">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="c6a6b-165">När du är inloggad omdirigerar webbläsaren anropet till din webb programs slut punkt med din auktoriseringskod.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-165">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="c6a6b-166">Till exempel omdirigeras följande exempel kod till `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="c6a6b-166">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="c6a6b-167">Spårning av auktoriseringskod</span><span class="sxs-lookup"><span data-stu-id="c6a6b-167">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="c6a6b-168">Hämta uppdateringstoken</span><span class="sxs-lookup"><span data-stu-id="c6a6b-168">Get refresh token</span></span>

<span data-ttu-id="c6a6b-169">Du måste sedan använda auktoriseringskod för att hämta en uppdateringstoken:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-169">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="c6a6b-170">Ring ett POST-anrop till inloggnings slut punkten för Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` med auktoriseringskod.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-170">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="c6a6b-171">Ett exempel finns i följande [exempel anrop](#sample-refresh-call).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-171">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="c6a6b-172">Notera den uppdateringstoken som returneras.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-172">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="c6a6b-173">Lagra uppdateringstoken i Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-173">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="c6a6b-174">Mer information finns i dokumentationen till [Key Vault API](/rest/api/keyvault/).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-174">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6a6b-175">Uppdateringstoken måste [lagras som en hemlighet](/rest/api/keyvault/setsecret/setsecret) i Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-175">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="c6a6b-176">Exempel på uppdaterings anrop</span><span class="sxs-lookup"><span data-stu-id="c6a6b-176">Sample refresh call</span></span>

<span data-ttu-id="c6a6b-177">Placeholder-begäran:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-177">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="c6a6b-178">Begärandetext:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-178">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="c6a6b-179">Plats hållarens svar:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-179">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="c6a6b-180">Svars text:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-180">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="c6a6b-181">Hämta åtkomsttoken</span><span class="sxs-lookup"><span data-stu-id="c6a6b-181">Get access token</span></span>

<span data-ttu-id="c6a6b-182">Du måste skaffa en åtkomsttoken innan du kan ringa till API: erna för partner Center.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-182">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="c6a6b-183">Du måste använda en uppdateringstoken för att få en åtkomsttoken eftersom åtkomsttoken ofta har en mycket begränsad livs längd (till exempel mindre än en timme).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-183">You must use a refresh token to obtain an access token because access token generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="c6a6b-184">Placeholder-begäran:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-184">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="c6a6b-185">Begärandetext:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-185">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="c6a6b-186">Plats hållarens svar:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-186">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="c6a6b-187">Svars text:</span><span class="sxs-lookup"><span data-stu-id="c6a6b-187">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="c6a6b-188">Gör API-anrop i Partner Center</span><span class="sxs-lookup"><span data-stu-id="c6a6b-188">Make Partner Center API calls</span></span>

<span data-ttu-id="c6a6b-189">Du måste använda din åtkomsttoken för att anropa API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-189">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="c6a6b-190">Se följande exempel anrop.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-190">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="c6a6b-191">Exempel-API-anrop för partner Center</span><span class="sxs-lookup"><span data-stu-id="c6a6b-191">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="c6a6b-192">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6a6b-192">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="c6a6b-193">Du kan använda [partner Center PowerShell-modulen](https://www.powershellgallery.com/packages/PartnerCenter) för att minska den infrastruktur som krävs för att utbyta en auktoriseringskod för en åtkomsttoken.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-193">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="c6a6b-194">Den här metoden är valfri för att göra [partner Center rest-anrop](#rest).</span><span class="sxs-lookup"><span data-stu-id="c6a6b-194">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="c6a6b-195">Mer information om den här processen finns i [säker app Model](/powershell/partnercenter/secure-app-model) PowerShell-dokumentation.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-195">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="c6a6b-196">Installera PowerShell-modulerna för Azure AD och partner Center.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-196">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="c6a6b-197">Använd kommandot **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** för att genomföra medgivande processen och avbilda den nödvändiga uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-197">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="c6a6b-198">Parametern **ServicePrincipal** används med kommandot **New-PartnerAccessToken** eftersom en Azure AD-App med en typ av **webb/API** används.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-198">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="c6a6b-199">Den här typen av app kräver att klient-ID och hemlighet tas med i åtkomsttokenbegäran.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-199">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="c6a6b-200">När kommandot **Get-Credential** anropas uppmanas du att ange ett användar namn och lösen ord.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-200">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="c6a6b-201">Ange program-ID: t som användar namn.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-201">Enter the application identifier as the username.</span></span> <span data-ttu-id="c6a6b-202">Ange program hemligheten som lösen ord.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-202">Enter the application secret as the password.</span></span> <span data-ttu-id="c6a6b-203">När kommandot **New-PartnerAccessToken** anropas uppmanas du att ange autentiseringsuppgifterna igen.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-203">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="c6a6b-204">Ange autentiseringsuppgifterna för det tjänst konto som du använder.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-204">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="c6a6b-205">Det här tjänst kontot bör vara ett partner konto med rätt behörighet.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-205">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="c6a6b-206">Kopiera värdet för uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-206">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="c6a6b-207">Du bör lagra värdet för uppdateringstoken i en säker lagrings plats, t. ex. Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c6a6b-207">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="c6a6b-208">Mer information om hur du använder den säkra modulen med PowerShell finns i artikeln [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) .</span><span class="sxs-lookup"><span data-stu-id="c6a6b-208">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
