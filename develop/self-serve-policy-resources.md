---
title: Resurser för självbetjäningsprincipen
description: En partner anger självbetjäningsprinciper för en kund.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffca78481572e201d3ef9f488e7d594a9c1176249b4415a347b488f4b9b81c51
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996775"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy-resurs

En partner anger självbetjäningsprinciper för en kund.

## <a name="selfservepolicy"></a>SelfServePolicy

Beskriver en kundvagn.

| Egenskap              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | En principidentifierare med självbetjäning som tillhandahålls när självbetjäningsprincipen har skapats.     |
| SelfServeEntity       | SelfServeEntity  | Entiteten med självbetjäning som beviljas åtkomst.                                                     |
| Beviljaren               | Beviljaren          | Den beviljande som beviljar åtkomst.                                                                    |
| Behörigheter           | Behörighetsmatris| En matris med [behörighetsresurser.](#permission)                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Representerar den entitet som beviljas behörigheter.

| Egenskap             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | sträng                           | Entiteten beviljas åtkomst, godkända värden: Kund.                                 |
| TenantID             | sträng                           | Klient-ID för den entitet som beviljas åtkomst.                                   |

## <a name="grantor"></a>Beviljaren

Representerar den beviljande som beviljar behörigheterna.

| Egenskap             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | sträng                           | Den beviljande som beviljar åtkomst, godkända värden: BillToPartner.                               |
| TenantID             | sträng                           | Klient-ID för den entitet som beviljar åtkomst.                                       |


## <a name="permission"></a>Behörighet

Representerar en behörighet i självbetjäningsprincipen.

| Egenskap             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Resurs             | sträng                           | Resursåtkomsten beviljas också: AzureReservedInstances.                          |
| Åtgärd               | sträng                           | Åtgärdsåtkomst beviljas för: Köp                                           |
