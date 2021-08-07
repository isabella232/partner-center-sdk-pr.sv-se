---
title: Avtalsmetadataresurser
description: Resurssamlingen AgreementMetadata beskriver de avtalstyper som partner kan använda för att bekräfta kundens godkännande.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 7c09dc2a8dd88e3d3a6a7925f6f61737cbbd410eabda6ecb4c3ead13d889de04
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991267"
---
# <a name="agreement-metadata-resources"></a>Avtalsmetadataresurser

**Gäller för:** Partnercenter

**Gäller inte för:** Partner Center som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**AgreementMetaData-resursen** stöds för närvarande endast av Partnercenter i det offentliga Microsoft-molnet. 

**AgreementMetaData-samlingen** innehåller metadata om alla avtalstyper. Partner kan använda den här samlingen för att bekräfta kundens godkännande av avtal. **AgreementMetaData-samlingen** returnerar metadata för båda avtalstyperna (**Microsoft Cloud-avtal** och **Microsoft-kundavtal**).

## <a name="agreementmetadata"></a>AgreementMetaData

Returnerade avtalsmetadata innehåller följande egenskaper:

| Egenskap      | Typ               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | sträng             | Unik identifierare för en avtalsmall.                                       |
| typ          | sträng             | Avtalstyp. Värden som stöds är **för närvarande MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement** (förhandsversion). |
| agreementLink | sträng             | URL för avtalsmallen.                                                    |
