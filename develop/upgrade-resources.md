---
title: Uppgradera resurser
description: Beskriver de resurser som används för att uppgradera en användare från en källprenumeration till en målprenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ea7499a21312378f4fad3d47eaa9e10993ee3ce7ddb1498f161fac16e09b8a5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992488"
---
# <a name="upgrade-resources"></a>Uppgradera resurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Beskriver de resurser som används för att uppgradera en användare från en källprenumeration till en målprenumeration.

## <a name="upgrade"></a>Uppgradera

Beskriver beteendet för en enskild uppgraderingsresurs.

| Egenskap      | Typ                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Erbjudande                  | Erbjudandet om målprenumerationen.                                                        |
| UpgradeType   | sträng                 | Typen av uppgradering: "none", "upgrade \_ only" (endast uppgradering) eller "upgrade \_ with license transfer" (uppgradera \_ med \_ licensöverföring).         |
| IsEligible    | boolean                | Anger om uppgraderingen kan utföras.                                                  |
| Kvantitet      | heltal                | Antalet nya erbjudanden som ska köpas. Standardvärdet är källprenumerationens kvantitet. |
| UpgradeErrors | matris med UpgradeErrors | Orsaker till att uppgraderingen inte kan utföras, om tillämpligt.                                      |
| Attribut    | ResourceAttributes     | Metadataattributen som motsvarar uppgraderingen.                                        |

## <a name="upgradeerror"></a>UpgradeError

Beskriver en orsak till varför en uppgradering inte kan utföras.

| Egenskap          | Typ               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | sträng             | Felkoden som är associerad med problemet: "other", "delegated \_ admin \_ permissions \_ disabled", "subscription \_ status not \_ \_ active", "conflicting \_ service \_ types", "concurrency \_ conflicts", "user \_ context \_ required", "subscription add ons present", "subscription does not have any upgrade \_ \_ \_ \_ \_ \_ \_ \_ \_ paths", "subscription target offer not found" eller "subscription not \_ \_ \_ \_ \_ \_ provisioned". |
| Description       | sträng             | Användarvänlig text som beskriver felet.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | sträng             | Ytterligare information om felet.                                                                                                                                                                                                                                                                                                                                                         |
| Attribut        | ResourceAttributes | Metadataattributen som motsvarar felet.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Beskriver resultatet av prenumerationsuppgraderingsprocessen.

| Egenskap             | Typ                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | sträng                      | Identifieraren för källprenumerationen.                                           |
| TargetSubscriptionID | sträng                      | Identifieraren för målprenumerationen.                                           |
| UpgradeType          | sträng                      | Typen av uppgradering: "none", "upgrade \_ only" (endast uppgradering) eller "upgrade \_ with license transfer" (uppgradera \_ med \_ licensöverföring). |
| UpgradeErrors        | matris med UpgradeErrors      | Fel påträffades vid försök att utföra uppgraderingen, om tillämpligt.           |
| LicenseErrors        | matris med UserLicenseErrrors | Fel påträffades vid försök att migrera användarlicenser, om tillämpligt.          |
| Attribut           | ResourceAttributes          | Metadataattributen som motsvarar licensen.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Beskriver fel som uppstår vid misslyckad överföring av användarlicens.

| Egenskap     | Typ                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | sträng                 | Det unika som identifierats av användarobjektet.                                 |
| Name         | sträng                 | Användarens namn.                                                     |
| E-post        | sträng                 | Användarens e-postadress.                                                    |
| Fel       | matris med ServiceFaults | En lista över undantag som visas när du försöker utföra överföring av användarlicens. |
| Attribut   | ResourceAttributes     | Metadataattributen som motsvarar licensen.                     |

