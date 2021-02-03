---
title: Rättighets resurser
description: Beskriver resurser som är relaterade till rättigheten.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 428ac6f8b4d67894092119a6246279045a04dac0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769300"
---
# <a name="entitlement-resources"></a>Rättighets resurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

## <a name="entitlement"></a>Berättigande

Den här resursen representerar de produkter som kunden har rätt att använda på, på grund av partner köp för artiklar från katalogen.

| Egenskap | Typ | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Den ordnings referens som ledde till rättigheten. |
| productId | sträng | ID för produkten. |
| skuID | sträng | ID för SKU: n. |
| quantity | int | Antalet rättigheter (exkluderar ej uppfyllda/överförda rättigheter). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Listan över Detaljer om rättighets information (antal artiklar och status för varje kvantitet). |
| entitlementType | sträng | Typ av rättighet. (Uppdaterad till sträng från [EntitlementType](#entitlementtype) i SDK 1,8.) |
| entitledArtifacts | IEnumerable<[artefakt](#artifact)> | Listan över artefakter som är associerade med rättigheten. |
| IncludedEntitlements | [Stöd](#artifact) för IEnumerable-<> | Listan över rättigheter, som inkluderas implicit till följd av ett ProductId/SkuId-köp från katalogen. |
| ExpiryDate | sträng i UTC-datum/tid-format  | Förnamnets förfallo datum (om tillämpligt). |

## <a name="referenceorder"></a>ReferenceOrder

Ordnings referensen för en rättighet.

| Egenskap | Typ | Description |
|----------|------|-------------|
| id | sträng | ID: t för den refererade ordern. |
| lineItemId | sträng | ID för det refererade order rads objektet. |
| alternateId | sträng | Alternativt-ID för det refererade order rads objektet. |

## <a name="quantitydetail"></a>QuantityDetail

Visar information om en rättighets antal.

| Egenskap | Typ | Description |
|----------|------|-------------|
| quantity | int | Antal objekt. |
| status | sträng | Status för kvantitet. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> Föråldrad i SDK v 1.9

En [uppräkning](/dotnet/api/system.enum) med värden som anger typen av rättighet.

| Värde | Beskrivning |
|-------|-------------|
| Programvara | Anger rättighets typ som är relaterad till program vara. |
| VirtualMachineReservedInstance | Anger rättighets typ som är relaterad till Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakten som är associerad med rättigheten.

| Egenskap | Typ | Description |
|----------|------|-------------|
| artifactType | sträng | Typ av artefakt. (Uppdaterad till sträng från [ArtifactType](#artifacttype) i SDK v 1.8) |
| dynamicAttributes | Ord lista &lt; sträng, objekt&gt; | Dynamiska attribut som innehåller artifacttype-angivna värden. Till exempel när artifactType = "reservedinstance" innehåller den här egenskapen "reservationType" = "virtualmachines" eller "reservationType" = "sqldatabases" som betecknar en reserverad instans för virtuell dator eller en Azure SQL reserverad instans. (Tillgängligt från och med SDK v 1.9) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Föråldrad i SDK v 1.9

En [Enum](/dotnet/api/system.enum) med värden som anger typen av rättighets artefakt.

| Värde                          | Beskrivning                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Anger artefakt aids med hämtning av Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakten som är associerad med en Azure reserverad instans rättighet. Den ärver från [artefakt](#artifact) klassen.

| Egenskap   | Typ                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| länka       | [Operationsföljdslänkkod](./utility-resources.md#link) | Länken för att hämta all associerad artefakt information.   |
| resourceID | sträng                         | ID för Azures reservations ordning eller resurs. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Representerar entiteten som returnerades vid anrop av artefakt länken för den reserverade Azure-instansen.

|   Egenskap   |           Typ           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          sträng          |                     Typ av artefakt.                     |
| reservera | IEnumerable<Reservation> | Anger ID för Azure-resurs eller reservations order. |

## <a name="reservation"></a>Reservation

Representerar en enskild reservation.

| Egenskap          | Typ                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | sträng                         | ID för reservationen.                                         |
| scopeType         | sträng                         | Den typ av omfång som är associerad med reservationen för den virtuella datorn. |
| displayName       | sträng                         | Visnings namnet för reservationen.                               |
| appliedScopes     | IEnumerable                    | Listan över tillämpade scope som är associerade med reservationen. (Endast tillgängligt när scopeType inte är delad.) |
| quantity          | int                            | Antalet virtuella datorer i reservationen.                 |
| expiryDateTime    | sträng i UTC-datum/tid-format | Förfallo datumet för reservationen.                                |
| effectiveDateTime | sträng i UTC-datum/tid-format | Det effektiva datumet för reservationen.                             |
| provisioningState | sträng                         | Etablerings status för reservationen.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Föråldrad i SDK v 1.9

Artefakten som är associerad med en Azure reserverad virtuell dator instans rättighet. Den ärver från [artefakt](#artifact) klassen.

| Egenskap   | Typ                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| länka       | [Operationsföljdslänkkod](utility-resources.md#link) | Länken för att hämta all associerad artefakt information.   |
| resourceID | sträng                            | ID för Azures reservations ordning eller resurs. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Föråldrad i SDK v 1.9

Representerar entiteten som returnerades vid anrop av artefakt länken för den reserverade virtuella Azure-datorns instans.

| Egenskap                    | Typ                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| typ                        | [ArtifactType](#artifacttype)                                        | Typ av artefakt. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Anger ID för Azure-resurs eller reservations order. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Föråldrad i SDK v 1.9

Representerar en enskild virtuell dator reservation.

|     Egenskap      |              Typ              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             sträng             |                                         ID för reservationen.                                         |
|     scopeType     |             sträng             |                     Den typ av omfång som är associerad med reservationen för den virtuella datorn.                     |
|    displayName    |             sträng             |                                    Visnings namnet för reservationen.                                    |
|   appliedScopes   |      IEnumerable<string>       | Listan över tillämpade scope som är associerade med reservationen. (Endast tillgängligt när scopeType inte är delad.) |
|     quantity      |              int               |                             Antalet virtuella datorer i reservationen.                             |
|  expiryDateTime   | sträng i UTC-datum/tid-format |                                    Förfallo datumet för reservationen.                                     |
| effectiveDateTime | sträng i UTC-datum/tid-format |                                   Det effektiva datumet för reservationen.                                   |
| provisioningState |             sträng             |                                 Etablerings status för reservationen.                                 |
