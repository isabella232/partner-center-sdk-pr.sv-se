---
title: Marginalresurser
description: Resurser som representerar marginaler. Innehåller resurser för att beskriva marginalerna.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 83ea2f95c72f4e5074e3396ef226462b5b007878
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646421"
---
# <a name="margin-resources"></a>Marginalresurser

Resurser som representerar tillgängliga marginaler. Innehåller resurser för att beskriva en marginal.  

Oberoende programvaruleverantör (ISV) kan skapa rabatter eller marginaler för specifika molnlösningsleverantörer (CPS). Nedan visas resurser som representerar och beskriver marginaler.
                
## <a name="margin"></a>Marginal                   
                        
Representerar en genomsnittlig marginal för en viss CSP.
                
| Namn            | Typ            | Description                               |
|-----------------|-----------------|-------------------------------------------|
| id              | sträng          | Unik identifierare för marginalen.         |
| marginPercentage | antal         | En procentuell rabatt som tillämpas på CSP-återförsäljarpriset.  |
| productId       | sträng          | Produkt-ID:t som marginalen är tillgänglig för.   |
| productTitle    | sträng          | Produkttiteln som marginalen är tillgänglig för. |
| productType     | sträng          | Den produkttyp som marginalen är tillgänglig för.   |
| publisherName   | sträng          | Namnet på den ISV som skapade marginalen.  |
| skuId           | sträng          | Det SKU-ID som marginalen är tillgänglig för.  |
| skuTitle        | sträng          | SKU-rubriken som marginalen är tillgänglig för. |
| Startdate       | sträng          | Startdatumet som marginalen är tillgänglig. |
| endDate         | sträng          | Slutdatumet för marginalen i är tillgängligt. |
| status          | sträng          | Status som anger om marginalen är tillgänglig. |
| statusDate      | sträng          | Det datum då statusen senast uppdaterades. |

## <a name="definitions"></a>Definitioner

Olika typer av artefakter som beskriver marginaler.                    

| Name            | Beskrivning          |
|-----------------|----------------------|
| Marginal |  Definierar en enskild marginal.  |    
| MarginSearchResponse |  Definierar marginalsvarsdata.  |  
        
## <a name="related-documentation"></a>Relaterad dokumentation

- [Översikt över marginaler i Partnercenter](/partner-center/csp-commercial-marketplace-margins)
- [Köpa Marketplace-erbjudanden](/partner-center/csp-commercial-marketplace-purchase)
- [Hantera Marketplace-erbjudanden](/partner-center/csp-commercial-marketplace-manage)
- [Hämta en lista över marginaler](get-margins.md)
- [Ladda ned en lista med marginaler](download-margins.md)
