---
title: Resurs användnings post resurser
description: Du kan använda ResourceUsageRecord-resursen för att beskriva den uppskattade självkostnaden för en prenumerations resurs nivå användning i den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b0a28620eec86e86630aef93b13f26c9dd675a5d
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274571"
---
# <a name="resource-usage-record-resources"></a>Resurs användnings post resurser

**Gäller för:**

- Partnercenter

Du kan använda **ResourceUsageRecord** -resursen för att beskriva den uppskattade självkostnaden för en prenumerations resurs nivå användning i den aktuella fakturerings perioden.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Egenskap          | Typ               | Beskrivning                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | sträng             | Hämtar eller anger prenumerations-ID. För Microsoft Azure (MS-AZR-0145P)-prenumerationer är det här värdet handels prenumerations-ID: t. För Azure-planer är det här värdet Azure plan-identifieraren. |
| ResourceUri       | sträng             | Hämtar eller anger resurs-URI. "                                                                                                                                                                            |
| ResourceType      | sträng             | Hämtar eller anger resurs typen.                                                                                                                                                                            |
| EntitlementId     | sträng             | Hämtar eller anger rättighets identifieraren (ID för Azure-prenumerationen).                                                                                                                               |
| EntitlementName   | sträng             | Hämtar eller anger namnet på rättigheten.                                                                                                                                                                         |
| ResourceGroupName | double             | Hämtar eller anger resurs gruppens namn.                                                                                                                                                                      |
| Name              | sträng             | Resursens namn.                                                                                                                                                                                  |
| ResourceName      | sträng             | Hämtar eller anger resursens namn.                                                                                                                                                                     |
| TotalCost         | decimal            | Hämtar eller anger den uppskattade totala kostnaden.                                                                                                                                                               |
| CurrencyCode      | sträng             | Hämtar eller anger valuta koden.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Hämtar eller anger den uppskattade totala kostnaden i USD.                                                                                                                                                              |
| LastModifiedDate  | sträng             | Den dag (i datum-och tids format) som posten senast ändrades.                                                                                                                                          |
| Attribut        | ResourceAttributes | De metadata-attribut som motsvarar resursen.                                                                                                                                                     |
