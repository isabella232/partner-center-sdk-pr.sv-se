---
title: Kund resurser
description: Kund resurser som representerar en kund eller åter försäljare.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: fbd72ab5710876ba303fd1e30e6e552ecf89c5cd
ms.sourcegitcommit: 741cfa8585901de207c2e5da5eeebe26db0b0ad1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/18/2020
ms.locfileid: "97770047"
---
# <a name="customer-resources"></a>Kund resurser

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

## <a name="customer"></a>Kund

**Kund** resursen representerar en kund eller åter försäljare. I stort sett kan en kund resurs vara en person, anställd eller organisation som vill göra affärer med Microsoft och Microsofts åter försäljare. Kunder har också en företags profil och en fakturerings profil.

>[!NOTE]
>**Kund** resursen har en hastighets begränsning på 500 förfrågningar per minut per klient-ID.

| Egenskap              | Typ                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sträng                                                           | Kund-ID.                                                                                                                             |
| commerceId            | sträng                                                           | Handels-ID: t.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Ytterligare information om företaget eller organisationen.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Ytterligare information som används för fakturering.                                                                                                     |
| relationshipToPartner | sträng                                                           | Definierar det licensierings program som partnern använder för kunden: "ingen", "åter försäljare", "Advisor", "syndikering" eller "Microsoft \_ Support". |
| allowDelegatedAccess  | boolean                                                          | Om partnern har beviljats delegerad administratörs behörighet för den här kunden. Den här egenskapen är endast tillgänglig när du hämtar en kund efter ID, inte i listan.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Användarautentiseringsuppgifter.                                                                                                                        |
| customDomains         | matris med strängar                                                 | Lista över anpassade domäner för en kund.                                                                                                        |
| associatedPartnerId   | sträng                                                           | Den indirekta åter försäljaren som är kopplad till det här kund kontot. Det här värdet kan bara anges av indirekta CSP-partner.                              |
| Länkar                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Resurs länkarna som finns i profilen.                                                                                             |
| dokumentattribut            | [ResourceAttributes](utility-resources.md#resourceattributes)   | De metadata-attribut som motsvarar profilen.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

**CustomerCompanyProfile** -resursen är ytterligare information om företaget eller organisationen.

| Egenskap    | Typ                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | sträng                                                         | Kundens klient-ID för Azure AD. Detta kallas även för en MicrosoftID. |
| domän      | sträng                                                         | Kundens namn, till exempel contoso.onmicrosoft.com.                             |
| companyName | sträng                                                         | Namnet på företaget eller organisationen.                                          |
| Länkar       | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som finns i profilen.                                  |
| dokumentattribut  | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar profilen.                             |

| organizationRegistrationNumber | Sträng | Kundens organisations registrerings nummer (kallas även för INN-nummer i vissa länder). Krävs endast för kundens företag/organisation i följande länder. Armenien (AM), Azerbajdzjan (AZ), Vitryssland (av), Ungern (Slovakien), Kazakstan (KZ), Kirgizistan (KG), Moldavien (MD), Ryssland (RU), Tadzjikistan (TJ), Uzbekistan (UZ), Ukraina (UA). För kundens företag/organisation i andra länder bör detta inte anges. |


## <a name="customerbillingprofile"></a>CustomerBillingProfile

**CustomerBillingProfile** -resursen är ytterligare information som används för att fakturera kunden.

| Egenskap       | Typ                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | sträng                                                         | Profil-ID.                                                                                                                                |
| firstName      | sträng                                                         | Fakturerings kontaktens förnamn hos kundens företag. Det här är den person som fakturor och annan fakturerings kommunikation kommer att riktas mot. |
| lastName       | sträng                                                         | Fakturerings kontaktens efter namn.                                                                                                                  |
| e-post          | sträng                                                         | Fakturerings kontaktens e-postadress                                                                                                                    |
| substrat        | sträng                                                         | Deras föredragna kultur för kommunikation och valuta, till exempel "en-US".                                                                               |
| language       | sträng                                                         | Deras föredragna språk för kommunikation.                                                                                                            |
| companyName    | sträng                                                         | Namnet på företaget eller organisationen.                                                                                                               |
| defaultAddress | [Adress](utility-resources.md#address)                       | Adressen som fakturor skickas till, där fakturerings kontakten fungerar.                                                                                   |
| Länkar          | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som finns i profilen.                                                                                                       |
| dokumentattribut     | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar profilen.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

**CustomerRelationshipRequest** -resursen innehåller den URL som används av kunden för att upprätta en åter försäljares relation med en partner.

| Egenskap   | Typ                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | sträng                                                         | Den URL som används av kunden för att upprätta en relation med en partner. |
| dokumentattribut | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar Relations förfrågan.       |