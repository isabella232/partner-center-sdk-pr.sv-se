---
title: Resurser för tjänstkostnader
description: Beskriver resurser relaterade till tjänster som köpts av en kund.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbddc1973dd9a904cedd549c1772cd4c74c69a60
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547418"
---
# <a name="service-costs-resources"></a>Resurser för tjänstkostnader

Beskriver resurser relaterade till tjänster som köpts av en kund.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** innehåller en sammanfattning som sammanställer alla tjänster som köpts av den angivna kunden under faktureringsperioden.

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| Detaljer | matris med [ServiceCostsSummaryDetail-objekt](#servicecostssummarydetail) | Detaljerad lista över tjänstkostnadssammanfattningar, unikt efter fakturatyp.|
| Länkar | [ResourceLinks](utility-resources.md#resourcelinks) | Resurslänkarna. |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. |

> [!IMPORTANT]
> **Fälten i följande tabell är inaktuella.** Om du vill hämta kostnadssammanfattningar för återkommande och engångstjänster använder du **informationsfältet** i stället. **Informationsfältet** beskrivs i föregående tabell. Se **informationsfältets** motsvarande datavärden, men inte fälten på rotnivå.

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| billingStartDate | date | Början av faktureringsperioden. |
| billingEndDate | date | Slutet av faktureringsperioden. |
| pretaxTotal | double | Summan före skatt av alla kostnader för kunden. |
| Skatt  | double | Den totala skatt som uppstått för alla artiklar som köpts av kunden. |
| afterTaxTotal | double | Den totala nettokostnaden för alla objekt som köpts av kunden. |
| currencyCode | sträng | Representerar den valuta som används för kostnaderna. |
| currencySymbol | sträng | Valutasymbolen som används för kostnaderna. |
| customerId | sträng | ID för den kund som gör köpet. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** beskriver en sammanfattning av tjänstkostnad som aggregerar alla tjänster som köpts av den angivna kunden under faktureringsperioden (från återkommande fakturor eller engångsfakturor).

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| invoiceType | sträng | Den invoiceType som tjänstkostnadssammanfattningen har genererats. |
| sammanfattning | [ServiceCostsSummary](#servicecostssummary) | Sammanfattning av tjänstkostnad sammanställd av en kund under en fakturatyp. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** beskriver ett enskilt objekt som köpts av kunden.

> [!IMPORTANT]
> Följande egenskaper  gäller endast för tjänstkostnadsradobjekt där produkten är ett engångsköp:  **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**. De här *egenskaperna gäller inte för tjänstradsobjekt* där produkten är ett *återkommande köp.* Dessa egenskaper gäller till *exempel inte för prenumerationsbaserade* Office 365 och Azure.

| Egenskap                 | Typ                           | Beskrivning                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| Startdate                | sträng i UTC-datum/tid-format | Startdatumet för avgiften.                                       |
| endDate                  | sträng i UTC-datum/tid-format | Slutdatumet för avgiften.                                         |
| subscriptionFriendlyName | sträng                         | Det egna namnet för prenumerationen.                              |
| subscriptionId           | sträng                         | Prenumerationsidentifieraren.                                         |
| Ordernr                  | sträng                         | Orderidentifieraren.                                                |
| offerId                  | sträng                         | Erbjudandeidentifieraren.                                                |
| offerName                | sträng                         | Erbjudandets namn.                                                      |
| resellerMPNId            | sträng                         | Används endast i partnerscenarier med två nivåer. Refererar till MPN-identifieraren. |
| chargeType               | sträng                         | Den associerade avgiftstypen.                                          |
| quantity                 | antal                         | Antalet enheter som används eller köpts.                             |
| unitPrice                | antal                         | Priset per enhet.                                                  |
| pretaxTotal              | antal                         | Den totala avgiften för det här objektet före skatter.                         |
| Skatt                      | antal                         | Den totala skatteavgiften för det här objektet.                         |
| afterTaxTotal            | antal                         | Den totala nettokostnaden för det här objektet.                                    |
| currencyCode             | sträng                         | Representerar valutan som används för kostnaderna.                          |
| currencySymbol           | sträng                         | Valutasymbolen som används för kostnaderna.                              |
| customerId               | sträng                         | ID för den kund som gör köpet.                          |
| customerName             | sträng                         | Namnet på kunden som gör köpet.                        |
| invoiceNumber            | sträng                         | Det fakturanummer som det här radobjektet tillhör.                   |
| productId                | sträng                         | Produktidentifieraren.                                              |
| skuId                    | sträng                         | SKU-identifieraren.                                                  |
| availabilityId           | sträng                         | Tillgänglighetsidentifieraren.                                         |
| Productname              | sträng                         | Produktnamnet.                                                    |
| skuName                  | sträng                         | SKU-namnet.                                                        |
| publisherName            | sträng                         | Utgivarens namn.                                                  |
| publisherId              | sträng                         | Utgivarens identifierare.                                            |
| termAndBillingCycle      | sträng                         | Period och faktureringsperiod.                                          |
| discountDetails          | sträng                         | Rabattinformationen.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Egenskap             | Typ                               | Beskrivning                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Länk](utility-resources.md#link) | URI:en för att hämta radobjekten. |
| Själv                 | [Länk](utility-resources.md#link) | Själv-URI.                       |
