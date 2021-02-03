---
title: Kund förbruknings resurser
description: Resurser för kunder med användnings prenumerationer och månatliga användnings budgetar (inklusive CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary och SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ec82fcfe6c08a8ad55dd1fb48984859b954dd3c8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768793"
---
# <a name="customer-usage-resources"></a>Kund förbruknings resurser

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Kunder med användnings prenumerationer kan ha en månads användnings budget. Den här budgeten anger en gräns för kundens maximala användning och gör det möjligt för partner att spåra deras användning över tid.

> [!NOTE]
> Kund användnings nummer är uppskattningar (ej slutliga värden) som inte ska användas för fakturerings syfte.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** representerar den uppskattade penning kostnaden för en kunds användning under den aktuella månaden.

| Egenskap         | Typ               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budget           | SpendingBudget     | Den utgifts budget som har allokerats för kunden.                          |
| PercentUsed      | decimal             | Procent andelen som används av den tilldelade budgeten.                        |
| ResourceId       | sträng             | Resursens unika identifierare.                                   |
| ResourceName     | sträng             | Resursens namn.                                                |
| TotalCost        | decimal             | Den uppskattade totala förbruknings kostnaden för resurserna i prenumerationen.|
| CurrencyLocale   | sträng             | Kundens valuta språk. Tillgängligt för Microsoft Azure (MS-AZR-0145P)-prenumerationer.            |
| CurrencyCode     | sträng             | Hämtar eller anger valuta koden. Tillgängligt för Azure-planer.           |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för Azure-planer.                                         |
| IsUpgraded       | boolesk             | Hämtar eller anger ett värde som anger om kundens Azure-prenumeration uppgraderas. Värdet **True** representerar kunder som har en Azure-prenumeration.                         |
| LastModifiedDate | date               | Datum då användnings data senast ändrades.                               |
| Attribut       | ResourceAttributes | De metadata-attribut som motsvarar användnings posten.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** representerar en sammanfattning av kundens användning för en hel fakturerings period.

| Egenskap         | Typ               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budget           | SpendingBudget     | Den utgifts budget som har allokerats för kunden.                                                                  |
| ResourceId       | sträng             | Resursens unika identifierare. I kontexten för CustomerMonthlyUsageRecord är detta ID kund-ID. |
| ResourceName     | sträng             | Resursens namn. I kontexten för CustomerMonthlyUsageRecord är detta kund namnet.               |
| BillingStartDate | date               | Start datumet för den aktuella fakturerings perioden.                                                                    |
| BillingEndDate   | date               | Slutdatum för den aktuella fakturerings perioden.                                                                      |
| TotalCost        | decimal             | Den uppskattade totala förbruknings kostnaden för resurserna i prenumerationen.                                         |
| CurrencyLocale   | sträng             | Kundens valuta språk. Tillgängligt för Microsoft Azure (MS-AZR-0145P)-prenumerationer.                                         |
| CurrencyCode     | sträng             | Hämtar eller anger valuta koden. Tillgängligt för Azure-planer.                                         |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för Azure plan Subscription-resurser.                                         |
| LastModifiedDate | date               | Datum då användnings data senast ändrades.                                                                       |
| Länkar            | ResourceLinks      | Resurs länkarna som motsvarar användnings sammanfattningen.                                                           |
| Attribut       | ResourceAttributes | De metadata-attribut som motsvarar användnings sammanfattningen.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** representerar en sammanfattning av användnings budgetering på partner nivå för alla kunder.

| Egenskap         | Typ               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | matris med strängar   | Listan med e-postadresser för meddelanden.                                                                   |
| CustomerOverBudget | heltal          | Antalet kunder som är över budget.                                                                    |
| CustomersTrendingOver | heltal       | Antalet kunder som är nära budget.                                                     |
| CustomersWithUsageBasedSubscriptions  | heltal | Antalet kunder med en användnings-baserad prenumeration.                                               |
| ResourceId       | sträng             | Resursens unika identifierare. I kontexten för CustomerMonthlyUsageRecord är detta ID kund-ID. |
| ResourceName     | sträng             | Resursens namn. I kontexten för CustomerMonthlyUsageRecord är detta kund namnet.               |
| BillingStartDate | date               | Start datumet för den aktuella fakturerings perioden.                                                                    |
| BillingEndDate   | date               | Slutdatum för den aktuella fakturerings perioden.                                                                      |
| TotalCost        | decimal             | Den uppskattade totalkostnaden för all kund användning baserat på aktuell användning från början av fakturerings perioden.      |
| CurrencyLocale   | sträng             | Valuta språket.                                                                                             |
| LastModifiedDate | date               | Datum då användnings data senast ändrades.                                                                       |
| Länkar            | ResourceLinks      | Resurs länkarna som motsvarar användnings sammanfattningen.                                                           |
| Attribut       | ResourceAttributes | De metadata-attribut som motsvarar användnings sammanfattningen.                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget** representerar den budget som har tilldelats den här kunden för användnings-baserade prenumerationer.

| Egenskap   | Typ               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Amount     | decimal             | Den tilldelade budgeten. Om värdet är null har ingen utgifts budget allokerats till kunden. |
| Attribut | ResourceAttributes | De metadata-attribut som motsvarar budgeten.                                                |
