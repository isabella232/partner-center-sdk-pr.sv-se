---
title: Erbjudanderesurser
description: Beskriver en produkt som anges i återförsäljarkatalogen och som de kan erbjuda sina kunder.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a7a0dd2dccc59536797c3ce533d9d8829a04f96
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009230"
---
# <a name="offer-resources"></a>Erbjudanderesurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Beskriver en produkt som anges i återförsäljarkatalogen och som de kan erbjuda sina kunder.

## <a name="offer"></a>Erbjudande

| Egenskap                    | Typ                      | Beskrivning                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | sträng                    | Erbjudandeidentifieraren.                                                                                           |
| name                        | sträng                    | Erbjudandets namn.                                                                                                 |
| beskrivning                 | sträng                    | En beskrivning av erbjudandet.                                                                                     |
| minimumQuantity             | int                       | Minsta tillgängliga kvantitet.                                                                                 |
| maximumQuantity             | int                       | Maximalt antal tillgängliga.                                                                                 |
| rangordning                        | int                       | Erbjudandets rangordning eller prioritet jämfört med andra kategorier i samma produktrad. Den här egenskapen ska endast anges om det finns fler än ett erbjudande för en viss produktrad.  |
| Uri                         | sträng                    | Erbjudandets URI.                                                                                                  |
| locale                      | sträng                    | Det språk som erbjudandet gäller för.                                                                          |
| land                     | sträng                    | Land/region där erbjudandet gäller.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Kategorin för erbjudandet.                                                                   |
| limitUnitOfMeasure          | sträng                    | Ett värde som anger typen av köpbegränsning. Möjliga värden är:<br/> "Ingen" – Det finns inga begränsningar för antalet prenumerationer baserat på det köpta erbjudandet.<br/> "Samtidiga" – Det antal prenumerationer som kan finnas i kundens klientorganisation vid en viss tidpunkt, inklusive prenumerationer som är aktiva eller annullerade. Det här värdet gäller främst för erbjudanden för små företag där antalet licenser är mindre än 300. Avetablering av prenumerationer räknas inte.<br/> "LifeTime" – Antalet prenumerationer som kan finnas under kundens klientorganisations livslängd. Det här värdet är mest tillämpligt för utvärderingsversioner. Avetablering av prenumerationer räknas inte.      |
| gräns                       | int                       | Antalet prenumerationer som kan köpas för det här erbjudandet baserat på limitUnitOfMeasure.                |
| prerequisiteOffers          | sträng                    | De nödvändiga erbjudandena.                                                                                        |
| isAddOn                     | boolean                   | Ett värde som anger om den här instansen är ett tillägg.                                                           |
| hasAddOns                   | boolean                   | Ett värde som anger om det här erbjudandet har några tillägg.                                                           |
| isAvailableForPurchase      | boolean                   | Ett värde som anger om den här instansen är tillgänglig för köp.                                             |
| fakturering                     | sträng                    | Anger faktureringstypen för radartikelinköpet: "none", "usage" eller "license".                           |
| supportedBillingCycles      | matris med strängar          | Anger de faktureringscykler som stöds för det här erbjudandet. Värden som stöds är de medlemsnamn som finns i [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | Ett värde som anger om erbjudandet förnyas automatiskt.                                                      |
| upgradeTargetOffers         | matris med strängar          | Listan över erbjudanden som det här erbjudandet kan uppgraderas till.                                                          |
| conversionTargetOffers      | matris med strängar          | Listan över erbjudanden som det här erbjudandet kan konverteras till.                                                         |
| reselleeQualifications      | matris med strängar          | De kvalificeringar som krävs av kunden för att en partner ska kunna köpa erbjudandet till den kunden.     |
| resellerQualifications      | matris med strängar          | De kvalificeringar som krävs av partnern för att kunna köpa erbjudandet till en kund.                       |
| salesGroupId                | sträng                    | En sträng som används för att gruppera erbjudanden i separata beställningar.                                                             |
| isTrial                     | boolean                   | Ett värde som anger om det här är ett utvärderingserbjudande.                                                               |
| produkt                     | [OfferProduct](#offerproduct)           | Hämtar erbjudandeprodukten.                                                                           |
| unitType                    | sträng                    | Typ av enhet.                                                                                      |
| Länkar                       | [OfferLinks](#offerlinks)               | Erbjudandets länk "Läs mer".                                                                    |
| Attribut                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar erbjudandet.                         |
| AttestationProperties       | [AttestationProperties](#attestationproperties) | Attestationsegenskaperna för en SKU.                   |

## <a name="offercategory"></a>OfferCategory

Beskriver kategorisering av ett erbjudande. Detta inkluderar rangordningen eller prioriteten för den här erbjudandekategorin jämfört med andra i samma produktrad.

| Egenskap   | Typ                                                           | Beskrivning                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | sträng                                                         | Kategoriidentifieraren.                                                                                                                                                   |
| name       | sträng                                                         | Kategorinamnet.                                                                                                                                                         |
| rangordning       | int                                                            | Kategorirankning eller prioritet jämfört med andra kategorier i samma erbjudande. Den här egenskapen ska bara anges om det finns fler än en erbjudandekategori för ett visst erbjudande. |
| locale     | sträng                                                         | Det språk som erbjudandet gäller i.                                                                                                                        |
| land    | sträng                                                         | Land/region där erbjudandet gäller.                                                                                                                   |
| Länkar      | [ResourceLinks](utility-resources.md#resourcelinks)           | Resursen länkar som motsvarar OfferCategory.                                                                                                                     |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar OfferCategory.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Innehåller länkar för att lära dig mer om erbjudandet.

| Egenskap  | Typ | Beskrivning                 |
|-----------|------|-----------------------------|
| learnMore | Länk | Länken "Läs mer".      |
| Själv      | Länk | Själv-URI                |
| nästa      | Länk | Nästa sida med objekt.     |
| Tidigare  | Länk | Föregående sida med objekt. |

## <a name="offerproduct"></a>OfferProduct

En produkt eller tjänst som kan ha fler än ett erbjudande kopplat till sig, var och en med olika uppsättningar funktioner och som är riktad mot olika kundbehov.

| Egenskap | Typ   | Beskrivning              |
|----------|--------|--------------------------|
| Id       | sträng | Kategoriidentifieraren. |
| Namn     | sträng | Kategorinamnet.       |
| Enhet     | sträng | Produktenheten.        |

## <a name="attestationproperties"></a>AttestationProperties

Representerar en attestationstyp och om det krävs för inköp.

| Egenskap              | Typ                                        | Beskrivning                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | sträng                                      | Anger attestationstyp. För Windows 365 är värdet Windows365. Windows 365-attestationstexten är "Jag förstår att varje person som använder Windows 365 Business med Windows Hybrid Benefit också måste ha en giltig kopia av Windows 10/11 Pro installerad på sin primära arbetsenhet." |
| enforceAttestation           | boolean                                      | Anger om attestation krävs för inköp.           |

