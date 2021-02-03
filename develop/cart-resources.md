---
title: Shopping vagns resurser
description: En partner placerar en order i en varukorg när en kund vill köpa en prenumeration från en lista över erbjudanden.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3aea428064654077ae67974132ec05918edfee65
ms.sourcegitcommit: a8fe6268fed2162843e7c92dca41c3919b25647d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "97769213"
---
# <a name="cart-resources"></a>Shopping vagns resurser

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

En partner placerar en order när en kund vill köpa en prenumeration från en lista över erbjudanden.

## <a name="cart"></a>Kundvagn

Beskriver en varukorg.

| Egenskap              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | Ett kundvagn-ID som anges när vagnen skapas.                               |
| creationTimeStamp     | DateTime         | Datumet då vagnen skapades i datum-/tids format. Används när vagnen har skapats.      |
| lastModifiedTimeStamp | DateTime         | Datumet då vagnen senast uppdaterades i datum-/tids format. Används när vagnen har skapats. |
| expirationTimeStamp   | DateTime         | Datumet då vagnen upphör att gälla, i datum-/tids format. Används när vagnen har skapats.          |
| lastModifiedUser      | sträng           | Den användare som senast uppdaterade vagnen. Används när vagnen har skapats.                          |
| Rad objekt             | Objekt mat ris | En matris med [CartLineItem](#cartlineitem) -resurser.                                                   |
| status                | sträng           | Status för vagnen. Möjliga värden är "aktiva" (kan uppdateras/skickas) och "beställt" (har redan skickats). |

## <a name="cartlineitem"></a>CartLineItem

Representerar ett objekt som ingår i en varukorg.

| Egenskap             | Typ                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sträng                           | En unik identifierare för ett vagn rads objekt. Används när vagnen har skapats.                                                                   |
| catalogItemId        | sträng                           | Katalog objekt identifierare.                                                                                                                          |
| friendlyName         | sträng                           | Valfritt. Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.                                                                 |
| quantity             | int                              | Antalet licenser eller instanser.                                                                                                                  |
| currencyCode         | sträng                           | Valuta koden.                                                                                                                                    |
| billingCycle         | Objekt                           | Typ av fakturerings cykel som angetts för den aktuella perioden.                                                                                                 |
| termDuration         | sträng                           | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (1 månad), P1Y (1 år) och P3Y (3 år).                                |
| deltagare         | Lista med objekt sträng par      | En samling partner on Record (MPNID) på köpet.                                                                                          |
| provisioningContext  | Ord listans<sträng, sträng>       | Ytterligare kontext som används vid etablering av den köpta artikeln. För att avgöra vilka värden som behövs för ett visst objekt, se SKU: s provisioningVariables-egenskap. |
| orderGroup           | sträng                           | En grupp som visar vilka objekt som kan skickas tillsammans i samma ordning.                                                                          |
| addonItems           | Lista över **CartLineItem** -objekt | En samling av vagn rads objekt för tillägg. De här objekten kommer att köpas mot bas prenumerationen som uppstår från inköpet av rot vagnens rad objekt. |
| fel                | Objekt                           | Tillämpas efter att vagnen har skapats om ett fel har uppstått.                                                                                                    |
| renewsTo             | Objekt mat ris                 | En matris med [RenewsTo](#renewsto) -resurser.                                                                            |

## <a name="renewsto"></a>RenewsTo

Representerar ett objekt som ingår i ett vagn rads objekt.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelse periodens varaktighet. De aktuella värdena som stöds är **P1M** (1 månad) och **P1Y** (1 år). |

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

## <a name="carterror"></a>CartError

Representerar ett fel som inträffar efter att en vagn har skapats.

| Egenskap         | Typ                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [Fel koder för partner Center](error-codes.md) | Typ av fel i kundvagn.                                                                       |
| errorDescription | sträng                                 | Fel beskrivningen, inklusive eventuella kommentarer om värden som stöds, standardvärden eller begränsningar. |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Representerar resultatet av en kundvagn-utcheckning.

| Egenskap    | Typ                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| beställningar      | Lista med [order](order-resources.md#order) objekt.         | Samlingen med beställningar.       |
| orderErrors | Lista över [OrderError](#ordererror) -objekt. | Samling av ordnings fel. |

## <a name="ordererror"></a>OrderError

Representerar ett fel som inträffar under en kundvagn när en order skapas.

| Egenskap     | Typ   | Description                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | sträng | Order grupp-ID: t för ordern med felet. |
| kod         | int    | Felkoden.                                 |
| beskrivning  | sträng | Beskrivningen av felet.                   |
