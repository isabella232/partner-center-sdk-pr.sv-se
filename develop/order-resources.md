---
title: Beställa resurser
description: En partner gör en beställning när en kund vill köpa en prenumeration från en lista över erbjudanden.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b841b73921c9727180e5649ec6a6213081442a8047c6b088e5f9fc6428ef0b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997863"
---
# <a name="order-resources"></a>Beställa resurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

En partner gör en beställning när en kund vill köpa en prenumeration från en lista över erbjudanden.

>[!NOTE]
>Order-resursen har en hastighetsbegränsning på 500 begäranden per minut per klient-ID.

## <a name="order"></a>Beställning

Beskriver en partners beställning.

| Egenskap           | Typ                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | sträng                                             | En orderidentifierare som anges när ordern har skapats.                                   |
| alternateId        | sträng                                             | En användarvänlig identifierare för beställningen.                                                                          |
|referenceCustomerId | sträng                                             | Kundidentifieraren. |
| billingCycle       | sträng                                             | Anger med vilken frekvens partnern faktureras för den här beställningen. Värden som stöds är de medlemsnamn som finns [i BillingCycleType](product-resources.md#billingcycletype). Standardvärdet är "Varje månad" eller "OneTime" när ordern skapas. Det här fältet tillämpas när ordern har skapats. |
| transactionType    | sträng                                             | Skrivskyddade. Beställningens transaktionstyp. Värden som stöds är "UserPurchase", "SystemPurchase" eller "SystemBilling" |
| lineItems          | matris med [OrderLineItem-resurser](#orderlineitem) | En specificerad lista över de erbjudanden som kunden köper, inklusive antalet.        |
| currencyCode       | sträng                                             | Skrivskyddade. Den valuta som används när du gör beställningen. Tillämpas när ordern har skapats.           |
| currencySymbol     | sträng                                             | Skrivskyddade. Valutasymbolen som är associerad med valutakoden. |
| creationDate       | datetime                                           | Skrivskyddade. Det datum då ordern skapades i datum/tid-format. Tillämpas när ordern har skapats.                                   |
| status             | sträng                                             | Skrivskyddade. Status för ordern.  Värden som stöds är de medlemsnamn som finns [**i OrderStatus**](#orderstatus).        |
| Länkar              | [OrderLinks](utility-resources.md#resourcelinks)           | Resursen länkar som motsvarar ordern.            |
| Attribut         | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar ordern.       |

## <a name="orderlineitem"></a>OrderLineItem

En order innehåller en specificerad lista över erbjudanden och varje objekt representeras som en OrderLineItem.

| Egenskap             | Typ                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Varje radobjekt i samlingen får ett unikt radnummer som räknas upp från 0 till count-1.                                                                                                                                                 |
| offerId              | sträng                                    | ID för erbjudandet.                                                                                                                                                                                                                       |
| subscriptionId       | sträng                                    | ID för prenumerationen.                                                                                                                                                                                                                |
| parentSubscriptionId | sträng                                    | Valfritt. ID:t för den överordnade prenumerationen i ett tilläggserbjudande. Gäller endast PATCH.                                                                                                                                                     |
| friendlyName         | sträng                                    | Valfritt. Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydighet.                                                                                                                                              |
| quantity             | int                                       | Antalet licenser eller instanser.                                                                                                                                                                                |
| termDuration         | sträng                                    | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds **är P1M** (1 månad), **P1Y** (1 år) och **P3Y** (3 år).                               |
| transactionType      | sträng                                    | Skrivskyddade. Radobjektets transaktionstyp. Värden som stöds är "new", "renew", "addQuantity", "removeQuantity", "cancel", "convert" eller "customerCredit". |
| partnerIdOnRecord    | sträng                                    | När en indirekt leverantör gör en beställning åt en indirekt återförsäljare fyller du i det här fältet med MPN-ID:t för den indirekta återförsäljaren **(aldrig** DEN indirekta leverantörens ID). Detta säkerställer korrekt redovisning av incitament. |
| provisioningContext  | Ordlista<sträng, sträng>            | Information som krävs för etablering för vissa objekt i katalogen. Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för specifika objekt i katalogen.                                                                                                                                               |
| Länkar                | [OrderLineItemLinks](#orderlineitemlinks) | Skrivskyddade. Resursen länkar som motsvarar orderradsobjektet.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Information om varaktighet för förnyelseperiod.                                                                           |
| AttestationAccepted             | boolesk                 | Anger avtal om att erbjuda eller SKU-villkor. Krävs endast för erbjudanden eller SKU:er där SkuAttestationProperties eller OfferAttestationProperties enforceAttestation är True.                                                                            |

## <a name="renewsto"></a>RenewsTo

Representerar information om förnyelseperiodens varaktighet.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelseperiodens varaktighet. De aktuella värdena som stöds **är P1M** (1 månad) och **P1Y** (1 år). |

## <a name="orderlinks"></a>OrderLinks

Representerar resurslänkarna som motsvarar ordern.

| Egenskap           | Typ                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Länk](utility-resources.md#link)            | När du har fyllt i länken för att hämta etableringsstatus för ordern.       |
| Själv               | [Länk](utility-resources.md#link)            | Länken för att hämta orderresursen.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Representerar den fullständiga prenumeration som är associerad med ordern.

| Egenskap           | Typ                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Länk](utility-resources.md#link)            | När det har fyllts i hämtar länken [etableringsstatusen](#orderlineitemprovisioningstatus) för radobjektet.       |
| sku                | [Länk](utility-resources.md#link)            | Länken för att hämta SKU-information för katalogobjektet som har köpts.                    |
| prenumeration       | [Länk](utility-resources.md#link)            | När du har fyllt i länken till den fullständiga prenumerationsinformationen.                       |
| activationLinks    | [Länk](utility-resources.md#link)            | När den är ifylld innehåller GET-resursen länkar för att aktivera prenumerationen.             |

## <a name="orderstatus"></a>OrderStatus

En [Enum/dotnet/api/system.enum) med värden som anger ordningens tillstånd.

| Värde              | Position     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| okänd            | 0            | Enum-initierare.                               |
| Avslutade          | 1            | Anger att ordern har slutförts.          |
| Väntar            | 2            | Anger att ordern fortfarande väntar.      |
| Annullerat          | 3            | Anger att ordern har avbrutits.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Representerar etableringsstatusen för [en OrderLineItem](#orderlineitem).

| Egenskap                        | Typ                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Det unika radnumret för orderradsobjektet. Värdena sträcker sig från 0 till count-1.             |
| status                          | sträng                              | Etableringsstatus för orderradsobjektet. Exempel på värden:</br>**Uppfyllt:** Slutförande av ordern har slutförts och användaren kommer att kunna använda reservationerna</br>**Unfulfilled:** Inte uppfyllt på grund av annullering</br>**PrefulfillmentPending (Förifyllning** väntar): Din begäran bearbetas fortfarande, slutförande har inte slutförts ännu |
| quantityProvisioningInformation | Lista<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | En lista med statusinformation för kvantitetsetablering för orderradsartikeln. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Representerar etableringsstatus efter kvantitet.

| Egenskap                           | Typ                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Antal objekt.                                 |
| status                             | sträng                                       | Status för antalet objekt.                   |
