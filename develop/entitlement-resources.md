---
title: Berättiganderesurser
description: Beskriver resurser relaterade till berättigande.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 929004fff804675218e267bb928b432f7b1209bf
ms.sourcegitcommit: 84a6f701190f46d2adcf6edcaeaafa32d58fbaba
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2021
ms.locfileid: "113510116"
---
# <a name="entitlement-resources"></a>Berättiganderesurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

## <a name="entitlement"></a>Berättigande

Den här resursen representerar de produkter som kunden har rätt att använda på grund av partnerinköp på objekt från katalogen.

| Egenskap | Typ | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Orderreferensen som resulterade i rättigheten. |
| productId | sträng | ID för produkten. |
| skuID | sträng | ID för SKU:n. |
| quantity | int | Antalet berättiganden (exkluderar ej ifyllda/överflyttningsberättiganden). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Listan med information om berättigandekvantitet (antalet objekt och status för varje kvantitet). |
| entitlementType | sträng | Typ av berättigande. (Uppdaterat till sträng från [EntitlementType](#entitlementtype) i SDK 1.8.) |
| entitledArtifacts | IEnumerable<[Artifact](#artifact)> | Listan över artefakter som är associerade med rättigheten. |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)> | Listan över rättigheter, som implicit ingår som ett resultat av productId/SkuId-köpet från katalogen. |
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

En [Uppräkning](/dotnet/api/system.enum) med värden som anger typen av berättigande.

| Värde | Beskrivning |
|-------|-------------|
| Programvara | Anger typ av berättigande som är relaterad till programvara. |
| VirtualMachineReservedInstance | Anger typ av berättigande som är Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakten som är associerad med rättigheten.

| Egenskap | Typ | Description |
|----------|------|-------------|
| artifactType | sträng | Typ av artefakt. (Uppdaterat till sträng från [ArtifactType](#artifacttype) i SDK V1.8) |
| dynamicAttributes | &lt;Ordlistesträng, objekt&gt; | Dynamiska attribut som innehåller artefakttypspecifika värden. Till exempel när artifactType = "reservedinstance" innehåller den här egenskapen "reservationType" = "virtualmachines" eller "reservationType" = "sqldatabases" som anger reserverad instans för virtuell dator eller reserverad Azure SQL-instans. (Tillgängligt från och med SDK v1.9) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Inaktuell i SDK v1.9

En [Uppräkning med](/dotnet/api/system.enum) värden som anger typen av berättigandeartefakt.

| Värde                          | Beskrivning                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Anger artefakthjälpmedel med hämtning av Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakten som är associerad med en rättighet för en reserverad Azure-instans. Den ärver från [klassen Artifact.](#artifact)

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
| scopeType         | sträng                         | Den typ av omfång som är associerad med reservationen av virtuella datorer. |
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
|     scopeType     |             sträng             |                     Den typ av omfång som är associerad med reservationen av virtuella datorer.                     |
|    displayName    |             sträng             |                                    Reservationens visningsnamn.                                    |
|   appliedScopes   |      `IEnumerable<string>`       | Listan över tillämpade omfång som är associerade med reservationen. (Endast tillgängligt när scopeType inte delas.) |
|     quantity      |              int               |                             Antalet virtuella datorer i reservationen.                             |
|  expiryDateTime   | sträng i UTC-datum/tid-format |                                    Reservationens förfallodatum.                                     |
| effectiveDateTime | sträng i UTC-datum/tid-format |                                   Reservationens effektiva datum.                                   |
| provisioningState |             sträng             |                                 Reservationens etableringstillstånd.                                 |
