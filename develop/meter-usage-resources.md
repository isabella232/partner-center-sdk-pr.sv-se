---
title: Post resurs för mätar användning
description: Du kan använda MeterUsageRecord-resursen för att beskriva den uppskattade penning kostnaden för en prenumerations mätnings nivå användning i den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c02c859d1d8ba3edd236d83d3056cb82533f7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768856"
---
# <a name="meter-usage-record-resource"></a>Post resurs för mätar användning

**Gäller för:**

- Partnercenter

Du kan använda **MeterUsageRecord** -resursen för att beskriva den uppskattade penning kostnaden för en prenumerations mätnings nivå användning i den aktuella fakturerings perioden.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Egenskap         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | sträng             | Ett GUID som motsvarar ID: t för en [prenumerations resurs](subscription-resources.md#subscription)för partner Center, som representerar en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan. För Microsoft Azure (MS-AZR-0145P)-prenumerationer är det här värdet handels prenumerations-ID: t. För prenumerations resurser i Azure plan är det här värdet Azure plan-identifieraren.                  |
| MeterId  | sträng             | Hämtar eller anger mätarens id.                                                        |
| MeterName          | sträng             | Hämtar eller anger mätarens namn.                                       |
| Kategori               | sträng             | Hämtar eller anger Azure-resursens kategori.                                                 |
| Underkategori             | sträng             |  Hämtar eller anger Azure-resursens under kategori.                                                     |
| QuantityUsed        | decimal             | Hämtar eller anger den mängd av Azure-resursen som används.   |
| Enhet   | sträng             | Hämtar eller anger mått enheten för Azure-resursen. |
| TotalCost   | decimal             | Hämtar eller anger den uppskattade totala kostnaden för användning. |
| CurrencyLocale   | sträng             | Språket som prenumerationen användes i. Den här egenskapen avgör vilken valuta som används på fakturan. Den här egenskapen är tillgänglig för Microsoft Azure (MS-AZR-0145P)-prenumerationer. |
| CurrencyCode   | sträng             | Hämtar eller anger valuta koden. Den här egenskapen är tillgänglig för Azure-planer.                                         |
| USDTotalCost   | decimal             | Hämtar eller anger den uppskattade totala kostnaden i USD. Den här egenskapen är tillgänglig för Azure-planer.                                         |
| LastModifiedDate | sträng             | Den dag (i datum-och tids format) som posten senast ändrades.                             |
| Attribut       | ResourceAttributes | De metadata-attribut som motsvarar resursen.                                        |                                           |
