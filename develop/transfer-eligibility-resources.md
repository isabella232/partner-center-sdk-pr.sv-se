---
title: Resurser som kan överföras
description: En partner kan skapa en överföring när en kund begär att en prenumeration hos partnern ska överföras till en annan partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffe72aa04de17cf6e45e49e9fdbec8ba08da2deed89f5d54425a17825c91a53a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996656"
---
# <a name="transfereligibility-resources"></a>Resurser som kan överföras

En partner kan skapa en överföring när en kund begär att en prenumeration hos partnern ska överföras till en annan partner. Använd TransferEligibility för att kontrollera om en prenumeration är berättigad att överföras.

## <a name="transfereligibility"></a>ÖverföringSEligibility

Beskriver överföringEligibility.

| Egenskap              | Typ             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | sträng           | Kundens prenumerations-ID.                                                  |
| isEligible            | boolesk             | Anger om prenumerationen är berättigad till överföringen.                         |
| Anledning                | sträng           | Orsaksegenskapen förklarar varför prenumerationen inte är berättigad till överföring. |