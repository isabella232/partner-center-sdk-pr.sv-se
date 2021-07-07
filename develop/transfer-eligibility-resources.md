---
title: TransferEligibility-resurser
description: En partner kan skapa en överföring när en kund begär sin prenumeration hos partnern som ska överföras till en annan partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530216"
---
# <a name="transfereligibility-resources"></a>TransferEligibility-resurser

En partner kan skapa en överföring när en kund begär sin prenumeration hos partnern som ska överföras till en annan partner. Använd TransferEligibility för att kontrollera om en prenumeration är berättigad att överföras.

## <a name="transfereligibility"></a>Överföringsbarhet

Beskriver överföringEligibility.

| Egenskap              | Typ             | Beskrivning                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | sträng           | Kundens prenumerations-ID.                                                  |
| isEligible            | boolesk             | Anger om prenumerationen är berättigad till överföringen.                         |
| Anledning                | sträng           | Orsaksegenskapen förklarar varför prenumerationen inte är berättigad till överföring. |