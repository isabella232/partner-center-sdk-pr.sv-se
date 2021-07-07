---
title: Konverteringsresurser
description: Lär dig mer om hur du använder konverteringsresurser i Partnercenter-API:et för att konvertera en utvärderingsprenumeration till en betald prenumeration.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1863c365627807d8de2534a2d3116807a5de70e1
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973901"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Konverteringsresurser för att konvertera utvärderingsprenumerationer till betalda

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Konverteringsresurser stöder konvertering av en utvärderingsprenumeration till en betald prenumeration.

## <a name="conversion"></a>Konvertering

Innehåller information som används för att konvertera en utvärderingsprenumeration till en betald prenumeration.

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| offerId | sträng | Erbjudandeidentifieraren för det ursprungliga utvärderingserbjudandet. |
| targetOfferId | sträng | Erbjudande-ID för målerbjudandet. |
| Ordernr | sträng | Orderidentifieraren. |
| quantity | int | Antalet licenser. Standardvärdet är antalet licenser i utvärderingsprenumerationen. |
| billingCycle | sträng | Anger hur ofta partnern debiteras för prenumerationen. Möjliga värden: **Varje** månad (partner faktureras månadsvis), **Årlig** (partner faktureras per år) eller **Ingen** (partner faktureras inte. Används för utvärderingsprenumerationer). |

## <a name="conversionerror"></a>ConversionError

Representerar ett fel som uppstod under konverteringen.

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| kod | sträng | Felkoden som är associerad med problemet. Möjliga värden: **Annat** (allmänt fel), **ConversionsNotFound** (det går inte att hitta några konverteringar för utvärderingsprenumerationen att konvertera till).
| beskrivning | sträng | Den egna texten som beskriver problemet. |

## <a name="conversionresult"></a>ConversionResult

Representerar resultatet av en prenumerationskonvertering.

| Egenskap       | Typ                                | Beskrivning                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | sträng                              | Prenumerationsidentifieraren.                                           |
| offerId        | sträng                              | Den ursprungliga erbjudandeidentifieraren.                                         |
| targetOfferId  | sträng                              | Erbjudande-ID för målerbjudandet.                             |
| fel          | [ConversionError](#conversionerror) | Felet påträffades vid försök till konverteringen, om tillämpligt. |