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
# <a name="partner-center-authentication"></a>Partner Center-autentisering

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Partnercenter använder Azure Active Directory för autentisering. När du interagerar med Partnercenter-API, SDK eller PowerShell-modulen måste du konfigurera ett Azure AD-program korrekt och sedan begära en åtkomsttoken. Åtkomst-token som hämtats med endast app eller app + User Authentication kan användas med partner Center. Det finns dock två viktiga objekt som måste beaktas

- Använd Multi-Factor Authentication vid åtkomst till API: et för partner Center med app + User Authentication. Mer information om den här ändringen finns i [Aktivera säker program modell](enable-secure-app-model.md).

- Inte alla åtgärder som partner Center API-stöd för endast appens autentisering. Det finns vissa scenarier där du måste använda app + User Authentication. Under rubriken *krav* för varje [artikel](scenarios.md)hittar du dokumentation som anger om endast appens autentisering, app + användarautentisering eller båda stöds.

## <a name="initial-setup"></a>Första konfigurationen

1. Innan du börjar måste du kontrol lera att du har både ett primärt Partner Center konto och ett konto för integrations Center för integration. Mer information finns i [Konfigurera Partner Center-konton för API-åtkomst](set-up-api-access-in-partner-center.md). Anteckna registrerings-ID och hemlighet för Azure AAD-appen (klient hemlighet krävs endast för identifiering av appar) för både ditt primära konto och ditt konto för integration sandbox.

2. Logga in på Azure AD från Azure Portal. Ange behörigheter för **Windows-Azure Active Directory** till **delegerade behörigheter** i **behörigheter till andra program** och välj både **åtkomst till katalogen som den inloggade användaren** och **Logga in och Läs användar profilen**.

3. **Lägg till program** i Azure Portal. Sök efter "Microsoft Partner Center", som är Microsoft Partner Center-programmet. Ange **delegerade behörigheter** för **åtkomst till Partner Center API**. Det här steget är obligatoriskt om du använder Partner Center för Microsoft Cloud Tyskland eller partner Center för Microsoft Cloud för amerikanska myndigheter. Om du använder global instans av Partner Center är det här steget valfritt. CSP-partner kan använda funktionen för hantering av appar i Partner Center-portalen för att kringgå det här steget för global instans av Partner Center.

## <a name="app-only-authentication"></a>Autentisering enbart appar

Om du vill använda endast app-autentisering för åtkomst till Partner Center REST API, .NET API, Java API eller PowerShell-modul kan du göra det genom att använda följande instruktioner.

## <a name="net-app-only-authentication"></a>.NET (endast app-autentisering)

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

## <a name="java-app-only-authentication"></a>Java (endast app-autentisering)

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

## <a name="rest-app-only-authentication"></a>REST (endast app-autentisering)

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

Tidigare har [tilldelningen av lösen ord för resurs ägare](https://tools.ietf.org/html/rfc6749#section-4.3) använts för att begära en åtkomsttoken för användning med Partner Center REST API, .NET API, Java API eller PowerShell-modul. Den metoden användes för att begära en åtkomsttoken från Azure Active Directory att använda klient-ID och användarautentiseringsuppgifter. Den här metoden fungerar dock inte längre eftersom Partner Center kräver Multi-Factor Authentication när du använder app + User Authentication. För att uppfylla detta krav har Microsoft infört ett säkert, skalbart ramverk för autentisering av CSP-partner (Cloud Solution Provider) och på kontroll panelens leverantörer (CPV) med Multi-Factor Authentication. Det här ramverket kallas säker program modell och den består av en medgivande process och en begäran om åtkomsttoken med hjälp av en uppdateringstoken.

### <a name="partner-consent"></a>Partner medgivande

Partner medgivande processen är en interaktiv process där partner autentiserar med Multi-Factor Authentication, samtycker till programmet och en uppdateringstoken lagras på en säker lagrings plats, till exempel Azure Key Vault. Vi rekommenderar att ett dedikerat konto för integrerings ändamål används för den här processen.

> [!IMPORTANT]
> Lämplig Multi-Factor Authentication-lösning ska vara aktive rad för det tjänst konto som används i partner medgivande processen. Om den inte är det kommer den resulterande uppdateringstoken inte att vara kompatibel med säkerhets kraven.

### <a name="samples-for-app--user-authentication"></a>Exempel för app + användarautentisering

Partner medgivande processen kan utföras på flera olika sätt. Vi har utvecklat följande exempel för att hjälpa våra partner att förstå hur du utför varje nödvändig åtgärd. När du implementerar lämplig lösning i din miljö är det viktigt att du utvecklar en lösning som följer dina kod standarder och säkerhets principer.

## <a name="net-appuser-authentication"></a>.NET (app + användarautentisering)

[Partner medgivande](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) exempel projektet visar hur du använder en webbplats som har utvecklats med ASP.net för att avbilda medgivande, begära en uppdateringstoken och lagra den på ett säkert sätt i Azure Key Vault. Utför följande steg för att skapa nödvändiga komponenter för det här exemplet.

1. Skapa en instans av Azure Key Vault med hjälp av Azure Portal eller följande PowerShell-kommandon. Innan du kör kommandot ska du se till att ändra parameter värden. Valv namnet måste vara unikt.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Mer information om hur du skapar en Azure Key Vault finns i [snabb start: Ange och hämta en hemlighet från Azure Key Vault med Azure Portal](/azure/key-vault/quick-create-portal) eller [snabb start: Ange och hämta en hemlighet från Azure Key Vault med PowerShell](/azure/key-vault/quick-create-powershell). Ange och hämta en hemlighet.

2. Skapa ett Azure AD-program och en nyckel med hjälp av Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Se till att anteckna program identifieraren och de hemliga värdena eftersom de används i stegen nedan.

3. Ge den nya Azure AD-appen behörigheten Läs hemligheter med hjälp av Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Skapa ett Azure AD-program som är konfigurerat för partner Center. Utför följande åtgärder för att slutföra det här steget.

    - Bläddra till [appens hanterings](https://partner.microsoft.com/pcv/apiintegration/appmanagement) funktion i instrument panelen för partner Center
    - Skapa en ny Azure AD-app genom att klicka på *Lägg till ny webbapp* .

    Se till att dokumentera *app-ID*, * konto-ID * * och *nyckel* värden eftersom de används i stegen nedan.

5. Klona databasen [partner Center-dotNet-samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) med Visual Studio eller följande kommando.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Öppna det *PartnerConsent* -projekt som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen.

7. Fyll i de program inställningar som finns i [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > Känslig information som program hemligheter bör inte lagras i konfigurationsfiler. Den gjordes här eftersom det är ett exempel program. Med ditt produktions program rekommenderar vi starkt att du använder certifikatbaserad autentisering. Mer information finns i [autentiseringsuppgifter för certifikat för programautentisering]( /azure/active-directory/develop/active-directory-certificate-credentials).

8. När du kör det här exempelprojektet kommer du att uppmanas att autentisera dig. När autentiseringen är klar begärs en åtkomsttoken från Azure AD. Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (app + User Authentication)

[Partner medgivande](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) exempel projektet visar hur du använder en webbplats som utvecklats med JSP för att fånga in medgivande, begära en uppdateringstoken och säker lagring i Azure Key Vault. Utför följande för att skapa nödvändiga komponenter för det här exemplet.

1. Skapa en instans av Azure Key Vault med hjälp av Azure Portal eller följande PowerShell-kommandon. Innan du kör kommandot ska du se till att ändra parameter värden. Valv namnet måste vara unikt.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Mer information om hur du skapar en Azure Key Vault finns i [snabb start: Ange och hämta en hemlighet från Azure Key Vault med Azure Portal](/azure/key-vault/quick-create-portal) eller [snabb start: Ange och hämta en hemlighet från Azure Key Vault med PowerShell](/azure/key-vault/quick-create-powershell).

2. Skapa ett Azure AD-program och en nyckel med hjälp av Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Se till att dokumentera program identifieraren och de hemliga värdena eftersom de används i stegen nedan.

3. Ge det nya Azure AD-programmet behörigheten Läs hemligheter med hjälp av Azure Portal eller följande kommandon.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Skapa ett Azure AD-program som är konfigurerat för partner Center. Utför följande för att slutföra det här steget.

    - Bläddra till [appens hanterings](https://partner.microsoft.com/pcv/apiintegration/appmanagement) funktion i instrument panelen för partner Center
    - Skapa en ny Azure AD-app genom att klicka på *Lägg till ny webbapp* .

    Se till att dokumentera *app-ID*, * konto-ID * * och *nyckel* värden eftersom de används i stegen nedan.

5. Klona databasen [partner Center-Java-samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Öppna det *PartnerConsent* -projekt som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen.

7. Fyll i de program inställningar som finns i [web.xmls ](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) filen

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
    > Känslig information som program hemligheter bör inte lagras i konfigurationsfiler. Den gjordes här eftersom det är ett exempel program. Med ditt produktions program rekommenderar vi starkt att du använder certifikatbaserad autentisering. Mer information finns i [Key Vault certifikatautentisering](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. När du kör det här exempelprojektet kommer du att uppmanas att autentisera dig. När autentiseringen är klar begärs en åtkomsttoken från Azure AD. Informationen som returneras från Azure AD innehåller en uppdateringstoken som lagras i den konfigurerade instansen av Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Cloud Solution Provider-autentisering

Leverantörer av moln lösningar kan använda den uppdateringstoken som erhållits genom [partner medgivande](#partner-consent) processen.

### <a name="samples-for-cloud-solution-provider-authentication"></a>Exempel för autentisering av moln lösnings leverantör

Vi har utvecklat följande exempel för att hjälpa våra partner att förstå hur du utför varje nödvändig åtgärd. När du implementerar lämplig lösning i din miljö är det viktigt att du utvecklar en lösning som följer dina kod standarder och säkerhets principer.

## <a name="net-csp-authentication"></a>.NET (CSP-autentisering)

1. Om du inte redan har gjort det kan du genomföra [partner medgivande processen](#partner-consent).

2. Klona [partner-Center-dotNet-samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) -lagringsplatsen med Visual Studio eller följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Öppna `CSPApplication` projektet som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen.

4. Uppdatera program inställningarna som finns i [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) -filen.

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

5. Ange lämpliga värden för variablerna **partner** och **CustomerId** som finns i [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) -filen.

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. När du kör det här exempelprojektet hämtas den uppdateringstoken som hämtades under partner medgivande processen. Sedan begär den en åtkomsttoken för att interagera med partner Center SDK för partnerns räkning. Slutligen begär den en åtkomsttoken för att interagera med Microsoft Graph för den angivna kundens räkning.

## <a name="java-csp-authentication"></a>Java (CSP-autentisering)

1. Om du inte redan har gjort det kan du genomföra [partner medgivande processen](#partner-consent).

2. Klona databasen [partner Center-Java-samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med Visual Studio eller följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Öppna `cspsample` projektet som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen.

4. Uppdatera program inställningarna som finns i filen [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) .

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. När du kör det här exempelprojektet hämtas den uppdateringstoken som hämtades under partner medgivande processen. Sedan begär den en åtkomsttoken för att interagera med partner Center SDK för partnerns räkning.

6. Valfritt-ta bort kommentarer till funktions anropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.

## <a name="control-panel-provider-authentication"></a>Autentisering på kontroll panelens Provider

Leverantörer av kontroll panelen måste ha varje partner som de har stöd för att genomföra [partner medgivande](#partner-consent) processen. När den uppdaterade token som har hämtats till den här processen används för att komma åt Partner Center REST API och .NET API.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Exempel för autentisering med moln panels leverantör

Vi har utvecklat följande exempel för att hjälpa leverantörer i kontroll panelen att förstå hur man utför varje nödvändig åtgärd. När du implementerar lämplig lösning i din miljö är det viktigt att du utvecklar en lösning som följer dina kod standarder och säkerhets principer.

## <a name="net-cpv-authentication"></a>.NET (CPV-autentisering)

1. Utveckla och distribuera en process för leverantörer av moln lösningar för att tillhandahålla ett lämpligt medgivande. Mer information ett exempel finns i [partner medgivande](#partner-consent).

    > [!IMPORTANT]
    > Användarens autentiseringsuppgifter från en moln lösnings leverantörs partner ska inte lagras. Den uppdateringstoken som erhållits genom partner medgivande processen bör lagras och användas för att begära åtkomsttoken för att interagera med alla Microsoft-API: er.

2. Klona [partner-Center-dotNet-samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) -lagringsplatsen med Visual Studio eller följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Öppna `CPVApplication` projektet som finns i `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogen.

4. Uppdatera program inställningarna som finns i [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) -filen.

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

5. Ange lämpliga värden för variablerna **partner** och **CustomerId** som finns i [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) -filen.

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. När du kör det här exempel projektet hämtar den uppdateringstoken för den angivna partnern. Sedan begär den en åtkomsttoken för att komma åt Partner Center och Azure AD Graph åt partnern. Nästa uppgift är att ta bort och skapa behörighets bidrag till kund innehavaren. Eftersom det inte finns någon relation mellan kontroll panelens tillverkare och kunden måste dessa behörigheter läggas till med partner Center-API: et. I följande exempel visas hur du utför det.

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

När de här behörigheterna har upprättats utför exemplet åtgärder med Azure AD Graph för kundens räkning.

## <a name="java-cpv-authentication"></a>Java (CPV-autentisering)

1. Utveckla och distribuera en process för leverantörer av moln lösningar för att tillhandahålla ett lämpligt medgivande. Mer information och ett exempel finns i [partner medgivande](#partner-consent).

    > [!IMPORTANT]
    > Användarens autentiseringsuppgifter från en moln lösnings leverantörs partner ska inte lagras. Den uppdateringstoken som erhållits genom partner medgivande processen bör lagras och användas för att begära åtkomsttoken för att interagera med alla Microsoft-API: er.

2. Klona databasen [partner Center-Java-samples](https://github.com/Microsoft/Partner-Center-Java-Samples) med följande kommando

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Öppna `cpvsample` projektet som finns i `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogen.

4. Uppdatera program inställningarna som finns i filen [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) .

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

    Värdet för `partnercenter.displayName` ska vara visnings namnet för ditt Marketplace-program.

5. Ange lämpliga värden för variablerna **partner** och **customerId** som finns i filen [program. java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) .

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. När du kör det här exempel projektet hämtar den uppdateringstoken för den angivna partnern. Sedan begär den en åtkomsttoken för åtkomst till Partner Center för partnerns räkning. Nästa uppgift är att ta bort och skapa behörighets bidrag till kund innehavaren. Eftersom det inte finns någon relation mellan kontroll panelens tillverkare och kunden måste dessa behörigheter läggas till med partner Center-API: et. I följande exempel visas hur du beviljar behörigheterna.

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

Ta bort kommentarer till funktions anropen *RunAzureTask* och *RunGraphTask* om du vill se hur du interagerar med Azure Resource Manager och Microsoft Graph för kundens räkning.
