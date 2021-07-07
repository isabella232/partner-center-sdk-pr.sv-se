---
title: Berättiganderesurser
description: Beskriver resurser relaterade till rättigheten.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a5ddf5dcd1189f686c5d41c05d7c66abc46605cc
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906362"
---
# <a name="entitlement-resources"></a>Berättiganderesurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

## <a name="entitlement"></a>Berättigande

Den här resursen representerar de produkter som kunden har rätt att använda på grund av partnerinköp på objekt från katalogen.

| Egenskap | Typ | Beskrivning |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Den orderreferens som resulterade i rättigheten. |
| productId | sträng | ID för produkten. |
| skuID | sträng | ID för SKU:n. |
| quantity | int | Antalet berättiganden (gäller inte ej ifyllda/överflyttningar av rättigheter). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Listan med information om berättigandekvantitet (antalet objekt och status för varje kvantitet). |
| entitlementType | sträng | Typ av berättigande. (Har uppdaterats till sträng [från EntitlementType](#entitlementtype) i SDK 1.8.) |
| entitledArtifacts | IEnumerable<[Artifact](#artifact)> | Listan över artefakter som är associerade med rättigheten. |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)> | Listan över rättigheter, som implicit ingår som ett resultat av ProductId/SkuId-köpet från katalogen. |
| ExpiryDate | sträng i UTC-datum/tid-format  | Förfallodatum för rättigheten (om tillämpligt). |

## <a name="referenceorder"></a>ReferenceOrder

Orderreferensen för en rättighet.

| Egenskap | Typ | Beskrivning |
|----------|------|-------------|
| id | sträng | ID:t för den refererade ordern. |
| lineItemId | sträng | ID för det refererade orderradsobjektet. |
| alternateId | sträng | Alternativt ID för det refererade orderradsobjektet. |

## <a name="quantitydetail"></a>QuantityDetail

Representerar information om en berättigandekvantitet.

| Egenskap | Typ | Beskrivning |
|----------|------|-------------|
| quantity | int | Antal objekt. |
| status | sträng | Status för kvantitet. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> Inaktuell i SDK v1.9

En [Enum](/dotnet/api/system.enum) med värden som anger typen av berättigande.

| Värde | Beskrivning |
|-------|-------------|
| Programvara | Anger typ av berättigande som är relaterad till programvara. |
| VirtualMachineReservedInstance | Anger typ av berättigande som är relaterad Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakten som är associerad med rättigheten.

| Egenskap | Typ | Beskrivning |
|----------|------|-------------|
| artifactType | sträng | Typ av artefakt. (Uppdaterat till sträng från [ArtifactType](#artifacttype) i SDK V1.8) |
| dynamicAttributes | &lt;Ordlistesträng, objekt&gt; | Dynamiska attribut som innehåller artefakttypspecifika värden. När till exempel artifactType = "reservedinstance" innehåller den här egenskapen "reservationType" = "virtualmachines" eller "reservationType" = "sqldatabases" som anger reserverad instans för virtuell dator eller reserverad Azure SQL-instans. (Tillgängligt från och med SDK v1.9) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Inaktuell i SDK v1.9

En [Uppräkning med](/dotnet/api/system.enum) värden som anger typen av berättigandeartefakt.

| Värde                          | Beskrivning                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Anger artefakthjälpmedel med hämtning av Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakten som är associerad med en rättighet för en reserverad Azure-instans. Den ärver från [klassen Artifact.](#artifact)

| Egenskap   | Typ                           | Beskrivning                                        |
|------------|--------------------------------|----------------------------------------------------|
| länka       | [Länk](./utility-resources.md#link) | Länken för att hämta all associerad artefaktinformation.   |
| resourceID | sträng                         | ID för Azure-reservationsbeställningen eller -resursen. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Representerar den entitet som returneras vid anrop av artefaktlänken för reserverad Azure-instans.

|   Egenskap   |           Typ           |                          Beskrivning                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          sträng          |                     Typ av artefakt.                     |
| Reservationer | Ienumerable<Reservation> | Anger Id för Azure-resurs eller reservationsbeställning. |

## <a name="reservation"></a>Reservation

Representerar en enskild reservation.

| Egenskap          | Typ                           | Beskrivning                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | sträng                         | ID för reservationen.                                         |
| scopeType         | sträng                         | Den typ av omfång som är associerad med reservationen av den virtuella datorn. |
| displayName       | sträng                         | Reservationens visningsnamn.                               |
| appliedScopes     | Ienumerable                    | Listan över tillämpade omfång som är associerade med reservationen. (Endast tillgängligt när scopeType inte delas.) |
| quantity          | int                            | Antalet virtuella datorer i reservationen.                 |
| expiryDateTime    | sträng i UTC-datum/tid-format | Reservationens förfallodatum.                                |
| effectiveDateTime | sträng i UTC-datum/tid-format | Reservationens effektiva datum.                             |
| provisioningState | sträng                         | Reservationens etableringstillstånd.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Inaktuell i SDK v1.9

Artefakten som är associerad med en Azure Reserved Virtual Machine Instance-berättigande. Den ärver från [klassen Artifact.](#artifact)

| Egenskap   | Typ                              | Beskrivning                                        |
|------------|-----------------------------------|----------------------------------------------------|
| länka       | [Länk](utility-resources.md#link) | Länken för att hämta all associerad artefaktinformation.   |
| resourceID | sträng                            | ID för Azure-reservationsbeställningen eller -resursen. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Inaktuell i SDK v1.9

Representerar den entitet som returneras vid anrop av artefaktlänken azure reserved virtual machine instance.

| Egenskap                    | Typ                                                                 | Beskrivning           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| typ                        | [ArtifactType](#artifacttype)                                        | Typ av artefakt. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Anger Id för Azure-resurs eller reservationsbeställning. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Inaktuell i SDK v1.9

Representerar en enskild virtuell datorreservation.

|     Egenskap      |              Typ              |                                                Beskrivning                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             sträng             |                                         ID för reservationen.                                         |
|     scopeType     |             sträng             |                     Den typ av omfång som är associerad med reservationen av den virtuella datorn.                     |
|    displayName    |             sträng             |                                    Reservationens visningsnamn.                                    |
|   appliedScopes   |      Ienumerable<string>       | Listan över tillämpade omfång som är associerade med reservationen. (Endast tillgängligt när scopeType inte delas.) |
|     quantity      |              int               |                             Antalet virtuella datorer i reservationen.                             |
|  expiryDateTime   | sträng i UTC-datum/tid-format |                                    Reservationens förfallodatum.                                     |
| effectiveDateTime | sträng i UTC-datum/tid-format |                                   Reservationens effektiva datum.                                   |
| provisioningState |             sträng             |                                 Reservationens etableringstillstånd.                                 |
