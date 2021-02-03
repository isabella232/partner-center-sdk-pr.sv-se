---
title: Avtals resurser
description: Avtals resursen representerar ett Microsoft Cloud kund avtal med information om certifieringen som tillhandahålls av partnern.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770020"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Avtals resurser som representerar ett Microsofts moln kund avtal

**Gäller för:**

- Partnercenter

**Avtals** resursen stöds för närvarande av Partner Center i det offentliga Microsoft-molnet. Den gäller inte för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

**Avtals** resursen representerar ett Microsofts moln kund avtal.

## <a name="agreement"></a>Avtal

**Avtals** resursen representerar information om certifieringen som tillhandahålls av partnern.

| Egenskap       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | sträng                         | Objekt identifierare för den inloggade användaren i partner innehavaren som tillhandahåller bekräftelse på uppdrag av partner organisationen. När du använder app + användarautentisering för att skapa en avtals resurs härleder Partner Center automatiskt in **userId** -attributvärdet från App + User token.                                                                             |
| primaryContact | [Kontakt](./utility-resources.md#contact) | Information om användaren från kund organisationen som har godkänt avtalet, inklusive:  **FirstName**, **LastName**, **email** och **telefonnummer** (valfritt). |
| dateAgreed     | sträng i UTC-datum/tid-format | Datumet då kunden godkände avtalet.                                 |
| templateId     |sträng                          | Unik identifierare för det avtal som kunden har accepterat. |
| typ           |sträng                          | Avtals typ. De värden som stöds för närvarande är **MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement**.|
| agreementLink  | sträng                         | URL till avtals mal len.                                                    |
