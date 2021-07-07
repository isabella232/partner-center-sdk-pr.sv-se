---
title: Lägg till en verifierad domän för en kund
description: Lär dig hur du lägger till en verifierad domän i listan över godkända domäner för en kund i Partnercenter. Gör det med Partner Center-API:er och REST-API:er.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a8157bff5ac37100713a057ac68ac94c89ba28b8
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025691"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Lägga till en verifierad domän i listan över godkända domäner för en befintlig kund 

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här lägger du till en verifierad domän i listan över godkända domäner för en befintlig kund.

## <a name="prerequisites"></a>Förutsättningar

- Du måste vara en partner som är domänregistrator.

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="adding-a-verified-domain"></a>Lägga till en verifierad domän

Om du är en partner som är domänregistrator kan du använda API:et för att publicera en ny domänresurs i listan över `verifieddomain` domäner för en befintlig kund. [](#domain) Det gör du genom att identifiera kunden med hjälp av kundens CustomerTenantId. Ange ett värde för egenskapen VerifiedDomainName. Skicka en [domänresurs](#domain) i begäran med de nödvändiga egenskaperna Name, Capability, AuthenticationType, Status och VerificationMethod inkluderade. Om du vill [](#domain) ange att den nya domänen är en [](#domain) federerad domän anger du egenskapen AuthenticationType i domänresursen till och inkluderar en `Federated` [DomainFederationSettings-resurs](#domain-federation-settings) i begäran. Om metoden lyckas innehåller svaret en domänresurs [för](#domain) den nya verifierade domänen.

### <a name="custom-verified-domains"></a>Anpassade verifierade domäner

När du lägger till en anpassad verifierad domän, en domän som inte är registrerad på **onmicrosoft.com,** måste du ange egenskapen [CustomerUser.immutableId](user-resources.md#customeruser) till ett unikt ID-värde för kunden som du lägger till domänen för. Den här unika identifieraren krävs under verifieringsprocessen när domänen verifieras. Mer information om kundanvändarkonton finns i [Skapa användarkonton för en kund.](create-user-accounts-for-a-customer.md)

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ange den kund som du lägger till en verifierad domän för.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.

| Namn                                                  | Typ   | Obligatorisk                                      | Beskrivning                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | sträng | Ja                                           | Det verifierade domännamnet. |
| [Domän](#domain)                                     | objekt | Ja                                           | Innehåller domäninformationen. |
| [DomainFederationSettings](#domain-federation-settings) | objekt | Ja (If AuthenticationType = `Federated` )     | De domänfederationsinställningar som ska användas om domänen är `Federated` en domän och inte en `Managed` domän. |

### <a name="domain"></a>Domain

I den här tabellen beskrivs de obligatoriska och **valfria domänegenskaperna** i begärandetexten.

| Namn               | Typ                                     | Obligatorisk | Beskrivning                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | sträng           | Ja      | Definierar om domänen är en `Managed` domän eller en `Federated` domän. Värden som stöds: `Managed` , `Federated` .|
| Funktion                                            | sträng           | Ja      | Anger domänkapaciteten. Till exempel `Email`.                  |
| IsDefault                                             | nullbar boolesk | Inga       | Anger om domänen är standarddomänen för klienten. Värden som stöds: `True` , `False` , `Null` .        |
| IsInitial                                             | nullbar boolesk | Inga       | Anger om domänen är en inledande domän. Värden som stöds: `True` , `False` , `Null` .                       |
| Name                                                  | sträng           | Ja      | Domännamnet.                                                          |
| RootDomain                                            | sträng           | No       | Namnet på rotdomänen.                                              |
| Status                                                | sträng           | Ja      | Domänstatus. Till exempel `Verified`. Värden som stöds:  `Unverified` , `Verified` , `PendingDeletion` .                               |
| VerificationMethod                                    | sträng           | Ja      | Typ av domänverifieringsmetod. Värden som stöds: `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Inställningar för domänfederation

I den här tabellen beskrivs de obligatoriska och **valfria Egenskaperna DomainFederationSettings** i begärandetexten.

| Namn   | Typ   | Obligatorisk | Beskrivning                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | sträng           | No      | Den inloggnings-URI som används av rich-klienter. Den här egenskapen är partnerns STS-autentiserings-URL. |
| DefaultInteractiveAuthenticationMethod | sträng           | No      | Anger standardautentiseringsmetoden som ska användas när ett program kräver att användaren har interaktiv inloggning. |
| FederationBrandName                    | sträng           | No      | Federationsnamnet.        |
| IssuerUri                              | sträng           | Ja     | Namnet på certifikatutfärdaren.                        |
| LogOffUri                              | sträng           | Ja     | Utloggnings-URI: en. Den här egenskapen beskriver den federerade URI:n för domänin logga ut.        |
| MetadataExchangeUri                    | sträng           | No      | Den URL som anger slutpunkten för metadatautbyte som används för autentisering från rich-klientprogram. |
| NextSigningCertificate                 | sträng           | No      | Certifikatet som används för den kommande framtiden av ADFS V2 STS för att signera anspråk. Den här egenskapen är en base64-kodad representation av certifikatet. |
| OpenIdConnectDiscoveryEndpoint         | sträng           | No      | OpenID-Anslut identifieringsslutpunkt för federerad IDP STS. |
| PassiveLogOnUri                        | sträng           | Ja     | Den inloggnings-URI som används av äldre passiva klienter. Den här egenskapen är adressen för att skicka federerade inloggningsbegäranden. |
| PreferredAuthenticationProtocol        | sträng           | Ja     | Formatet för autentiseringstoken. Till exempel `WsFed`. Värden som stöds: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | sträng           | Ja     | Beteendetypen för inloggning vid prompt.  Till exempel `TranslateToFreshPasswordAuth`. Värden som stöds: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate                     | sträng           | Ja     | Certifikatet som för närvarande används av ADFS V2 STS för att signera anspråk. Den här egenskapen är en base64-kodad representation av certifikatet. |
| SigningCertificateUpdateStatus         | sträng           | No      | Anger uppdateringsstatus för signeringscertifikatet. |
| SigningCertificateUpdateStatus         | nullbar boolesk | Inga      | Anger om IDP STS stöder MFA. Värden som stöds: `True` , `False` , `Null` .|

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

Om det lyckas returnerar detta API en [domänresurs](#domain) för den nya verifierade domänen.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
