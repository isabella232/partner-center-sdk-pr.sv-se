---
title: Erbjudande resurser
description: Beskriver en produkt som listas i åter försäljar katalogen som de kan erbjuda sina kunder.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45af02705d2a03c7586ba6bf3a5537c3e4eec3c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768850"
---
# <a name="offer-resources"></a>Erbjudande resurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Beskriver en produkt som listas i åter försäljar katalogen som de kan erbjuda sina kunder.

## <a name="offer"></a>Erbjudande

| Egenskap                    | Typ                      | Description                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | sträng                    | Erbjudande-ID.                                                                                           |
| name                        | sträng                    | Namnet på erbjudandet.                                                                                                 |
| beskrivning                 | sträng                    | En beskrivning av erbjudandet.                                                                                     |
| minimumQuantity             | int                       | Den minsta tillgängliga kvantiteten.                                                                                 |
| maximumQuantity             | int                       | Högsta tillgängliga kvantitet.                                                                                 |
| rangordning                        | int                       | Rangordningen för erbjudandet eller prioriteten jämfört med andra kategorier i samma produkt serie. Den här egenskapen ska endast anges om det finns fler än ett erbjudande för en angiven produkt linje.  |
| URI                         | sträng                    | Erbjudande-URI.                                                                                                  |
| locale                      | sträng                    | Språkvarianten där erbjudandet gäller.                                                                          |
| land                     | sträng                    | Landet/regionen där erbjudandet gäller.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Erbjudandets kategori.                                                                   |
| limitUnitOfMeasure          | sträng                    | Ett värde som anger typen av inköps begränsning. Möjliga värden är:<br/> "Ingen" – det finns inga begränsningar för antalet prenumerationer baserat på det köpta erbjudandet.<br/> "Samtidig" – antalet prenumerationer som kan finnas på kundens klient vid en specifik tidpunkt, detta omfattar prenumerationer som är aktiva eller annullerade. Det här värdet gäller främst för små företags erbjudanden där licens antalet är mindre än 300. De provisionioned prenumerationerna räknas inte.<br/> "Livstid" – antalet prenumerationer som kan finnas för kundens livs längd. Det här värdet är mest tillämpligt för test versioner. De provisionioned prenumerationerna räknas inte.      |
| gräns                       | int                       | Mängden prenumerationer som kan köpas av det här erbjudandet baserat på limitUnitOfMeasure.                |
| prerequisiteOffers          | sträng                    | Nödvändiga erbjudanden.                                                                                        |
| isAddOn                     | boolean                   | Ett värde som anger om den här instansen är ett tillägg.                                                           |
| hasAddOns                   | boolean                   | Ett värde som anger om det här erbjudandet har något tillägg.                                                           |
| isAvailableForPurchase      | boolean                   | Ett värde som anger om den här instansen är tillgänglig för köp.                                             |
| fakturering                     | sträng                    | Anger fakturerings typen för rad artikel köpet: "ingen", "användning" eller "licens".                           |
| supportedBillingCycles      | matris med strängar          | Anger de fakturerings cykler som stöds för det här erbjudandet. De värden som stöds är medlems namnen som finns i [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | Ett värde som anger om Erbjudandet förnyas automatiskt.                                                      |
| upgradeTargetOffers         | matris med strängar          | Listan med erbjudanden som det här erbjudandet kan uppgraderas till.                                                          |
| conversionTargetOffers      | matris med strängar          | Listan med erbjudanden som det här erbjudandet kan konverteras till.                                                         |
| reselleeQualifications      | matris med strängar          | De kvalifikationer som krävs av kunden för att en partner ska kunna köpa erbjudandet för kunden.     |
| resellerQualifications      | matris med strängar          | De kvalifikationer som krävs av partnern för att kunna köpa erbjudandet för en kund.                       |
| salesGroupId                | sträng                    | En sträng som används för att gruppera erbjudanden i separata beställningar.                                                             |
| isTrial                     | boolean                   | Ett värde som anger om detta är ett utvärderings erbjudande.                                                               |
| produkt                     | [OfferProduct](#offerproduct)           | Hämtar produkt för erbjudandet.                                                                           |
| unitType                    | sträng                    | Enhetens typ.                                                                                      |
| Länkar                       | [OfferLinks](#offerlinks)               | Länken "Läs mer" för erbjudandet.                                                                    |
| dokumentattribut                  | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar erbjudandet.                         |

## <a name="offercategory"></a>OfferCategory

Beskriver kategoriseringen av ett erbjudande. Detta inkluderar rangordningen eller prioriteten för denna erbjudande kategori jämfört med andra på samma produkt serie.

| Egenskap   | Typ                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | sträng                                                         | Kategori-ID.                                                                                                                                                   |
| name       | sträng                                                         | Kategori namnet.                                                                                                                                                         |
| rangordning       | int                                                            | Kategorin rang eller prioritet jämfört med andra kategorier i samma erbjudande. Den här egenskapen ska endast anges om det finns mer än en erbjudande kategori för ett erbjudande. |
| locale     | sträng                                                         | Språkvarianten där erbjudandet gäller.                                                                                                                        |
| land    | sträng                                                         | Landet/regionen där erbjudandet gäller.                                                                                                                   |
| Länkar      | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som motsvarar OfferCategory.                                                                                                                     |
| dokumentattribut | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar OfferCategory.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Innehåller länkar till mer information om erbjudandet.

| Egenskap  | Typ | Description                 |
|-----------|------|-----------------------------|
| learnMore | Länk | Länken "Läs mer".      |
| ständiga      | Länk | Själv URI                |
| nästa      | Länk | Nästa sida med objekt.     |
| ursprungliga  | Länk | Föregående sida med objekt. |

## <a name="offerproduct"></a>OfferProduct

En produkt eller tjänst som kan ha fler än ett erbjudande som är kopplat till den, var och en med olika uppsättning funktioner och riktas mot olika kund behov.

| Egenskap | Typ   | Description              |
|----------|--------|--------------------------|
| Id       | sträng | Kategori-ID. |
| Name     | sträng | Kategori namnet.       |
| Enhet     | sträng | Produkt enheten.        |
