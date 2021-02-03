---
title: Avtals resurser för metadata
description: Resurs samlingen AgreementMetadata beskriver avtals typer som partner kan använda för att bekräfta kund godkännande.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768838"
---
# <a name="agreement-metadata-resources"></a>Avtals resurser för metadata

**Gäller för:**

- Partnercenter

**AgreementMetaData** -resursen stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*. Den här resursen gäller inte:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

**AgreementMetaData** -samlingen innehåller metadata om alla avtals typer. Partner kan använda den här samlingen för att tillhandahålla bekräftelse av kund godkännande av avtal. **AgreementMetaData** -samlingen Returnerar metadata för båda avtals typerna (**Microsoft Cloud avtal** och **Microsofts kund avtal**).

## <a name="agreementmetadata"></a>AgreementMetaData

Avtalade metadata som returneras innehåller följande egenskaper:

| Egenskap      | Typ               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | sträng             | Unikt ID för en avtals mal len.                                       |
| typ          | sträng             | Avtals typ. De värden som stöds för närvarande är **MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement** (för hands version). |
| agreementLink | sträng             | URL till avtals mal len.                                                    |
