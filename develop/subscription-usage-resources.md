---
title: Resurser för prenumerationsanvändning
description: Resurser för prenumerationsanvändning beskriver prenumerationer med användningsbaserad fakturering. Dessa prenumerationer har dagliga och månatliga användningsposter, tillsammans med en användningssammanfattning för varje betalningsperiod.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcb24dcf5ca8165ec23c4b187def38d05772e1de
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547384"
---
# <a name="subscription-usage-resources"></a>Resurser för prenumerationsanvändning

**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Du kan använda följande prenumerationsanvändningsresurser för att hämta användningsinformation för en specifik prenumeration med användningsbaserad fakturering. Dessa prenumerationer har dagliga och månatliga användningsposter, tillsammans med en användningssammanfattning för varje betalningsperiod.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*Resursen **SubscriptionDailyUsageRecord** är föråldrad och kan ge felaktiga resultat. Vi rekommenderar att du uppdaterar dina program så att de använder API:erna som beskrivs i Hämta en kunds användningsposter för [Azure](get-a-customer-s-utilization-record-for-azure.md) och [Hämta priser för Microsoft Azure stället.](get-prices-for-microsoft-azure.md)*

Resursen **SubscriptionDailyUsageRecord** beskriver hur mycket en prenumeration används under en dag.

| Egenskap         | Typ               | Beskrivning                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | sträng             | Den dag i datum/tid-format som prenumerationen användes.                                 |
| ResourceId       | sträng             | Guid. Unikt ID för resursen.                                                          |
| ResourceName     | sträng             | Namnet på resursen.                                                                     |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för att använda resurserna i prenumerationen på den angivna dagen.     |
| CurrencyLocale   | sträng             | Det språk som prenumerationen användes i avgör vilken valuta som ska användas på fakturan. |
| LastModifiedDate | sträng             | Dagen, i datum/tid-format, som den här posten senast ändrades.                             |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar resursen.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

Resursen **SubscriptionMonthlyUsageRecord** beskriver hur mycket en prenumeration används under en månad.

| Egenskap         | Typ               | Beskrivning                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Status           | sträng             | Status för prenumerationen: "none", "active", "suspended" eller "deleted".                  |
| PartnerOnRecord  | sträng             | "MPN-ID för partnern i posten."                                                        |
| OfferId          | sträng             | Guid. ID:t för erbjudandet som är relaterat till den här prenumerationen.                                       |
| Id               | sträng             | Guid. ID för prenumerationen eller resursen.                                                 |
| Name             | sträng             | Namnet på prenumerationen eller resursen.                                                     |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för att använda resurserna i prenumerationen under den angivna månaden.   |
| CurrencyLocale   | sträng             | Det språk som prenumerationen användes i avgör vilken valuta som ska användas på fakturan. Tillgängligt för Microsoft Azure prenumerationer (MS-AZR-0145P). |
| CurrencyCode     | sträng             | Hämtar eller anger valutakoden. Tillgängligt för prenumerationsresurser för Azure-plan.                                         |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för Azure-planer.                                         |
| LastModifiedDate | sträng             | Dagen, i datum/tid-format, som den här posten senast ändrades.                             |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar resursen.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

Resursen **SubscriptionUsageSummary** beskriver hur mycket en viss prenumeration användes under den aktuella faktureringsperioden.

| Egenskap         | Typ               | Beskrivning                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | sträng             | Guid. ID för prenumerationen eller resursen. I kontexten CustomerMonthlyUsageRecord är detta ID kund-ID. |
| ResourceName     | sträng             | Namnet på prenumerationen eller resursen. I kontexten CustomerMonthlyUsageRecord är det här namnet kundnamnet. |
| BillingStartDate | date               | Startdatumet för den aktuella faktureringsperioden i datum/tid-format.                                                     |
| BillingEndDate   | date               | Slutdatumet för den aktuella faktureringsperioden i datum/tid-format.                                                       |
| TotalCost        | double             | Den uppskattade totala kostnaden för att använda resurserna i prenumerationen under den angivna faktureringsperioden.               |
| CurrencyLocale   | sträng             | Det språk som prenumerationen användes i avgör vilken valuta som ska användas på fakturan. Tillgängligt för Microsoft Azure prenumerationer (MS-AZR-0145P). |
| CurrencyCode   | sträng             | Hämtar eller anger valutakoden. Tillgängligt för Azure-planer.                                         |
| USDTotalCost   | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för prenumerationsresurser för Azure-plan.                                         |
| LastModifiedDate | sträng             | Dagen, i datum/tid-format, som den här posten senast ändrades.                                                      |
| Länkar            | ResourceLinks      | Resursen länkar som motsvarar SubscriptionUsageSummary.                                                      |
| Attribut       | ResourceAttributes | Metadataattributen som motsvarar SubscriptionUsageSummary.                                                 |
