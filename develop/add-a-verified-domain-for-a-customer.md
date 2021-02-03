---
title: Lägg till en verifierad domän för en kund
description: 'Lär dig hur du lägger till en verifierad domän i listan över godkända domäner för en kund i Partner Center. Använd API: er för partner Center och REST API: er.'
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d0ea9998324e99c7986645dc90fdfba0a2a71571
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769966"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Lägg till en verifierad domän i listan över godkända domäner för en befintlig kund 

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här lägger du till en verifierad domän i listan över godkända domäner för en befintlig kund.

## <a name="prerequisites"></a>Förutsättningar

- Du måste vara en partner som är en domän registrator.

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="adding-a-verified-domain"></a>Lägga till en verifierad domän

Om du är en partner som är en domän registrator kan du använda `verifieddomain` API: et för att publicera en ny [domän](#domain) resurs i listan över domäner för en befintlig kund. Det gör du genom att identifiera kunden med hjälp av deras CustomerTenantId. Ange ett värde för egenskapen VerifiedDomainName. Skicka en [domän](#domain) resurs i begäran med de egenskaper som krävs, Capability, AuthenticationType, status och VerificationMethod som ingår. Om du vill ange att den nya [domänen](#domain) är en federerad domän anger du egenskapen AuthenticationType i [domän](#domain) resursen till `Federated` och inkluderar en [DomainFederationSettings](#domain-federation-settings) -resurs i begäran. Om metoden lyckas, kommer svaret att innehålla en [domän](#domain) resurs för den nya verifierade domänen.

### <a name="custom-verified-domains"></a>Anpassade domäner som verifierats

När du lägger till en anpassad verifierad domän, en domän som inte är registrerad på **onmicrosoft.com**, måste du ställa in egenskapen [CustomerUser. immutableId](user-resources.md#customeruser) på ett unikt ID-värde för kunden som du lägger till domänen för. Den här unika identifieraren krävs under validerings processen när domänen verifieras. Mer information om kund användar konton finns i [skapa användar konton för en kund](create-user-accounts-for-a-customer.md).

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{CustomerTenantId}/verifieddomain http/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ange kunden som du lägger till en verifierad domän för.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.

| Namn                                                  | Typ   | Obligatorisk                                      | Beskrivning                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | sträng | Yes                                           | Det verifierade domän namnet. |
| [Domän](#domain)                                     | objekt | Yes                                           | Innehåller domän informationen. |
| [DomainFederationSettings](#domain-federation-settings) | objekt | Ja (om AuthenticationType = `Federated` )     | De domän Federations inställningar som ska användas om domänen är en `Federated` domän och inte en `Managed` domän. |

### <a name="domain"></a>Domain

I den här tabellen beskrivs de obligatoriska och valfria **domän** egenskaperna i begär ande texten.

| Namn               | Typ                                     | Obligatorisk | Beskrivning                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | sträng           | Yes      | Definierar om domänen är en `Managed` domän eller en `Federated` domän. Värden som stöds: `Managed` , `Federated` .|
| Funktion                                            | sträng           | Yes      | Anger domänens funktion. Ett exempel är `Email`.                  |
| IsDefault                                             | boolesk värde, null | No       | Anger om domänen är standard domänen för klienten. Värden som stöds: `True` , `False` , `Null` .        |
| IsInitial                                             | boolesk värde, null | No       | Anger om domänen är en första domän. Värden som stöds: `True` , `False` , `Null` .                       |
| Name                                                  | sträng           | Yes      | Domän namnet.                                                          |
| RootDomain                                            | sträng           | No       | Namnet på rot domänen.                                              |
| Status                                                | sträng           | Yes      | Domänens status. Ett exempel är `Verified`. Värden som stöds:  `Unverified` , `Verified` , `PendingDeletion` .                               |
| VerificationMethod                                    | sträng           | Yes      | Typ av domän verifierings metod. Värden som stöds: `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Domän Federations inställningar

I den här tabellen beskrivs de obligatoriska och valfria **DomainFederationSettings** -egenskaperna i begär ande texten.

| Namn   | Typ   | Obligatorisk | Beskrivning                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | sträng           | No      | Den inloggnings-URI som används av rika klienter. Den här egenskapen är partnerns URL för STS-autentisering. |
| DefaultInteractiveAuthenticationMethod | sträng           | No      | Anger standard metoden för autentisering som ska användas när ett program kräver att användaren har interaktiv inloggning. |
| FederationBrandName                    | sträng           | No      | Federationens varumärkes namn.        |
| IssuerUri                              | sträng           | Yes     | Namnet på utfärdaren av certifikaten.                        |
| LogOffUri                              | sträng           | Yes     | Utloggnings-URI: n. Den här egenskapen beskriver den federerade domän inloggnings-URI: n.        |
| MetadataExchangeUri                    | sträng           | No      | URL: en som anger den slut punkt för metadata som används för autentisering från omfattande klient program. |
| NextSigningCertificate                 | sträng           | No      | Certifikatet som används för att komma framtiden av ADFS v2 STS för att signera anspråk. Den här egenskapen är en Base64-kodad representation av certifikatet. |
| OpenIdConnectDiscoveryEndpoint         | sträng           | No      | OpenID Connect Discovery-slutpunkten för den federerade IDP STS. |
| PassiveLogOnUri                        | sträng           | Yes     | Den inloggnings-URI som används av äldre passiva klienter. Den här egenskapen är adressen som används för att skicka federerade inloggnings begär Anden. |
| PreferredAuthenticationProtocol        | sträng           | Yes     | Formatet för autentiseringstoken. Ett exempel är `WsFed`. Värden som stöds: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | sträng           | Yes     | Beteende typen prompt login.  Ett exempel är `TranslateToFreshPasswordAuth`. Värden som stöds: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate                     | sträng           | Yes     | Det certifikat som för närvarande används av ADFS v2 STS för att signera anspråk. Den här egenskapen är en Base64-kodad representation av certifikatet. |
| SigningCertificateUpdateStatus         | sträng           | No      | Anger uppdaterings status för signerings certifikatet. |
| SigningCertificateUpdateStatus         | boolesk värde, null | No      | Anger om IDP STS stöder MFA. Värden som stöds: `True` , `False` , `Null` .|

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>REST-svar

Om detta lyckas returnerar detta API en [domän](#domain) resurs för den nya verifierade domänen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```
