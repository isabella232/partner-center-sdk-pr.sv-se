---
title: Berättiganderesurser
description: Beskriver resurser relaterade till berättigande.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9582bb0d886078062ae14d0461accb8e0179bed2e33e9a264cc1da8b06383706
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989159"
---
# <a name="entitlement-resources"></a>Berättiganderesurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

## <a name="entitlement"></a>Berättigande

Den här resursen representerar de produkter som kunden har rätt att använda på grund av partnerinköp på objekt från katalogen.

| Egenskap | Typ | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Orderreferensen som resulterade i rättigheten. |
| productId | sträng | ID för produkten. |
| skuID | sträng | ID för SKU:n. |
| quantity | int | Antalet berättiganden (utesluter ej ifyllda/överflyttningsberättiganden). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Listan över information om berättigandekvantitet (antalet objekt och status för varje kvantitet). |
| entitlementType | sträng | Typ av berättigande. (Har uppdaterats till sträng [från EntitlementType](#entitlementtype) i SDK 1.8.) |
| entitledArtifacts | IEnumerable<[Artifact](#artifact)> | Listan över artefakter som är associerade med rättigheten. |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)> | Listan över rättigheter, som ingår implicit som ett resultat av ProductId/SkuId-köpet från katalogen. |
| ExpiryDate | sträng i UTC-datum/tid-format  | Förfallodatum för rättigheten (om tillämpligt). |

## <a name="referenceorder"></a>ReferenceOrder

Orderreferensen för en rättighet.

| Egenskap | Typ | Description |
|----------|------|-------------|
| id | sträng | ID:t för den refererade ordern. |
| lineItemId | sträng | ID för det refererade orderradsobjektet. |
| alternateId | sträng | Alternativt ID för det refererade orderradsobjektet. |

## <a name="quantitydetail"></a>QuantityDetail

Representerar information om en berättigandekvantitet.

| Egenskap | Typ | Description |
|----------|------|-------------|
| quantity | int | Antal objekt. |
| status | sträng | Status för kvantitet. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> Inaktuell i SDK v1.9

En [Uppräkning](/dotnet/api/system.enum) med värden som anger typ av berättigande.

| Värde | Beskrivning |
|-------|-------------|
| Programvara | Anger typ av berättigande som är relaterad till programvara. |
| VirtualMachineReservedInstance | Anger typ av berättigande som är relaterad Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakten som är associerad med rättigheten.

| Egenskap | Typ | Description |
|----------|------|-------------|
| artifactType | sträng | Typ av artefakt. (Uppdaterad till sträng från [ArtifactType](#artifacttype) i SDK V1.8) |
| dynamicAttributes | &lt;Ordlistesträng, objekt&gt; | Dynamiska attribut som innehåller artefakttypsspecifika värden. Till exempel när artifactType = "reservedinstance" innehåller den här egenskapen "reservationType" = "virtualmachines" eller "reservationType" = "sqldatabases" som anger reserverad instans för virtuell dator eller reserverad Azure SQL-instans. (Tillgängligt från och med SDK v1.9) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Inaktuell i SDK v1.9

En [Uppräkning](/dotnet/api/system.enum) med värden som anger typen av berättigandeartefakt.

| Värde                          | Beskrivning                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Anger artefakten underlättar hämtningen av Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakten som är associerad med en reserverad Azure-instans-rättighet. Den ärver från [klassen Artifact.](#artifact)

| Egenskap   | Typ                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| länka       | [Länk](./utility-resources.md#link) | Länken för att hämta all associerad artefaktinformation.   |
| resourceID | sträng                         | ID för Azure-reservationsbeställningen eller -resursen. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Representerar den entitet som returneras vid anrop av artefaktlänken för reserverad Azure-instans.

|   Egenskap   |           Typ           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          sträng          |                     Typ av artefakt.                     |
| Reservationer | `IEnumerable<Reservation>` | Anger Identifierare för Azure-resurs eller reservationsbeställning. |

## <a name="reservation"></a>Reservation

Representerar en enskild reservation.

| Egenskap          | Typ                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | sträng                         | RESERVATIONENS ID.                                         |
| scopeType         | sträng                         | Den typ av omfång som associeras med reservationen av den virtuella datorn. |
| displayName       | sträng                         | Reservationens visningsnamn.                               |
| appliedScopes     | Ienumerable                    | Listan över tillämpade omfång som är associerade med reservationen. (Endast tillgängligt när scopeType inte delas.) |
| quantity          | int                            | Antalet virtuella datorer i reservationen.                 |
| expiryDateTime    | sträng i UTC-datum/tid-format | Reservationens förfallodatum.                                |
| effectiveDateTime | sträng i UTC-datum/tid-format | Reservationens effektiva datum.                             |
| provisioningState | sträng                         | Reservationens etableringstillstånd.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Inaktuell i SDK v1.9

Artefakten som är associerad med en Azure Reserved Virtual Machine Instance-rättighet. Den ärver från [klassen Artifact.](#artifact)

| Egenskap   | Typ                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| länka       | [Länk](utility-resources.md#link) | Länken för att hämta all associerad artefaktinformation.   |
| resourceID | sträng                            | ID för Azure-reservationsbeställningen eller -resursen. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Inaktuell i SDK v1.9

Representerar den entitet som returneras vid anrop av artefaktlänken azure reserved virtual machine instance.

| Egenskap                    | Typ                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| typ                        | [ArtifactType](#artifacttype)                                        | Typ av artefakt. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Anger Identifierare för Azure-resurs eller reservationsbeställning. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Inaktuell i SDK v1.9

Representerar en enskild reservation av virtuell dator.

|     Egenskap      |              Typ              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             sträng             |                                         RESERVATIONENS ID.                                         |
|     scopeType     |             sträng             |                     Den typ av omfång som associeras med reservationen av den virtuella datorn.                     |
|    displayName    |             sträng             |                                    Reservationens visningsnamn.                                    |
|   appliedScopes   |      `IEnumerable<string>`       | Listan över tillämpade omfång som är associerade med reservationen. (Endast tillgängligt när scopeType inte delas.) |
|     quantity      |              int               |                             Antalet virtuella datorer i reservationen.                             |
|  expiryDateTime   | sträng i UTC-datum/tid-format |                                    Reservationens förfallodatum.                                     |
| effectiveDateTime | sträng i UTC-datum/tid-format |                                   Reservationens effektiva datum.                                   |
| provisioningState |             sträng             |                                 Reservationens etableringstillstånd.                                 |
