---
title: Kundresurser
description: Kundresurser som representerar en kund eller återförsäljare.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 10798ae0bfae8c1a4e38777096861427992b8aee3799ee2dd9154c6f0e0c0799
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995177"
---
# <a name="customer-resources"></a>Kundresurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

## <a name="customer"></a>Kund

Resursen **Kund** representerar en kund eller återförsäljare. Oftast kan en kundresurs vara vilken person, medarbetare eller organisation som helst som vill göra affärer med Microsoft och Microsofts återförsäljare. Kunder har också en företagsprofil och en faktureringsprofil.

>[!NOTE]
>**Kundresursen** har en hastighetsgräns på 500 begäranden per minut per klient-ID.

| Egenskap              | Typ                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sträng                                                           | Kund-ID:t.                                                                                                                             |
| commerceId            | sträng                                                           | Handels-ID: t.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Ytterligare information om företaget eller organisationen.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Ytterligare information som används för fakturering.                                                                                                     |
| relationshipToPartner | sträng                                                           | Definierar licensprogrammet som partnern använder för den här kunden: "none", "reseller", "advisor", "syndication" eller "microsoft \_ support". |
| allowDelegatedAccess  | boolean                                                          | Anger om partnern har beviljats delegerade administratörsbehörigheter av den här kunden. Den här egenskapen är endast tillgänglig när du hämtar en kund via ID, inte efter lista.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Autentiseringsuppgifterna för användaren.                                                                                                                        |
| customDomains         | matris med strängar                                                 | Lista över anpassade domäner för en kund.                                                                                                        |
| associatedPartnerId   | sträng                                                           | Den indirekta återförsäljare som är associerad med det här kundkontot. Det här värdet kan bara anges av indirekta CSP-partner.                              |
| Länkar                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Resurslänkarna i profilen.                                                                                             |
| Attribut            | [ResourceAttributes](utility-resources.md#resourceattributes)   | Metadataattributen som motsvarar profilen.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

Resursen **CustomerCompanyProfile** är ytterligare information om företaget eller organisationen.

| Egenskap    | Typ                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | sträng                                                         | Kundens klientorganisations-ID för Azure AD. Detta kallas även för ett MicrosoftID. |
| domän      | sträng                                                         | Kundens namn, till exempel contoso.onmicrosoft.com.                             |
| companyName | sträng                                                         | Namnet på företaget eller organisationen.                                          |
| Länkar       | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurslänkarna i profilen.                                  |
| Attribut  | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar profilen.                             |
|organizationRegistrationNumber|Sträng|Kundens organisationsregistreringsnummer (kallas även INN-nummer i vissa länder). Krävs endast för kundens företag/organisation som finns i följande länder: Förarg(AM), Förarg(AM), Förarg(AZ), För kundens företag/organisation i följande länder: Det vill sig inte att kunden gör det: För att göra det kan du till exempel skriva ett e-post för att få hjälp med att göra det, t.ex. för att få hjälp med att göra det. För kundens företag/organisation som finns i andra länder ska detta inte anges.|


## <a name="customerbillingprofile"></a>CustomerBillingProfile

Resursen **CustomerBillingProfile** är ytterligare information som används för att fakturera kunden.

| Egenskap       | Typ                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | sträng                                                         | Profilidentifieraren.                                                                                                                                |
| firstName      | sträng                                                         | Förnamnet på faktureringskontakten på kundens företag. Det här är den person som fakturor och annan faktureringskommunikation kommer att dirigeras till. |
| lastName       | sträng                                                         | Efternamnet på faktureringskontakten.                                                                                                                  |
| e-post          | sträng                                                         | Faktureringskontaktens e-postadress                                                                                                                    |
| Kultur        | sträng                                                         | Deras önskade kultur för kommunikation och valuta, till exempel "en-us".                                                                               |
| language       | sträng                                                         | Deras föredragna språk för kommunikation.                                                                                                            |
| companyName    | sträng                                                         | Namnet på företaget eller organisationen.                                                                                                               |
| defaultAddress | [Adress](utility-resources.md#address)                       | Den adress som fakturorna skickas till, där faktureringskontakten fungerar.                                                                                   |
| Länkar          | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurslänkarna i profilen.                                                                                                       |
| Attribut     | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar profilen.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

Resursen **CustomerRelationshipRequest** innehåller den URL som används av kunden för att upprätta en återförsäljarrelation med en partner.

| Egenskap   | Typ                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | sträng                                                         | Den URL som används av kunden för att upprätta en relation med en partner. |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar relationsbegäran.       |