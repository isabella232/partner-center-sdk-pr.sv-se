---
title: Service kostnads resurser
description: Beskriver resurser som är relaterade till tjänster som köpts av en kund.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0236329d93d8ddc9019a15fb67a81a3af3e7620
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769198"
---
# <a name="service-costs-resources"></a>Service kostnads resurser

**Gäller för:**

- Partnercenter

Beskriver resurser som är relaterade till tjänster som köpts av en kund.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** innehåller en sammanfattning som sammanställer alla tjänster som köpts av den angivna kunden under fakturerings perioden.

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| information | matris med [ServiceCostsSummaryDetail](#servicecostssummarydetail) -objekt | Detalj listan för tjänst kostnads sammanfattning, särskiljs efter faktura typ.|
| Länkar | [ResourceLinks](utility-resources.md#resourcelinks) | Resurs länkarna. |
| dokumentattribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. |

> [!IMPORTANT]
> **Fälten i följande tabell är föråldrade.** Om du vill hämta återkommande och engångs kostnads summeringar använder du fältet **information** i stället. **Informations** fältet beskrivs i föregående tabell. Mer **information** finns i data fältets motsvarande datavärden, men inte på rot nivå fälten.

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| billingStartDate | date | Fakturerings periodens början. |
| billingEndDate | date | Slutet av fakturerings perioden. |
| pretaxTotal | double | Summan före skatt för alla kostnader för kunden. |
| Tax  | double | Den totala skatt som gjorts för alla artiklar som köpts av kunden. |
| afterTaxTotal | double | Den totala totalkostnaden för alla objekt som har köpts av kunden. |
| currencyCode | sträng | Representerar valutan som används för kostnaderna. |
| currencySymbol | sträng | Valuta symbolen som används för kostnaderna. |
| customerId | sträng | ID för kunden som gör köpet. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** beskriver en sammanfattning för tjänst kostnader som sammanställer alla tjänster som köpts av den angivna kunden under fakturerings perioden (från antingen återkommande eller engångs fakturor).

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| invoiceType | sträng | Den invoiceType som service kostnads sammanfattningen har genererats för. |
| sammanfattning | [ServiceCostsSummary](#servicecostssummary) | Tjänste kostnads sammanfattningen som aggregeras av en kund under en faktura typ. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** beskriver ett enda objekt som köps av kunden.

> [!IMPORTANT]
> Följande egenskaper *gäller bara för* service kostnads rad objekt där produkten är ett *Engångs köp*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**. Dessa egenskaper *gäller inte för* service rad objekt där produkten är ett *återkommande köp*. Dessa egenskaper gäller till exempel *inte* för prenumerations Office 365-och Azure-datorer.

| Egenskap                 | Typ                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| /SD                | sträng i UTC-datum/tid-format | Start datumet för avgiften.                                       |
| endDate                  | sträng i UTC-datum/tid-format | Slutdatumet för avgiften.                                         |
| subscriptionFriendlyName | sträng                         | Det egna namnet för prenumerationen.                              |
| subscriptionId           | sträng                         | Prenumerations-ID.                                         |
| orderId                  | sträng                         | Order-ID.                                                |
| offerId                  | sträng                         | Erbjudande-ID.                                                |
| offerName                | sträng                         | Namnet på erbjudandet.                                                      |
| resellerMPNId            | sträng                         | Används endast i scenarier på 2-nivå partner. Hänvisar till MPN-ID: n. |
| chargeType               | sträng                         | Den associerade avgifts typen.                                          |
| quantity                 | antal                         | Antalet enheter som används eller köps.                             |
| unitPrice                | antal                         | Priset per enhet.                                                  |
| pretaxTotal              | antal                         | Den totala kostnaden för den här artikeln före skatt.                         |
| Tax                      | antal                         | Den totala moms avgiften som tillkommer för den här artikeln.                         |
| afterTaxTotal            | antal                         | Den totala netto kostnaden för den här artikeln.                                    |
| currencyCode             | sträng                         | Representerar valutan som används för kostnaderna.                          |
| currencySymbol           | sträng                         | Valuta symbolen som används för kostnaderna.                              |
| customerId               | sträng                         | ID för kunden som gör köpet.                          |
| customerName             | sträng                         | Namnet på kunden som gör köpet.                        |
| invoiceNumber            | sträng                         | Faktura numret som det här rad objektet tillhör.                   |
| productId                | sträng                         | Produkt-ID.                                              |
| skuId                    | sträng                         | SKU-identifieraren.                                                  |
| availabilityId           | sträng                         | Tillgänglighets identifieraren.                                         |
| Namn              | sträng                         | Produkt namnet.                                                    |
| skuName                  | sträng                         | SKU-namn.                                                        |
| publisherName            | sträng                         | Utgivar namnet.                                                  |
| publisherId              | sträng                         | Utgivar-ID.                                            |
| termAndBillingCycle      | sträng                         | Termen och fakturerings perioden.                                          |
| discountDetails          | sträng                         | Rabatt information.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Egenskap             | Typ                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Operationsföljdslänkkod](utility-resources.md#link) | URI: n för att hämta rad objekten. |
| ständiga                 | [Operationsföljdslänkkod](utility-resources.md#link) | Själv URI.                       |
