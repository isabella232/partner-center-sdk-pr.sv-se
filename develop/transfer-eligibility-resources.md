---
title: TransferEligibility-resurser
description: En partner skapar en överföring när en kund vill att prenumerationen på partnern ska överföras till en annan partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768961"
---
# <a name="transfereligibility-resources"></a>TransferEligibility-resurser

**Gäller för:**

- Partnercenter

En partner skapar en överföring när en kund vill att prenumerationen på partnern ska överföras till en annan partner.

## <a name="transfereligibility"></a>TransferEligibility

Beskriver en transferEligibility.

| Egenskap              | Typ             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | sträng           | Kundens prenumerations-ID.                                                  |
| isEligible            | boolesk             | Anger om prenumerationen är giltig för överföringen.                         |
| Orsak                | sträng           | Egenskapen orsak förklarar varför prenumerationen inte är berättigad till överföring. |