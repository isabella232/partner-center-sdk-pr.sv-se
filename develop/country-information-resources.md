---
title: Resurser för landsinformation
description: Lär dig mer om att använda Partner Center-API:er med resurser för landsinformation och beskrivande metadata relaterade till ett visst land eller en viss region.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b570b27466699d8d85819f7603794888f8dd943038ee28a0a734b7ef9aa0d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991828"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>Resurser för landsinformation som är tillgängliga från Partner Center-API:er

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Följande resurser är beskrivande metadata för ett land/en region.

## <a name="countryinformation"></a>CountryInformation

| Egenskap                      | Typ               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | sträng             | Tilläggsdata.                                                                                |
| Iso2Code                      | sträng             | En ISO-2-kod.                                                                                     |
| Iso3Code                      | sträng             | En ISO-3-kod.                                                                                     |
| DefaultCulture                | sträng             | Standardkulturen.                                                                               |
| IsStateRequired               | boolean            | Anger om en delstat/provins krävs eller inte.                                             |
| SupportedStatesList           | matris med strängar   | Om en delstat/provins krävs returnerar den fullständiga listan för det landet/den regionen.                    |
| SupportedLanguagesList        | matris med strängar   | En lista över språk som stöds.                                                                     |
| SupportedCulturesList         | matris med strängar   | En lista över kulturer som stöds.                                                                      |
| IsPostalCodeRequired          | boolean            | Anger om ett postnummer eller postnummer krävs eller inte.                                    |
| PostalCodeRegex               | sträng             | Det reguljära uttryck som definierar postnummer.                                          |
| IsCityRequired                | boolean            | Anger om en stad krävs eller inte.                                                       |
| IsVatIdSupported              | boolean            | Anger om ett momsregistreringsnummer krävs eller inte.                                                     |
| TaxIdFormat                   | sträng             | Skatte-ID-formatet.                                                                                 |
| TaxIdSample                   | sträng             | Exemplet på skatte-ID.                                                                                 |
| VatIdRegex                    | sträng             | Reguljärt uttryck för skatte-ID.                                                                     |
| PhoneNumberRegex              | sträng             | Det reguljära telefonnumrets uttryck.                                                               |
| IsRegistrationNumberSupported | boolean            | Anger om ett registreringsnummer stöds eller inte.                                       |
| IsTaxIdSupported              | boolean            | Anger om ett skatte-ID stöds eller inte. Detta skiljer sig från IsVatIdSupported. |
| ResellerAgreementRegion       | sträng             | Återförsäljares avtalsregion.                                                                     |
| GeographicRegion              | sträng             | Den geografiska regionen.                                                                             |
| CountryCallingCodesList       | matris med strängar   | De anropskoder som stöds i landet/regionen.                                                 |
| Attribut                    | ResourceAttributes | Metadataattributen som motsvarar resursen CountryInformation.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Beskriver adressformateringsreglerna för ett land/en region.

| Egenskap                | Typ               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | sträng             | En ISO-2-kod.                                                                                     |
| DefaultCulture          | sträng             | Standardkulturen.                                                                               |
| IsStateRequired         | boolean            | Anger om en delstat/provins krävs eller inte.                                             |
| SupportedStatesList     | matris med strängar   | Om en delstat/provins krävs returnerar den fullständiga listan för det landet/den regionen.                    |
| SupportedLanguagesList  | matris med strängar   | En lista över språk som stöds.                                                                     |
| SupportedCulturesList   | matris med strängar   | En lista över kulturer som stöds.                                                                      |
| IsPostalCodeRequired    | boolean            | Anger om ett postnummer eller postnummer krävs eller inte.                                    |
| PostalCodeRegex         | sträng             | Det reguljära uttryck som definierar postnummer.                                          |
| IsCityRequired          | boolean            | Anger om en stad krävs eller inte.                                                       |
| IsVatIdSupported        | boolean            | Anger om ett momsregistreringsnummer krävs eller inte.                                                     |
| TaxIdFormat             | sträng             | Skatte-ID-formatet.                                                                                 |
| TaxIdSample             | sträng             | Exemplet på skatte-ID.                                                                                 |
| VatIdRegex              | sträng             | Reguljärt uttryck för skatte-ID.                                                                     |
| PhoneNumberRegex        | sträng             | Det reguljära telefonnumrets uttryck.                                                               |
| IsTaxIdSupported        | boolean            | Anger om ett skatte-ID stöds eller inte. Den här egenskapen skiljer sig från IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Anger om ett skatte-ID är valfritt eller inte.                                                     |
| CountryCallingCodesList | matris med strängar   | De anropskoder som stöds i landet/regionen.                                                 |
| Attribut              | ResourceAttributes | Metadataattributen som motsvarar resursen CountryInformation.                          |
