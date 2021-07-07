---
title: Resurser för kundanvändning
description: Resurser för kunder med användningsbaserade prenumerationer och budgetar för månatlig användning (inklusive CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary och SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eae516e2f759dfc2e8f80e946a835d70760c5c9e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973051"
---
# <a name="customer-usage-resources"></a>Resurser för kundanvändning

**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Kunder med användningsbaserade prenumerationer kan ha en månatlig användningsbudget. Den här budgeten anger en gräns för kundens maximala användning och gör att partnern kan spåra sin användning över tid.

> [!NOTE]
> Kundanvändningsnummer är uppskattningar (inte slutliga värden) som inte ska användas i faktureringssyfte.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** representerar den uppskattade penningkostnaden för en kunds användning under den aktuella månaden.

| Egenskap         | Typ               | Beskrivning                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budget           | Utgiftsbudget     | Den allokerade utgiftsbudgeten för kunden.                          |
| PercentUsed      | decimal             | Procentandelen som används av den allokerade budgeten.                        |
| ResourceId       | sträng             | Resursens unika identifierare.                                   |
| ResourceName     | sträng             | Namnet på resursen.                                                |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för användning av resurserna i prenumerationen.|
| CurrencyLocale   | sträng             | Kundens nationella valuta. Tillgängligt för Microsoft Azure prenumerationer (MS-AZR-0145P).            |
| CurrencyCode     | sträng             | Hämtar eller anger valutakoden. Tillgängligt för Azure-planer.           |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för Azure-planer.                                         |
| IsUpgraded       | boolesk             | Hämtar eller anger ett värde som anger om kundens Azure-prenumeration har uppgraderats. Värdet true **representerar** kunder som har en Azure-plan.                         |
| LastModifiedDate | date               | Det datum då användningsdata senast ändrades.                               |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar användningsposten.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** representerar en sammanfattning av kundens användning under en hel faktureringsperiod.

| Egenskap         | Typ               | Beskrivning                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budget           | Utgiftsbudget     | Den allokerade utgiftsbudgeten för kunden.                                                                  |
| ResourceId       | sträng             | Resursens unika identifierare. I kontexten CustomerMonthlyUsageRecord är detta ID kund-ID. |
| ResourceName     | sträng             | Namnet på resursen. I kontexten CustomerMonthlyUsageRecord är det här kundnamnet.               |
| BillingStartDate | date               | Startdatumet för den aktuella faktureringsperioden.                                                                    |
| BillingEndDate   | date               | Slutdatumet för den aktuella faktureringsperioden.                                                                      |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för användning av resurserna i prenumerationen.                                         |
| CurrencyLocale   | sträng             | Kundens nationella valuta. Tillgängligt för Microsoft Azure prenumerationer (MS-AZR-0145P).                                         |
| CurrencyCode     | sträng             | Hämtar eller anger valutakoden. Tillgängligt för Azure-planer.                                         |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för prenumerationsresurser för Azure-prenumeration.                                         |
| LastModifiedDate | date               | Det datum då användningsdata senast ändrades.                                                                       |
| Länkar            | ResourceLinks      | Resursen länkar som motsvarar användningssammanfattningen.                                                           |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar användningssammanfattningen.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** representerar en sammanfattning på partnernivå av användningsbudgetering för alla kunder.

| Egenskap         | Typ               | Beskrivning                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailToNotify   | matris med strängar   | Listan över e-postadresser för meddelanden.                                                                   |
| CustomerOverBudget | heltal          | Antalet kunder som är över budget.                                                                    |
| CustomersTrendingOver | heltal       | Antalet kunder som är nära att gå över budgeten.                                                     |
| CustomersWithUsageBasedSubscriptions  | heltal | Antalet kunder med en användningsbaserad prenumeration.                                               |
| ResourceId       | sträng             | Resursens unika identifierare. I kontexten CustomerMonthlyUsageRecord är detta ID kund-ID. |
| ResourceName     | sträng             | Namnet på resursen. I kontexten CustomerMonthlyUsageRecord är det här kundnamnet.               |
| BillingStartDate | date               | Startdatumet för den aktuella faktureringsperioden.                                                                    |
| BillingEndDate   | date               | Slutdatumet för den aktuella faktureringsperioden.                                                                      |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för all kundanvändning baserat på aktuell användning från början av faktureringsperioden.      |
| CurrencyLocale   | sträng             | Nationella valuta.                                                                                             |
| LastModifiedDate | date               | Det datum då användningsdata senast ändrades.                                                                       |
| Länkar            | ResourceLinks      | Resursen länkar som motsvarar användningssammanfattningen.                                                           |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar användningssammanfattningen.                                                      |

## <a name="spendingbudget"></a>Utgiftsbudget

**SpendingBudget** representerar den budget som tilldelats kunden för användningsbaserade prenumerationer.

| Egenskap   | Typ               | Beskrivning                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Amount     | decimal             | Den allokerade budgeten. Om värdet är null allokeras ingen utgiftsbudget till den här kunden. |
| Attribut | ResourceAttributes | Metadataattributen som motsvarar budgeten.                                                |
