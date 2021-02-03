---
title: Status för direkt signering (direkt godkännande) för ett kund avtal.
description: DirectSignedCustomerAgreementStatus-resursen representerar statusen för direkt signering (direkt godkännande) för ett kund avtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768796"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Direkt signering (direkt godkännande) status för ett kund avtal

**Gäller för:**

- Partnercenter

**DirectSignedCustomerAgreementStatus** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet.

Den här resursen är *inte tillämplig* för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

**DirectSignedCustomerAgreementStatus** -resursen representerar statusen för det direkta godkännandet för ett kund avtal.

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

En **DirectSignedCustomerAgreementStatus** -resurs innehåller följande egenskaper:

| Egenskap       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | boolean | Anger om kund avtalet har varit direkt signerat (accepterat) av kunden. |
