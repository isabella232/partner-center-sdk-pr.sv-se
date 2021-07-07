---
title: Resurser för självbetjäningsprincipen
description: En partner anger självbetjäningsprinciper för en kund.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446725"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy-resurs

En partner anger självbetjäningsprinciper för en kund.

## <a name="selfservepolicy"></a>SelfServePolicy

Beskriver en kundvagn.

| Egenskap              | Typ             | Beskrivning                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | En principidentifierare med självbetjäning som tillhandahålls när självbetjäningsprincipen har skapats.     |
| SelfServeEntity       | SelfServeEntity  | Entiteten med självbetjäning som beviljas åtkomst.                                                     |
| Beviljaren               | Beviljaren          | Den beviljande som beviljar åtkomst.                                                                    |
| Behörigheter           | Behörighetsmatris| En matris med [behörighetsresurser.](#permission)                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Representerar den entitet som beviljas behörigheter.

| Egenskap             | Typ|Beskrivning|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | sträng                           | Entiteten beviljas åtkomst, godkända värden: Kund.                                 |
| TenantID             | sträng                           | Klient-ID för den entitet som beviljas åtkomst.                                   |

## <a name="grantor"></a>Beviljaren

Representerar den beviljande som beviljar behörigheterna.

| Egenskap             | Typ|Beskrivning|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | sträng                           | Den beviljande som beviljar åtkomst, godkända värden: BillToPartner.                               |
| TenantID             | sträng                           | Klient-ID för den entitet som beviljar åtkomst.                                       |


## <a name="permission"></a>Behörighet

Representerar en behörighet i självbetjäningsprincipen.

| Egenskap             | Typ|Beskrivning|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Resurs             | sträng                           | Resursåtkomsten beviljas också: AzureReservedInstances.                          |
| Action               | sträng                           | Åtgärdsåtkomst beviljas för: Köp                                           |
