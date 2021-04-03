---
title: Verktygsresurser
description: 'Partner Center REST API innehåller många resurser som beskriver generella data modeller som används i SDK: n.'
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 115b0508f956c4b60e4db53193ef2585fa0c9a34
ms.sourcegitcommit: 204e518e794b6b076a17488ee9ca1aaaa4beaaec
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/01/2021
ms.locfileid: "106103988"
---
# <a name="utility-resources"></a>Verktygsresurser

**Gäller för**

- Partnercenter
- Partnercenter drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Partner Center REST API innehåller många resurser som beskriver generella data modeller som används i SDK: n.

## <a name="address"></a>Adress

Adress som ska användas för kund-eller partner profilerna. Mer information om format och egenskaper som stöds i olika länder/regioner finns i avsnittet [Hämta adress format regler per marknad](get-market-specific-validation-data.md).

| Egenskap     | Typ   | Längd (min, max) | Beskrivning                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | sträng | (1, 200)          | Den första raden i adressen.                                                                   |
| AddressLine2 | sträng | (0, 200)          | Den andra raden i adressen. Den här egenskapen är valfri.                                       |
| City         | sträng | saknas               | Staden.                                                                                        |
| Tillstånd        | sträng | (0, 2)            | Status.                                                                                       |
| Postnummer   | sträng | saknas               | POST nummer.                                                                     |
| Land      | sträng | (2, 2)            | Land/region i ISO-format för landskod.                                                   |
| Region       | sträng | saknas               | Regionen.                                                                                      |
| FirstName    | sträng | (1, 50)           | Förnamnet på en kontakt på kundens företag/organisation.                              |
| MiddleName   | sträng | (1, 50)           | Det mittersta namnet på en kontakt på kundens företag/organisation. Den här egenskapen är valfri.  |
| LastName     | sträng | (1, 50)           | Efter namnet på en kontakt på kundens företag/organisation.                               |
| PhoneNumber  | sträng | saknas               | Telefonnumret till en kontakt på kundens företag/organisation. Den här egenskapen är valfri.|
|PhoneNumber|sträng|saknas|Telefonnumret till en kontakt på kundens företag/organisation. I kund profil är den här egenskapen obligatorisk för kundens företag/organisation i följande länder: Armenien (AM), Azerbajdzjan (AZ). Vitryssland (BY), Ungern (HU), Kazakstan (KZ), Kirgizistan (KG), Moldavien (MD), Ryssland (RU), Tadzjikistan (TJ), Uzbekistan (UZ), Ukraina (UA), Indien, Brasilien, Sydafrika, Polen, Förenade Arabemiraten, Saudiarabien, Turkiet, Thailand, Vietnam, Myanmar, Irak, Sydsudan och Venezuela. Annars är detta valfritt..|


## <a name="contact"></a>Kontakt

Beskriver kontakt information för en viss individ.

| Egenskap    | Typ   | Beskrivning                  |
|-------------|--------|------------------------------|
| FirstName   | sträng | Kontaktens förnamn.    |
| LastName    | sträng | Kontaktens efter namn.     |
| E-post       | sträng | Kontaktens e-postadress. |
| PhoneNumber | sträng | Kontaktens telefonnummer.  |

## <a name="fieldfilter"></a>FieldFilter

Beskriver ett filter som kan tillämpas på Sök resultat.

| Egenskap | Typ   | Beskrivning                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operator | sträng | Filter operatorn: "är lika med", "är \_ lika med", "större \_ än", "större \_ än \_ eller \_ lika med", "mindre \_ än", "mindre \_ än \_ eller \_ lika med", "under sträng", ",", "eller", "börjar \_ med", " \_ börjar inte \_ med". |

## <a name="fileinfo"></a>FileInfo

Representerar en extern fil som överförts till Partner Center.

| Egenskap                 | Typ   | Beskrivning                                   |
|--------------------------|--------|-----------------------------------------------|
| Kommentar                  | sträng | En kommentar som är associerad med fil uppladdningen.    |
| FileExtension            | sträng | Fil namns tillägget.                           |
| FileNameWithoutExtension | sträng | Filens namn, tillägget ingår inte. |
| Storlek                 | long   | Filens storlek.                         |
| Id                       | sträng | Unikt ID för fil uppladdning.            |

## <a name="link"></a>Länk

Innehåller en URI-länk och associerad information.

| Egenskap | Typ                   | Beskrivning                        |
|----------|------------------------|------------------------------------|
| URI      | sträng                 | URI: n.                           |
| Metod   | sträng                 | Den metod som representeras av URI: n. |
| Sidhuvuden  | Matris med KeyValuePairs | Länkens sidhuvud.          |

## <a name="passwordprofile"></a>PasswordProfile

Beskriver ett särskilt lösen ord och om lösen ordet måste ändras.

>[!NOTE]
>Stöds inte på Partner Center som drivs av 21Vianet.

| Egenskap            | Typ                          | Beskrivning                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Lösenord            | [SecureString](#securestring) | Lösen ordet.                                                          |
| ForceChangePassword | boolean                       | Anger om lösen ordet måste ändras vid nästa inloggning. |

## <a name="resourcelinks"></a>ResourceLinks

Innehåller en lista med länkar till en resurs.

| Egenskap   | Typ                                      | Beskrivning                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Själv       | [Länk](#link)                             | Själv URI.                                      |
| Nästa       | [Länk](#link)                             | Nästa sida med objekt.                            |
| Föregående   | [Länk](#link)                             | Föregående sida med objekt.                        |
| Attribut | [ResourceAttributes](#resourceattributes) | De metadata-attribut som motsvarar användaren. |

## <a name="resourceattributes"></a>ResourceAttributes

Innehåller metadata för attribut för en resurs.

| Egenskap   | Typ   | Beskrivning                                 |
|------------|--------|---------------------------------------------|
| Etag       | sträng | Etag, även kallat objekt version. |
| ObjectType | sträng | Typ av objekt för bas resursen.    |

## <a name="securestring"></a>SecureString

Lagrar skyddad information, till exempel ett lösen ord.

| Egenskap | Typ | Beskrivning                       |
|----------|------|-----------------------------------|
| Längd   | int  | Den skyddade strängens längd. |

## <a name="validationcode"></a>ValidationCode

Representerar en partners verifierings kod för den offentliga community-molnet.

| Egenskap         | Typ         | Beskrivning                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| Partner        | GUID         | Partner-ID                                                       |
| OrganizationName | sträng       | Organisations namnet som angavs under validerings processen             |
| ValidationId     | int          | En unik identifierare för verifiering                                       |
| MaxCreates       | null-bara heltal | Maximalt antal kunder som får skapas med den här verifierings koden    |
| RemainingCreates | null-bara heltal | Återstående kund skapar under detta validerings-ID                      |
| ETag             | sträng       | Den angivna versionen av den här resursen. Ändringar när resursen ändras. |
