---
title: Konverterings resurser
description: Läs om hur du konverterar en utvärderings prenumeration till en betald prenumeration med hjälp av konverterings resurser för partner Center API.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3ade5a5af76e7c637962b6bfe076ac806f337bf
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770068"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Konverterings resurser för att konvertera utvärderings prenumerationer till betalda

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Konverterings resurser stöder konvertering av en utvärderings prenumeration till en betald prenumeration.

## <a name="conversion"></a>Konvertering

Innehåller information som används för att konvertera en utvärderings prenumeration till en betald prenumeration.

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| offerId | sträng | ID för den ursprungliga utvärderings versionen av erbjudandet. |
| targetOfferId | sträng | Erbjudande-ID för mål erbjudandet. |
| orderId | sträng | Order-ID. |
| quantity | int | Antalet licenser. Standardvärdet är antalet licenser i utvärderings prenumerationen. |
| billingCycle | sträng | Anger hur ofta partnern debiteras för prenumerationen. Möjliga värden: **månads** vis (partner faktureras per månad), **årlig** (partner faktureras per år) eller **ingen** (partner faktureras inte. Används för utvärderings prenumerationer). |

## <a name="conversionerror"></a>ConversionError

Representerar ett fel som inträffade under konverteringen.

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| kod | sträng | Felkoden som är kopplad till problemet. Möjliga värden: **övrigt** (allmänt fel), **ConversionsNotFound** (det går inte att hitta några konverteringar för utvärderings prenumerationen att konvertera till).
| beskrivning | sträng | En användarvänlig text som beskriver problemet. |

## <a name="conversionresult"></a>ConversionResult

Representerar resultatet av en prenumerations konvertering.

| Egenskap       | Typ                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | sträng                              | Prenumerations-ID.                                           |
| offerId        | sträng                              | Den ursprungliga erbjudande identifieraren.                                         |
| targetOfferId  | sträng                              | Erbjudande-ID för mål erbjudandet.                             |
| fel          | [ConversionError](#conversionerror) | Felet som påträffades vid försöket att konvertera, om tillämpligt.. |