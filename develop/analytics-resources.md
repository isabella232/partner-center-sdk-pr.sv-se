---
title: Analysresurser
description: PartnerCenter-resurser innehåller data om användning, distribution och förbrukning. Innehåller insikter om licensdistribution och användning av partner och kunder.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: fc665e8e4468648f71f242992780fbc66a02522a0b8b957a5ce68147ab33eaac
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993205"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Analytics API-resurser som hjälper dig att rapportera om licensanvändning, distribution och förbrukning

De resurser som definieras här innehåller data som används för att rapportera om användning, distribution och förbrukning.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

Resursen **PartnerLicensesDeploymentInsights** innehåller insikter på partnernivå om licensdistribution.

| Egenskap                  | Typ                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | antal                                                         | Procentandelen distribuerade licenser.                                                |
| licenserSålda              | antal                                                         | Antalet sålda licenser.                                                        |
| processedDateTime         | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                     |
| Tjänstnamn               | sträng                                                         | Tjänstens namn (till exempel o365, crm).                                                  |
| Kanal                   | sträng                                                         | Kanalnamnet för tjänsten (till exempel återförsäljare).                                    |
| Attribut                | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

Resursen **PartnerLicensesUsageInsights** innehåller information på partnernivå om licensanvändning.

| Egenskap                     | Typ                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | antal                                                         | Procentandelen distribuerade licenser.                                           |
| workloadName                 | sträng                                                         | Namnet på arbetsbelastningen (till exempel: exchange).                                             |
| processedDateTime            | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                |
| Tjänstnamn                  | sträng                                                         | Tjänstens namn (till exempel o365, crm).                                             |
| Kanal                      | sträng                                                         | Kanalnamnet för tjänsten (till exempel återförsäljare).                               |
| Attribut                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

Resursen **CustomerLicensesDeploymentInsights** innehåller insikter på kundnivå om licensdistribution.

| Egenskap          | Typ                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | antal                                                         | Antalet distribuerade licenser.                                                     |
| licenserSålda      | antal                                                         | Antalet sålda licenser.                                                         |
| deploymentPercent | antal                                                         | Den justerade procentandelen licenser som distribuerats.                                        |
| customerId        | sträng                                                         | Kundidentifieraren.                                                             |
| customerName      | sträng                                                         | Kundens namn.                                                                   |
| Productname       | sträng                                                         | Produktnamnet.                                                                    |
| serviceCode       | sträng                                                         | Licensens tjänstkod.                                                     |
| processedDateTime | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                      |
| Tjänstnamn       | sträng                                                         | Tjänstens namn (till exempel o365, crm).                                                   |
| Kanal           | sträng                                                         | Kanalnamnet för tjänsten (till exempel återförsäljare).                                     |
| Attribut        | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. Innehåller "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

Resursen **CustomerLicensesUsageInsights** innehåller insikter på kundnivå om licensanvändning.

| Egenskap          | Typ                                                           | Description                                                                     |
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