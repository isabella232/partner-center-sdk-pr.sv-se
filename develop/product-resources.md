---
title: Produktresurser
description: Resurser som representerar inköpbara varor eller tjänster. Innehåller resurser för att beskriva produkttyp och form (SKU) och för att kontrollera tillgängligheten för produkten i en inventering.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b0269b55810a57dc3a4897027a9817baaebc8ed5f4e98dc66e2eadfa210f362f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997455"
---
# <a name="products-resources"></a>Produktresurser

Resurser som representerar inköpbara varor eller tjänster. Innehåller resurser för att beskriva produkttyp och form (SKU) och för att kontrollera tillgängligheten för produkten i en inventering.

## <a name="product"></a>Produkt

Representerar en köpbar vara eller tjänst. En produkt i sig är inte ett köpbart objekt.

| Egenskap           | Typ                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | sträng                        | ID:t för den här produkten.                                                 |
| title              | sträng                        | Produkttiteln.                                                       |
| beskrivning        | sträng                        | Produktbeskrivningen.                                                 |
| productType        | [ItemType](#itemtype)         | Ett objekt som beskriver typkategorisering(er) för den här produkten.     |
| isMicrosoftProduct | boolesk                          | Anger om det här är en Microsoft-produkt.                          |
| publisherName      | sträng                        | Namnet på produktens utgivare om det är tillgängligt.                          |
| Länkar              | [ProductLinks](#productlinks) | Resurslänkarna i produkten.                         |

## <a name="itemtype"></a>ItemType

Representerar typen av en produkt.

| Egenskap        | Typ                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | sträng                        | Typidentifieraren.                                                                 |
| displayName     | sträng                        | Visningsnamnet för den här typen.                                                      |
| Subtyp         | [ItemType](#itemtype)         | Valfritt. Ett objekt som beskriver en undertypskategorisering för den här objekttypen.     |

## <a name="productlinks"></a>ProductLinks

Innehåller en lista med länkar för en [produkt](#product).

| Egenskap        | Typ                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Sku            | [Länk](utility-resources.md#link)                             | Länken för åtkomst till de underliggande SKU:erna.          |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurslänkarna i den här resursen.   |

## <a name="sku"></a>Sku

Representerar en köpbar lagerhållningsenhet (SKU) under en produkt. Dessa representerar olika former av produkten.

| Egenskap               | Typ             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | sträng           | ID:t för denna SKU. Det här ID:t är endast unikt inom kontexten för dess överordnade produkt. |
| title                  | sträng           | Rubriken på SKU:n.                                                                 |
| beskrivning            | sträng           | Beskrivning av SKU:n.                                                           |
| productId              | sträng           | ID:t för den överordnade [produkt](#product) som innehåller denna SKU.                      |
| minimumQuantity        | int              | Den minsta kvantitet som tillåts för inköp.                                            |
| maximumQuantity        | int              | Den maximala kvantitet som tillåts för inköp.                                            |
| isTrial                | boolesk             | Anger om denna SKU är ett utvärderingsobjekt.                                           |
| supportedBillingCycles | matris med strängar | Listan över faktureringscykler som stöds för denna SKU. Värden som stöds är de medlemsnamn som finns [i BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | matris med strängar | Listan över nödvändiga steg eller åtgärder som krävs innan du köper det här objektet. Värdena som stöds är:<br/>  "InventoryCheck" – Anger att objektets inventering ska utvärderas innan du försöker köpa det här objektet.<br/> "AzureSubscriptionRegistration" – Anger att en Azure-prenumeration krävs och måste registreras innan du försöker köpa det här objektet.  |
| inventoryVariables     | matris med strängar | Listan över variabler som behövs för att utföra en inventeringskontroll för det här objektet. Värdena som stöds är:<br/> "CustomerId" – ID:t för kunden som köpet gäller.<br/> "AzureSubscriptionId" – ID:t för den Azure-prenumeration som ska användas för ett Azure-reservationsköp.</br> "ArmRegionName" – Den region som inventeringen ska verifieras för. Det här värdet måste matcha "ArmRegionName" från SKU:ns DynamicAttributes. |
| provisioningVariables  | matris med strängar | Listan över variabler som måste anges i etableringskontexten för ett kundvagnsradsobjekt [när du](cart-resources.md#cartlineitem) köper det här objektet. Värdena som stöds är:<br/> Omfång – Omfånget för ett Azure-reservationsköp: "Enkel", "Delad".<br/> "SubscriptionId" – ID:t för den Azure-prenumeration som ska användas för ett Azure-reservationsköp.<br/> "Duration" – Varaktigheten för Azure-reservationen: "1Year", "3Year".  |
| dynamicAttributes      | nyckel/värde-par  | Ordlistan med dynamiska egenskaper som gäller för det här objektet. Egenskaperna i den här ordlistan är dynamiska och kan ändras utan föregående meddelande. Du bör inte skapa starka beroenden på specifika nycklar som finns i värdet för den här egenskapen.    |
| Länkar                  | [ResourceLinks](utility-resources.md#resourcelinks) | Resurslänkarna i SKU:n.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | Attestationsegenskaperna för en SKU.                   |

## <a name="availability"></a>Tillgänglighet

Representerar en konfiguration där en SKU är tillgänglig för inköp (till exempel land, valuta och branschsegment).

| Egenskap        | Typ                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | sträng                        | ID för den här tillgängligheten. Det här ID:t är endast unikt inom kontexten för dess [överordnade produkt](#product) och [SKU.](#sku) **Obs!** Detta ID kan ändras med tiden. Du bör bara förlita dig på det här värdet inom ett kort tidsintervall när du har hämtat det.  |
| productId       | sträng                        | ID:t för [den produkt](#product) som innehåller den här tillgängligheten.           |
| skuId           | sträng                        | ID för den [SKU som](#sku) innehåller den här tillgängligheten.                   |
| catalogItemId   | sträng                        | Den unika identifieraren för det här objektet i katalogen. Detta är det ID som måste fyllas i i egenskaperna [OrderLineItem.OfferId](order-resources.md#orderlineitem) eller [CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) när du köper den överordnade [SKU:n](#sku). **Obs!** Detta ID kan ändras med tiden. Du bör bara förlita dig på det här värdet inom en kort tid efter att det har hämtas. Den bör endast nås och användas vid tidpunkten för köpet.  |
| defaultCurrency | sträng                        | Standardvalutan som stöds för den här tillgängligheten.                               |
| segment         | sträng                        | Branschsegmentet för den här tillgängligheten. Värden som stöds är: Commercial, Education, Government, NonProfit. |
| land         | sträng                                              | Land eller region (i ISO-landskodsformat) där den här tillgängligheten gäller. |
| isPurchasable   | boolesk                                                | Anger om den här tillgängligheten är köpbar. |
| isRenewable     | boolesk                                                | Anger om den här tillgängligheten kan förnyas. |
| produkt      | [Produkt](#product)               | Den produkt som tillgängligheten motsvarar. |
| sku          | [Sku](#sku)            | Den SKU som tillgängligheten motsvarar. |
| Villkor           | matris med [termresurser](#term)  | Den samling villkor som gäller för den här tillgängligheten. |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks) | Resurslänkarna som finns i tillgängligheten. |

## <a name="term"></a>Period

Representerar en term som tillgängligheten kan köpas för.

| Egenskap              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| varaktighet              | sträng                                      | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (1 månad), P1Y (1 år) och P3Y (3 år). |
| beskrivning           | sträng                                      | Beskrivning av termen.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Representerar en begäran om att kontrollera inventeringen mot vissa katalogobjekt.

| Egenskap         | Typ                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | matris med [InventoryItem](#inventoryitem)            | Listan över katalogobjekt som inventeringskontrollen ska utvärdera.                           |
| inventoryContext | nyckel/värde-par                                     | Ordlistan med kontextvärden som behövs för att utföra inventeringskontrollerna. Varje [SKU](#sku) för produkterna definierar vilka värden (om några) som behövs för att utföra den här åtgärden.  |
| Länkar            | [ResourceLinks](utility-resources.md#resourcelinks) | Resurslänkarna i inventeringskontrollens begäran.                            |

## <a name="inventoryitem"></a>InventoryItem

Representerar ett enskilt objekt i en inventeringskontrollåtgärd. Den här resursen används för att ange målobjekten i en indatabegäran och används också för att representera utdataresultatet från inventeringskontrollen.

| Egenskap         | Typ                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | sträng                                                            | (Krävs) ID för [produkten](#product).                            |
| skuId            | sträng                                                            | ID för [SKU:n](#sku). När du använder den här resursen som indata för en inventeringsbegäran är det här värdet valfritt. Om det här värdet inte anges betraktas alla SKU:er under produkten som målobjekt i inventeringskontrollen.      |
| isRestricted     | boolesk                                                              | Anger om det här objektet hittades för ett begränsat lager.            |
| Begränsningar     | matris med [InventoryRestriction](#inventoryrestriction)            | Information om eventuella begränsningar som hittas för det här objektet. Den här egenskapen fylls bara i om **isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Visar information om en inventeringsbegränsning. Detta gäller endast för inventeringskontrollens utdataresultat, inte för indatabegäranden.

| Egenskap         | Typ                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | sträng                | Den kod som identifierar orsaken till begränsningen.                                    |
| beskrivning      | sträng                | Beskrivning av inventeringsbegränsningen.                                               |
| properties       | nyckel/värde-par       | Ordlistan med egenskaper som kan ge ytterligare information om begränsningen.           |

## <a name="billingcycletype"></a>BillingCycleType

En [Enum/dotnet/api/system.enum) med värden som anger en typ av faktureringsperiod.

| Värde              | Position     | Beskrivning                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Okänt            | 0            | Enum-initierare.                                                                          |
| Månadsvis            | 1            | Anger att partnern debiteras månadsvis.                                        |
| Årsvis             | 2            | Anger att partnern debiteras per år.                                       |
| Ingen               | 3            | Anger att partnern inte kommer att debiteras. Det här värdet kan användas för utvärderingsobjekt.    |
| Onetime            | 4            | Anger att partnern debiteras en gång.                                       |

## <a name="attestationproperties"></a>AttestationProperties

Representerar en attestationstyp och om det krävs för inköp.

| Egenskap              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | sträng                                      | Anger attestationstyp. För Windows 365 är värdet Windows365. Windows 365-attereringstexten är "Jag förstår att varje person som använder Windows 365 Business med Windows Hybrid Benefit också måste ha en giltig kopia av Windows 10/11 Pro installerad på sin primära arbetsenhet." |
| enforceAttestation           | boolean                                      | Anger om attestation krävs för inköp.           |
