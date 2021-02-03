---
title: Beställ resurser
description: En partner placerar en order när en kund vill köpa en prenumeration från en lista över erbjudanden.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9db07337a98214b4aaa93e2c8b43b84702249b77
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769231"
---
# <a name="order-resources"></a>Beställ resurser

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

En partner placerar en order när en kund vill köpa en prenumeration från en lista över erbjudanden.

>[!NOTE]
>Order resursen har en hastighets begränsning på 500 förfrågningar per minut per klient-ID.

## <a name="order"></a>Beställning

Beskriver en partners beställning.

| Egenskap           | Typ                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | sträng                                             | En beställnings identifierare som anges när beställningen har skapats.                                   |
| alternateId        | sträng                                             | En egen identifierare för ordern.                                                                          |
|referenceCustomerId | sträng                                             | Kund-ID. |
| billingCycle       | sträng                                             | Anger med vilken frekvens partnern faktureras för den här ordern. De värden som stöds är medlems namnen som finns i [BillingCycleType](product-resources.md#billingcycletype). Standardvärdet är "Monthly" eller "Databasmigrering" när ordern skapas. Det här fältet används när beställningen har skapats. |
| transactionType    | sträng                                             | Skrivskyddad. Transaktions typen för ordern. De värden som stöds är "UserPurchase", "SystemPurchase" eller "SystemBilling" |
| Rad objekt          | matris med [OrderLineItem](#orderlineitem) -resurser | En lista med specificerade erbjudanden som kunden köper inklusive kvantiteten.        |
| currencyCode       | sträng                                             | Skrivskyddad. Den valuta som används när ordern placeras. Används när beställningen har skapats.           |
| currencySymbol     | sträng                                             | Skrivskyddad. Valuta symbolen som är kopplad till valuta koden. |
| creationDate       | datetime                                           | Skrivskyddad. Datumet då ordern skapades i datum-/tids format. Används när beställningen har skapats.                                   |
| status             | sträng                                             | Skrivskyddad. Status för ordern.  De värden som stöds är medlems namnen som finns i [**OrderStatus**](#orderstatus).        |
| Länkar              | [OrderLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som motsvarar beställningen.            |
| dokumentattribut         | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar beställningen.       |

## <a name="orderlineitem"></a>OrderLineItem

En order innehåller en lista över erbjudanden och varje objekt representeras som en OrderLineItem.

| Egenskap             | Typ                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Varje rad objekt i samlingen får ett unikt rad nummer, räknat från 0 till count-1.                                                                                                                                                 |
| offerId              | sträng                                    | ID för erbjudandet.                                                                                                                                                                                                                       |
| subscriptionId       | sträng                                    | Prenumerationens ID.                                                                                                                                                                                                                |
| parentSubscriptionId | sträng                                    | Valfritt. ID: t för den överordnade prenumerationen i ett tilläggs erbjudande. Gäller enbart för korrigering.                                                                                                                                                     |
| friendlyName         | sträng                                    | Valfritt. Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate.                                                                                                                                              |
| quantity             | int                                       | Antalet licenser eller instanser.                                                                                                                                                                                |
| termDuration         | sträng                                    | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är **P1M** (1 månad), **P1Y** (1 år) och **P3Y** (3 år).                               |
| transactionType      | sträng                                    | Skrivskyddad. Transaktions typen för rad artikeln. De värden som stöds är "New", "renew", "addQuantity", "removeQuantity", "Cancel", "Convert" eller "customerCredit". |
| partnerIdOnRecord    | sträng                                    | När en indirekt åter försäljare placerar en indirekt åter försäljare, fyller du i det här fältet med MPN-ID: t för den **indirekta åter försäljaren** (aldrig ID: t för den indirekta providern). Detta säkerställer korrekt redovisning av incitament. |
| provisioningContext  | Ord listans<sträng, sträng>            | Information krävs för etablering av vissa objekt i katalogen. Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för vissa objekt i katalogen.                                                                                                                                               |
| Länkar                | [OrderLineItemLinks](#orderlineitemlinks) | Skrivskyddad. Resurs länkarna som motsvarar order rads objektet.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Varaktighets information för förnyelsens giltighets tid.                                                                           |

## <a name="renewsto"></a>RenewsTo

Representerar varaktigheten för förnyelsens giltighets tid.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelse periodens varaktighet. De aktuella värdena som stöds är **P1M** (1 månad) och **P1Y** (1 år). |

## <a name="orderlinks"></a>OrderLinks

Representerar resurs länkarna som motsvarar beställningen.

| Egenskap           | Typ                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Operationsföljdslänkkod](utility-resources.md#link)            | När du har fyllt i länken kan du hämta etablerings statusen för ordern.       |
| ständiga               | [Operationsföljdslänkkod](utility-resources.md#link)            | Länken för att hämta order resursen.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Representerar den fullständiga prenumeration som är associerad med ordern.

| Egenskap           | Typ                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Operationsföljdslänkkod](utility-resources.md#link)            | När du har fyllt i länken så hämtas [etablerings statusen](#orderlineitemprovisioningstatus) för rad objektet.       |
| sku                | [Operationsföljdslänkkod](utility-resources.md#link)            | Länken för att hämta SKU-information för det köpta katalogobjektet.                    |
| prenumeration       | [Operationsföljdslänkkod](utility-resources.md#link)            | När du har fyllt i länken till den fullständiga prenumerations informationen.                       |
| activationLinks    | [Operationsföljdslänkkod](utility-resources.md#link)            | När du har fyllt i länken Hämta resurs för länkar för att aktivera prenumerationen.             |

## <a name="orderstatus"></a>OrderStatus

En [Enum/dotNet/API/system. Enum) med värden som anger status för ordern.

| Värde              | Position     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| okänd            | 0            | Uppräknings initierare.                               |
| ATS          | 1            | Anger att ordern har slutförts.          |
| Väntar            | 2            | Anger att ordern fortfarande är väntande.      |
| avbröts          | 3            | Anger att ordern har annullerats.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Representerar etablerings statusen för en [OrderLineItem](#orderlineitem).

| Egenskap                        | Typ                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Det unika rad numret för order rads posten. Värden sträcker sig från 0 till count-1.             |
| status                          | sträng                              | Etablerings status för order rads objektet. Exempel på värden:</br>"Uppfyllt": beställningen av ordern har slutförts och användaren kommer att kunna använda reservationerna</br>"Ej uppfyllda": inte uppfyllt på grund av annullering</br>"PrefulfillmentPending": din begäran håller fortfarande på att bearbetas är inte slutförd än |
| quantityProvisioningInformation | Visa<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | En lista med information om kvantitets etablerings status för order rads objektet. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Representerar etablerings statusen per kvantitet.

| Egenskap                           | Typ                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Antal objekt.                                 |
| status                             | sträng                                       | Status för antalet objekt.                   |
