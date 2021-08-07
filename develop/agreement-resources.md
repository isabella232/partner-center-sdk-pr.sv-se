---
title: Avtalsresurser
description: Avtalsresursen representerar ett Microsoft-molnkundavtal med information om certifiering som tillhandahålls av partnern.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: dc67d93a40cdced977412ff8151a661f6655c0fa1d079c8f1bc468f0f8b1eea2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992490"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Avtalsresurser som representerar ett Microsoft Cloud-kundavtal

**Gäller för:** Partnercenter

**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**Avtalsresursen** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.

**Avtalsresursen** representerar ett Microsoft Cloud-kundavtal.

## <a name="agreement"></a>Avtal

**Avtalsresursen** representerar information om certifiering som tillhandahålls av partnern.

| Egenskap       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | sträng                         | Objektidentifierare för den inloggade användaren i partnerklientorganisationen som bekräftar för partnerorganisationens räkning. När du använder app- och användarautentisering för att skapa en avtalsresurs, härleder Partnercenter automatiskt **userId-attributvärdet** från app- och användartoken.                                                                             |
| primaryContact | [Kontakt](./utility-resources.md#contact) | Information om användaren från kundorganisationen som godkände avtalet, inklusive:  **firstName,** **lastName,** **email** och **phoneNumber** (valfritt). |
| dateAgreed     | sträng i UTC-datum/tid-format | Det datum då kunden godkände avtalet.                                 |
| templateId     |sträng                          | Unik identifierare för det avtal som kunden har accepterat. |
| typ           |sträng                          | Avtalstyp. Värden som stöds är för **närvarande MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement.**|
| agreementLink  | sträng                         | URL för avtalsmallen.                                                    |
