---
title: Registrera resurser för Azure-användning
description: Azure-användningsposten innehåller information om användningen av en Azure-prenumerationsresurs.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 868381fcb29eb1391efcdf79154f7b998e3032e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974309"
---
# <a name="azure-utilization-record-resources"></a>Registrera resurser för Azure-användning

**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Azure-användningsposten innehåller information om användningen av en Azure-prenumerationsresurs. Om du är en molntjänstleverantörspartner som äger faktureringsrelationen för dina kunders Azure-prenumerationer kan du använda den här REST API för att tillhandahålla ett skalbart sätt att spåra användning som uppstår för prenumerationerna för att skicka en faktura till dina kunder i slutet av varje faktureringsperiod.

Om du vill spåra användning och hjälpa till att förutsäga din månadsfaktura och fakturorna för enskilda kunder kan du kombinera en Rate Card-fråga för att [hämta priser](get-prices-for-microsoft-azure.md) för Microsoft Azure med en begäran om att hämta en [kunds](get-a-customer-s-utilization-record-for-azure.md)användningsposter för Azure .

Priserna varierar beroende på marknad och valuta, och det här API:et tar hänsyn till platsen. Som standard använder API:et dina partnerprofilinställningar i Partnercenter och ditt webbläsarspråk, och dessa inställningar är anpassningsbara. Platsmedvetenhet är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Beskriver egenskaperna för en resurs för en Azure-användningspost.

| Egenskap       | Typ                                      | Obligatorisk | Beskrivning                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | sträng                                    | Ja      | Starttidsintervallet för användningsaggregeringen. Svaret grupperas efter förbrukningstid (när resursen användes jämfört med när rapporterades den till faktureringssystemet). |
| usageEndTime   | sträng                                    | Ja      | Slutet på användningsaggregeringens tidsintervall. Svaret grupperas efter förbrukningstid. Det vill säga när resursen användes jämfört med när rapporterades den till faktureringssystemet.   |
| resource       | objekt                                    | Ja      | Innehåller ett [AzureResource-objekt.](#azureresource)                                                                                                                                     |
| quantity       | antal                                    | Ja      | Den kvantitet som förbrukas av [AzureResource.](#azureresource)                                                                                                                           |
| unit           | sträng                                    | No       | Typ av kvantitet (timmar, byte osv.) Den här egenskapen är valfri                                                                                                                     |
| infoFields     | objekt                                    | Ja      | Nyckel/värde-par med information på instansnivå. Det här objektet kan vara tomt.                                                                                                                    |
| instanceData   | objekt                                    | Inga       | Innehåller ett [AzureInstanceData-objekt](#azureinstancedata) som innehåller nyckel/värde-par med information på instansnivå. Den här egenskapen är valfri och kan inte inkluderas.                  |
| Attribut     | [ResourceAttributes](utility-resources.md#resourceattributes) | Ja      | Metadataattributen. Innehåller "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Åtgärder på AzureUtilizationRecord-resursen

- [Hämta en kunds användningsposter för Azure](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Beskriver egenskaperna för en Azure-resurs.

| Egenskap    | Typ   | Obligatorisk | Beskrivning                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | sträng | Ja      | Unik identifierare för Azure-resursen. Kallas även resourceID eller resurs-GUID. |
| name        | sträng | No       | Eget namn på den resurs som förbrukas. Den här egenskapen är valfri.            |
| category    | sträng | No       | Kategorin för den förbrukade resursen. Den här egenskapen är valfri.                   |
| Underkategori | sträng | No       | Underkategorin för den förbrukade resursen. Den här egenskapen är valfri.               |
| region      | sträng | No       | Regionen för den förbrukade resursen. Den här egenskapen är valfri.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Beskriver egenskaperna för en Azure Instance Data-resurs.

| Egenskap       | Typ             | Obligatorisk | Beskrivning                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | sträng           | Ja      | Det fullständigt kvalificerade Azure-resurs-ID:t, som innehåller resursgrupperna och instansnamnet.                   |
| location       | sträng           | Ja      | Region där tjänsten har körts.                                                                               |
| partNumber     | objekt           | Ja      | Unikt namnområde som används för att identifiera resursen för användning från tredje part på den kommersiella marknadsplatsen. Den här egenskapen kan vara en tom sträng. |
| orderNumber    | antal           | Ja      | Unikt namnområde som används för att identifiera tredjepartsbeställningen för den kommersiella marknadsplatsen. Den här egenskapen kan vara en tom sträng.          |
| tags           | matris med strängar | Inga       | Resurstaggar som anges av användaren. Den här egenskapen är valfri och kan inte inkluderas.                            |
| additionalInfo | matris med strängar | Inga       | Ytterligare data för en Azure-resurs. Den här egenskapen är valfri och kan inte inkluderas.                          |