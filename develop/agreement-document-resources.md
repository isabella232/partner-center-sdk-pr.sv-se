---
title: Avtals dokument resurser
description: AgreementDocument-resursen är ett Microsoft Agreement-dokument för för hands version och nedladdning. Den stöds av Partner Center i det offentliga Microsoft-molnet.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770029"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Avtals dokument resurser som stöds av Partner Center i det offentliga Microsoft-molnet

**Gäller för:**

- Partnercenter

**AgreementDocument** -resursen stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*. Den här resursen är inte tillämplig för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

**AgreementDocument** -resursen representerar ett Microsoft Agreement-dokument som är tillgängligt för för hands version och nedladdning.

## <a name="agreementdocument"></a>AgreementDocument

En **AgreementDocument** -resurs innehåller följande egenskaper:

| Egenskap       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| land | sträng | Landet eller marknaden som detta dokument gäller. |
| language | sträng | Språket som det här dokumentet är lokaliserat till. |
| displayUri | sträng | En länk för att förhandsgranska avtals dokumentet i en webbläsare.  |
| downloadUri |sträng | En länk för att ladda ned avtals dokumentet (i Microsoft Word-format). |
