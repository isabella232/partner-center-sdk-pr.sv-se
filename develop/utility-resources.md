---
title: Verktygsresurser
description: 'Partner Center REST API innehåller många resurser som beskriver generella data modeller som används i SDK: n.'
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 53d39e4f76684128d48eacdce75706d853c7ce74
ms.sourcegitcommit: f5178dca1d9a51059738972810235d8858e6a67a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/18/2020
ms.locfileid: "97770059"
---
# <a name="utility-resources"></a>Verktygsresurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Partner Center REST API innehåller många resurser som beskriver generella data modeller som används i SDK: n.

## <a name="address"></a>Adress

Adress som ska användas för kund-eller partner profilerna. Mer information om format och egenskaper som stöds i olika länder/regioner finns i avsnittet [Hämta adress format regler per marknad](get-market-specific-validation-data.md).

| Egenskap     | Typ   | Längd (min, max) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | sträng | (1, 200)          | Den första raden i adressen.                                                                   |
| AddressLine2 | sträng | (0, 200)          | Den andra raden i adressen. Den här egenskapen är valfri.                                       |
| City         | sträng | saknas               | Staden.                                                                                        |
| Stat        | sträng | (0, 2)            | Status.                                                                                       |
| Postnummer   | sträng | saknas               | POST nummer.                                                                     |
| Land      | sträng | (2, 2)            | Land/region i ISO-format för landskod.                                                   |
| Region       | sträng | saknas               | Regionen.                                                                                      |
| FirstName    | sträng | (1, 50)           | Förnamnet på en kontakt på kundens företag/organisation.                              |
| MiddleName   | sträng | (1, 50)           | Det mittersta namnet på en kontakt på kundens företag/organisation. Den här egenskapen är valfri.  |
| LastName     | sträng | (1, 50)           | Efter namnet på en kontakt på kundens företag/organisation.                               |
| PhoneNumber  | sträng | saknas               | Telefonnumret till en kontakt på kundens företag/organisation. Den här egenskapen är valfri.|
|PhoneNumber|sträng|saknas|Telefonnumret till en kontakt på kundens företag/organisation. I kund profil är den här egenskapen obligatorisk för kundens företag/organisation i följande länder. Armenien (AM), Azerbajdzjan (AZ), Vitryssland (av), Ungern (Slovakien), Kazakstan (KZ), Kirgizistan (KG), Moldavien (MD), Ryssland (RU), Tadzjikistan (TJ), Uzbekistan (UZ), Ukraina (UA). Annars är detta valfritt.|


## <a name="contact"></a>Kontakt

Beskriver kontakt information för en viss individ.

| Egenskap    | Typ   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | sträng | Kontaktens förnamn.    |
| LastName    | sträng | Kontaktens efter namn.     |
| E-post       | sträng | Kontaktens e-postadress. |
| PhoneNumber | sträng | Kontaktens telefonnummer.  |

## <a name="fieldfilter"></a>FieldFilter

Beskriver ett filter som kan tillämpas på Sök resultat.

| Egenskap | Typ   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operator | sträng | Filter operatorn: "är lika med", "är \_ lika med", "större \_ än", "större \_ än \_ eller \_ lika med", "mindre \_ än", "mindre \_ än \_ eller \_ lika med", "under sträng", ",", "eller", "börjar \_ med", " \_ börjar inte \_ med". |

## <a name="fileinfo"></a>FileInfo

Representerar en extern fil som överförts till Partner Center.

| Egenskap                 | Typ   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Kommentar                  | sträng | En kommentar som är associerad med fil uppladdningen.    |
| FileExtension            | sträng | Fil namns tillägget.                           |
| FileNameWithoutExtension | sträng | Filens namn, tillägget ingår inte. |
| Storlek                 | long   | Filens storlek.                         |
| Id                       | sträng | Unikt ID för fil uppladdning.            |

## <a name="link"></a>Länk

Innehåller en URI-länk och associerad information.

| Egenskap | Typ                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | sträng                 | URI: n.                           |
| Metod   | sträng                 | Den metod som representeras av URI: n. |
| Sidhuvuden  | Matris med KeyValuePairs | Länkens sidhuvud.          |

## <a name="passwordprofile"></a>PasswordProfile

Beskriver ett särskilt lösen ord och om lösen ordet måste ändras.

>[!NOTE]
>Stöds inte på Partner Center som drivs av 21Vianet.

| Egenskap            | Typ                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Lösenord            | [SecureString](#securestring) | Lösen ordet.                                                          |
| ForceChangePassword | boolean                       | Anger om lösen ordet måste ändras vid nästa inloggning. |

## <a name="resourcelinks"></a>ResourceLinks

Innehåller en lista med länkar till en resurs.

| Egenskap   | Typ                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Själv       | [Operationsföljdslänkkod](#link)                             | Själv URI.                                      |
| Nästa       | [Operationsföljdslänkkod](#link)                             | Nästa sida med objekt.                            |
| Föregående   | [Operationsföljdslänkkod](#link)                             | Föregående sida med objekt.                        |
| Attribut | [ResourceAttributes](#resourceattributes) | De metadata-attribut som motsvarar användaren. |

## <a name="resourceattributes"></a>ResourceAttributes

Innehåller metadata för attribut för en resurs.

| Egenskap   | Typ   | Description                                 |
|------------|--------|---------------------------------------------|
| Etag       | sträng | Etag, även kallat objekt version. |
| ObjectType | sträng | Typ av objekt för bas resursen.    |

## <a name="securestring"></a>SecureString

Lagrar skyddad information, till exempel ett lösen ord.

| Egenskap | Typ | Description                       |
|----------|------|-----------------------------------|
| Längd   | int  | Den skyddade strängens längd. |

## <a name="validationcode"></a>ValidationCode

Representerar en partners verifierings kod för den offentliga community-molnet.

| Egenskap         | Typ         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| Partner        | GUID         | Partner-ID                                                       |
| OrganizationName | sträng       | Organisations namnet som angavs under validerings processen             |
| ValidationId     | int          | En unik identifierare för verifiering                                       |
| MaxCreates       | null-bara heltal | Maximalt antal kunder som får skapas med den här verifierings koden    |
| RemainingCreates | null-bara heltal | Återstående kund skapar under detta validerings-ID                      |
| ETag             | sträng       | Den angivna versionen av den här resursen. Ändringar när resursen ändras. |
