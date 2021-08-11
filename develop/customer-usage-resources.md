---
title: Resurser för kundanvändning
description: Resurser för kunder med användningsbaserade prenumerationer och budgetar för månatlig användning (inklusive CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary och SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066fd84f872365b419796f00125c097c685f4579731aaacd67e826bf671bd789
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995160"
---
# <a name="customer-usage-resources"></a>Resurser för kundanvändning

**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Kunder med användningsbaserade prenumerationer kan ha en månatlig användningsbudget. Den här budgeten anger en gräns för kundens maximala användning och gör att partnern kan spåra sin användning över tid.

> [!NOTE]
> Kundanvändningsnummer är uppskattningar (inte slutliga värden), som inte ska användas i faktureringssyfte.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** representerar den uppskattade penningkostnaden för en kunds användning under den aktuella månaden.

| Egenskap         | Typ               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budget           | Utgiftsbudget     | Den allokerade utgiftsbudgeten för kunden.                          |
| Procentanvänd      | decimal             | Procentandelen som används av den allokerade budgeten.                        |
| ResourceId       | sträng             | Resursens unika identifierare.                                   |
| ResourceName     | sträng             | Namnet på resursen.                                                |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för användning för resurserna i prenumerationen.|
| CurrencyLocale   | sträng             | Kundens nationella valuta. Tillgängligt för Microsoft Azure prenumerationer (MS-AZR-0145P).            |
| CurrencyCode     | sträng             | Hämtar eller anger valutakoden. Tillgängligt för Azure-planer.           |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för Azure-planer.                                         |
| IsUpgraded       | boolesk             | Hämtar eller anger ett värde som anger om kundens Azure-prenumeration har uppgraderats. Värdet true **representerar** kunder som har en Azure-plan.                         |
| LastModifiedDate | date               | Det datum då användningsdata senast ändrades.                               |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar användningsposten.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** representerar en sammanfattning av kundens användning under en hel faktureringsperiod.

| Egenskap         | Typ               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budget           | Utgiftsbudget     | Den allokerade utgiftsbudgeten för kunden.                                                                  |
| ResourceId       | sträng             | Resursens unika identifierare. I kontexten CustomerMonthlyUsageRecord är detta ID kund-ID. |
| ResourceName     | sträng             | Namnet på resursen. I kontexten CustomerMonthlyUsageRecord är det här kundnamnet.               |
| BillingStartDate | date               | Startdatumet för den aktuella faktureringsperioden.                                                                    |
| BillingEndDate   | date               | Slutdatumet för den aktuella faktureringsperioden.                                                                      |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för användning för resurserna i prenumerationen.                                         |
| CurrencyLocale   | sträng             | Kundens nationella valuta. Tillgängligt för Microsoft Azure prenumerationer (MS-AZR-0145P).                                         |
| CurrencyCode     | sträng             | Hämtar eller anger valutakoden. Tillgängligt för Azure-planer.                                         |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för prenumerationsresurser för Azure-plan.                                         |
| LastModifiedDate | date               | Det datum då användningsdata senast ändrades.                                                                       |
| Länkar            | ResourceLinks      | Resursen länkar som motsvarar användningssammanfattningen.                                                           |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar användningssammanfattningen.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary representerar** en sammanfattning av användningsbudgetering på partnernivå för alla kunder.

| Egenskap         | Typ               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | matris med strängar   | Listan över e-postadresser för meddelanden.                                                                   |
| CustomerOverBudget | heltal          | Antalet kunder som är över budget.                                                                    |
| CustomersTrendingOver | heltal       | Antalet kunder som är nära att gå över budgeten.                                                     |
| CustomersWithUsageBasedSubscriptions  | heltal | Antalet kunder med en användningsbaserad prenumeration.                                               |
| ResourceId       | sträng             | Resursens unika identifierare. I kontexten CustomerMonthlyUsageRecord är detta ID kund-ID. |
| ResourceName     | sträng             | Namnet på resursen. I kontexten CustomerMonthlyUsageRecord är det här kundnamnet.               |
| BillingStartDate | date               | Startdatumet för den aktuella faktureringsperioden.                                                                    |
| BillingEndDate   | date               | Slutdatumet för den aktuella faktureringsperioden.                                                                      |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för all kundanvändning baserat på aktuell användning från faktureringsperiodens början.      |
| CurrencyLocale   | sträng             | Nationella valuta.                                                                                             |
| LastModifiedDate | date               | Det datum då användningsdata senast ändrades.                                                                       |
| Länkar            | ResourceLinks      | Resursen länkar som motsvarar användningssammanfattningen.                                                           |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar användningssammanfattningen.                                                      |

## <a name="spendingbudget"></a>Utgiftsbudget

**SpendingBudget** representerar den budget som tilldelats kunden för användningsbaserade prenumerationer.

| Egenskap   | Typ               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Amount     | decimal             | Den allokerade budgeten. Om värdet är null allokeras ingen utgiftsbudget till den här kunden. |
| Attribut | ResourceAttributes | Metadataattributen som motsvarar budgeten.                                                |
