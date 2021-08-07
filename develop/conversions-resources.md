---
title: Konverteringsresurser
description: Läs mer om hur du använder partnercenter-API-konverteringsresurser för att konvertera en utvärderingsprenumeration till en betald prenumeration.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e7f8985fa15f4959f3cb5a729e492bbb9f3f624a5812f5b87fc119f841dc87e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991879"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Konverteringsresurser för att konvertera utvärderingsprenumerationer till betalda

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Konverteringsresurser stöder konvertering av en utvärderingsprenumeration till en betald prenumeration.

## <a name="conversion"></a>Konvertering

Innehåller information som används för att konvertera en utvärderingsprenumeration till en betald prenumeration.

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| offerId | sträng | Erbjudandeidentifieraren för det ursprungliga utvärderingserbjudandet. |
| targetOfferId | sträng | Erbjudandeidentifieraren för målerbjudandet. |
| Ordernr | sträng | Orderidentifieraren. |
| quantity | int | Antalet licenser. Standardvärdet är antalet licenser i utvärderingsprenumerationen. |
| billingCycle | sträng | Anger hur ofta partnern debiteras för prenumerationen. Möjliga värden: **Varje** månad (partner faktureras månadsvis), **Årlig** (partner faktureras per år) eller **Ingen** (Partner faktureras inte. Används för utvärderingsprenumerationer). |

## <a name="conversionerror"></a>ConversionError

Representerar ett fel som inträffade under konverteringen.

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| kod | sträng | Felkoden som är associerad med problemet. Möjliga värden: **Annat** (allmänt fel), **ConversionsNotFound** (det går inte att hitta några konverteringar för utvärderingsprenumerationen att konvertera till).
| beskrivning | sträng | Den text som beskriver problemet. |

## <a name="conversionresult"></a>ConversionResult

Representerar resultatet av en prenumerationskonvertering.

| Egenskap       | Typ                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | sträng                              | Prenumerationsidentifieraren.                                           |
| offerId        | sträng                              | Den ursprungliga erbjudandeidentifieraren.                                         |
| targetOfferId  | sträng                              | Erbjudandeidentifieraren för målerbjudandet.                             |
| fel          | [ConversionError](#conversionerror) | Felet påträffades vid försök till konverteringen, om tillämpligt. |