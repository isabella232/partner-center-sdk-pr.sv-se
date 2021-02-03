---
title: Uppgradera resurser
description: Beskriver de resurser som används för att uppgradera en användare från en käll prenumeration till en mål prenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bdbef383370761a01eb462f90284ad826a38ddaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768991"
---
# <a name="upgrade-resources"></a>Uppgradera resurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Beskriver de resurser som används för att uppgradera en användare från en käll prenumeration till en mål prenumeration.

## <a name="upgrade"></a>Uppgradera

Beskriver beteendet för en enskild uppgraderings resurs.

| Egenskap      | Typ                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Erbjudande                  | Erbjudandet för mål prenumerationen.                                                        |
| UpgradeType   | sträng                 | Typ av uppgradering: "ingen", "endast uppgradering \_ " eller "uppgradera \_ med \_ licens \_ överföring".         |
| IsEligible    | boolean                | Anger om uppgraderingen kan utföras.                                                  |
| Antal      | heltal                | Kvantifieraren för det nya erbjudandet som ska köpas. Standardvärdet för källans prenumerations antal. |
| UpgradeErrors | matris med UpgradeErrors | Orsaker till att uppgraderingen inte kan utföras, om tillämpligt.                                      |
| Attribut    | ResourceAttributes     | De metadata-attribut som motsvarar uppgraderingen.                                        |

## <a name="upgradeerror"></a>UpgradeError

Beskriver en orsak till varför en uppgradering inte kan utföras.

| Egenskap          | Typ               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | sträng             | Felkoden som är kopplad till problemet: "andra", "delegerade \_ Administratörs \_ behörigheter \_ inaktiverade", "prenumerations \_ status \_ inte \_ aktiv", "motstridiga \_ tjänst \_ typer", "samtidighets \_ konflikter", "användar \_ kontext \_ krävs", "prenumerations \_ tillägg \_ finns inte", \_ "prenumerationen innehåller inga \_ \_ \_ \_ \_ uppgraderings \_ Sök vägar", "det \_ gick inte att hitta prenumerations mål \_ erbjudandet \_ \_ " eller "prenumerationen är \_ inte etablerad" \_ . |
| Description       | sträng             | Användarvänlig text som beskriver felet.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | sträng             | Ytterligare information om felet.                                                                                                                                                                                                                                                                                                                                                         |
| Attribut        | ResourceAttributes | De metadata-attribut som motsvarar felet.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Beskriver resultatet av uppgraderings processen för prenumerationen.

| Egenskap             | Typ                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | sträng                      | Käll prenumerationens identifierare.                                           |
| TargetSubscriptionID | sträng                      | Identifieraren för mål prenumerationen.                                           |
| UpgradeType          | sträng                      | Typ av uppgradering: "ingen", "endast uppgradering \_ " eller "uppgradera \_ med \_ licens \_ överföring". |
| UpgradeErrors        | matris med UpgradeErrors      | Fel påträffades vid försök att utföra uppgraderingen, om tillämpligt.           |
| LicenseErrors        | matris med UserLicenseErrrors | Fel påträffades vid försök att migrera användar licenser, om tillämpligt.          |
| Attribut           | ResourceAttributes          | De metadata-attribut som motsvarar licensen.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Beskriver fel som uppstår vid misslyckad användar licens överföring.

| Egenskap     | Typ                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | sträng                 | Unikt identifierat användar objekt.                                 |
| Name         | sträng                 | Användarens namn.                                                     |
| E-post        | sträng                 | Användarens e-postadress.                                                    |
| Fel       | matris med ServiceFaults | En lista över undantag som har utlösts vid försök att utföra användar licens överföring. |
| Attribut   | ResourceAttributes     | De metadata-attribut som motsvarar licensen.                     |

