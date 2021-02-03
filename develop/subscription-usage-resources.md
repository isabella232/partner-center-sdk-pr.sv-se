---
title: Prenumerations användnings resurser
description: Prenumerations användnings resurser beskriver prenumerationer med användnings baserad fakturering. Dessa prenumerationer har dagliga och månatliga användnings poster, tillsammans med en användnings översikt för varje betalnings period.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8e23287d80f19084860f4597754448e81c01049f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768943"
---
# <a name="subscription-usage-resources"></a>Prenumerations användnings resurser

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan använda följande resurser för prenumerations användning för att få användnings information för en speciell prenumeration med användnings baserad fakturering. Dessa prenumerationer har dagliga och månatliga användnings poster, tillsammans med en användnings översikt för varje betalnings period.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

***SubscriptionDailyUsageRecord** -resursen är föråldrad och kan generera felaktiga resultat. Vi rekommenderar att du uppdaterar dina program för att använda API: erna som beskrivs i [Hämta en kunds användnings poster för Azure](get-a-customer-s-utilization-record-for-azure.md) och [få priser för Microsoft Azure](get-prices-for-microsoft-azure.md) i stället.*

**SubscriptionDailyUsageRecord** -resursen beskriver hur mycket en prenumeration används på en enda dag.

| Egenskap         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | sträng             | Den dag i formatet för datum/tid som prenumerationen användes.                                 |
| ResourceId       | sträng             | LED. Resursens unika ID.                                                          |
| ResourceName     | sträng             | Resursens namn.                                                                     |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för att använda resurserna i prenumerationen på den angivna dagen.     |
| CurrencyLocale   | sträng             | Språket som prenumerationen användes i avgör vilken valuta som ska användas på fakturan. |
| LastModifiedDate | sträng             | Den dag, i datum-och tids format, som posten senast ändrades.                             |
| Attribut       | ResourceAttributes | De metadata-attribut som motsvarar resursen.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

**SubscriptionMonthlyUsageRecord** -resursen beskriver hur mycket en prenumeration används i en enda månad.

| Egenskap         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Status           | sträng             | Prenumerationens status: "ingen", "aktiv", "pausad" eller "borttagen".                  |
| PartnerOnRecord  | sträng             | "MPN-ID för partnern på posten".                                                        |
| OfferId          | sträng             | LED. ID för erbjudandet som är relaterat till den här prenumerationen.                                       |
| Id               | sträng             | LED. ID: t för prenumerationen eller resursen.                                                 |
| Name             | sträng             | Namnet på prenumerationen eller resursen.                                                     |
| TotalCost        | decimal             | Den uppskattade totala kostnaden för att använda resurserna i prenumerationen under den angivna månaden.   |
| CurrencyLocale   | sträng             | Språket som prenumerationen användes i avgör vilken valuta som ska användas på fakturan. Tillgängligt för Microsoft Azure (MS-AZR-0145P)-prenumerationer. |
| CurrencyCode     | sträng             | Hämtar eller anger valuta koden. Tillgängligt för Azure plan Subscription-resurser.                                         |
| USDTotalCost     | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för Azure-planer.                                         |
| LastModifiedDate | sträng             | Den dag, i datum-och tids format, som posten senast ändrades.                             |
| Attribut       | ResourceAttributes | De metadata-attribut som motsvarar resursen.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

**SubscriptionUsageSummary** -resursen beskriver hur mycket en viss prenumeration har använts under den aktuella fakturerings perioden.

| Egenskap         | Typ               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | sträng             | LED. ID: t för prenumerationen eller resursen. I kontexten för CustomerMonthlyUsageRecord är det här ID: t kund-ID. |
| ResourceName     | sträng             | Namnet på prenumerationen eller resursen. I kontexten för CustomerMonthlyUsageRecord är namnet kundens namn. |
| BillingStartDate | date               | Start datumet för den aktuella fakturerings perioden i datum-/tids format.                                                     |
| BillingEndDate   | date               | Slutdatumet för den aktuella fakturerings perioden, i datum-/tids format.                                                       |
| TotalCost        | double             | Den uppskattade totalkostnaden för att använda resurserna i prenumerationen under den angivna fakturerings perioden.               |
| CurrencyLocale   | sträng             | Språket som prenumerationen användes i avgör vilken valuta som ska användas på fakturan. Tillgängligt för Microsoft Azure (MS-AZR-0145P)-prenumerationer. |
| CurrencyCode   | sträng             | Hämtar eller anger valuta koden. Tillgängligt för Azure-planer.                                         |
| USDTotalCost   | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Tillgängligt för Azure plan Subscription-resurser.                                         |
| LastModifiedDate | sträng             | Den dag, i datum-och tids format, som posten senast ändrades.                                                      |
| Länkar            | ResourceLinks      | Resurs länkarna som motsvarar SubscriptionUsageSummary.                                                      |
| Attribut       | ResourceAttributes | De metadata-attribut som motsvarar SubscriptionUsageSummary.                                                 |
