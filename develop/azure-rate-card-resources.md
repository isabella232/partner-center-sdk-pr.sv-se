---
title: Azure-priskort – aktuella Azure-priser
description: Lär dig hur du använder Azure-priskortet för att få aktuella priser för Azure-erbjudanden i realtid i din region. Azure Rate Card nås via PartnerCenter-REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e0b1bc9d764e2132315205653f46cef73b25e02f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974343"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Kortresurser med Azure-priser för att få aktuella Azure-priser på Azure-erbjudanden i din region

**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Azure-priskortet ger realtidspriser för Azure-erbjudanden. Prissättningen för Azure är dynamisk och ändras ofta. Microsoft publicerar uppdateringar i Partnercenter, men REST API det snabbaste sättet för Molnlösningsleverantör partner att få aktuella priser.

Om du vill spåra användning och hjälpa till att förutsäga din månadsfaktura och fakturorna för enskilda kunder kan du kombinera en Rate Card-fråga till [Hämta priser](get-prices-for-microsoft-azure.md) för Microsoft Azure med en begäran om att hämta en [kunds](get-a-customer-s-utilization-record-for-azure.md)användningsposter för Azure .

Priserna varierar beroende på marknad och valuta, och det här API:et tar hänsyn till platsen. Som standard använder API:et dina partnerprofilinställningar i Partnercenter och ditt webbläsarspråk, och dessa inställningar är anpassningsbara. Platsmedvetenhet är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.

## <a name="azureratecard"></a>AzureRateCard

Beskriver egenskaperna för en Azure Rate Card-resurs.

| Egenskap      | Typ                                      | Beskrivning                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | sträng                                    | Valutan som kurserna tillhandahålls i.                     |
| isTaxIncluded | boolean                                   | Alla priser är före skatt, så den här egenskapen returneras som `false` . |
| locale        | sträng                                    | Den kultur där resursinformationen är lokaliserad.       |
| Meter        | matris med objekt                          | Matris med [AzureMeter-objekt.](#azuremeter)                       |
| offerTerms    | matris med objekt                          | Matris med [AzureOfferTerm-objekt.](#azureofferterm)               |
| Attribut    | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Åtgärder på AzureRateCard-resursen

- [Hämta priser för Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Egenskap         | Typ             | Beskrivning                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | sträng           | Mätarens unika identifierare.                                                                    |
| name             | sträng           | Eget namn på mätaren.                                                                   |
| Priser            | objekt           | Mätarpriser. Nyckeln är mätarkvantiteten (sträng) och värdet är mätarhastigheten (talet). |
| tags             | matris med strängar | Valfria mätartaggar. Matrisen kan vara tom.                                                 |
| category         | sträng           | Resurskategori.                                                                     |
| Underkategori      | sträng           | Underkategori för resursen.                                                                 |
| region           | sträng           | Region för ID:t.                                                                             |
| unit             | sträng           | Typ av kvantitet (timmar, byte osv.)                                                     |
| includedQuantity | antal           | Mätarkvantitet som ingår utan kostnad.                                               |
| effectiveDate    | sträng           | Det datum då mätaren gäller.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Egenskap         | Typ             | Beskrivning                             |
|------------------|------------------|-----------------------------------------|
| name             | sträng           | Eget namn på erbjudandetermen.        |
| discount         | antal           | Den tillämpade rabatten, om en eventuell.           |
| excludedMeterIds | matris med strängar | Mätare som undantagits från erbjudandet, om det finns några. |
| effectiveDate    | sträng           | Det datum då erbjudandet gäller.        |
