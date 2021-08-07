---
title: Avtalsdokumentresurser
description: AgreementDocument-resursen är ett Microsoft-avtalsdokument för förhandsgranskning och nedladdning. Det stöds av Partner Center i det offentliga Microsoft-molnet.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: eddde1e8072c6aeeee814b52f46c7648d870b6ba63c09b20e4270b17f8386383
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991114"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Avtalsdokumentresurser som stöds av PartnerCenter i Microsofts offentliga moln

**Gäller för:** Partnercenter

**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**AgreementDocument-resursen** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.

**AgreementDocument-resursen** representerar ett Microsoft-avtalsdokument som är tillgängligt för förhandsgranskning och nedladdning.

## <a name="agreementdocument"></a>AgreementDocument

En **AgreementDocument-resurs** innehåller följande egenskaper:

| Egenskap       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| land | sträng | Det land eller den marknad som det här dokumentet gäller för. |
| language | sträng | Det språk som det här dokumentet lokaliseras till. |
| displayUri | sträng | En länk för att förhandsgranska avtalsdokumentet i en webbläsare.  |
| downloadUri |sträng | En länk för att ladda ned avtalsdokumentet (i Microsoft Word format). |
