---
title: Produkt resurser
description: Resurser som representerar köpbara-varor eller-tjänster. Innehåller resurser för att beskriva produkt typ och-form (SKU) och för att kontrol lera tillgängligheten för produkten i en inventering.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a3cfacd3654e85a9824759295f97792ff740d85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769228"
---
# <a name="products-resources"></a>Produkt resurser

**Gäller för**

- Partnercenter

Resurser som representerar köpbara-varor eller-tjänster. Innehåller resurser för att beskriva produkt typ och-form (SKU) och för att kontrol lera tillgängligheten för produkten i en inventering.

## <a name="product"></a>Produkt

Representerar en köpbara-eller tjänst. En produkt som själva är inte ett köpbara-objekt.

| Egenskap           | Typ                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | sträng                        | ID för den här produkten.                                                 |
| title              | sträng                        | Produkt titeln.                                                       |
| beskrivning        | sträng                        | Produkt beskrivningen.                                                 |
| productType        | [ItemType](#itemtype)         | Ett objekt som beskriver typ kategorisering (er) av den här produkten.     |
| isMicrosoftProduct | boolesk                          | Anger om det här är en Microsoft-produkt.                          |
| publisherName      | sträng                        | Namnet på produktens utgivare om det är tillgängligt.                          |
| Länkar              | [ProductLinks](#productlinks) | Resurs länkarna som ingår i produkten.                         |

## <a name="itemtype"></a>ItemType

Representerar typen av en produkt.

| Egenskap        | Typ                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | sträng                        | Typ identifieraren.                                                                 |
| displayName     | sträng                        | Visnings namnet för den här typen.                                                      |
| Undertyp         | [ItemType](#itemtype)         | Valfritt. Ett objekt som beskriver kategorisering av under typer för den här objekt typen.     |

## <a name="productlinks"></a>ProductLinks

Innehåller en lista med länkar till en [produkt](#product).

| Egenskap        | Typ                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| enheter            | [Operationsföljdslänkkod](utility-resources.md#link)                             | Länken för att komma åt de underliggande SKU: erna.          |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som finns i den här resursen.   |

## <a name="sku"></a>Sku

Representerar en köpbara lagerhållnings enhet (SKU) under en produkt. Dessa representerar olika former av produkten.

| Egenskap               | Typ             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | sträng           | ID för denna SKU. Detta ID är endast unikt inom kontexten för den överordnade produkten. |
| title                  | sträng           | Rubriken på SKU: n.                                                                 |
| beskrivning            | sträng           | Beskrivningen av SKU: n.                                                           |
| productId              | sträng           | ID för den överordnade [produkten](#product) som innehåller denna SKU.                      |
| minimumQuantity        | int              | Den minsta kvantitet som tillåts för köp.                                            |
| maximumQuantity        | int              | Den högsta kvantitet som tillåts för köp.                                            |
| isTrial                | boolesk             | Indikerar om denna SKU är ett utvärderings objekt.                                           |
| supportedBillingCycles | matris med strängar | Listan över fakturerings cykler som stöds för denna SKU. De värden som stöds är medlems namnen som finns i [BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | matris med strängar | Listan över nödvändiga steg eller åtgärder som krävs innan du köper det här objektet. De värden som stöds är:<br/>  "InventoryCheck" – anger att objektets inventering ska utvärderas innan du försöker köpa den här artikeln.<br/> "AzureSubscriptionRegistration" – visar att en Azure-prenumeration behövs och måste registreras innan du försöker köpa det här objektet.  |
| inventoryVariables     | matris med strängar | En lista med variabler som krävs för att köra en inventerings kontroll på det här objektet. De värden som stöds är:<br/> "CustomerId" – ID: t för kunden som köpet är för.<br/> "AzureSubscriptionId" – ID: t för den Azure-prenumeration som ska användas för ett Azure reservations köp.</br> "ArmRegionName" – den region som du vill verifiera inventeringen för. Värdet måste matcha "ArmRegionName" från SKU: n DynamicAttributes. |
| provisioningVariables  | matris med strängar | En lista med variabler som måste tillhandahållas i etablerings kontexten för ett [vagn rads objekt](cart-resources.md#cartlineitem) vid köp av den här artikeln. De värden som stöds är:<br/> Omfattning – omfånget för ett Azure reservations köp: "Single", "Shared".<br/> "SubscriptionId" – ID: t för den Azure-prenumeration som ska användas för ett Azure reservations köp.<br/> "Varaktighet" – varaktigheten för Azure-reservationen: "1Year", "3Year".  |
| dynamicAttributes      | nyckel/värde-par  | Ord listan för dynamiska egenskaper som gäller för det här objektet. Observera att egenskaperna i den här ord listan är dynamiska och kan ändras utan föregående meddelande. Du bör inte skapa starka beroenden för vissa nycklar som är befintliga i värdet för den här egenskapen.    |
| Länkar                  | [ResourceLinks](utility-resources.md#resourcelinks) | Resurs länkarna som ingår i SKU: n.                   |

## <a name="availability"></a>Tillgänglighet

Representerar en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta och bransch segment).

| Egenskap        | Typ                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | sträng                        | ID för denna tillgänglighet. Detta ID är endast unikt inom kontexten för den överordnade [produkten](#product) och [SKU: n](#sku). **Obs!** Detta ID kan ändras med tiden. Använd bara det här värdet inom ett kort tidsintervall efter att du har hämtat det.  |
| productId       | sträng                        | ID för den [produkt](#product) som innehåller denna tillgänglighet.           |
| skuId           | sträng                        | ID för den [SKU](#sku) som innehåller denna tillgänglighet.                   |
| catalogItemId   | sträng                        | Den unika identifieraren för det här objektet i katalogen. Detta är det ID som måste vara ifyllt i egenskaperna [OrderLineItem. OfferID](order-resources.md#orderlineitem) eller [CartLineItem. CatalogItemId](cart-resources.md#cartlineitem) när du köper den överordnade [SKU: n](#sku). **Obs!** Detta ID kan ändras med tiden. Du bör endast använda detta värde inom kort tid efter att det har hämtats. Den bör endast användas och användas vid tidpunkten för köpet.  |
| defaultCurrency | sträng                        | Standard valutan som stöds för denna tillgänglighet.                               |
| segment         | sträng                        | Bransch segmentet för denna tillgänglighet. De värden som stöds är: kommersiell, utbildning, myndigheter, icke-vinst. |
| land         | sträng                                              | Landet eller regionen (i ISO-format för landskod) där denna tillgänglighet gäller. |
| isPurchasable   | boolesk                                                | Indikerar om denna tillgänglighet är köpbara. |
| isRenewable     | boolesk                                                | Anger om den här tillgängligheten har förnyats. |
| produkt      | [Produkt](#product)               | Produkten som denna tillgänglighet motsvarar. |
| sku          | [SKU](#sku)            | SKU: n som denna tillgänglighet motsvarar. |
| begreppen           | matris med [term](#term) resurser  | Den samling av villkor som gäller för denna tillgänglighet. |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks) | Resurs länkarna som finns i tillgänglighet. |

## <a name="term"></a>Term

Representerar en period för vilken tillgänglighet kan köpas.

| Egenskap              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| varaktighet              | sträng                                      | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (1 månad), P1Y (1 år) och P3Y (3 år). |
| beskrivning           | sträng                                      | Beskrivningen av termen.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Representerar en begäran om att kontrol lera lagret mot vissa katalog objekt.

| Egenskap         | Typ                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | matris med [InventoryItem](#inventoryitem)            | Listan över katalog objekt som inventerings kontrollen kommer att utvärdera.                           |
| inventoryContext | nyckel/värde-par                                     | Ord listan för de kontext värden som behövs för att genomföra lager kontroll (er). Varje [SKU](#sku) av produkterna definierar vilka värden (om sådana finns) som krävs för att utföra den här åtgärden.  |
| Länkar            | [ResourceLinks](utility-resources.md#resourcelinks) | Resurs länkarna i begäran om inventerings kontroll.                            |

## <a name="inventoryitem"></a>InventoryItem

Representerar ett enskilt objekt i en inventerings kontroll. Den här resursen används för att ange mål objekt i en indata-begäran och används också för att representera resultatet av resultatet av inventerings kontrollen.

| Egenskap         | Typ                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | sträng                                                            | Kunna [Produktens](#product)ID.                            |
| skuId            | sträng                                                            | ID för SKU: [n](#sku). Det här värdet är valfritt när du använder den här resursen som indatamängd för en inventerings förfrågan. Om det här värdet inte anges kommer alla SKU: er under produkten att anses som mål objekt i inventerings kontrollen.      |
| isRestricted     | boolesk                                                              | Anger om det här objektet hittades ha en begränsad inventering.            |
| rättigheter     | matris med [InventoryRestriction](#inventoryrestriction)            | Information om eventuella begränsningar som har hittats för det här objektet. Den här egenskapen kommer bara att fyllas i om **isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Visar information om en inventerings begränsning. Detta gäller endast för resultat från inventerings kontroll, inte för indata-begäranden.

| Egenskap         | Typ                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | sträng                | Den kod som identifierar orsaken till begränsningen.                                    |
| beskrivning      | sträng                | Beskrivningen av inventerings begränsningen.                                               |
| properties       | nyckel/värde-par       | Ord lista med egenskaper som kan innehålla ytterligare information om begränsningen.           |

## <a name="billingcycletype"></a>BillingCycleType

En [Enum/dotNet/API/system. Enum) med värden som anger en typ av fakturerings cykel.

| Värde              | Position     | Beskrivning                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Okänt            | 0            | Uppräknings initierare.                                                                          |
| Varje månad            | 1            | Anger att partnern debiteras månads vis.                                        |
| Årsvis             | 2            | Anger att partnern ska debiteras per år.                                       |
| Inget               | 3            | Anger att partnern inte kommer att debiteras. Det här värdet kan användas för utvärderings objekt.    |
| Databasmigrering            | 4            | Anger att partnern kommer att debiteras en gången.                                       |
