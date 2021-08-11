---
title: Resursanvändning registrera resurser
description: Du kan använda resursen ResourceUsageRecord för att beskriva den uppskattade penningkostnaden för en prenumerations resursnivåanvändning i den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b330c49518bc12a63f2be731eef5c57884f5b15b706ce4007bbdf1a7bb8fab0e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996945"
---
# <a name="resource-usage-record-resources"></a>Resursanvändning registrera resurser

Du kan använda resursen **ResourceUsageRecord** för att beskriva den uppskattade penningkostnaden för en prenumerations resursnivåanvändning i den aktuella faktureringsperioden.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Egenskap          | Typ               | Description                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | sträng             | Hämtar eller anger prenumerationsidentifieraren. För Microsoft Azure prenumerationer (MS-AZR-0145P) är det här värdet identifieraren för handelsprenumerationen. För Azure-planer är det här värdet Identifieraren för Azure-planen). |
| ResourceUri       | sträng             | Hämtar eller anger resurs-URI."                                                                                                                                                                            |
| ResourceType      | sträng             | Hämtar eller anger resurstypen.                                                                                                                                                                            |
| EntitlementId     | sträng             | Hämtar eller anger berättigandeidentifieraren (Azure-prenumerations-ID).                                                                                                                               |
| EntitlementName   | sträng             | Hämtar eller anger rättighetsnamnet.                                                                                                                                                                         |
| ResourceGroupName | double             | Hämtar eller anger resursgruppens namn.                                                                                                                                                                      |
| Name              | sträng             | Namnet på resursen.                                                                                                                                                                                  |
| ResourceName      | sträng             | Hämtar eller anger namnet på resursen.                                                                                                                                                                     |
| TotalCost         | decimal            | Hämtar eller anger den uppskattade totala kostnadsanvändningen.                                                                                                                                                               |
| CurrencyCode      | sträng             | Hämtar eller anger valutakoden.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Hämtar eller anger den uppskattade totala kostnaden i USD.                                                                                                                                                              |
| LastModifiedDate  | sträng             | Den dag (i datum/tid-format) som posten senast ändrades.                                                                                                                                          |
| Attribut        | ResourceAttributes | Metadataattributen som motsvarar resursen.                                                                                                                                                     |
