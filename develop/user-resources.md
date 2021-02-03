---
title: Användar resurser
description: Beskriver en enskild partner Center-användare, deras personliga och konto information och de behörigheter de har i Partner Center.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c88b9b65dfb925712ff85fb42d34251cca6e0b5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768709"
---
# <a name="user-resources"></a>Användar resurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Beskriver en enskild partner Center-användare, deras personliga och konto information och de behörigheter de har i Partner Center.

## <a name="user"></a>User

Beskriver en enskild användare.

| Egenskap              | Typ                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sträng                                                         | Användar-ID.                                                                                                                                                                                                       |
| userPrincipalName     | sträng                                                         | Användarens huvud-ID.                                                                                                                                                                                             |
| firstName             | sträng                                                         | Användarens förnamn.                                                                                                                                                                                                |
| lastName              | sträng                                                         | Användarens efter namn.                                                                                                                                                                                                 |
| displayName           | sträng                                                         | Användarens visade namn.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Användarens lösen ords profil.                                                                                                                                                                                               |
| phoneNumber           | sträng                                                         | Användarens telefonnummer.                                                                                                                                                                                                   |
| lastDirectorySyncTime | sträng i UTC-datum/tid-format                                 | Den senaste gången som information för den här användaren synkroniserades mellan Azure Active Directory och lokala Active Directory. Ett datum/tid-värde visas bara om Azure AD Connect Sync är aktiverat. Annars är värdet null. |
| userDomainType        | sträng                                                         | Användar domän typen: "ingen", "hanterad" eller "federerad".                                                                                                                                                                   |
| state                 | sträng                                                         | Användarens tillstånd: "Active", "inaktiv" (för en borttagen användare).                                                                                                                                                          |
| softDeletionTime      | sträng i UTC-datum/tid-format                                 | Representerar början på den trettio dag period efter vilken data som är associerade med en borttagen användare tas bort permanent och därför inte kan återställas.                                                                          |
| Länkar                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna.                                                                                                                                                                                                        |
| dokumentattribut            | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Beskriver en kund användare.

| Egenskap              | Typ                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | sträng                                                         | Den plats där användaren tänker använda licensen.                                                                                                                                                                    |
| id                    | sträng                                                         | Användar-ID.                                                                                                                                                                                                       |
| userPrincipalName     | sträng                                                         | Användarens huvud-ID.                                                                                                                                                                                             |
| firstName             | sträng                                                         | Användarens förnamn.                                                                                                                                                                                                |
| lastName              | sträng                                                         | Användarens efter namn.                                                                                                                                                                                                 |
| displayName           | sträng                                                         | Användarens visade namn.                                                                                                                                                                                            |
| immutableId           | sträng                                                         | Användarens oföränderliga ID.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Användarens lösen ords profil.                                                                                                                                                                                               |
| phoneNumber           | sträng                                                         | Användarens telefonnummer.                                                                                                                                                                                                   |
| lastDirectorySyncTime | sträng i UTC-datum/tid-format                                 | Den senaste gången som information för den här användaren synkroniserades mellan Azure Active Directory och lokala Active Directory. Ett datum/tid-värde visas bara om Azure AD Connect Sync är aktiverat. Annars är värdet null. |
| userDomainType        | sträng                                                         | Användar domän typen: "ingen", "hanterad" eller "federerad".                                                                                                                                                                   |
| state                 | sträng                                                         | Användarens tillstånd: "Active", "inaktiv" (för en borttagen användare).                                                                                                                                                          |
| softDeletionTime      | sträng i UTC-datum/tid-format                                 | Representerar början på den trettio dag period efter vilken data som är associerade med en borttagen användare tas bort permanent och därför inte kan återställas.                                                                          |
| Länkar                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna.                                                                                                                                                                                                        |
| dokumentattribut            | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Beskriver en användares inloggnings uppgifter.

| Egenskap | Typ                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | sträng                                             | Användarens namn.                |
| password | [SecureString](utility-resources.md#securestring) | Användarens säkert lagrade lösen ord. |

## <a name="usermember"></a>UserMember

Beskriver en användares medlems information.

| Egenskap          | Typ                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | sträng                                                         | Det namn som visas för användaren.   |
| userPrincipalName | sträng                                                         | Namnet på användarens huvud namn.    |
| roleId            | sträng                                                         | Identifieraren för användarens roll. |
| id                | sträng                                                         | Medlemmens identifierare.      |
| dokumentattribut        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.           |

