---
title: Resurs poster för Azure-användning
description: Azure-nyttjande posten innehåller information om användningen av en Azure-prenumerations resurs.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 21d39c4497c00f5abeeeb771dfe20cd1e2b1c13a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768832"
---
# <a name="azure-utilization-record-resources"></a>Resurs poster för Azure-användning

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Azure-nyttjande posten innehåller information om användningen av en Azure-prenumerations resurs. Om du är en partner för moln tjänst leverantörer som äger fakturerings förhållandet för dina kunders Azure-prenumerationer kan du använda den här REST API för att ge ett skalbart sätt att spåra användningen av prenumerationerna för att skicka en faktura till kunderna i slutet av varje fakturerings period.

Om du vill spåra användningen och förutsäga din månads faktura och fakturor för enskilda kunder kan du kombinera en pris fråga för att [få priser för Microsoft Azure](get-prices-for-microsoft-azure.md) med en begäran om att [få en kunds användnings poster för Azure](get-a-customer-s-utilization-record-for-azure.md).

Priserna skiljer sig mellan marknaden och valutan, och detta API tar hänsyn till. Som standard använder API dina partner profil inställningar i Partner Center och ditt webb läsar språk, och dessa inställningar är anpassningsbara. Plats medvetenheten är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Beskriver egenskaperna för en resurs för Azure förbruknings poster.

| Egenskap       | Typ                                      | Obligatorisk | Beskrivning                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | sträng                                    | Yes      | Början av tidsintervallet för användnings aggregatet. Svaret grupperas efter tidpunkten för förbrukningen (när resursen faktiskt användes jämfört med när den rapporterades till fakturerings systemet). |
| usageEndTime   | sträng                                    | Yes      | Slutet av tidsintervallet för användnings aggregatet. Svaret grupperas efter förbruknings tiden. Det vill säga när resursen faktiskt användes jämfört med när den rapporterades till fakturerings systemet.   |
| resource       | objekt                                    | Yes      | Innehåller ett [AzureResource](#azureresource) -objekt.                                                                                                                                     |
| quantity       | antal                                    | Yes      | Förbrukat antal för [AzureResource.](#azureresource)                                                                                                                           |
| unit           | sträng                                    | No       | Typ av kvantitet (timmar, byte osv.) Den här egenskapen är valfri                                                                                                                     |
| infoFields     | objekt                                    | Yes      | Nyckel/värde-par för information om instans nivå. Det här objektet kan vara tomt.                                                                                                                    |
| instanceData   | objekt                                    | No       | Innehåller ett [AzureInstanceData](#azureinstancedata) -objekt som innehåller nyckel/värde-par av information om instans nivå. Den här egenskapen är valfri och får inte tas med.                  |
| dokumentattribut     | [ResourceAttributes](utility-resources.md#resourceattributes) | Yes      | Attribut för metadata. Innehåller "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Åtgärder på AzureUtilizationRecord-resursen

- [Hämta en kunds användningsposter för Azure](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Beskriver egenskaperna för en Azure-resurs.

| Egenskap    | Typ   | Obligatorisk | Beskrivning                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | sträng | Yes      | Unikt ID för Azure-resursen. Kallas även resourceID eller resurs-GUID. |
| name        | sträng | No       | Eget namn på den resurs som används. Den här egenskapen är valfri.            |
| category    | sträng | No       | Kategorin för den förbrukade resursen. Den här egenskapen är valfri.                   |
| under kategori | sträng | No       | Den förbrukade resursens under kategori. Den här egenskapen är valfri.               |
| region      | sträng | No       | Regionen för den förbrukade resursen. Den här egenskapen är valfri.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Beskriver egenskaperna för en Azure instance data-resurs.

| Egenskap       | Typ             | Obligatorisk | Beskrivning                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | sträng           | Yes      | Det fullständigt kvalificerade Azure-resurs-ID: t, som innehåller resurs grupperna och instans namnet.                   |
| location       | sträng           | Yes      | Region där tjänsten kördes.                                                                               |
| partNumber     | objekt           | Yes      | Unikt namn område som används för att identifiera resursen för användning av tredje part från kommersiell marknads plats. Den här egenskapen kan vara en tom sträng. |
| orderNumber    | antal           | Yes      | Unikt namn område som används för att identifiera tredje parts ordning för kommersiell marknads plats. Den här egenskapen kan vara en tom sträng.          |
| tags           | matris med strängar | No       | Resurs koder som anges av användaren. Den här egenskapen är valfri och får inte tas med.                            |
| additionalInfo | matris med strängar | No       | Ytterligare data för en Azure-resurs. Den här egenskapen är valfri och får inte tas med.                          |