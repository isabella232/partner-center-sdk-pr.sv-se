---
title: Uppgradera resurser
description: Beskriver de resurser som används för att uppgradera en användare från en källprenumeration till en målprenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c57994d1b1e7659df5e6448578422f6d9c21fee
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529825"
---
# <a name="upgrade-resources"></a>Uppgradera resurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Beskriver de resurser som används för att uppgradera en användare från en källprenumeration till en målprenumeration.

## <a name="upgrade"></a>Uppgradera

Beskriver beteendet för en enskild uppgraderingsresurs.

| Egenskap      | Typ                   | Beskrivning                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Erbjudande                  | Erbjudandet för målprenumerationen.                                                        |
| UpgradeType   | sträng                 | Typen av uppgradering: "none", "upgrade \_ only" (endast uppgradering) eller "upgrade \_ with license transfer" (uppgradera \_ med \_ licensöverföring).         |
| IsEligible    | boolean                | Anger om uppgraderingen kan utföras.                                                  |
| Kvantitet      | heltal                | Kvantiteten för det nya erbjudandet som ska köpas. Standardvärdet är antalet källprenumeration. |
| UpgradeErrors | matris med UpgradeErrors | Orsaker till att uppgraderingen inte kan utföras, om tillämpligt.                                      |
| Attribut    | ResourceAttributes     | Metadataattributen som motsvarar uppgraderingen.                                        |

## <a name="upgradeerror"></a>UpgradeError

Beskriver en orsak till varför en uppgradering inte kan utföras.

| Egenskap          | Typ               | Beskrivning                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | sträng             | Felkoden som är associerad med problemet: "other", "delegated \_ admin \_ permissions \_ disabled", "subscription \_ status not \_ \_ active", "conflicting \_ service \_ types", "concurrency \_ conflicts", "user \_ context required", "subscription add ons present", "subscription does not have any upgrade \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ paths", "subscription target offer not found" eller "subscription not \_ \_ \_ \_ \_ \_ provisioned". |
| Description       | sträng             | Användarvänlig text som beskriver felet.                                                                                                                                                                                                                                                                                                                                                             |
| Ytterligare information | sträng             | Ytterligare information om felet.                                                                                                                                                                                                                                                                                                                                                         |
| Attribut        | ResourceAttributes | Metadataattributen som motsvarar felet.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Beskriver resultatet av prenumerationsuppgraderingsprocessen.

| Egenskap             | Typ                        | Beskrivning                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | sträng                      | Identifieraren för källprenumerationen.                                           |
| TargetSubscriptionID | sträng                      | Identifieraren för målprenumerationen.                                           |
| UpgradeType          | sträng                      | Typen av uppgradering: "none", "upgrade \_ only" (endast uppgradering) eller "upgrade \_ with license transfer" (uppgradera \_ med \_ licensöverföring). |
| UpgradeErrors        | matris med UpgradeErrors      | Fel påträffades vid försök att utföra uppgraderingen, om tillämpligt.           |
| LicenseErrors        | matris med UserLicenseErrrors | Fel påträffades vid försök att migrera användarlicenser, om tillämpligt.          |
| Attribut           | ResourceAttributes          | Metadataattributen som motsvarar licensen.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Beskriver fel som uppstår vid misslyckad överföring av användarlicens.

| Egenskap     | Typ                   | Beskrivning                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | sträng                 | Det unika som identifierats av användarobjektet.                                 |
| Name         | sträng                 | Användarens namn.                                                     |
| E-post        | sträng                 | Användarens e-postadress.                                                    |
| Fel       | matris med ServiceFaults | En lista över undantag som visas när du försöker utföra en överföring av användarlicensen. |
| Attribut   | ResourceAttributes     | Metadataattributen som motsvarar licensen.                     |

