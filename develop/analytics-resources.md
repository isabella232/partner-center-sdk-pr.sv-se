---
title: Analysresurser
description: Partner Center-resurser innehåller data om användning, distribution och förbrukning. Innehåller insikter om licensdistribution och användning av partner och kunder.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 69c6c195ba1a0d657a91320b2f9b08b5269a8499
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025606"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Api-analysresurser som hjälper dig att rapportera om licensanvändning, distribution och förbrukning

De resurser som definieras här innehåller data som används för att rapportera om användning, distribution och förbrukning.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

Resursen **PartnerLicensesDeploymentInsights** innehåller insikter på partnernivå om licensdistribution.

| Egenskap                  | Typ                                                           | Beskrivning                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | antal                                                         | Procentandelen licenser som distribuerats.                                                |
| licenserSåld              | antal                                                         | Antalet sålda licenser.                                                        |
| processedDateTime         | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                     |
| Tjänstnamn               | sträng                                                         | Tjänstnamnet (till exempel o365, crm).                                                  |
| Kanal                   | sträng                                                         | Kanalnamnet för tjänsten (till exempel återförsäljare).                                    |
| Attribut                | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

Resursen **PartnerLicensesUsageInsights** innehåller insikter på partnernivå om licensanvändning.

| Egenskap                     | Typ                                                           | Beskrivning                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | antal                                                         | Procentandelen licenser som distribuerats.                                           |
| workloadName                 | sträng                                                         | Namnet på arbetsbelastningen (till exempel: exchange).                                             |
| processedDateTime            | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                |
| Tjänstnamn                  | sträng                                                         | Tjänstnamnet (till exempel o365, crm).                                             |
| Kanal                      | sträng                                                         | Kanalnamnet för tjänsten (till exempel återförsäljare).                               |
| Attribut                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

Resursen **CustomerLicensesDeploymentInsights** innehåller insikter på kundnivå om licensdistribution.

| Egenskap          | Typ                                                           | Beskrivning                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | antal                                                         | Antalet distribuerade licenser.                                                     |
| licenserSåld      | antal                                                         | Antalet sålda licenser.                                                         |
| deploymentPercent | antal                                                         | Den justerade procentandelen licenser som distribuerats.                                        |
| customerId        | sträng                                                         | Kundidentifieraren.                                                             |
| customerName      | sträng                                                         | Kundens namn.                                                                   |
| Productname       | sträng                                                         | Produktnamnet.                                                                    |
| serviceCode       | sträng                                                         | Licensens tjänstkod.                                                     |
| processedDateTime | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                      |
| Tjänstnamn       | sträng                                                         | Tjänstnamnet (till exempel o365, crm).                                                   |
| Kanal           | sträng                                                         | Kanalnamnet för tjänsten (till exempel återförsäljare).                                     |
| Attribut        | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

Resursen **CustomerLicensesUsageInsights** innehåller insikter på kundnivå om licensanvändning.

| Egenskap          | Typ                                                           | Beskrivning                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | sträng                                                         | Arbetsbelastningskoden.                                                              |
| workloadName      | antal                                                         | Namnet på arbetsbelastningen (till exempel: Exchange).                                              |
| usagePercent      | antal                                                         | Den justerade procentandelen licenser som används.                                       |
| licensesActive    | antal                                                         | Antalet aktiva licenser.                                                  |
| licensesQualified | antal                                                         | Antalet kvalificerade licenser.                                               |
| customerId        | sträng                                                         | Kundidentifieraren.                                                        |
| customerName      | sträng                                                         | Kundens namn.                                                              |
| Productname       | sträng                                                         | Produktnamnet.                                                               |
| serviceCode       | sträng                                                         | Licensens tjänstkod.                                                |
| processedDateTime | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                 |
| Tjänstnamn       | sträng                                                         | Tjänstnamnet (till exempel o365, crm).                                              |
| Kanal           | sträng                                                         | Kanalnamnet för tjänsten (till exempel återförsäljare).                                |
| Attribut        | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller "objectType": "CustomerLicensesUsageInsights" |