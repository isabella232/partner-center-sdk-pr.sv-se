---
title: Partner Center-autentisering
description: Partner center använder Azure AD för autentisering och för att använda Partner Center-API:er måste du konfigurera autentiseringsinställningarna korrekt.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 75d60ca983cd5b8fe53134ec7481319b153e128a
ms.sourcegitcommit: 07b9a11f5c615ed1e716081392032cea2124bd98
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/04/2021
ms.locfileid: "115104201"
---
# <a name="partner-center-authentication"></a>Partner Center-autentisering

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Partnercenter använder Azure Active Directory för autentisering. När du interagerar med Partnercenter-API, SDK eller PowerShell-modulen måste du konfigurera ett Azure AD-program korrekt och sedan begära en åtkomsttoken. Åtkomsttoken som hämtas med endast appen eller app - och användarautentisering kan användas med Partnercenter. Det finns dock två viktiga objekt som måste beaktas

- Använd multifaktorautentisering vid åtkomst till Partner center-API:et med hjälp av app - och användarautentisering. Mer information om den här ändringen finns i [Aktivera säker programmodell.](enable-secure-app-model.md)

- Inte alla åtgärder som Partner Center-API:et stöder endast appautentisering. Det finns vissa scenarier där du måste använda app - och användarautentisering. Under rubriken *Förutsättningar i* varje artikel [hittar](scenarios.md)du dokumentation som anger om endast appautentisering, app + användarautentisering eller båda stöds.

## <a name="initial-setup"></a>Inledande konfiguration

1. För att börja måste du se till att du har både ett primärt PartnerCenter-konto och ett PartnerCenter-konto för sandbox-integrering. Mer information finns i Konfigurera [Partner Center-konton för API-åtkomst.](set-up-api-access-in-partner-center.md) Anteckna registrerings-ID:t och hemligheten för Azure AAD-appen (klienthemlighet krävs endast för identifiering av appar) för både ditt primära konto och ditt sandbox-konto för integrering.

2. Logga in på Azure AD från Azure Portal. I **behörigheter till andra program** anger du behörigheter för **Windows Azure Active Directory** delegerade behörigheter **och** väljer både Access the directory as **the signed-in user** (Åtkomst till katalogen som den inloggade användaren) och Sign in and read user profile (Logga in och läs **användarprofil).**

3. I Azure Portal Lägg **till program**. Sök efter "Microsoft Partner Center", som är Microsoft Partner Center-programmet. Ange **delegerade behörigheter för** åtkomst **till Partner Center API.** Om du använder Partnercenter för Microsoft Cloud Tyskland eller Partnercenter för Microsoft Cloud for US Government är det här steget obligatoriskt. Om du använder global instans i Partnercenter är det här steget valfritt. CSP-partner kan använda apphanteringsfunktionen i Partnercenter-portalen för att kringgå det här steget för global Partner Center-instans.

## <a name="app-only-authentication"></a>Appbaserad autentisering

Om du vill använda appbaserad autentisering för att få åtkomst till Partner Center-modulen REST API, .NET API, Java API eller PowerShell kan du göra det med hjälp av följande anvisningar.

## <a name="net-app-only-authentication"></a>.NET (appbaserad autentisering)

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

## <a name="java-app-only-authentication"></a>Java (endast appautentisering)

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

## <a name="rest-app-only-authentication"></a>REST (appbaserad autentisering)

### <a name="rest-request"></a>REST-begäran

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

### <a name="rest-response"></a>REST-svar

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>App + användarautentisering

Tidigare har [](https://tools.ietf.org/html/rfc6749#section-4.3) beviljandet av autentiseringsuppgifter för resursägares lösenord använts för att begära en åtkomsttoken för användning med partnercenter-REST API-, .NET-API-, Java API- eller PowerShell-modulen. Den metoden användes för att begära en åtkomsttoken från Azure Active Directory med en klientidentifierare och användarautentiseringsuppgifter. Den här metoden fungerar dock inte längre eftersom Partnercenter kräver multifaktorautentisering när du använder app - och användarautentisering. För att uppfylla detta krav har Microsoft infört ett säkert, skalbart ramverk för autentisering av Molnlösningsleverantör-partner (CSP) och kontrollpanelens leverantörer (CPV) med hjälp av multifaktorautentisering. Det här ramverket kallas för Modell för säkra program och består av en medgivandeprocess och en begäran om en åtkomsttoken med hjälp av en uppdateringstoken.

### <a name="partner-consent"></a>Partnermedgivande

Processen för partnermedgivande är en interaktiv process där partnern autentiseras med hjälp av multifaktorautentisering, medgivanden till programmet och en uppdateringstoken lagras på en säker lagringsplats, till exempel Azure Key Vault. Vi rekommenderar att du använder ett dedikerat konto för integrering i den här processen.

> [!IMPORTANT]
> Lämplig multifaktorautentiseringslösning ska aktiveras för det tjänstkonto som används i partnerns medgivandeprocess. Om den inte är det kommer den resulterande uppdateringstoken inte att vara kompatibel med säkerhetskraven.

### <a name="samples-for-app--user-authentication"></a>Exempel för app - och användarautentisering

Processen för partnermedgivande kan utföras på flera olika sätt. För att hjälpa partner att förstå hur de utför varje åtgärd som krävs har vi utvecklat följande exempel. När du implementerar rätt lösning i din miljö är det viktigt att du utvecklar en lösning som är klagomål mot kodningsstandarder och säkerhetsprinciper.

## <a name="net-appuser-authentication"></a>.NET (app+användarautentisering)

Exempelprojektet [för partnermedgivande](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) visar hur du använder en webbplats som utvecklats med ASP.NET för att samla in medgivande, begära en uppdateringstoken och på ett säkert sätt lagra den i Azure Key Vault. Utför följande steg för att skapa de nödvändiga förutsättningarna för det här exemplet.

1. Skapa en instans av Azure Key Vault med hjälp Azure Portal eller följande PowerShell-kommandon. Innan du kör kommandot måste du ändra parametervärdena därefter. Valvnamnet måste vara unikt.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Mer information om hur du skapar en Azure Key Vault finns i [Snabbstart:](/azure/key-vault/quick-create-portal) Ange och hämta en hemlighet från Azure Key Vault med hjälp av Azure Portal eller [Snabbstart: Ange](/azure/key-vault/quick-create-powershell)och hämta en hemlighet från Azure Key Vault med Hjälp av PowerShell . Ange och hämta sedan en hemlighet.

2. Skapa ett Azure AD-program och en nyckel med Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Se till att anteckna värdena för programidentifierare och hemligheter eftersom de kommer att användas i stegen nedan.

3. Ge det nyligen skapade Azure AD-programmet läshemlighetsbehörigheter med hjälp Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Skapa ett Azure AD-program som har konfigurerats för Partnercenter. Utför följande åtgärder för att slutföra det här steget.

    - Bläddra till [apphanteringsfunktionen](https://partner.microsoft.com/pcv/apiintegration/appmanagement) i instrumentpanelen i Partnercenter
    - Välj *Lägg till ny webbapp* för att skapa ett nytt Azure AD-program.

    Se till att dokumentera *värdena app-ID,**konto-ID** och nyckel eftersom de kommer att användas i stegen nedan. 

5. Klona [lagringsplatsen Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Öppna projektet *PartnerConsent* som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen .

7. Fyll i programinställningarna som finns i [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > Känslig information, till exempel programhemligheter, bör inte lagras i konfigurationsfiler. Det gjordes här eftersom det här är ett exempelprogram. Med ditt produktionsprogram rekommenderar vi starkt att du använder certifikatbaserad autentisering. Mer information finns i [Certifikatautentiseringsuppgifter för programautentisering.]( /azure/active-directory/develop/active-directory-certificate-credentials)

8. När du kör det här exempelprojektet uppmanas du att autentisera dig. När autentiseringen är klar begärs en åtkomsttoken från Azure AD. Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (app+användarautentisering)

Exempelprojektet [för partnermedgivande](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) visar hur du använder en webbplats som utvecklats med JSP för att samla in medgivande, begära en uppdateringstoken och skydda lagring i Azure Key Vault. Utför följande för att skapa de nödvändiga förutsättningarna för det här exemplet.

1. Skapa en instans av Azure Key Vault med hjälp Azure Portal eller följande PowerShell-kommandon. Innan du kör kommandot måste du ändra parametervärdena därefter. Valvnamnet måste vara unikt.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Mer information om hur du skapar en Azure Key Vault finns i [Snabbstart:](/azure/key-vault/quick-create-portal) Ange och hämta en hemlighet från Azure Key Vault med hjälp av Azure Portal eller [Snabbstart: Ange](/azure/key-vault/quick-create-powershell)och hämta en hemlighet från Azure Key Vault med Hjälp av PowerShell .

2. Skapa ett Azure AD-program och en nyckel med Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Se till att dokumentera värdena för programidentifierare och hemligheter eftersom de kommer att användas i stegen nedan.

3. Ge det nyligen skapade Azure AD-programmet läshemlighetsbehörighet med hjälp Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Skapa ett Azure AD-program som har konfigurerats för Partnercenter. Utför följande för att slutföra det här steget.

    - Bläddra till [apphanteringsfunktionen](https://partner.microsoft.com/pcv/apiintegration/appmanagement) i instrumentpanelen i Partnercenter
    - Välj *Lägg till ny webbapp* för att skapa ett nytt Azure AD-program.

    Se till att dokumentera *värdena app-ID,**konto-ID** och nyckel eftersom de kommer att användas i stegen nedan. 

5. Klona [lagringsplatsen Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Öppna projektet *PartnerConsent* som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen .

7. Fyll i programinställningarna som finns i [web.xmlfilen](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)

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
    > Känslig information, till exempel programhemligheter, bör inte lagras i konfigurationsfiler. Det gjordes här eftersom det här är ett exempelprogram. Med ditt produktionsprogram rekommenderar vi starkt att du använder certifikatbaserad autentisering. Mer information finns i Key Vault [certifikatautentisering](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. När du kör det här exempelprojektet uppmanas du att autentisera dig. När autentiseringen är klar begärs en åtkomsttoken från Azure AD. Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Molnlösningsleverantör autentisering

Molnlösningsleverantör partner kan använda den uppdateringstoken som erhållits via [processen för partnermedgivande.](#partner-consent)

### <a name="samples-for-cloud-solution-provider-authentication"></a>Exempel för Molnlösningsleverantör autentisering

För att hjälpa partner att förstå hur de utför varje åtgärd som krävs har vi utvecklat följande exempel. När du implementerar rätt lösning i din miljö är det viktigt att du utvecklar en lösning som är klagomål mot kodningsstandarder och säkerhetsprinciper.

## <a name="net-csp-authentication"></a>.NET (CSP-autentisering)

1. Om du inte redan har gjort det utför du [processen för partnermedgivande.](#partner-consent)

2. Klona [lagringsplatsen Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Öppna projektet `CSPApplication` som finns i katalogen `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .

4. Uppdatera programinställningarna som [](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) finns iApp.configfilen.

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

5. Ange lämpliga värden för **variablerna PartnerId** **och CustomerId** som finns i [filen Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. När du kör det här exempelprojektet hämtas den uppdateringstoken som erhölls under partnerns medgivandeprocess. Sedan begär den en åtkomsttoken för att interagera Partnercenter-SDK för partnerns räkning. Slutligen begär den en åtkomsttoken för att interagera med Microsoft Graph åt den angivna kunden.

## <a name="java-csp-authentication"></a>Java (CSP-autentisering)

1. Om du inte redan har gjort det utför du [processen för partnermedgivande.](#partner-consent)

2. Klona [lagringsplatsen Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med Visual Studio eller följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Öppna projektet `cspsample` som finns i katalogen `Partner-Center-Java-Samples\secure-app-model\keyvault` .

4. Uppdatera programinställningarna som finns i [filen application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. När du kör det här exempelprojektet hämtas den uppdateringstoken som erhölls under partnerns medgivandeprocess. Sedan begär den en åtkomsttoken för att interagera Partnercenter-SDK för partnerns räkning.

6. Valfritt – avkommentera funktionsanropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.

## <a name="control-panel-provider-authentication"></a>Kontrollpanelen providerautentisering

Kontrollpanelens leverantörer måste ha varje partner som de stöder för att utföra [processen för partnermedgivande.](#partner-consent) När det är klart används den uppdateringstoken som hämtas via den processen för att få åtkomst till Partner Center REST API och .NET API.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Exempel för autentisering av molnpanelsprovider

För att hjälpa kontrollpanelens leverantörer att förstå hur de utför varje åtgärd som krävs har vi utvecklat följande exempel. När du implementerar rätt lösning i din miljö är det viktigt att du utvecklar en lösning som är klagomål mot kodningsstandarder och säkerhetsprinciper.

## <a name="net-cpv-authentication"></a>.NET (CPV-autentisering)

1. Utveckla och distribuera en process för Molnlösningsleverantör partner för att ge lämpligt medgivande. Mer information om ett exempel finns i [Medgivande från partner.](#partner-consent)

    > [!IMPORTANT]
    > Användarautentiseringsuppgifter från Molnlösningsleverantör partner ska inte lagras. Uppdateringstoken som erhålls via partnerns medgivandeprocess ska lagras och användas för att begära åtkomsttoken för interaktion med microsoft-API:er.

2. Klona [lagringsplatsen Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Öppna projektet `CPVApplication` som finns i katalogen `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .

4. Uppdatera programinställningarna som [](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) finns iApp.configfilen.

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

5. Ange lämpliga värden för **variablerna PartnerId** **och CustomerId** som finns i [filen Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. När du kör det här exempelprojektet hämtar det uppdateringstoken för den angivna partnern. Sedan begär den en åtkomsttoken för att få åtkomst till Partnercenter och Azure AD Graph åt partnern. Nästa uppgift som den utför är att ta bort och skapa behörighetsstipendier till kundens klientorganisation. Eftersom det inte finns någon relation mellan kontrollpanelens leverantör och kunden måste dessa behörigheter läggas till med partnercenter-API:et. I följande exempel visas hur du gör det.

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

När dessa behörigheter har upprättats utför exemplet åtgärder med hjälp av Azure AD Graph för kundens räkning.

## <a name="java-cpv-authentication"></a>Java (CPV-autentisering)

1. Utveckla och distribuera en process för Molnlösningsleverantör partner för att ge lämpligt medgivande. Mer information och ett exempel finns i [medgivande från partnern.](#partner-consent)

    > [!IMPORTANT]
    > Användarautentiseringsuppgifter från Molnlösningsleverantör partner ska inte lagras. Uppdateringstoken som erhålls via partnerns medgivandeprocess ska lagras och användas för att begära åtkomsttoken för interaktion med microsoft-API:er.

2. Klona [lagringsplatsen Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Öppna projektet `cpvsample` som finns i katalogen `Partner-Center-Java-Samples\secure-app-model\keyvault` .

4. Uppdatera programinställningarna som finns i [filen application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)

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

    Värdet för ska `partnercenter.displayName` vara visningsnamnet för ditt Marketplace-program.

5. Ange lämpliga värden för **variablerna partnerId** **och customerId** som finns i [filen Program.java.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. När du kör det här exempelprojektet hämtar det uppdateringstoken för den angivna partnern. Sedan begär den en åtkomsttoken för att få åtkomst till Partnercenter för partnerns räkning. Nästa uppgift som den utför är att ta bort och skapa behörighetsstipendier till kundens klientorganisation. Eftersom det inte finns någon relation mellan kontrollpanelens leverantör och kunden måste dessa behörigheter läggas till med partnercenter-API:et. I följande exempel visas hur du beviljar behörigheterna.

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

Avkommentera funktionsanropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.
