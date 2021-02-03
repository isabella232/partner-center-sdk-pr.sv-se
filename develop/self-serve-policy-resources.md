---
title: Självbetjänings princip resurser
description: En partner ställer in självbetjänings principer för en kund.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768952"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy-resurs

**Gäller för:**

- Partnercenter

En partner ställer in självbetjänings principer för en kund.

## <a name="selfservepolicy"></a>SelfServePolicy

Beskriver en varukorg.

| Egenskap              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | En princip identifierare för egen installation som anges när du skapar den själv fungerande principen.     |
| SelfServeEntity       | SelfServeEntity  | Den själv betjänande entitet som beviljas åtkomst.                                                     |
| Den beviljande användaren               | Den beviljande användaren          | Den beviljande behörighet som beviljar åtkomst.                                                                    |
| Behörigheter           | Behörighets mat ris| En matris med [behörighets](#permission) resurser.                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Representerar den entitet som beviljats behörigheter.

| Egenskap             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | sträng                           | Entiteten beviljas åtkomst, godkända värden: kund.                                 |
| TenantID             | sträng                           | Klient-ID: n för den entitet som har beviljats åtkomst.                                   |

## <a name="grantor"></a>Den beviljande användaren

Representerar den beviljande behörighet som beviljar behörighet.

| Egenskap             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | sträng                           | Den beviljande användaren beviljar åtkomst, godkända värden: BillToPartner.                               |
| TenantID             | sträng                           | Klient-ID för entiteten som beviljar åtkomst.                                       |


## <a name="permission"></a>Behörighet

Representerar en behörighet i den självbetjänings principen.

| Egenskap             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Resurs             | sträng                           | Resurs åtkomsten beviljas för: AzureReservedInstances.                          |
| Action               | sträng                           | Åtkomst till åtgärden beviljas för: Köp                                           |
