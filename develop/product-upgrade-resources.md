---
title: Produktuppgraderingsresurser
description: Du kan använda flera resurser relaterade till Partner Center-produktuppgraderingar till en Azure-plan. Dessa inkluderar ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct och ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a251168dbe1e153365beec212feca6fafddaef1700ad8651ec9d459aebf24600
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997404"
---
# <a name="product-upgrade-resources"></a>Produktuppgraderingsresurser

Du kan använda följande resurser för information om produktuppgraderingar i Partnercenter från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

Resursen **ProductUpgradesRequest innehåller** information om objektet för begäran om produktuppgraderingar.

| Egenskap      | Typ                                                          | Description                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | sträng                                                        | En GUID-formaterad sträng som identifierar kunden.      |
| productFamily | sträng                                                        | Den produktfamilj som uppgraderingen begärs för. |
| Attribut    | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

Resursen **ProductUpgradesEligibility** innehåller information om kundens behörighet att uppgradera en produkt.

| Egenskap      | Typ                                                          | Description                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | sträng                                                        | En GUID-formaterad sträng som identifierar kunden.                            |
| productFamily | sträng                                                        | Den produktfamilj som uppgraderingen begärs för.                       |
| isEligible    | boolesk                                                          | Bool-värdet anger om kunden är berättigad till begärd uppgradering. |
| upgradeId     | sträng                                                        | Uppgraderings-ID:t om en produktuppgradering för en viss familj redan finns på plats.        |
| orsak        | sträng                                                        | Orsaken till varför kunden inte är berättigad till produktuppgradering.                |
| productFamily | sträng                                                        | Den produktfamilj som uppgraderingen begärs för.                       |
| Attribut    | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

Resursen **ProductUpgradesStatus** innehåller information om statusen för en produktuppgradering.

| Egenskap | Typ   | Description                                          |
|----------|--------|------------------------------------------------------|
| Id       | sträng | En GUID-formaterad sträng som identifierar uppgraderingen. |
| productFamily       | sträng                                                         | Den produktfamilj som uppgraderingen begärs för.
| status              | sträng                                                         | Status för produktuppgraderingen.
| lineItems           | matris med [UpgradesLineItem-resurser](#upgradeslineitem)       | En matris med objekt som innehåller information om uppgraderingsinformationen för varje radobjekt som ingick i begärandetexten.
| errorDetails        | [ErrorDetails-resurs](#errordetails)                         | Felinformationen för den begärda uppgraderingen.
| Attribut          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

Resursen **UpgradesLineItem** beskriver statusen för produktuppgraderingsinformationen för varje radobjekt i begäran.

| Egenskap      | Typ                                                          | Description                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct | [UpgradeProduct-objekt](#upgradeproduct)                      | Information om källprodukten som uppgraderas. |
| targetProduct | [UpgradeProduct-objekt](#upgradeproduct)                      | Information om målprodukten efter uppgraderingen.   |
| upgradedDate  | sträng i UTC-datum/tid-format                                | Det datum då prenumerationen uppgraderades.           |
| status        | sträng                                                        | Status för produktuppgraderingen.                |
| errorDetails  | [ErrorDetails-resurs](#errordetails)                        | Felinformationen för den begärda uppgraderingen.          |
| Attribut    | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                          |

## <a name="upgradeproduct"></a>UpgradeProduct

Resursen **UpgradeProduct** innehåller information om den produkt som uppgraderas.

| Egenskap   | Typ                                                          | Description                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| id         | sträng                                                        | En GUID-formaterad sträng som identifierar produkten. |
| name       | sträng                                                        | Det egna namnet på den produkt som uppgraderas.         |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                             |

## <a name="errordetails"></a>ErrorDetails

**ErrorDetails-resursen** innehåller information om fel under uppgraderingsprocessen.

| Egenskap   | Typ                                                          | Description                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| kod       | sträng                                                        | En felkod när produktuppgraderingen misslyckas.      |
| meddelande    | sträng                                                        | Felmeddelandet när produktuppgraderingen misslyckas. |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                          |
