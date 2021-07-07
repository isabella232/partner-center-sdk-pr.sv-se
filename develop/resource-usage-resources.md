---
title: Resursanvändning registrera resurser
description: Du kan använda resursen ResourceUsageRecord för att beskriva den uppskattade penningkostnaden för en prenumerations resursnivåanvändning i den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eb626b9d4cb4c57a07f45bcf7b914f534e62ab68
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446589"
---
# <a name="resource-usage-record-resources"></a>Resursanvändning registrera resurser

Du kan använda resursen **ResourceUsageRecord** för att beskriva den uppskattade penningkostnaden för en prenumerations resursnivåanvändning i den aktuella faktureringsperioden.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Egenskap          | Typ               | Beskrivning                                                                                                                                                                                                |
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
