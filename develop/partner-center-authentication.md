---
title: Partner Center-autentisering
description: Partner center använder Azure AD för autentisering och för att använda Partner Center-API:er måste du konfigurera autentiseringsinställningarna korrekt.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: e54feba7ea727bb7f7eff8de76dcdf28c8a453ee
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548081"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="49701-103">Partner Center-autentisering</span><span class="sxs-lookup"><span data-stu-id="49701-103">Partner Center authentication</span></span>

<span data-ttu-id="49701-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="49701-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="49701-105">Partnercenter använder Azure Active Directory för autentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-105">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="49701-106">När du interagerar med Partnercenter-API, SDK eller PowerShell-modulen måste du konfigurera ett Azure AD-program korrekt och sedan begära en åtkomsttoken.</span><span class="sxs-lookup"><span data-stu-id="49701-106">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="49701-107">Åtkomsttoken som hämtas med endast appen eller app - och användarautentisering kan användas med Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="49701-107">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="49701-108">Det finns dock två viktiga objekt som måste beaktas</span><span class="sxs-lookup"><span data-stu-id="49701-108">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="49701-109">Använd multifaktorautentisering vid åtkomst till Partner center-API:et med hjälp av app - och användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-109">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="49701-110">Mer information om den här ändringen finns i [Aktivera säker programmodell.](enable-secure-app-model.md)</span><span class="sxs-lookup"><span data-stu-id="49701-110">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="49701-111">Inte alla åtgärder som Partner Center-API:et stöder endast appautentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-111">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="49701-112">Det finns vissa scenarier där du måste använda app - och användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-112">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="49701-113">Under rubriken *Förutsättningar i* varje artikel [hittar](scenarios.md)du dokumentation som anger om endast appautentisering, app + användarautentisering eller båda stöds.</span><span class="sxs-lookup"><span data-stu-id="49701-113">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="49701-114">Inledande konfiguration</span><span class="sxs-lookup"><span data-stu-id="49701-114">Initial setup</span></span>

1. <span data-ttu-id="49701-115">För att börja måste du se till att du har både ett primärt PartnerCenter-konto och ett PartnerCenter-konto för sandbox-integrering.</span><span class="sxs-lookup"><span data-stu-id="49701-115">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="49701-116">Mer information finns i Konfigurera [Partner Center-konton för API-åtkomst.](set-up-api-access-in-partner-center.md)</span><span class="sxs-lookup"><span data-stu-id="49701-116">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="49701-117">Anteckna registrerings-ID:t och hemligheten för Azure AAD-appen (klienthemlighet krävs endast för identifiering av appar) för både ditt primära konto och ditt sandbox-konto för integrering.</span><span class="sxs-lookup"><span data-stu-id="49701-117">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="49701-118">Logga in på Azure AD från Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="49701-118">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="49701-119">I **behörigheter till andra program** anger du behörigheter för **Windows Azure Active Directory** delegerade behörigheter **och** väljer både Access the directory as **the signed-in user** (Åtkomst till katalogen som den inloggade användaren) och Sign in and read user profile (Logga in och läs **användarprofil).**</span><span class="sxs-lookup"><span data-stu-id="49701-119">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="49701-120">I Azure Portal Lägg **till program**.</span><span class="sxs-lookup"><span data-stu-id="49701-120">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="49701-121">Sök efter "Microsoft Partner Center", som är Microsoft Partner Center-programmet.</span><span class="sxs-lookup"><span data-stu-id="49701-121">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="49701-122">Ange **delegerade behörigheter för** åtkomst **till Partner Center API.**</span><span class="sxs-lookup"><span data-stu-id="49701-122">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="49701-123">Om du använder Partnercenter för Microsoft Cloud Tyskland eller Partnercenter för Microsoft Cloud for US Government är det här steget obligatoriskt.</span><span class="sxs-lookup"><span data-stu-id="49701-123">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="49701-124">Om du använder global instans i Partnercenter är det här steget valfritt.</span><span class="sxs-lookup"><span data-stu-id="49701-124">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="49701-125">CSP-partner kan använda apphanteringsfunktionen i Partnercenter-portalen för att kringgå det här steget för global Partner Center-instans.</span><span class="sxs-lookup"><span data-stu-id="49701-125">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="49701-126">Appbaserad autentisering</span><span class="sxs-lookup"><span data-stu-id="49701-126">App-only authentication</span></span>

<span data-ttu-id="49701-127">Om du vill använda appbaserad autentisering för att få åtkomst till Partner Center-modulen REST API, .NET API, Java API eller PowerShell kan du göra det med hjälp av följande anvisningar.</span><span class="sxs-lookup"><span data-stu-id="49701-127">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by using the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="49701-128">.NET (appbaserad autentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-128">.NET (app-only authentication)</span></span>

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

## <a name="java-app-only-authentication"></a><span data-ttu-id="49701-129">Java (endast appautentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-129">Java (app-only authentication)</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

## <a name="rest-app-only-authentication"></a><span data-ttu-id="49701-130">REST (appbaserad autentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-130">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="49701-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="49701-131">REST request</span></span>

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

### <a name="rest-response"></a><span data-ttu-id="49701-132">REST-svar</span><span class="sxs-lookup"><span data-stu-id="49701-132">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="49701-133">App + användarautentisering</span><span class="sxs-lookup"><span data-stu-id="49701-133">App + User authentication</span></span>

<span data-ttu-id="49701-134">Tidigare har [](https://tools.ietf.org/html/rfc6749#section-4.3) beviljandet av autentiseringsuppgifter för resursägares lösenord använts för att begära en åtkomsttoken för användning med partnercenter-REST API-, .NET-API-, Java API- eller PowerShell-modulen.</span><span class="sxs-lookup"><span data-stu-id="49701-134">Historically, the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="49701-135">Den metoden användes för att begära en åtkomsttoken från Azure Active Directory med en klientidentifierare och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="49701-135">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="49701-136">Den här metoden fungerar dock inte längre eftersom Partnercenter kräver multifaktorautentisering när du använder app - och användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-136">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="49701-137">För att uppfylla detta krav har Microsoft infört ett säkert, skalbart ramverk för autentisering av Molnlösningsleverantör-partner (CSP) och kontrollpanelens leverantörer (CPV) med hjälp av multifaktorautentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-137">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="49701-138">Det här ramverket kallas för Modell för säkra program och består av en medgivandeprocess och en begäran om en åtkomsttoken med hjälp av en uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="49701-138">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="49701-139">Partnermedgivande</span><span class="sxs-lookup"><span data-stu-id="49701-139">Partner consent</span></span>

<span data-ttu-id="49701-140">Processen för partnermedgivande är en interaktiv process där partnern autentiseras med hjälp av multifaktorautentisering, medgivanden till programmet och en uppdateringstoken lagras på en säker lagringsplats, till exempel Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="49701-140">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="49701-141">Vi rekommenderar att du använder ett dedikerat konto för integrering i den här processen.</span><span class="sxs-lookup"><span data-stu-id="49701-141">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49701-142">Lämplig multifaktorautentiseringslösning ska aktiveras för det tjänstkonto som används i partnerns medgivandeprocess.</span><span class="sxs-lookup"><span data-stu-id="49701-142">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="49701-143">Om den inte är det kommer den resulterande uppdateringstoken inte att vara kompatibel med säkerhetskraven.</span><span class="sxs-lookup"><span data-stu-id="49701-143">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="49701-144">Exempel för app - och användarautentisering</span><span class="sxs-lookup"><span data-stu-id="49701-144">Samples for App + User authentication</span></span>

<span data-ttu-id="49701-145">Processen för partnermedgivande kan utföras på flera olika sätt.</span><span class="sxs-lookup"><span data-stu-id="49701-145">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="49701-146">För att hjälpa partner att förstå hur de utför varje åtgärd som krävs har vi utvecklat följande exempel.</span><span class="sxs-lookup"><span data-stu-id="49701-146">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="49701-147">När du implementerar rätt lösning i din miljö är det viktigt att du utvecklar en lösning som är klagomål mot kodningsstandarder och säkerhetsprinciper.</span><span class="sxs-lookup"><span data-stu-id="49701-147">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="49701-148">.NET (app+användarautentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-148">.NET (app+user authentication)</span></span>

<span data-ttu-id="49701-149">Exempelprojektet [för partnermedgivande](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) visar hur du använder en webbplats som utvecklats med ASP.NET för att samla in medgivande, begära en uppdateringstoken och på ett säkert sätt lagra den i Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="49701-149">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="49701-150">Utför följande steg för att skapa de nödvändiga förutsättningarna för det här exemplet.</span><span class="sxs-lookup"><span data-stu-id="49701-150">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="49701-151">Skapa en instans av Azure Key Vault med hjälp Azure Portal eller följande PowerShell-kommandon.</span><span class="sxs-lookup"><span data-stu-id="49701-151">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="49701-152">Innan du kör kommandot måste du ändra parametervärdena därefter.</span><span class="sxs-lookup"><span data-stu-id="49701-152">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="49701-153">Valvnamnet måste vara unikt.</span><span class="sxs-lookup"><span data-stu-id="49701-153">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="49701-154">Mer information om hur du skapar en Azure Key Vault finns i [Snabbstart:](/azure/key-vault/quick-create-portal) Ange och hämta en hemlighet från Azure Key Vault med hjälp av Azure Portal eller [Snabbstart: Ange](/azure/key-vault/quick-create-powershell)och hämta en hemlighet från Azure Key Vault med Hjälp av PowerShell .</span><span class="sxs-lookup"><span data-stu-id="49701-154">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="49701-155">Ange och hämta sedan en hemlighet.</span><span class="sxs-lookup"><span data-stu-id="49701-155">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="49701-156">Skapa ett Azure AD-program och en nyckel med Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="49701-156">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="49701-157">Se till att anteckna värdena för programidentifierare och hemligheter eftersom de kommer att användas i stegen nedan.</span><span class="sxs-lookup"><span data-stu-id="49701-157">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="49701-158">Ge det nyligen skapade Azure AD-programmet läshemlighetsbehörigheter med hjälp Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="49701-158">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="49701-159">Skapa ett Azure AD-program som har konfigurerats för Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="49701-159">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="49701-160">Utför följande åtgärder för att slutföra det här steget.</span><span class="sxs-lookup"><span data-stu-id="49701-160">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="49701-161">Bläddra till [apphanteringsfunktionen](https://partner.microsoft.com/pcv/apiintegration/appmanagement) i instrumentpanelen i Partnercenter</span><span class="sxs-lookup"><span data-stu-id="49701-161">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="49701-162">Välj *Lägg till ny webbapp* för att skapa ett nytt Azure AD-program.</span><span class="sxs-lookup"><span data-stu-id="49701-162">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="49701-163">Se till att dokumentera *värdena app-ID,\*\*konto-ID*\* och nyckel eftersom de kommer att användas i stegen nedan. </span><span class="sxs-lookup"><span data-stu-id="49701-163">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="49701-164">Klona [lagringsplatsen Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando.</span><span class="sxs-lookup"><span data-stu-id="49701-164">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="49701-165">Öppna projektet *PartnerConsent* som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen .</span><span class="sxs-lookup"><span data-stu-id="49701-165">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="49701-166">Fyll i programinställningarna som finns i [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span><span class="sxs-lookup"><span data-stu-id="49701-166">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!--
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="49701-167">Känslig information, till exempel programhemligheter, bör inte lagras i konfigurationsfiler.</span><span class="sxs-lookup"><span data-stu-id="49701-167">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="49701-168">Det gjordes här eftersom det här är ett exempelprogram.</span><span class="sxs-lookup"><span data-stu-id="49701-168">It was done here because this is a sample application.</span></span> <span data-ttu-id="49701-169">Med ditt produktionsprogram rekommenderar vi starkt att du använder certifikatbaserad autentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-169">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="49701-170">Mer information finns i [Certifikatautentiseringsuppgifter för programautentisering.]( /azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="49701-170">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="49701-171">När du kör det här exempelprojektet uppmanas du att autentisera dig.</span><span class="sxs-lookup"><span data-stu-id="49701-171">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="49701-172">När autentiseringen är klar begärs en åtkomsttoken från Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49701-172">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="49701-173">Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="49701-173">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="49701-174">Java (app+användarautentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-174">Java (app+user authentication)</span></span>

<span data-ttu-id="49701-175">Exempelprojektet [för partnermedgivande](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) visar hur du använder en webbplats som utvecklats med JSP för att samla in medgivande, begära en uppdateringstoken och skydda lagring i Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="49701-175">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="49701-176">Utför följande för att skapa de nödvändiga förutsättningarna för det här exemplet.</span><span class="sxs-lookup"><span data-stu-id="49701-176">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="49701-177">Skapa en instans av Azure Key Vault med hjälp Azure Portal eller följande PowerShell-kommandon.</span><span class="sxs-lookup"><span data-stu-id="49701-177">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="49701-178">Innan du kör kommandot måste du ändra parametervärdena därefter.</span><span class="sxs-lookup"><span data-stu-id="49701-178">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="49701-179">Valvnamnet måste vara unikt.</span><span class="sxs-lookup"><span data-stu-id="49701-179">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="49701-180">Mer information om hur du skapar en Azure Key Vault finns i [Snabbstart:](/azure/key-vault/quick-create-portal) Ange och hämta en hemlighet från Azure Key Vault med hjälp av Azure Portal eller [Snabbstart: Ange](/azure/key-vault/quick-create-powershell)och hämta en hemlighet från Azure Key Vault med Hjälp av PowerShell .</span><span class="sxs-lookup"><span data-stu-id="49701-180">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="49701-181">Skapa ett Azure AD-program och en nyckel med Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="49701-181">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="49701-182">Se till att dokumentera värdena för programidentifierare och hemligheter eftersom de kommer att användas i stegen nedan.</span><span class="sxs-lookup"><span data-stu-id="49701-182">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="49701-183">Ge det nyligen skapade Azure AD-programmet läshemlighetsbehörighet med hjälp Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="49701-183">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="49701-184">Skapa ett Azure AD-program som har konfigurerats för Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="49701-184">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="49701-185">Utför följande för att slutföra det här steget.</span><span class="sxs-lookup"><span data-stu-id="49701-185">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="49701-186">Bläddra till [apphanteringsfunktionen](https://partner.microsoft.com/pcv/apiintegration/appmanagement) i instrumentpanelen i Partnercenter</span><span class="sxs-lookup"><span data-stu-id="49701-186">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="49701-187">Välj *Lägg till ny webbapp* för att skapa ett nytt Azure AD-program.</span><span class="sxs-lookup"><span data-stu-id="49701-187">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="49701-188">Se till att dokumentera *värdena app-ID,\*\*konto-ID*\* och nyckel eftersom de kommer att användas i stegen nedan. </span><span class="sxs-lookup"><span data-stu-id="49701-188">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="49701-189">Klona [lagringsplatsen Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando</span><span class="sxs-lookup"><span data-stu-id="49701-189">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="49701-190">Öppna projektet *PartnerConsent* som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen .</span><span class="sxs-lookup"><span data-stu-id="49701-190">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="49701-191">Fyll i programinställningarna som finns i [web.xmlfilen](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)</span><span class="sxs-lookup"><span data-stu-id="49701-191">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="49701-192">Känslig information, till exempel programhemligheter, bör inte lagras i konfigurationsfiler.</span><span class="sxs-lookup"><span data-stu-id="49701-192">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="49701-193">Det gjordes här eftersom det här är ett exempelprogram.</span><span class="sxs-lookup"><span data-stu-id="49701-193">It was done here because this is a sample application.</span></span> <span data-ttu-id="49701-194">Med ditt produktionsprogram rekommenderar vi starkt att du använder certifikatbaserad autentisering.</span><span class="sxs-lookup"><span data-stu-id="49701-194">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="49701-195">Mer information finns i Key Vault [certifikatautentisering](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="49701-195">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="49701-196">När du kör det här exempelprojektet uppmanas du att autentisera dig.</span><span class="sxs-lookup"><span data-stu-id="49701-196">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="49701-197">När autentiseringen är klar begärs en åtkomsttoken från Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49701-197">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="49701-198">Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="49701-198">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="49701-199">Molnlösningsleverantör autentisering</span><span class="sxs-lookup"><span data-stu-id="49701-199">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="49701-200">Molnlösningsleverantör partner kan använda den uppdateringstoken som erhållits via [processen för partnermedgivande.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="49701-200">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="49701-201">Exempel för Molnlösningsleverantör autentisering</span><span class="sxs-lookup"><span data-stu-id="49701-201">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="49701-202">För att hjälpa partner att förstå hur de utför varje åtgärd som krävs har vi utvecklat följande exempel.</span><span class="sxs-lookup"><span data-stu-id="49701-202">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="49701-203">När du implementerar rätt lösning i din miljö är det viktigt att du utvecklar en lösning som är klagomål mot kodningsstandarder och säkerhetsprinciper.</span><span class="sxs-lookup"><span data-stu-id="49701-203">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="49701-204">.NET (CSP-autentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-204">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="49701-205">Om du inte redan har gjort det utför du [processen för partnermedgivande.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="49701-205">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="49701-206">Klona [lagringsplatsen Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando</span><span class="sxs-lookup"><span data-stu-id="49701-206">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="49701-207">Öppna `CSPApplication` projektet som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen .</span><span class="sxs-lookup"><span data-stu-id="49701-207">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="49701-208">Uppdatera programinställningarna som finns i [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) filen.</span><span class="sxs-lookup"><span data-stu-id="49701-208">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. <span data-ttu-id="49701-209">Ange lämpliga värden för **variablerna PartnerId** **och CustomerId** som finns i [filen Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="49701-209">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="49701-210">När du kör det här exempelprojektet hämtas den uppdateringstoken som erhölls under partnerns medgivandeprocess.</span><span class="sxs-lookup"><span data-stu-id="49701-210">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="49701-211">Sedan begär den en åtkomsttoken för att interagera Partnercenter-SDK för partnerns räkning.</span><span class="sxs-lookup"><span data-stu-id="49701-211">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="49701-212">Slutligen begär den en åtkomsttoken för att interagera med Microsoft Graph åt den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="49701-212">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="49701-213">Java (CSP-autentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-213">Java (CSP authentication)</span></span>

1. <span data-ttu-id="49701-214">Om du inte redan har gjort det utför du [processen för partnermedgivande.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="49701-214">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="49701-215">Klona [lagringsplatsen Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med Visual Studio eller följande kommando</span><span class="sxs-lookup"><span data-stu-id="49701-215">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="49701-216">Öppna `cspsample` projektet som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen .</span><span class="sxs-lookup"><span data-stu-id="49701-216">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="49701-217">Uppdatera programinställningarna som finns i [filen application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)</span><span class="sxs-lookup"><span data-stu-id="49701-217">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="49701-218">När du kör det här exempelprojektet hämtas den uppdateringstoken som erhölls under partnerns medgivandeprocess.</span><span class="sxs-lookup"><span data-stu-id="49701-218">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="49701-219">Sedan begär den en åtkomsttoken för att interagera Partnercenter-SDK för partnerns räkning.</span><span class="sxs-lookup"><span data-stu-id="49701-219">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="49701-220">Valfritt – avkommentera funktionsanropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="49701-220">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="49701-221">Kontrollpanelen providerautentisering</span><span class="sxs-lookup"><span data-stu-id="49701-221">Control Panel Provider authentication</span></span>

<span data-ttu-id="49701-222">Kontrollpanelens leverantörer måste ha varje partner som de stöder för att utföra [processen för partnermedgivande.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="49701-222">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="49701-223">När det är klart används den uppdateringstoken som erhållits via den processen för att få åtkomst till PartnerCenter REST API och .NET API.</span><span class="sxs-lookup"><span data-stu-id="49701-223">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="49701-224">Exempel för autentisering av molnpanelsprovider</span><span class="sxs-lookup"><span data-stu-id="49701-224">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="49701-225">För att hjälpa kontrollpanelens leverantörer att förstå hur de utför varje åtgärd som krävs har vi utvecklat följande exempel.</span><span class="sxs-lookup"><span data-stu-id="49701-225">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="49701-226">När du implementerar rätt lösning i din miljö är det viktigt att du utvecklar en lösning som är klagomål mot kodningsstandarder och säkerhetsprinciper.</span><span class="sxs-lookup"><span data-stu-id="49701-226">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="49701-227">.NET (CPV-autentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-227">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="49701-228">Utveckla och distribuera en process för Molnlösningsleverantör partner för att ge lämpligt medgivande.</span><span class="sxs-lookup"><span data-stu-id="49701-228">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="49701-229">Mer information om ett exempel finns i [Medgivande från partner.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="49701-229">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="49701-230">Användarautentiseringsuppgifter från Molnlösningsleverantör partner ska inte lagras.</span><span class="sxs-lookup"><span data-stu-id="49701-230">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="49701-231">Uppdateringstoken som erhålls via processen för partnermedgivande ska lagras och användas för att begära åtkomsttoken för interaktion med Microsoft-API:er.</span><span class="sxs-lookup"><span data-stu-id="49701-231">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="49701-232">Klona [lagringsplatsen Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando</span><span class="sxs-lookup"><span data-stu-id="49701-232">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="49701-233">Öppna `CPVApplication` projektet som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen .</span><span class="sxs-lookup"><span data-stu-id="49701-233">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="49701-234">Uppdatera programinställningarna som finns i [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) filen.</span><span class="sxs-lookup"><span data-stu-id="49701-234">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. <span data-ttu-id="49701-235">Ange lämpliga värden för **variablerna PartnerId** **och CustomerId** som finns i [filen Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="49701-235">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="49701-236">När du kör det här exempelprojektet hämtar det uppdateringstoken för den angivna partnern.</span><span class="sxs-lookup"><span data-stu-id="49701-236">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="49701-237">Sedan begär den en åtkomsttoken för att få åtkomst till Partnercenter och Azure AD Graph åt partnern.</span><span class="sxs-lookup"><span data-stu-id="49701-237">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="49701-238">Nästa uppgift som den utför är att ta bort och skapa behörighetsstipendier till kundens klientorganisation.</span><span class="sxs-lookup"><span data-stu-id="49701-238">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="49701-239">Eftersom det inte finns någon relation mellan kontrollpanelens leverantör och kunden måste dessa behörigheter läggas till med partnercenter-API:et.</span><span class="sxs-lookup"><span data-stu-id="49701-239">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="49701-240">I följande exempel visas hur du gör det.</span><span class="sxs-lookup"><span data-stu-id="49701-240">The following example shows how to accomplish that.</span></span>

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

<span data-ttu-id="49701-241">När dessa behörigheter har upprättats utför exemplet åtgärder med hjälp av Azure AD Graph åt kunden.</span><span class="sxs-lookup"><span data-stu-id="49701-241">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="49701-242">Java (CPV-autentisering)</span><span class="sxs-lookup"><span data-stu-id="49701-242">Java (CPV authentication)</span></span>

1. <span data-ttu-id="49701-243">Utveckla och distribuera en process för Molnlösningsleverantör partner för att ge lämpligt medgivande.</span><span class="sxs-lookup"><span data-stu-id="49701-243">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="49701-244">Mer information och ett exempel finns i [medgivande för partner.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="49701-244">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="49701-245">Användarautentiseringsuppgifter från Molnlösningsleverantör partner ska inte lagras.</span><span class="sxs-lookup"><span data-stu-id="49701-245">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="49701-246">Uppdateringstoken som erhålls via processen för partnermedgivande ska lagras och användas för att begära åtkomsttoken för interaktion med Microsoft-API:er.</span><span class="sxs-lookup"><span data-stu-id="49701-246">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="49701-247">Klona [lagringsplatsen Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando</span><span class="sxs-lookup"><span data-stu-id="49701-247">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="49701-248">Öppna `cpvsample` projektet som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen .</span><span class="sxs-lookup"><span data-stu-id="49701-248">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="49701-249">Uppdatera programinställningarna som finns i [filen application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)</span><span class="sxs-lookup"><span data-stu-id="49701-249">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    <span data-ttu-id="49701-250">Värdet för ska `partnercenter.displayName` vara visningsnamnet för ditt Marketplace-program.</span><span class="sxs-lookup"><span data-stu-id="49701-250">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="49701-251">Ange lämpliga värden för **variablerna partnerId** **och customerId** som finns i [filen Program.java.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)</span><span class="sxs-lookup"><span data-stu-id="49701-251">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="49701-252">När du kör det här exempelprojektet hämtar det uppdateringstoken för den angivna partnern.</span><span class="sxs-lookup"><span data-stu-id="49701-252">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="49701-253">Sedan begär den en åtkomsttoken för att få åtkomst till Partnercenter för partnerns räkning.</span><span class="sxs-lookup"><span data-stu-id="49701-253">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="49701-254">Nästa uppgift som den utför är att ta bort och skapa behörighetsstipendier till kundens klientorganisation.</span><span class="sxs-lookup"><span data-stu-id="49701-254">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="49701-255">Eftersom det inte finns någon relation mellan kontrollpanelens leverantör och kunden måste dessa behörigheter läggas till med partnercenter-API:et.</span><span class="sxs-lookup"><span data-stu-id="49701-255">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="49701-256">I följande exempel visas hur du beviljar behörigheterna.</span><span class="sxs-lookup"><span data-stu-id="49701-256">The following example shows how to grant the permissions.</span></span>

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

<span data-ttu-id="49701-257">Avkommentera funktionsanropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="49701-257">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
