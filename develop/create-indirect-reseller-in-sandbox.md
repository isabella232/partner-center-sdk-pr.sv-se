---
title: Skapa indirekt återförsäljare i sandbox-miljö
description: Innehåller information för indirekta sandbox-leverantörer om hur du aktiverar testning från slutet till slut med hjälp av API:er.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973442"
---
# <a name="create-indirect-reseller-in-sandbox"></a>Skapa indirekt återförsäljare i sandbox-miljö

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Tyskland

Det här dokumentet visar hur du skapar indirekta sandbox-providers och aktiverar testning från slutet till slut med hjälp av API:er.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.

## <a name="csp-indirect-provider"></a>CSP Indirect Provider

| Produktionsfunktioner             | Sandbox-funktioner                            |
|-------------------------------------|-------------------------------------------------|
| Säljer via den indirekta återförsäljaren till slutanvändaren | Stöds |
| Äger all försäljning, fakturering, etablering och hantering/support | Stöds |
| Begära ett samarbete med återförsäljarna | Stöds |
| Visa kunder efter återförsäljare | Stöds |
| Lägga till nya kunder efter återförsäljare | Stöds |
| Bjud in kunder | Begäran om kundrelationer stöds inte i sandbox-miljön |
| Indirekt sandbox-provider kan välja Sandbox IR (MPN ID) som LEVERANTÖR när transaktionen placeras | Stöds |
| Stöds inte i produktion | Sandbox Indirect Provider kan skapa indirekt Sandbox-återförsäljare |
| MPN-ID för sandbox-miljö ska anges. Produktens MPN-ID fungerar inte | Stöds inte i produktion |
| Stöds inte i produktion | Sandbox Indirect Provider kan ta bort Sandbox Indirect Reseller |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a>Sandbox Indirect Provider – Skapa indirekt Sandbox-återförsäljare

Den här funktionen är bara tillgänglig i sandbox-miljön och ger indirekta sandbox-leverantörer möjlighet att skapa indirekta sandbox-återförsäljare.

1. Gräns på fem indirekta sandbox-återförsäljare som tillåts per indirekt sandbox-provider
2. Indirekta sandbox-leverantörer kan skapa kunder med `associatedPartnerId` sandbox-återförsäljare
3. Ange [MPN-ID för](/partner-center/mpn-create-a-partner-center-account) en viss region när du skapar en indirekt Sandbox-återförsäljare. Flera indirekta sandbox-återförsäljare kan skapas med samma MPN-ID för sandbox-miljö.
4. Endast 75 kunder tillåts per indirekt sandbox-provider

## <a name="sandbox-indirect-resellers--view-customers"></a>Sandbox Indirect Resellers – Visa kunder

1. Sandbox Indirect Resellers kan visa listan över sandbox-kunder av sandbox-leverantörer.
2. Indirekta sandbox-återförsäljare kan hantera kundkontot med hjälp av delegerade administratörsbehörigheter.

## <a name="create-sandbox-indirect-reseller-through-api"></a>Skapa indirekt sandbox-återförsäljare via API

### <a name="rest-request"></a>REST-begäran

#### <a name="request-syntax"></a>Begärandesyntax

| **Metod** | **URI för förfrågan**                                                        |
|------------|------------------------------------------------------------------------|
| **Inlägg**   | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller |

#### <a name="request-headers"></a>Begärandehuvuden

- Det här API:et är idempotent (det ger inte ett annat resultat om du anropar det flera gånger).
- Ett begärande-ID och korrelations-ID krävs.
- Mer information finns i [Partner Center REST-huvuden.](headers.md)

#### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.

| Egenskap             | Typ           | Beskrivning                                      |
|----------------------|----------------|--------------------------------------------------|
| mpnId                | sträng         | MPN-ID för IR i en viss region         |
| tenant               | &lt;Ordlistesträng, sträng&gt; | Samling grundläggande information som definierar ett konto som ska skapas |
| legalBusinessProfile | &lt;Ordlistesträng, sträng&gt; | Insamling av information som representerar den juridiska enheten, till exempel kontakt, adress och namn |
| organizationProfileLanguage | &lt;Ordlistesträng, sträng&gt; | Organisationsspråksidentifieraren |

I den här tabellen beskrivs de nödvändiga egenskaperna i **klientattributet.**

| Egenskap           | Typ           | Beskrivning                         |
|--------------------|----------------|-------------------------------------|
| domainPrefix       | Sträng; Unik | Domän för klientkontot       |
| name               | sträng         | Eget namn på klientorganisationen         |
| displayName        | sträng         | Visningsnamn för kontot        |
| adminUserName      | sträng         | Användarnamn för kontot för inloggning |
| adminfirstname     | sträng         | Förnamn för administratörsanvändaren       |
| adminlastname      | sträng         | Efternamn för administratörsanvändaren        |
| adminAlernateEmail | sträng         | e-post för administratörsanvändaren            |
| land            | sträng         | Land för kontot              |
| Kultur            | sträng         | Språkpreferens för konto     |

I den här tabellen beskrivs de obligatoriska egenskaperna i **attributet legalBusinessProfile.**

| Egenskap       | Typ                             | Beskrivning                          |
|----------------|----------------------------------|--------------------------------------|
| companyName    | sträng                           | Företagsnamn för juridisk person        |
| adress        | &lt;Ordlistesträng, sträng&gt; | Adress för den juridiska personens plats |
| primaryContact | &lt;Ordlistesträng, sträng&gt; | Kontaktuppgifter för företaget       |
| Kultur        | sträng                           | Språk som företaget föredrar    |

### <a name="request-example"></a>Exempel på begäran

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den ifyllda Sandbox IR-resursen i svarstexten.

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
