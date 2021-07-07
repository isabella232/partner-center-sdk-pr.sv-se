---
title: Avtalsdokumentresurser
description: AgreementDocument-resursen är ett Microsoft-avtalsdokument för förhandsgranskning och nedladdning. Det stöds av Partner Center i Microsofts offentliga moln.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 1a81da4f75594f241669db831125bd437872561c
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025674"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Avtalsdokumentresurser som stöds av PartnerCenter i Microsofts offentliga moln

**Gäller för:** Partnercenter

**Gäller inte för:** Partner Center som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**AgreementDocument-resursen** stöds för närvarande endast av PartnerCenter i Det offentliga Microsoft-molnet.

**AgreementDocument-resursen** representerar ett Microsoft-avtalsdokument som är tillgängligt för förhandsgranskning och nedladdning.

## <a name="agreementdocument"></a>AgreementDocument

En **AgreementDocument-resurs** innehåller följande egenskaper:

| Egenskap       | Typ   | Beskrivning                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| land | sträng | Land eller marknad som det här dokumentet gäller för. |
| language | sträng | Det språk som det här dokumentet är lokaliserat på. |
| displayUri | sträng | En länk för att förhandsgranska avtalsdokumentet i en webbläsare.  |
| downloadUri |sträng | En länk för att ladda ned avtalsdokumentet (i Microsoft Word format). |
