---
title: Övergångsresurser
description: Beskriver de resurser som används för att övergå till nya handelsprenumerationer.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 44867be3823414ab43957e789c0cd29aef44d956
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457326"
---
# <a name="transition-resources"></a>Övergångsresurser

**Gäller för**

- Partnercenter

**Lämpliga roller**

- Global administratör
- Administratörsagent

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365.

Beskriver de resurser som används för att övergå från en ny handelsprenumeration till en annan.

## <a name="transitioneliblity"></a>TransitionEliblity

Beskriver beteendet för en enskild prenumerationsövergångsresurs.

| Egenskap          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| CatalogItemId | sträng                  | Katalogobjektets ID som kontrolleras. |
| Rubrik  | sträng                  | SKU-rubriken. |
| Description | sträng                  | SKU-beskrivningen. |
| Kvantitet | heltal                 | Antalet nya erbjudanden som ska köpas. |
| Eligibilities | lista över TransitionEligibilityDetail | En lista över information om berättigande till övergång. | 

## <a name="transitioneligibilitydetail"></a>TransitionEligibilityDetail

Beskriver beteendet för en enskild resurs för övergångsberättigande.

| Egenskap          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| IsEligible | boolean | Returnerar berättigandet är giltigt eller inte. |
| TransitionType | TransitionType | Typ av övergång. Kan vara transition_with_license_transfer eller transition_only. |
| Fel | Lista över TransitionErrors | Metadataattributen som motsvarar felet. |

## <a name="transition"></a>Övergången

Beskriver beteendet för en enskild prenumerationsövergångsresurs.

| Egenskap          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| FromCatalogItemId | sträng                  | Från katalogobjekt-ID. |
| ToCatalogItemId   | sträng                  | Till katalogobjekt-ID. |
| ToSubscriptionId  | sträng                  | Till prenumerations-ID. Detta fylls bara i om prenumerationen ändras. För närvarande behöver endast äldre uppgraderingar detta, men modern partiell övergång kommer också att göra det. |
| Kvantitet          | heltal                 | Kvantiteten som övergår till målkatalogobjektet. |
| TransitionType    | sträng              | Övergångstypen. Möjliga värden – transition_only, transition_with_license_transfer.   |
| Händelser            | lista över TransitionEvents | Övergångshändelserna. |

## <a name="transitionevent"></a>TransitionEvent

Beskriver en orsak till varför en uppgradering inte kan utföras.

| Egenskap          | Typ               | Beskrivning                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|------------------------------------------------------------------------------|
| Name | sträng | Namnet på övergångshändelsen. Möjliga värden Konvertering eller LicenseReassignment. |
| Status | sträng  | Status för övergångshändelsen. Möjliga värden InProgress, Completed eller Failed.  |
| Timestamp | DateTime | UTC-tidsstämpeln för händelsen. |
| Fel | Lista över TransitionErrors | Metadataattributen som motsvarar felet. |

## <a name="transitionerror"></a>TransitionError

Representerar ett fel för berättigande till prenumerationsöverföring. Anger en orsak till varför en övergång inte kan utföras.

| Egenskap          | Typ               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|--------------------------------------------------------------|
| Kod | TransitionErrorCode | Felkoden som är associerad med problemet. |
| Description | sträng  | Användarvänlig text som beskriver felet. |

