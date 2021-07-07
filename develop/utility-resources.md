---
title: Verktygsresurser
description: PartnerCenter-REST API innehåller många resurser som beskriver datamodeller för generell användning som används i hela SDK:n.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 095cf36d47b147eb6df28d8747889e218c270659
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529672"
---
# <a name="utility-resources"></a>Verktygsresurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

PartnerCenter-REST API innehåller många resurser som beskriver datamodeller för generell användning som används i hela SDK:n.

## <a name="address"></a>Adress

Adress som ska användas för kund- eller partnerprofiler. Mer information om de format och egenskaper som stöds i olika länder/regioner finns i [Hämta regler för adressformatering efter marknad.](get-market-specific-validation-data.md)

| Egenskap     | Typ   | Längd (min, max) | Beskrivning                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | sträng | (1, 200)          | Den första adressraden.                                                                   |
| AddressLine2 | sträng | (0, 200)          | Den andra raden i adressen. Den här egenskapen är valfri.                                       |
| City         | sträng | saknas               | Staden.                                                                                        |
| Tillstånd        | sträng | (0, 2)            | Tillståndet.                                                                                       |
| Postnummer   | sträng | saknas               | Postnummer.                                                                     |
| Land      | sträng | (2, 2)            | Land/region i ISO-landskodformat.                                                   |
| Region       | sträng | saknas               | Regionen.                                                                                      |
| FirstName    | sträng | (1, 50)           | Förnamnet på en kontakt på kundens företag/organisation.                              |
| MiddleName   | sträng | (1, 50)           | Mellannamnet på en kontakt på kundens företag/organisation. Den här egenskapen är valfri.  |
| LastName     | sträng | (1, 50)           | Efternamnet på en kontakt på kundens företag/organisation.                               |
| PhoneNumber  | sträng | saknas               | Telefonnummer till en kontakt på kundens företag/organisation. Den här egenskapen är valfri.|
|PhoneNumber|sträng|saknas|Telefonnummer till en kontakt på kundens företag/organisation. I kundprofilen är den här egenskapen obligatorisk för kundens företag/organisation som finns i följande länder: Gör(AM), Gör(AZ), Gör(BY), Gör(BY), Arv(KZ), Kyrgyzstan(KG), Hubs(MD), Ryssland(RU), Kerikistan(TJ), Hubs(CUS), Kerten (UA)), Indien, Brasilien, Sydafrika, Schweiz, Förenade Arabemiraten, Saudiarabien, Anda, Andre, Huven, Etaa, Vietnam, Dos, SouthUdan och Katalys. Annars är detta valfritt.|


## <a name="contact"></a>Kontakt

Beskriver kontaktinformation för en viss person.

| Egenskap    | Typ   | Beskrivning                  |
|-------------|--------|------------------------------|
| FirstName   | sträng | Kontaktens förnamn.    |
| LastName    | sträng | Kontaktens efternamn.     |
| E-post       | sträng | Kontaktens e-postadress. |
| PhoneNumber | sträng | Kontaktens telefonnummer.  |

## <a name="fieldfilter"></a>FieldFilter

Beskriver ett filter som kan tillämpas på sökresultat.

| Egenskap | Typ   | Beskrivning                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operator | sträng | Filteroperatorn: "equals", "not \_ equals", \_ "greater than", "greater than or \_ \_ \_ equals", "less \_ than", "less \_ than or \_ \_ equals", "substring", "and", "or", "starts \_ with", "not \_ starts \_ with". |

## <a name="fileinfo"></a>FileInfo

Representerar en extern fil som laddats upp till Partnercenter.

| Egenskap                 | Typ   | Beskrivning                                   |
|--------------------------|--------|-----------------------------------------------|
| Kommentar                  | sträng | En kommentar som är associerad med filuppladdningen.    |
| FileExtension            | sträng | Filnamnstillägget.                           |
| FileNameWithoutExtension | sträng | Namnet på filen, tillägget ingår inte. |
| Filstorlek                 | long   | Filens storlek.                         |
| Id                       | sträng | Det unika ID:t för filuppladdningen.            |

## <a name="link"></a>Länk

Innehåller en URI-länk och tillhörande information.

| Egenskap | Typ                   | Beskrivning                        |
|----------|------------------------|------------------------------------|
| URI      | sträng                 | URI:en.                           |
| Metod   | sträng                 | Metoden som representeras av URI:en. |
| Sidhuvuden  | Matris med KeyValuePairs | Rubrikerna för länken.          |

## <a name="passwordprofile"></a>PasswordProfile

Beskriver ett specifikt lösenord och om lösenordet måste ändras.

>[!NOTE]
>Stöds inte i Partnercenter som drivs av 21Vianet.

| Egenskap            | Typ                          | Beskrivning                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Lösenord            | [SecureString](#securestring) | Lösenordet.                                                          |
| Forcechangepassword | boolean                       | Anger om lösenordet måste ändras med två eller flera tecken vid nästa inloggning. |

## <a name="resourcelinks"></a>ResourceLinks

Innehåller en lista över länkar för en resurs.

| Egenskap   | Typ                                      | Beskrivning                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Själv       | [Länk](#link)                             | Själv-URI:t.                                      |
| Nästa       | [Länk](#link)                             | Nästa sida med objekt.                            |
| Föregående   | [Länk](#link)                             | Föregående sida med objekt.                        |
| Attribut | [ResourceAttributes](#resourceattributes) | Metadataattributen som motsvarar användaren. |

## <a name="resourceattributes"></a>ResourceAttributes

Innehåller attributmetadata för en resurs.

| Egenskap   | Typ   | Beskrivning                                 |
|------------|--------|---------------------------------------------|
| Etag       | sträng | etag, även kallat objektversion. |
| ObjectType | sträng | Typ av objekt för basresursen.    |

## <a name="securestring"></a>SecureString

Lagrar skyddad information, till exempel ett lösenord.

| Egenskap | Typ | Beskrivning                       |
|----------|------|-----------------------------------|
| Längd   | int  | Längden på den skyddade strängen. |

## <a name="validationcode"></a>ValidationCode

Representerar en partners Government Community Cloud verifieringskod.

| Egenskap         | Typ         | Beskrivning                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Partneridentifierare                                                       |
| OrganizationName | sträng       | Organisationsnamnet som angavs under verifieringsprocessen             |
| ValidationId     | int          | En unik identifierare för validering                                       |
| MaxSkapar       | nullable int | Det högsta antal kunder som får skapas med den här valideringskoden    |
| ÅterståendeSkapar | nullable int | Återstående kund skapas under det här validerings-ID:t                      |
| Etag             | sträng       | Den specifika versionen av den här resursen. Ändras när resursen ändras. |
