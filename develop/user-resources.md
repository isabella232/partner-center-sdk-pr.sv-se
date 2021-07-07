---
title: Användarresurser
description: Beskriver en enskild Partnercenter-användare, deras personliga information och kontoinformation samt de behörigheter som de har i Partnercenter.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 26bb202db3eefd9be8fe57ed2cc4dc220c8807d4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529689"
---
# <a name="user-resources"></a>Användarresurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Beskriver en enskild Partnercenter-användare, deras personliga information och kontoinformation samt de behörigheter som de har i Partnercenter.

## <a name="user"></a>Användare

Beskriver en enskild användare.

| Egenskap              | Typ                                                           | Beskrivning                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sträng                                                         | Användaridentifieraren.                                                                                                                                                                                                       |
| userPrincipalName     | sträng                                                         | Användarens huvudnamnsidentifierare.                                                                                                                                                                                             |
| firstName             | sträng                                                         | Användarens förnamn.                                                                                                                                                                                                |
| lastName              | sträng                                                         | Användarens efternamn.                                                                                                                                                                                                 |
| displayName           | sträng                                                         | Användarens namn som visas.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Användarens lösenordsprofil.                                                                                                                                                                                               |
| phoneNumber           | sträng                                                         | Användarens telefonnummer.                                                                                                                                                                                                   |
| lastDirectorySyncTime | sträng i UTC-datum/tid-format                                 | Den senaste gången informationen för den här användaren synkroniserades mellan Azure Active Directory och lokal Active Directory. Ett datum/tid-värde visas bara om Azure AD Anslut har aktiverats. Annars är värdet null. |
| userDomainType        | sträng                                                         | Användardomäntypen: "none", "managed" eller "federated".                                                                                                                                                                   |
| state                 | sträng                                                         | Tillståndet för användaren: "active", "inactive" (för en borttagna användare).                                                                                                                                                          |
| softDeletionTime      | sträng i UTC-datum/tid-format                                 | Representerar början av 30-dagarsperioden efter vilken data som är associerade med en borttagna användare tas bort permanent och därför inte kan återställas.                                                                          |
| Länkar                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurslänkarna.                                                                                                                                                                                                        |
| Attribut            | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Beskriver en kundanvändare.

| Egenskap              | Typ                                                           | Beskrivning                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | sträng                                                         | Den plats där användaren har för avsikt att använda licensen.                                                                                                                                                                    |
| id                    | sträng                                                         | Användaridentifieraren.                                                                                                                                                                                                       |
| userPrincipalName     | sträng                                                         | Användarens huvudnamnsidentifierare.                                                                                                                                                                                             |
| firstName             | sträng                                                         | Användarens förnamn.                                                                                                                                                                                                |
| lastName              | sträng                                                         | Användarens efternamn.                                                                                                                                                                                                 |
| displayName           | sträng                                                         | Användarens namn som visas.                                                                                                                                                                                            |
| immutableId           | sträng                                                         | Användarens oföränderliga ID.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Användarens lösenordsprofil.                                                                                                                                                                                               |
| phoneNumber           | sträng                                                         | Användarens telefonnummer.                                                                                                                                                                                                   |
| lastDirectorySyncTime | sträng i UTC-datum/tid-format                                 | Den senaste gången informationen för den här användaren synkroniserades mellan Azure Active Directory och lokal Active Directory. Ett datum/tid-värde visas bara om Azure AD Anslut har aktiverats. Annars är värdet null. |
| userDomainType        | sträng                                                         | Användardomäntypen: "none", "managed" eller "federated".                                                                                                                                                                   |
| state                 | sträng                                                         | Tillståndet för användaren: "active", "inactive" (för en borttagna användare).                                                                                                                                                          |
| softDeletionTime      | sträng i UTC-datum/tid-format                                 | Representerar början av 30-dagarsperioden efter vilken data som är associerade med en borttagna användare tas bort permanent och därför inte kan återställas.                                                                          |
| Länkar                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurslänkarna.                                                                                                                                                                                                        |
| Attribut            | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Beskriver en användares inloggningsuppgifter.

| Egenskap | Typ                                               | Beskrivning                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | sträng                                             | Användarens namn.                |
| password | [SecureString](utility-resources.md#securestring) | Användarens lösenord lagras på ett säkert sätt. |

## <a name="usermember"></a>UserMember

Beskriver en användares medlemsinformation.

| Egenskap          | Typ                                                           | Beskrivning                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | sträng                                                         | Användarens namn som visas.   |
| userPrincipalName | sträng                                                         | Namnet på användarens huvudnamn.    |
| roleId            | sträng                                                         | Identifieraren för användarens roll. |
| id                | sträng                                                         | Medlemmens identifierare.      |
| Attribut        | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.           |

