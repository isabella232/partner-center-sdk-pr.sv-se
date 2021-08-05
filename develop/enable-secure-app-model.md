---
title: Aktivera säker programmodell
description: Skydda dina Partnercenter- och kontrollpanelens appar.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36a81c7b235c68e49bb425b5bd0d4615882f88ef
ms.sourcegitcommit: 07b9a11f5c615ed1e716081392032cea2124bd98
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/04/2021
ms.locfileid: "115104218"
---
# <a name="enabling-the-secure-application-model-framework"></a>Aktivera Secure Application Model-ramverket

Microsoft introducerar ett säkert, skalbart ramverk för autentisering av molnlösningsleverantörer (CSP) och kontrollpanelsleverantörer (CPV) via MFA-arkitekturen (Microsoft Azure Active Directory Multi-Factor Authentication).

Du kan använda den nya modellen för att höja säkerheten för Partner Center API-integreringssamtal. Detta hjälper alla parter (inklusive Microsoft, CSP-partner och CPV:er) att skydda sin infrastruktur och sina kunddata mot säkerhetsrisker.

## <a name="scope"></a>Omfång

Den här artikeln handlar om följande aktörer:

- CPV
  - En CPV är en oberoende programvaruleverantör som utvecklar appar som CSP-partner använder för att integrera med Partnercenter-API:er.
  - En CPV är inte en CSP-partner med direkt åtkomst till Partnercenter-instrumentpanelen eller -API:er.

- Indirekta CSP-leverantörer och CSP-direktpartner som använder app-ID + användarautentisering och integrerar direkt med Partner Center-API:er.

## <a name="security-requirements"></a>Säkerhetskrav

Mer information om säkerhetskrav finns i [Säkerhetskrav för partner.](/partner-center/partner-security-requirements)

## <a name="secure-application-model"></a>Modell för säkra program

Marketplace-program måste personifiera CSP-partnerbehörigheter för att anropa Microsoft-API:er. Säkerhetsattacker mot dessa känsliga program kan leda till att kunddata kompromettens.

Om du vill ha en översikt och information om det nya autentiseringsramverket [kan du Modell för säkra program dokumentet om ramverket](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) för autentisering. Det här dokumentet beskriver principer och metodtips för att göra marketplace-program hållbara och robusta från säkerhetskompromettering.

## <a name="samples"></a>Exempel

Följande översiktsdokument och exempelkod beskriver hur partner kan implementera Modell för säkra program ramverket:

- [Översiktsdokument för CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Översiktsdokument för CSP](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET-exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java-exempel](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [REST-instruktioner och exempel](#rest)
- [PowerShell-instruktioner och -exempel](#powershell)

## <a name="rest"></a>REST

Om du vill göra REST-anrop Modell för säkra program ramverket med exempelkod följer du dessa steg:

1. [Skapa en webbapp](#create-a-web-app)

2. [Hämta en auktoriseringskod](#get-authorization-code)

3. [Hämta en uppdateringstoken](#get-refresh-token)

4. [Hämta en åtkomsttoken](#get-access-token)

5. [Gör ett Partnercenter-API-anrop](#make-partner-center-api-calls)

> [!TIP]
> Du kan använda Partner Center PowerShell-modulen för att hämta en auktoriseringskod och en uppdateringstoken. Du kan välja det här alternativet i stället för steg 2 och 3. Mer information finns i [PowerShell-avsnittet och i exemplen](#powershell).

### <a name="create-a-web-app"></a>Skapa en webbapp

Du måste skapa och registrera en webbapp i Partnercenter innan du gör REST-anrop.

1. Logga in på [Azure-portalen](https://portal.azure.com).

2. Skapa en Azure Active Directory (Azure AD).

3. Ge delegerade programbehörigheter till följande *resurser, beroende på programmets krav*. Om det behövs kan du lägga till fler delegerade behörigheter för programresurser.

   1. **Microsoft Partner Center** (vissa klienter visar detta som **SampleBECApp**)

   2. **Azure Management-API:er** (om du planerar att anropa Azure-API:er)

   3. **Windows Azure Active Directory**

4. Kontrollera att appens hem-URL är inställd på en slutpunkt där en live-webbapp körs. Den här appen måste godkänna [auktoriseringskoden från](#get-authorization-code) Azure AD-inloggningssamtalet. I exempelkoden i följande avsnitt [körs](#get-authorization-code)till exempel webbappen på `https://localhost:44395/` .

5. Observera följande information från webbappens inställningar i Azure AD:

   - Program-ID:t
   - Apphemlighet

> [!NOTE]
> Vi rekommenderar att du [använder ett certifikat som din programhemlighet.](/azure/active-directory/develop/active-directory-certificate-credentials) Du kan dock också skapa en programnyckel i Azure Portal. Exempelkoden i [följande avsnitt använder](#get-authorization-code) en programnyckel.

### <a name="get-authorization-code"></a>Hämta auktoriseringskod

Du måste få en auktoriseringskod som din webbapp kan godkänna från Azure AD-inloggningssamtalet:

1. Logga in på Azure AD på följande URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Se till att logga in med det användarkonto som du ska göra API-anrop från i Partnercenter (till exempel en administratörsagent eller ett agentkonto för försäljning).

2. Ersätt **Program-ID med** ditt Azure AD-app-ID (GUID).

3. När du uppmanas till det loggar du in med ditt användarkonto med MFA konfigurerat.

4. När du uppmanas till det anger du ytterligare MFA-information (telefonnummer eller e-postadress) för att verifiera inloggningen.

5. När du har loggat in omdirigerar webbläsaren anropet till slutpunkten för webbappen med din auktoriseringskod. Följande exempelkod omdirigerar till exempel till `https://localhost:44395/` .

#### <a name="authorization-code-call-trace"></a>Anropsspårning för auktoriseringskod

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

### <a name="get-refresh-token"></a>Hämta uppdateringstoken

Du måste sedan använda din auktoriseringskod för att hämta en uppdateringstoken:

1. Gör ett POST-anrop till Azure AD-inloggningsslutpunkten `https://login.microsoftonline.com/CSPTenantID/oauth2/token` med auktoriseringskoden. Ett exempel finns i följande exempel [på anrop](#sample-refresh-call).

2. Observera uppdateringstoken som returneras.

3. Lagra uppdateringstoken i Azure Key Vault. Mer information finns i [API Key Vault dokumentationen](/rest/api/keyvault/).

> [!IMPORTANT]
> Uppdateringstoken måste [lagras som en hemlighet](/rest/api/keyvault/setsecret/setsecret) i Key Vault.

#### <a name="sample-refresh-call"></a>Exempel på uppdateringssamtal

Platshållarbegäran:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

Begärandetext:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

Platshållarsvar:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Svarstext:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Hämta åtkomsttoken

Du måste hämta en åtkomsttoken innan du kan göra anrop till Partner Center-API:erna. Du måste använda en uppdateringstoken för att hämta en åtkomsttoken eftersom åtkomsttoken vanligtvis har en mycket begränsad livslängd (till exempel mindre än en timme).

Platshållarbegäran:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

Begärandetext:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

Platshållarsvar:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Svarstext:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Göra PARTNER Center API-anrop

Du måste använda din åtkomsttoken för att anropa Partner Center-API:erna. Se följande exempel på anrop.

#### <a name="example-partner-center-api-call"></a>Exempel på partnercenter-API-anrop

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Du kan använda [Partner Center PowerShell-modulen för att](https://www.powershellgallery.com/packages/PartnerCenter) minska den infrastruktur som krävs för att utbyta en auktoriseringskod för en åtkomsttoken. Den här metoden är valfri för att göra [Partner Center REST-anrop](#rest).

Mer information om den här processen finns i [Dokumentationen för Secure Appmodell](/powershell/partnercenter/secure-app-model) PowerShell.

1. Installera PowerShell-modulerna för Azure AD och Partner Center.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Använd kommandot **[New-PartnerAccessToken för](/powershell/module/partnercenter/new-partneraccesstoken)** att utföra medgivandeprocessen och samla in nödvändig uppdateringstoken.

    ```powershell
    $credential = Get-Credential

    $token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > Parametern **ServicePrincipal** används med kommandot **New-PartnerAccessToken** eftersom en Azure AD-app med en typ av **webb/API** används. Den här typen av app kräver att en klientidentifierare och en hemlighet ingår i begäran om åtkomsttoken. När **kommandot Get-Credential** anropas uppmanas du att ange ett användarnamn och lösenord. Ange programidentifieraren som användarnamn. Ange programhemligheten som lösenord. När kommandot **New-PartnerAccessToken** anropas uppmanas du att ange autentiseringsuppgifter igen. Ange autentiseringsuppgifterna för det tjänstkonto som du använder. Det här tjänstkontot ska vara ett partnerkonto med rätt behörigheter.

3. Kopiera värdet för uppdateringstoken.

    ```powershell
    $token.RefreshToken | clip
    ```

Du bör lagra värdet för uppdateringstoken i en säker lagringsplats, till exempel Azure Key Vault. Mer information om hur du använder modulen för säkra program med PowerShell finns i artikeln [om multifaktorautentisering.](/powershell/partnercenter/multi-factor-auth)
