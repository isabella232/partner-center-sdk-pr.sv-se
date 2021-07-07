---
title: Resurser för avtalsmetadata
description: AgreementMetadata-resurssamlingen beskriver avtalstyper som partner kan använda för att bekräfta kundens godkännande.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025639"
---
# <a name="agreement-metadata-resources"></a>Resurser för avtalsmetadata

**Gäller för:** Partnercenter

**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**AgreementMetaData-resursen** stöds för närvarande endast av Partnercenter i det offentliga Microsoft-molnet. 

**AgreementMetaData-samlingen** innehåller metadata om alla avtalstyper. Partner kan använda den här samlingen för att bekräfta kundens godkännande av avtal. **AgreementMetaData-samlingen** returnerar metadata för båda avtalstyperna (**Microsoft Cloud-avtal** **och Microsoft-kundavtal**).

## <a name="agreementmetadata"></a>AgreementMetaData

Returnerade avtalsmetadata innehåller följande egenskaper:

| Egenskap      | Typ               | Beskrivning                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | sträng             | Unik identifierare för en avtalsmall.                                       |
| typ          | sträng             | Avtalstyp. Värden som stöds är för **närvarande MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement** (förhandsversion). |
| agreementLink | sträng             | URL för avtalsmallen.                                                    |
