---
title: Produktuppgraderingsresurser
description: Du kan använda flera resurser som rör uppgraderingar av Partner Center-produkter till en Azure-plan. Dessa omfattar ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct och ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0245141dc99832f47bff9b68741724d5d313ab8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768886"
---
# <a name="product-upgrade-resources"></a>Produktuppgraderingsresurser

**Gäller för:**

- Partnercenter

Du kan använda följande resurser för information om Partner Center-produktuppdateringar från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

**ProductUpgradesRequest** -resursen innehåller information om objektet för produkt uppgraderings begär Anden.

| Egenskap | Typ | Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| customerId           | sträng                                       | En GUID-formaterad sträng som identifierar kunden. |
| productFamily        | sträng                                       | Produkt familjen för vilken uppgraderingen begärs. |
| dokumentattribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

**ProductUpgradesEligibility** -resursen ger information om kundens berättigande till uppgradering av en produkt.

| Egenskap | Typ | Description |
|----------------------|--------------------------------------------- |----------------------------------------------------------------|
| customerId           | sträng                                       | En GUID-formaterad sträng som identifierar kunden. |          | productFamily        | sträng                                       | Produkt familjen för vilken uppgraderingen begärs. |
| isEligible           | boolesk                                         | Värdet bool anger om kunden är berättigad till den begärda uppgraderingen. |
| upgradeId            | sträng                                       | Uppgraderings-ID: t om en produkt uppgradering för den aktuella familjen redan är på plats. |
| orsak               | sträng                                       | Orsaken till att kunden inte är berättigad till produkt uppgradering. |
| productFamily        | sträng                                       | Produkt familjen för vilken uppgraderingen begärs. |
| dokumentattribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

**ProductUpgradesStatus** -resursen innehåller information om statusen för en produkt uppgradering.

| Egenskap | Typ | Description |
|---------------------|----------------------------------------------------------------|-----------------------------------------------|
| Id                  | sträng                                                         | En GUID-formaterad sträng som identifierar uppgraderingen. |
| productFamily       | sträng                                                         | Produkt familjen för vilken uppgraderingen begärs.
| status              | sträng                                                         | Status för produkt uppgraderingen.
| Rad objekt           | matris med [UpgradesLineItem](#upgradeslineitem) -resurser       | En matris med objekt som innehåller information om uppgraderings informationen för varje rad objekt som var en del av begär ande texten.
| errorDetails        | [ErrorDetails](#errordetails) -resurs                         | Fel informationen för den begärda uppgraderingen.
| dokumentattribut          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

**UpgradesLineItem** -resursen beskriver status för produkt uppgraderings information för varje rad objekt i begäran.

| Egenskap | Typ | Description |
|-----------------|-----------------------------------------------------|--------------------------------------------------------------|
| sourceProduct   | [UpgradeProduct](#upgradeproduct) -objekt            | Information om käll produkten som uppgraderas. |
| targetProduct   | [UpgradeProduct](#upgradeproduct) -objekt            | Information om mål produktens publicerings uppgradering. |
| upgradedDate    | sträng i UTC-datum/tid-format                      | Det datum då prenumerationen uppgraderades. |
| status          | sträng                                              | Status för produkt uppgraderingen. |
| errorDetails    | [ErrorDetails](#errordetails) -resurs              | Fel informationen för den begärda uppgraderingen. |
| dokumentattribut      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.  |

## <a name="upgradeproduct"></a>UpgradeProduct

**UpgradeProduct** -resursen innehåller information om den produkt som uppgraderas.

| Egenskap | Typ |Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| id                   | sträng                                       | En GUID-formaterad sträng som identifierar produkten. |
| name                 | sträng                                       | Det egna namnet på produkten som uppgraderas. |
| dokumentattribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. |

## <a name="errordetails"></a>ErrorDetails

**ErrorDetails** -resursen innehåller information om fel under uppgraderings processen.

| Egenskap | Typ | Description |
|-------------------------|----------------------------------------------|-------------------------------------------------------------|
| kod                    | sträng                                       | En felkod när produkt uppgraderingen Miss lyckas. |
| meddelande                 | sträng                                       | Fel meddelandet när produkt uppgraderingen Miss lyckas. |
| dokumentattribut              | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. |
