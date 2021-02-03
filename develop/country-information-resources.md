---
title: Informations resurser för land
description: 'Lär dig mer om att använda API: er för partner Center med information om land och beskrivande metadata för ett särskilt land eller en region.'
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0974cf736ff86038f8abf9c77d6a648984d1df
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770142"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>Informations resurser för land som är tillgängliga från API: er för partner Center

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Följande resurser är beskrivande metadata för ett land/en region.

## <a name="countryinformation"></a>CountryInformation

| Egenskap                      | Typ               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | sträng             | Tilläggs data.                                                                                |
| Iso2Code                      | sträng             | En ISO-2-kod.                                                                                     |
| Iso3Code                      | sträng             | En ISO-3-kod.                                                                                     |
| DefaultCulture                | sträng             | Standard kulturen.                                                                               |
| IsStateRequired               | boolean            | Anger om en region krävs eller inte.                                             |
| SupportedStatesList           | matris med strängar   | Om en region krävs returnerar den fullständiga listan för landet/regionen.                    |
| SupportedLanguagesList        | matris med strängar   | En lista över språk som stöds.                                                                     |
| SupportedCulturesList         | matris med strängar   | En lista över kulturer som stöds.                                                                      |
| IsPostalCodeRequired          | boolean            | Anger om ett post nummer krävs eller inte.                                    |
| PostalCodeRegex               | sträng             | Det reguljära uttrycket som definierar post numret.                                          |
| IsCityRequired                | boolean            | Anger om en stad krävs eller inte.                                                       |
| IsVatIdSupported              | boolean            | Anger om ett moms-ID krävs eller inte.                                                     |
| TaxIdFormat                   | sträng             | Formatet för skatte-ID.                                                                                 |
| TaxIdSample                   | sträng             | Exempel på skatte-ID.                                                                                 |
| VatIdRegex                    | sträng             | Reguljärt uttryck för skatte-ID.                                                                     |
| PhoneNumberRegex              | sträng             | Reguljärt uttryck för telefonnummer.                                                               |
| IsRegistrationNumberSupported | boolean            | Anger om ett registrerings nummer stöds eller inte.                                       |
| IsTaxIdSupported              | boolean            | Anger om ett skatte-ID stöds eller inte. Detta skiljer sig från IsVatIdSupported. |
| ResellerAgreementRegion       | sträng             | Region för åter försäljnings avtal.                                                                     |
| GeographicRegion              | sträng             | Den geografiska regionen.                                                                             |
| CountryCallingCodesList       | matris med strängar   | De anrops koder som stöds i landet/regionen.                                                 |
| Attribut                    | ResourceAttributes | De metadata-attribut som motsvarar CountryInformation-resursen.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Beskriver reglerna för adress formatering för ett land/en region.

| Egenskap                | Typ               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | sträng             | En ISO-2-kod.                                                                                     |
| DefaultCulture          | sträng             | Standard kulturen.                                                                               |
| IsStateRequired         | boolean            | Anger om en region krävs eller inte.                                             |
| SupportedStatesList     | matris med strängar   | Om en region krävs returnerar den fullständiga listan för landet/regionen.                    |
| SupportedLanguagesList  | matris med strängar   | En lista över språk som stöds.                                                                     |
| SupportedCulturesList   | matris med strängar   | En lista över kulturer som stöds.                                                                      |
| IsPostalCodeRequired    | boolean            | Anger om ett post nummer krävs eller inte.                                    |
| PostalCodeRegex         | sträng             | Det reguljära uttrycket som definierar post numret.                                          |
| IsCityRequired          | boolean            | Anger om en stad krävs eller inte.                                                       |
| IsVatIdSupported        | boolean            | Anger om ett moms-ID krävs eller inte.                                                     |
| TaxIdFormat             | sträng             | Formatet för skatte-ID.                                                                                 |
| TaxIdSample             | sträng             | Exempel på skatte-ID.                                                                                 |
| VatIdRegex              | sträng             | Reguljärt uttryck för skatte-ID.                                                                     |
| PhoneNumberRegex        | sträng             | Reguljärt uttryck för telefonnummer.                                                               |
| IsTaxIdSupported        | boolean            | Anger om ett skatte-ID stöds eller inte. Den här egenskapen skiljer sig från IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Anger om ett skatte-ID är valfritt eller inte.                                                     |
| CountryCallingCodesList | matris med strängar   | De anrops koder som stöds i landet/regionen.                                                 |
| Attribut              | ResourceAttributes | De metadata-attribut som motsvarar CountryInformation-resursen.                          |
