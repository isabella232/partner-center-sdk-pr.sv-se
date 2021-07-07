---
title: Avtalsresurser
description: Avtalsresursen representerar ett Microsoft-molnkundavtal med information om certifiering som tillhandahålls av partnern.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025633"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Avtalsresurser som representerar ett Microsoft Cloud-kundavtal

**Gäller för:** Partnercenter

**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**Avtalsresursen** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.

**Avtalsresursen** representerar ett Microsoft Cloud-kundavtal.

## <a name="agreement"></a>Avtal

**Avtalsresursen** representerar information om certifiering som tillhandahålls av partnern.

| Egenskap       | Typ   | Beskrivning                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | sträng                         | Objektidentifierare för den inloggade användaren i partnerklientorganisationen som bekräftar för partnerorganisationens räkning. När du använder app- och användarautentisering för att skapa en avtalsresurs, härleder Partnercenter automatiskt **userId-attributvärdet** från app- och användartoken.                                                                             |
| primaryContact | [Kontakt](./utility-resources.md#contact) | Information om användaren från kundorganisationen som godkände avtalet, inklusive:  **firstName,** **lastName,** **email** och **phoneNumber** (valfritt). |
| dateAgreed     | sträng i UTC-datum/tid-format | Det datum då kunden godkände avtalet.                                 |
| templateId     |sträng                          | Unik identifierare för det avtal som kunden har accepterat. |
| typ           |sträng                          | Avtalstyp. Värden som stöds är för **närvarande MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement.**|
| agreementLink  | sträng                         | URL för avtalsmallen.                                                    |
