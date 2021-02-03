---
title: Azure Rate-kort – aktuellt Azure-pris
description: Lär dig hur du använder Azure Rate-kortet för att få aktuella priser för Azure-erbjudanden i real tid i din region. Azure Rate-kortet nås via partner Center REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 2d011153f508ea0a745413b88003333452d0af24
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770014"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Azure Rate Card-resurser för att få real tids aktuella Azure-priser på Azure-erbjudanden i din region

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Azure Rate-kortet ger real tids priser för Azure-erbjudanden. Azures priser är helt dynamiska och förändringar ofta. Microsoft publicerar uppdateringar på Partner Center, men REST API ger det snabbaste sättet för leverantörer av moln lösningar att få aktuella priser.

Om du vill spåra användningen och förutsäga din månads faktura och fakturor för enskilda kunder kan du kombinera en pris fråga för att [få priser för Microsoft Azure](get-prices-for-microsoft-azure.md) med en begäran om att [få en kunds användnings poster för Azure](get-a-customer-s-utilization-record-for-azure.md).

Priserna skiljer sig mellan marknaden och valutan, och detta API tar hänsyn till. Som standard använder API dina partner profil inställningar i Partner Center och ditt webb läsar språk, och dessa inställningar är anpassningsbara. Plats medvetenheten är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.

## <a name="azureratecard"></a>AzureRateCard

Beskriver egenskaperna för en Azure Rate Card-resurs.

| Egenskap      | Typ                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | sträng                                    | Den valuta i vilken priserna anges.                     |
| isTaxIncluded | boolean                                   | Alla hastigheter är Pretax, så den här egenskapen returnerar as `false` . |
| locale        | sträng                                    | Kulturen som resursinformationen är lokaliserad till.       |
| mäta        | objekt mat ris                          | Matris med [AzureMeter](#azuremeter) -objekt.                       |
| offerTerms    | objekt mat ris                          | Matris med [AzureOfferTerm](#azureofferterm) -objekt.               |
| dokumentattribut    | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. Ingår `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Åtgärder på AzureRateCard-resursen

- [Hämta priser för Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Egenskap         | Typ             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | sträng           | Mätarens unika identifierare.                                                                    |
| name             | sträng           | Eget namn på mätaren.                                                                   |
| timkostnader            | objekt           | Mätar frekvens. Nyckeln är mätnings antalet (sträng) och värdet är mätar frekvensen (tal). |
| tags             | matris med strängar | Valfria mätnings etiketter. Matrisen kan vara tom.                                                 |
| category         | sträng           | Resurs kategori.                                                                     |
| under kategori      | sträng           | Resursens under kategori.                                                                 |
| region           | sträng           | Region i ID.                                                                             |
| unit             | sträng           | Typ av kvantitet (timmar, byte osv.)                                                     |
| includedQuantity | antal           | Uppmätt kvantitet som ingår kostnads fritt.                                               |
| effectiveDate    | sträng           | Det datum då mätaren gäller.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Egenskap         | Typ             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | sträng           | Eget namn på erbjudande villkoret.        |
| discount         | antal           | Eventuell rabatt som används.           |
| excludedMeterIds | matris med strängar | Mätare som inte ingår i erbjudandet. |
| effectiveDate    | sträng           | Det datum då erbjudandet gäller.        |
