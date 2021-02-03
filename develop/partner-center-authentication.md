---
title: Partner Center-autentisering
description: 'Partner Center använder Azure AD för autentisering och för att använda API: er för partner Center måste du konfigurera dina autentiseringsinställningar på rätt sätt.'
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: 46ef9c6bc151c368281e943b7d24ebc07e34b66d
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/19/2020
ms.locfileid: "97770289"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="db13b-103">Partner Center-autentisering</span><span class="sxs-lookup"><span data-stu-id="db13b-103">Partner Center authentication</span></span>

<span data-ttu-id="db13b-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="db13b-104">**Applies to:**</span></span>

- <span data-ttu-id="db13b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="db13b-105">Partner Center</span></span>
- <span data-ttu-id="db13b-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="db13b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="db13b-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="db13b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="db13b-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="db13b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="db13b-109">Partnercenter använder Azure Active Directory för autentisering.</span><span class="sxs-lookup"><span data-stu-id="db13b-109">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="db13b-110">När du interagerar med Partnercenter-API, SDK eller PowerShell-modulen måste du konfigurera ett Azure AD-program korrekt och sedan begära en åtkomsttoken.</span><span class="sxs-lookup"><span data-stu-id="db13b-110">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="db13b-111">Åtkomst-token som hämtats med endast app eller app + User Authentication kan användas med partner Center.</span><span class="sxs-lookup"><span data-stu-id="db13b-111">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="db13b-112">Det finns dock två viktiga objekt som måste beaktas</span><span class="sxs-lookup"><span data-stu-id="db13b-112">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="db13b-113">Använd Multi-Factor Authentication vid åtkomst till API: et för partner Center med app + User Authentication.</span><span class="sxs-lookup"><span data-stu-id="db13b-113">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="db13b-114">Mer information om den här ändringen finns i [Aktivera säker program modell](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="db13b-114">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="db13b-115">Inte alla åtgärder som partner Center API-stöd för endast appens autentisering.</span><span class="sxs-lookup"><span data-stu-id="db13b-115">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="db13b-116">Det finns vissa scenarier där du måste använda app + User Authentication.</span><span class="sxs-lookup"><span data-stu-id="db13b-116">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="db13b-117">Under rubriken *krav* för varje [artikel](scenarios.md)hittar du dokumentation som anger om endast appens autentisering, app + användarautentisering eller båda stöds.</span><span class="sxs-lookup"><span data-stu-id="db13b-117">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="db13b-118">Första konfigurationen</span><span class="sxs-lookup"><span data-stu-id="db13b-118">Initial setup</span></span>

1. <span data-ttu-id="db13b-119">Innan du börjar måste du kontrol lera att du har både ett primärt Partner Center konto och ett konto för integrations Center för integration.</span><span class="sxs-lookup"><span data-stu-id="db13b-119">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="db13b-120">Mer information finns i [Konfigurera Partner Center-konton för API-åtkomst](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="db13b-120">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="db13b-121">Anteckna registrerings-ID och hemlighet för Azure AAD-appen (klient hemlighet krävs endast för identifiering av appar) för både ditt primära konto och ditt konto för integration sandbox.</span><span class="sxs-lookup"><span data-stu-id="db13b-121">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="db13b-122">Logga in på Azure AD från Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="db13b-122">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="db13b-123">Ange behörigheter för **Windows-Azure Active Directory** till **delegerade behörigheter** i **behörigheter till andra program** och välj både **åtkomst till katalogen som den inloggade användaren** och **Logga in och Läs användar profilen**.</span><span class="sxs-lookup"><span data-stu-id="db13b-123">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="db13b-124">**Lägg till program** i Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="db13b-124">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="db13b-125">Sök efter "Microsoft Partner Center", som är Microsoft Partner Center-programmet.</span><span class="sxs-lookup"><span data-stu-id="db13b-125">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="db13b-126">Ange **delegerade behörigheter** för **åtkomst till Partner Center API**.</span><span class="sxs-lookup"><span data-stu-id="db13b-126">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="db13b-127">Det här steget är obligatoriskt om du använder Partner Center för Microsoft Cloud Tyskland eller partner Center för Microsoft Cloud för amerikanska myndigheter.</span><span class="sxs-lookup"><span data-stu-id="db13b-127">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="db13b-128">Om du använder global instans av Partner Center är det här steget valfritt.</span><span class="sxs-lookup"><span data-stu-id="db13b-128">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="db13b-129">CSP-partner kan använda funktionen för hantering av appar i Partner Center-portalen för att kringgå det här steget för global instans av Partner Center.</span><span class="sxs-lookup"><span data-stu-id="db13b-129">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="db13b-130">Autentisering enbart appar</span><span class="sxs-lookup"><span data-stu-id="db13b-130">App-only authentication</span></span>

<span data-ttu-id="db13b-131">Om du vill använda endast app-autentisering för åtkomst till Partner Center REST API, .NET API, Java API eller PowerShell-modul kan du göra det genom att använda följande instruktioner.</span><span class="sxs-lookup"><span data-stu-id="db13b-131">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by leveraging the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="db13b-132">.NET (endast app-autentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-132">.NET (app-only authentication)</span></span>

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

## <a name="java-app-only-authentication"></a><span data-ttu-id="db13b-133">Java (endast app-autentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-133">Java (app-only authentication)</span></span>

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

## <a name="rest-app-only-authentication"></a><span data-ttu-id="db13b-134">REST (endast app-autentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-134">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="db13b-135">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="db13b-135">REST request</span></span>

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

### <a name="rest-response"></a><span data-ttu-id="db13b-136">REST-svar</span><span class="sxs-lookup"><span data-stu-id="db13b-136">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="db13b-137">App + användarautentisering</span><span class="sxs-lookup"><span data-stu-id="db13b-137">App + User authentication</span></span>

<span data-ttu-id="db13b-138">Tidigare har [tilldelningen av lösen ord för resurs ägare](https://tools.ietf.org/html/rfc6749#section-4.3) använts för att begära en åtkomsttoken för användning med Partner Center REST API, .NET API, Java API eller PowerShell-modul.</span><span class="sxs-lookup"><span data-stu-id="db13b-138">Historically the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="db13b-139">Den metoden användes för att begära en åtkomsttoken från Azure Active Directory att använda klient-ID och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="db13b-139">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="db13b-140">Den här metoden fungerar dock inte längre eftersom Partner Center kräver Multi-Factor Authentication när du använder app + User Authentication.</span><span class="sxs-lookup"><span data-stu-id="db13b-140">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="db13b-141">För att uppfylla detta krav har Microsoft infört ett säkert, skalbart ramverk för autentisering av CSP-partner (Cloud Solution Provider) och på kontroll panelens leverantörer (CPV) med Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="db13b-141">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="db13b-142">Det här ramverket kallas säker program modell och den består av en medgivande process och en begäran om åtkomsttoken med hjälp av en uppdateringstoken.</span><span class="sxs-lookup"><span data-stu-id="db13b-142">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="db13b-143">Partner medgivande</span><span class="sxs-lookup"><span data-stu-id="db13b-143">Partner consent</span></span>

<span data-ttu-id="db13b-144">Partner medgivande processen är en interaktiv process där partner autentiserar med Multi-Factor Authentication, samtycker till programmet och en uppdateringstoken lagras på en säker lagrings plats, till exempel Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="db13b-144">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="db13b-145">Vi rekommenderar att ett dedikerat konto för integrerings ändamål används för den här processen.</span><span class="sxs-lookup"><span data-stu-id="db13b-145">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db13b-146">Lämplig Multi-Factor Authentication-lösning ska vara aktive rad för det tjänst konto som används i partner medgivande processen.</span><span class="sxs-lookup"><span data-stu-id="db13b-146">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="db13b-147">Om den inte är det kommer den resulterande uppdateringstoken inte att vara kompatibel med säkerhets kraven.</span><span class="sxs-lookup"><span data-stu-id="db13b-147">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="db13b-148">Exempel för app + användarautentisering</span><span class="sxs-lookup"><span data-stu-id="db13b-148">Samples for App + User authentication</span></span>

<span data-ttu-id="db13b-149">Partner medgivande processen kan utföras på flera olika sätt.</span><span class="sxs-lookup"><span data-stu-id="db13b-149">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="db13b-150">Vi har utvecklat följande exempel för att hjälpa våra partner att förstå hur du utför varje nödvändig åtgärd.</span><span class="sxs-lookup"><span data-stu-id="db13b-150">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="db13b-151">När du implementerar lämplig lösning i din miljö är det viktigt att du utvecklar en lösning som följer dina kod standarder och säkerhets principer.</span><span class="sxs-lookup"><span data-stu-id="db13b-151">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="db13b-152">.NET (app + användarautentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-152">.NET (app+user authentication)</span></span>

<span data-ttu-id="db13b-153">[Partner medgivande](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) exempel projektet visar hur du använder en webbplats som har utvecklats med ASP.net för att avbilda medgivande, begära en uppdateringstoken och lagra den på ett säkert sätt i Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="db13b-153">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="db13b-154">Utför följande steg för att skapa nödvändiga komponenter för det här exemplet.</span><span class="sxs-lookup"><span data-stu-id="db13b-154">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="db13b-155">Skapa en instans av Azure Key Vault med hjälp av Azure Portal eller följande PowerShell-kommandon.</span><span class="sxs-lookup"><span data-stu-id="db13b-155">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="db13b-156">Innan du kör kommandot ska du se till att ändra parameter värden.</span><span class="sxs-lookup"><span data-stu-id="db13b-156">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="db13b-157">Valv namnet måste vara unikt.</span><span class="sxs-lookup"><span data-stu-id="db13b-157">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="db13b-158">Mer information om hur du skapar en Azure Key Vault finns i [snabb start: Ange och hämta en hemlighet från Azure Key Vault med Azure Portal](/azure/key-vault/quick-create-portal) eller [snabb start: Ange och hämta en hemlighet från Azure Key Vault med PowerShell](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="db13b-158">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="db13b-159">Ange och hämta en hemlighet.</span><span class="sxs-lookup"><span data-stu-id="db13b-159">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="db13b-160">Skapa ett Azure AD-program och en nyckel med hjälp av Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="db13b-160">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="db13b-161">Se till att anteckna program identifieraren och de hemliga värdena eftersom de används i stegen nedan.</span><span class="sxs-lookup"><span data-stu-id="db13b-161">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="db13b-162">Ge den nya Azure AD-appen behörigheten Läs hemligheter med hjälp av Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="db13b-162">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="db13b-163">Skapa ett Azure AD-program som är konfigurerat för partner Center.</span><span class="sxs-lookup"><span data-stu-id="db13b-163">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="db13b-164">Utför följande åtgärder för att slutföra det här steget.</span><span class="sxs-lookup"><span data-stu-id="db13b-164">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="db13b-165">Bläddra till [appens hanterings](https://partner.microsoft.com/pcv/apiintegration/appmanagement) funktion i instrument panelen för partner Center</span><span class="sxs-lookup"><span data-stu-id="db13b-165">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="db13b-166">Skapa en ny Azure AD-app genom att klicka på *Lägg till ny webbapp* .</span><span class="sxs-lookup"><span data-stu-id="db13b-166">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="db13b-167">Se till att dokumentera *app-ID*, \* konto-ID \* \* och *nyckel* värden eftersom de används i stegen nedan.</span><span class="sxs-lookup"><span data-stu-id="db13b-167">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="db13b-168">Klona databasen [partner Center-dotNet-samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando.</span><span class="sxs-lookup"><span data-stu-id="db13b-168">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="db13b-169">Öppna det *PartnerConsent* -projekt som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen.</span><span class="sxs-lookup"><span data-stu-id="db13b-169">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="db13b-170">Fyll i de program inställningar som finns i [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span><span class="sxs-lookup"><span data-stu-id="db13b-170">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

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
    > <span data-ttu-id="db13b-171">Känslig information som program hemligheter bör inte lagras i konfigurationsfiler.</span><span class="sxs-lookup"><span data-stu-id="db13b-171">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="db13b-172">Den gjordes här eftersom det är ett exempel program.</span><span class="sxs-lookup"><span data-stu-id="db13b-172">It was done here because this is a sample application.</span></span> <span data-ttu-id="db13b-173">Med ditt produktions program rekommenderar vi starkt att du använder certifikatbaserad autentisering.</span><span class="sxs-lookup"><span data-stu-id="db13b-173">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="db13b-174">Mer information finns i [autentiseringsuppgifter för certifikat för programautentisering]( /azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="db13b-174">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="db13b-175">När du kör det här exempelprojektet kommer du att uppmanas att autentisera dig.</span><span class="sxs-lookup"><span data-stu-id="db13b-175">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="db13b-176">När autentiseringen är klar begärs en åtkomsttoken från Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db13b-176">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="db13b-177">Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="db13b-177">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="db13b-178">Java (app + User Authentication)</span><span class="sxs-lookup"><span data-stu-id="db13b-178">Java (app+user authentication)</span></span>

<span data-ttu-id="db13b-179">[Partner medgivande](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) exempel projektet visar hur du använder en webbplats som utvecklats med JSP för att fånga in medgivande, begära en uppdateringstoken och säker lagring i Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="db13b-179">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="db13b-180">Utför följande för att skapa nödvändiga komponenter för det här exemplet.</span><span class="sxs-lookup"><span data-stu-id="db13b-180">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="db13b-181">Skapa en instans av Azure Key Vault med hjälp av Azure Portal eller följande PowerShell-kommandon.</span><span class="sxs-lookup"><span data-stu-id="db13b-181">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="db13b-182">Innan du kör kommandot ska du se till att ändra parameter värden.</span><span class="sxs-lookup"><span data-stu-id="db13b-182">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="db13b-183">Valv namnet måste vara unikt.</span><span class="sxs-lookup"><span data-stu-id="db13b-183">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="db13b-184">Mer information om hur du skapar en Azure Key Vault finns i [snabb start: Ange och hämta en hemlighet från Azure Key Vault med Azure Portal](/azure/key-vault/quick-create-portal) eller [snabb start: Ange och hämta en hemlighet från Azure Key Vault med PowerShell](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="db13b-184">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="db13b-185">Skapa ett Azure AD-program och en nyckel med hjälp av Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="db13b-185">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="db13b-186">Se till att dokumentera program identifieraren och de hemliga värdena eftersom de används i stegen nedan.</span><span class="sxs-lookup"><span data-stu-id="db13b-186">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="db13b-187">Ge det nya Azure AD-programmet behörigheten Läs hemligheter med hjälp av Azure Portal eller följande kommandon.</span><span class="sxs-lookup"><span data-stu-id="db13b-187">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="db13b-188">Skapa ett Azure AD-program som är konfigurerat för partner Center.</span><span class="sxs-lookup"><span data-stu-id="db13b-188">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="db13b-189">Utför följande för att slutföra det här steget.</span><span class="sxs-lookup"><span data-stu-id="db13b-189">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="db13b-190">Bläddra till [appens hanterings](https://partner.microsoft.com/pcv/apiintegration/appmanagement) funktion i instrument panelen för partner Center</span><span class="sxs-lookup"><span data-stu-id="db13b-190">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="db13b-191">Skapa en ny Azure AD-app genom att klicka på *Lägg till ny webbapp* .</span><span class="sxs-lookup"><span data-stu-id="db13b-191">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="db13b-192">Se till att dokumentera *app-ID*, \* konto-ID \* \* och *nyckel* värden eftersom de används i stegen nedan.</span><span class="sxs-lookup"><span data-stu-id="db13b-192">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="db13b-193">Klona databasen [partner Center-Java-samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando</span><span class="sxs-lookup"><span data-stu-id="db13b-193">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="db13b-194">Öppna det *PartnerConsent* -projekt som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen.</span><span class="sxs-lookup"><span data-stu-id="db13b-194">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="db13b-195">Fyll i de program inställningar som finns i [web.xmls ](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) filen</span><span class="sxs-lookup"><span data-stu-id="db13b-195">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

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
    > <span data-ttu-id="db13b-196">Känslig information som program hemligheter bör inte lagras i konfigurationsfiler.</span><span class="sxs-lookup"><span data-stu-id="db13b-196">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="db13b-197">Den gjordes här eftersom det är ett exempel program.</span><span class="sxs-lookup"><span data-stu-id="db13b-197">It was done here because this is a sample application.</span></span> <span data-ttu-id="db13b-198">Med ditt produktions program rekommenderar vi starkt att du använder certifikatbaserad autentisering.</span><span class="sxs-lookup"><span data-stu-id="db13b-198">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="db13b-199">Mer information finns i [Key Vault certifikatautentisering](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="db13b-199">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="db13b-200">När du kör det här exempelprojektet kommer du att uppmanas att autentisera dig.</span><span class="sxs-lookup"><span data-stu-id="db13b-200">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="db13b-201">När autentiseringen är klar begärs en åtkomsttoken från Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db13b-201">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="db13b-202">Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="db13b-202">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="db13b-203">Cloud Solution Provider-autentisering</span><span class="sxs-lookup"><span data-stu-id="db13b-203">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="db13b-204">Leverantörer av moln lösningar kan använda den uppdateringstoken som erhållits genom [partner medgivande](#partner-consent) processen.</span><span class="sxs-lookup"><span data-stu-id="db13b-204">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="db13b-205">Exempel för autentisering av moln lösnings leverantör</span><span class="sxs-lookup"><span data-stu-id="db13b-205">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="db13b-206">Vi har utvecklat följande exempel för att hjälpa våra partner att förstå hur du utför varje nödvändig åtgärd.</span><span class="sxs-lookup"><span data-stu-id="db13b-206">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="db13b-207">När du implementerar lämplig lösning i din miljö är det viktigt att du utvecklar en lösning som följer dina kod standarder och säkerhets principer.</span><span class="sxs-lookup"><span data-stu-id="db13b-207">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="db13b-208">.NET (CSP-autentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-208">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="db13b-209">Om du inte redan har gjort det kan du genomföra [partner medgivande processen](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="db13b-209">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="db13b-210">Klona [partner-Center-dotNet-samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) -lagringsplatsen med Visual Studio eller följande kommando</span><span class="sxs-lookup"><span data-stu-id="db13b-210">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="db13b-211">Öppna `CSPApplication` projektet som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen.</span><span class="sxs-lookup"><span data-stu-id="db13b-211">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="db13b-212">Uppdatera program inställningarna som finns i [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) -filen.</span><span class="sxs-lookup"><span data-stu-id="db13b-212">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="db13b-213">Ange lämpliga värden för variablerna **partner** och **CustomerId** som finns i [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) -filen.</span><span class="sxs-lookup"><span data-stu-id="db13b-213">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="db13b-214">När du kör det här exempelprojektet hämtas den uppdateringstoken som hämtades under partner medgivande processen.</span><span class="sxs-lookup"><span data-stu-id="db13b-214">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="db13b-215">Sedan begär den en åtkomsttoken för att interagera med partner Center SDK för partnerns räkning.</span><span class="sxs-lookup"><span data-stu-id="db13b-215">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="db13b-216">Slutligen begär den en åtkomsttoken för att interagera med Microsoft Graph för den angivna kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="db13b-216">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="db13b-217">Java (CSP-autentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-217">Java (CSP authentication)</span></span>

1. <span data-ttu-id="db13b-218">Om du inte redan har gjort det kan du genomföra [partner medgivande processen](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="db13b-218">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="db13b-219">Klona databasen [partner Center-Java-samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med Visual Studio eller följande kommando</span><span class="sxs-lookup"><span data-stu-id="db13b-219">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="db13b-220">Öppna `cspsample` projektet som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen.</span><span class="sxs-lookup"><span data-stu-id="db13b-220">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="db13b-221">Uppdatera program inställningarna som finns i filen [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) .</span><span class="sxs-lookup"><span data-stu-id="db13b-221">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="db13b-222">När du kör det här exempelprojektet hämtas den uppdateringstoken som hämtades under partner medgivande processen.</span><span class="sxs-lookup"><span data-stu-id="db13b-222">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="db13b-223">Sedan begär den en åtkomsttoken för att interagera med partner Center SDK för partnerns räkning.</span><span class="sxs-lookup"><span data-stu-id="db13b-223">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="db13b-224">Valfritt-ta bort kommentarer till funktions anropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="db13b-224">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="db13b-225">Autentisering på kontroll panelens Provider</span><span class="sxs-lookup"><span data-stu-id="db13b-225">Control Panel Provider authentication</span></span>

<span data-ttu-id="db13b-226">Leverantörer av kontroll panelen måste ha varje partner som de har stöd för att genomföra [partner medgivande](#partner-consent) processen.</span><span class="sxs-lookup"><span data-stu-id="db13b-226">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="db13b-227">När den uppdaterade token som har hämtats till den här processen används för att komma åt Partner Center REST API och .NET API.</span><span class="sxs-lookup"><span data-stu-id="db13b-227">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="db13b-228">Exempel för autentisering med moln panels leverantör</span><span class="sxs-lookup"><span data-stu-id="db13b-228">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="db13b-229">Vi har utvecklat följande exempel för att hjälpa leverantörer i kontroll panelen att förstå hur man utför varje nödvändig åtgärd.</span><span class="sxs-lookup"><span data-stu-id="db13b-229">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="db13b-230">När du implementerar lämplig lösning i din miljö är det viktigt att du utvecklar en lösning som följer dina kod standarder och säkerhets principer.</span><span class="sxs-lookup"><span data-stu-id="db13b-230">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="db13b-231">.NET (CPV-autentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-231">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="db13b-232">Utveckla och distribuera en process för leverantörer av moln lösningar för att tillhandahålla ett lämpligt medgivande.</span><span class="sxs-lookup"><span data-stu-id="db13b-232">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="db13b-233">Mer information ett exempel finns i [partner medgivande](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="db13b-233">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="db13b-234">Användarens autentiseringsuppgifter från en moln lösnings leverantörs partner ska inte lagras.</span><span class="sxs-lookup"><span data-stu-id="db13b-234">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="db13b-235">Den uppdateringstoken som erhållits genom partner medgivande processen bör lagras och användas för att begära åtkomsttoken för att interagera med alla Microsoft-API: er.</span><span class="sxs-lookup"><span data-stu-id="db13b-235">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="db13b-236">Klona [partner-Center-dotNet-samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) -lagringsplatsen med Visual Studio eller följande kommando</span><span class="sxs-lookup"><span data-stu-id="db13b-236">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="db13b-237">Öppna `CPVApplication` projektet som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen.</span><span class="sxs-lookup"><span data-stu-id="db13b-237">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="db13b-238">Uppdatera program inställningarna som finns i [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) -filen.</span><span class="sxs-lookup"><span data-stu-id="db13b-238">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="db13b-239">Ange lämpliga värden för variablerna **partner** och **CustomerId** som finns i [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) -filen.</span><span class="sxs-lookup"><span data-stu-id="db13b-239">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="db13b-240">När du kör det här exempel projektet hämtar den uppdateringstoken för den angivna partnern.</span><span class="sxs-lookup"><span data-stu-id="db13b-240">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="db13b-241">Sedan begär den en åtkomsttoken för att komma åt Partner Center och Azure AD Graph åt partnern.</span><span class="sxs-lookup"><span data-stu-id="db13b-241">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="db13b-242">Nästa uppgift är att ta bort och skapa behörighets bidrag till kund innehavaren.</span><span class="sxs-lookup"><span data-stu-id="db13b-242">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="db13b-243">Eftersom det inte finns någon relation mellan kontroll panelens tillverkare och kunden måste dessa behörigheter läggas till med partner Center-API: et.</span><span class="sxs-lookup"><span data-stu-id="db13b-243">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="db13b-244">I följande exempel visas hur du utför det.</span><span class="sxs-lookup"><span data-stu-id="db13b-244">The following example shows how to accomplish that.</span></span>

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

<span data-ttu-id="db13b-245">När de här behörigheterna har upprättats utför exemplet åtgärder med Azure AD Graph för kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="db13b-245">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="db13b-246">Java (CPV-autentisering)</span><span class="sxs-lookup"><span data-stu-id="db13b-246">Java (CPV authentication)</span></span>

1. <span data-ttu-id="db13b-247">Utveckla och distribuera en process för leverantörer av moln lösningar för att tillhandahålla ett lämpligt medgivande.</span><span class="sxs-lookup"><span data-stu-id="db13b-247">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="db13b-248">Mer information och ett exempel finns i [partner medgivande](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="db13b-248">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="db13b-249">Användarens autentiseringsuppgifter från en moln lösnings leverantörs partner ska inte lagras.</span><span class="sxs-lookup"><span data-stu-id="db13b-249">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="db13b-250">Den uppdateringstoken som erhållits genom partner medgivande processen bör lagras och användas för att begära åtkomsttoken för att interagera med alla Microsoft-API: er.</span><span class="sxs-lookup"><span data-stu-id="db13b-250">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="db13b-251">Klona databasen [partner Center-Java-samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando</span><span class="sxs-lookup"><span data-stu-id="db13b-251">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="db13b-252">Öppna `cpvsample` projektet som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen.</span><span class="sxs-lookup"><span data-stu-id="db13b-252">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="db13b-253">Uppdatera program inställningarna som finns i filen [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) .</span><span class="sxs-lookup"><span data-stu-id="db13b-253">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

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

    <span data-ttu-id="db13b-254">Värdet för `partnercenter.displayName` ska vara visnings namnet för ditt Marketplace-program.</span><span class="sxs-lookup"><span data-stu-id="db13b-254">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="db13b-255">Ange lämpliga värden för variablerna **partner** och **customerId** som finns i filen [program. java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) .</span><span class="sxs-lookup"><span data-stu-id="db13b-255">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="db13b-256">När du kör det här exempel projektet hämtar den uppdateringstoken för den angivna partnern.</span><span class="sxs-lookup"><span data-stu-id="db13b-256">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="db13b-257">Sedan begär den en åtkomsttoken för åtkomst till Partner Center för partnerns räkning.</span><span class="sxs-lookup"><span data-stu-id="db13b-257">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="db13b-258">Nästa uppgift är att ta bort och skapa behörighets bidrag till kund innehavaren.</span><span class="sxs-lookup"><span data-stu-id="db13b-258">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="db13b-259">Eftersom det inte finns någon relation mellan kontroll panelens tillverkare och kunden måste dessa behörigheter läggas till med partner Center-API: et.</span><span class="sxs-lookup"><span data-stu-id="db13b-259">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="db13b-260">I följande exempel visas hur du beviljar behörigheterna.</span><span class="sxs-lookup"><span data-stu-id="db13b-260">The following example shows how to grant the permissions.</span></span>

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

<span data-ttu-id="db13b-261">Ta bort kommentarer till funktions anropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="db13b-261">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
