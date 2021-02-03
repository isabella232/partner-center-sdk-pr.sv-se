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
# <a name="enabling-the-secure-application-model-framework"></a>Aktivera Secure Application Model-ramverket

**Gäller för:**

- Partnercenter

Microsoft presenterar ett säkert, skalbart ramverk för att autentisera leverantörer av moln lösnings leverantörer och kontroll panels leverantörer (CPV) via Microsoft Azure Multi-Factor Authentication (MFA)-arkitekturen.

Du kan använda den nya modellen för att öka säkerheten för API-integrerings anrop i Partner Center. Detta gör att alla parter (inklusive Microsoft, CSP-partner och CPVs) kan skydda sin infrastruktur och kund information från säkerhets risker.

## <a name="scope"></a>Omfång

Den här artikeln gäller följande aktörer:

- CPV
  - En CPV är en oberoende programvaruleverantör som utvecklar appar som CSP-partner använder för att integrera med Partnercenter-API:er.
  - En CPV är inte en CSP-partner med direkt åtkomst till Partnercenter-instrumentpanelen eller -API:er.

- CSP-indirekta providers och CSP Direct-partners som använder app-ID + användarautentisering och som integreras direkt med API: er för partner Center.

## <a name="security-requirements"></a>Säkerhetskrav

Mer information om säkerhets krav finns i [säkerhets krav för partner](/partner-center/partner-security-requirements).

## <a name="secure-application-model"></a>Säker program modell

Marketplace-program måste personifiera CSP-partnerns behörigheter för att anropa Microsoft API: er. Säkerhets attacker på dessa känsliga program kan leda till att kunddata komprometteras.

Om du vill ha en översikt och information om det nya Authentication Framework laddar du ned dokumentet för [säker program modell ramverk](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) . Det här dokumentet beskriver principer och bästa praxis för att göra Marketplace-program hållbara och robusta mot säkerhets kompromisser.

## <a name="samples"></a>Exempel

Följande översikts dokument och exempel kod beskriver hur partner kan implementera säkra program modell ramverk:

- [Översikts dokument för CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Översikts dokument för CSP](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET-exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java-exempel](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [REST-instruktioner och exempel](#rest)
- [PowerShell-instruktioner och exempel](#powershell)

## <a name="rest"></a>REST

Följ dessa steg om du vill göra REST-anrop med den säkra program modell ramverket med exempel kod:

1. [Skapa en webbapp](#create-a-web-app)

2. [Hämta en auktoriseringskod](#get-authorization-code)

3. [Hämta en uppdateringstoken](#get-refresh-token)

4. [Hämta en åtkomsttoken](#get-access-token)

5. [Gör ett Partnercenter-API-anrop](#make-partner-center-api-calls)

> [!TIP]
> Du kan använda Partner Center PowerShell-modulen för att hämta en auktoriseringskod och en uppdateringstoken. Du kan välja det här alternativet i stället för steg 2 och 3. Mer information finns i PowerShell- [avsnittet och exempel](#powershell).

### <a name="create-a-web-app"></a>Skapa en webbapp

Du måste skapa och registrera en webbapp i Partner Center innan du kan göra REST-anrop.

1. Logga in på [Azure-portalen](https://portal.azure.com).

2. Skapa en Azure Active Directory-app (Azure AD).

3. Ge delegerade program behörigheter till följande resurser, *beroende på programmets krav*. Om det behövs kan du lägga till fler delegerade behörigheter för program resurser.

   1. **Microsoft Partner Center** (vissa klienter visar detta som **SampleBECApp**)

   2. **API: er för Azure-hantering** (om du planerar att anropa Azure API: er)

   3. **Windows Azure Active Directory**

4. Kontrol lera att appens hem-URL är inställd på en slut punkt där en Live-webbapp körs. Den här appen måste acceptera [auktoriseringskod](#get-authorization-code) från inloggnings anropet för Azure AD. I exempel koden i [följande avsnitt](#get-authorization-code)körs webb programmet på `https://localhost:44395/` .

5. Observera följande information från webbappens inställningar i Azure AD:

   - Program-ID
   - Apphemlighet

> [!NOTE]
> Vi rekommenderar att du [använder ett certifikat som program hemlighet](/azure/active-directory/develop/active-directory-certificate-credentials). Men du kan också skapa en program nyckel i Azure Portal. Exempel koden i [följande avsnitt](#get-authorization-code) använder en program nyckel.

### <a name="get-authorization-code"></a>Hämta auktoriseringskod

Du måste hämta en auktoriseringskod för att din webbapp ska accepteras från Azure AD-inloggnings anropet:

1. Logga in på Azure AD på följande URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Var noga med att logga in med det användar konto som du ska använda för API-anrop i Partner Center (till exempel en administratörs agent eller ett försäljnings agent konto).

2. Ersätt **program-ID** med ditt Azure AD App-ID (GUID).

3. När du uppmanas till det loggar du in med ditt användar konto med MFA konfigurerat.

4. När du uppmanas till det anger du ytterligare MFA-information (telefonnummer eller e-postadress) för att verifiera din inloggning.

5. När du är inloggad omdirigerar webbläsaren anropet till din webb programs slut punkt med din auktoriseringskod. Till exempel omdirigeras följande exempel kod till `https://localhost:44395/` .

#### <a name="authorization-code-call-trace"></a>Spårning av auktoriseringskod

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

Du måste sedan använda auktoriseringskod för att hämta en uppdateringstoken:

1. Ring ett POST-anrop till inloggnings slut punkten för Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` med auktoriseringskod. Ett exempel finns i följande [exempel anrop](#sample-refresh-call).

2. Notera den uppdateringstoken som returneras.

3. Lagra uppdateringstoken i Azure Key Vault. Mer information finns i dokumentationen till [Key Vault API](/rest/api/keyvault/).

> [!IMPORTANT]
> Uppdateringstoken måste [lagras som en hemlighet](/rest/api/keyvault/setsecret/setsecret) i Key Vault.

#### <a name="sample-refresh-call"></a>Exempel på uppdaterings anrop

Placeholder-begäran:

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

Plats hållarens svar:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Svars text:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Hämta åtkomsttoken

Du måste skaffa en åtkomsttoken innan du kan ringa till API: erna för partner Center. Du måste använda en uppdateringstoken för att få en åtkomsttoken eftersom åtkomsttoken ofta har en mycket begränsad livs längd (till exempel mindre än en timme).

Placeholder-begäran:

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

Plats hållarens svar:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Svars text:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Gör API-anrop i Partner Center

Du måste använda din åtkomsttoken för att anropa API: er för partner Center. Se följande exempel anrop.

#### <a name="example-partner-center-api-call"></a>Exempel-API-anrop för partner Center

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Du kan använda [partner Center PowerShell-modulen](https://www.powershellgallery.com/packages/PartnerCenter) för att minska den infrastruktur som krävs för att utbyta en auktoriseringskod för en åtkomsttoken. Den här metoden är valfri för att göra [partner Center rest-anrop](#rest).

Mer information om den här processen finns i [säker app Model](/powershell/partnercenter/secure-app-model) PowerShell-dokumentation.

1. Installera PowerShell-modulerna för Azure AD och partner Center.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Använd kommandot **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** för att genomföra medgivande processen och avbilda den nödvändiga uppdateringstoken.

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > Parametern **ServicePrincipal** används med kommandot **New-PartnerAccessToken** eftersom en Azure AD-App med en typ av **webb/API** används. Den här typen av app kräver att klient-ID och hemlighet tas med i åtkomsttokenbegäran. När kommandot **Get-Credential** anropas uppmanas du att ange ett användar namn och lösen ord. Ange program-ID: t som användar namn. Ange program hemligheten som lösen ord. När kommandot **New-PartnerAccessToken** anropas uppmanas du att ange autentiseringsuppgifterna igen. Ange autentiseringsuppgifterna för det tjänst konto som du använder. Det här tjänst kontot bör vara ett partner konto med rätt behörighet.

3. Kopiera värdet för uppdateringstoken.

    ```powershell
    $token.RefreshToken | clip
    ```

Du bör lagra värdet för uppdateringstoken i en säker lagrings plats, t. ex. Azure Key Vault. Mer information om hur du använder den säkra modulen med PowerShell finns i artikeln [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) .
