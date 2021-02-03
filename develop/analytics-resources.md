---
title: Analys resurser
description: Partner Center-resurser innehåller data om användning, distribution och konsumtion. Innehåller insikter om licens distribution och användning av partner och kunder.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 9bd47b99f0abaa181e5f255dd6e46151363917e7
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770002"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Analytics API-resurser som hjälper dig att rapportera om licens användning, distribution och konsumtion

**Gäller för:**

- Partnercenter

De resurser som definieras här innehåller data som används för att rapportera om användning, distribution och konsumtion.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

**PartnerLicensesDeploymentInsights** -resursen innehåller insikter om licens distribution på partner nivå.

| Egenskap                  | Typ                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | antal                                                         | Procent andelen licenser som distribuerats.                                                |
| licensesSold              | antal                                                         | Antalet sålda licenser.                                                        |
| processedDateTime         | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                     |
| serviceName               | sträng                                                         | Tjänst namnet (till exempel: O365, CRM).                                                  |
| kanalig                   | sträng                                                         | Kanal namnet för tjänsten (till exempel: åter försäljare).                                    |
| dokumentattribut                | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. Inkluderar "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

**PartnerLicensesUsageInsights** -resursen innehåller insikter på partner nivå om licens användning.

| Egenskap                     | Typ                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | antal                                                         | Procent andelen licenser som distribuerats.                                           |
| workloadName                 | sträng                                                         | Arbets belastnings namnet (till exempel: Exchange).                                             |
| processedDateTime            | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                |
| serviceName                  | sträng                                                         | Tjänst namnet (till exempel: O365, CRM).                                             |
| kanalig                      | sträng                                                         | Kanal namnet för tjänsten (till exempel: åter försäljare).                               |
| dokumentattribut                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. Inkluderar "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

**CustomerLicensesDeploymentInsights** -resursen innehåller insikter om licens distribution på kund nivå.

| Egenskap          | Typ                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | antal                                                         | Antalet distribuerade licenser.                                                     |
| licensesSold      | antal                                                         | Antalet sålda licenser.                                                         |
| deploymentPercent | antal                                                         | Den justerade procent andelen licenser som har distribuerats.                                        |
| customerId        | sträng                                                         | Kund-ID.                                                             |
| customerName      | sträng                                                         | Kundens namn.                                                                   |
| Namn       | sträng                                                         | Produkt namnet.                                                                    |
| serviceCode       | sträng                                                         | Tjänst koden för licensen.                                                     |
| processedDateTime | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                      |
| serviceName       | sträng                                                         | Tjänst namnet (till exempel: O365, CRM).                                                   |
| kanalig           | sträng                                                         | Kanal namnet för tjänsten (till exempel: åter försäljare).                                     |
| dokumentattribut        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. Inkluderar "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

**CustomerLicensesUsageInsights** -resursen innehåller insikter på kund nivå om licens användning.

| Egenskap          | Typ                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | sträng                                                         | Arbets belastnings koden.                                                              |
| workloadName      | antal                                                         | Arbets belastnings namnet (till exempel: Exchange).                                              |
| usagePercent      | antal                                                         | Den justerade procent andelen licenser som används.                                       |
| licensesActive    | antal                                                         | Antalet aktiva licenser.                                                  |
| licensesQualified | antal                                                         | Antalet kvalificerade licenser.                                               |
| customerId        | sträng                                                         | Kund-ID.                                                        |
| customerName      | sträng                                                         | Kundens namn.                                                              |
| Namn       | sträng                                                         | Produkt namnet.                                                               |
| serviceCode       | sträng                                                         | Tjänst koden för licensen.                                                |
| processedDateTime | sträng i UTC-datum/tid-format                                 | Datum och tid då data aggregerades.                                 |
| serviceName       | sträng                                                         | Tjänst namnet (till exempel: O365, CRM).                                              |
| kanalig           | sträng                                                         | Kanal namnet för tjänsten (till exempel: åter försäljare).                                |
| dokumentattribut        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. Inkluderar "objectType": "CustomerLicensesUsageInsights" |