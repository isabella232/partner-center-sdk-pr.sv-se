---
title: Enhets distributions resurser
description: Resurser som rör distribution av Partner Center-enheter.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a464cdad3979c305df16a3bdc9133ce70a7ac688
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768784"
---
# <a name="device-deployment-resources"></a>Enhets distributions resurser

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland

Följande resurser är relaterade till enhets distribution.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** innehåller information om en konfigurations princip.

| Egenskap             | Typ                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | sträng                                       | En GUID-formaterad sträng som identifierar principen.                                  |
| name                 | sträng                                       | Det egna namnet på principen.                                                    |
| category             | sträng                                       | Kategorin.                                                                        |
| beskrivning          | sträng                                       | Princip beskrivningen.                                                              |
| devicesAssignedCount | antal                                       | Antalet enheter som har tilldelats den här principen.                                       |
| policySettings       | matris med strängar                             | Princip inställningarna: "ingen", "ta bort \_ OEM \_ -förinstallationer", "OOBE \_ User \_ not \_ Local \_ admin", "hoppa över \_ Express \_ Inställningar", "hoppa över \_ OEM \_ -registrering", "hoppa över \_ EULA".    |
| createdDate          | sträng i UTC-datum/tid-format               | Datum och tid då principen skapades.                                            |
| lastModifiedDate     | sträng i UTC-datum/tid-format               | Datum och tid då principen senast ändrades.                                      |
| dokumentattribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.                                            |

## <a name="device"></a>Enhet

**Enheten** tillhandahåller information om en enhet.

| Egenskap            | Typ                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | sträng                                                         | En GUID-formaterad sträng som identifierar enheten.                      |
| serialNumber        | sträng                                                         | Serie numret som är unikt för enheten.                   |
| productKey          | sträng                                                         | Produkt nyckeln som är unik för enheten.                     |
| hardwareHash        | sträng                                                         | Maskinvaru-hash som unikt associeras med enheten.                   |
| modelName           | sträng                                                         | Modell namnet som är associerat med enheten.                               |
| oemManufacturerName | sträng                                                         | Namnet på OEM-tillverkaren som är associerad med enheten.             |
| policies            | objekt mat ris                                               | Listan över principer som tilldelats enheten.                             |
| uploadedDate        | sträng i UTC-datum/tid-format                                 | Datum och tid då enhets informationen laddades upp.                      |
| allowedOperations   | matris med strängar                                               | Listan över HTTP-metoder som tillåts på en enhets-synkronisering som GET, PATCH, DELETE. |
| dokumentattribut          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** beskriver statusen för en enhets batch-överföring av information om varje enhet i en lista över enheter.

| Egenskap        | Typ     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | sträng   | En GUID-formaterad sträng som är associerad med den grupp med enheter som har överförts. |
| status          | sträng   | Status för batch-överföringen: "okänd", "köade", "bearbetar", "avslutad", "klart \_ med \_ fel". |
| startedTime     | sträng i UTC-datum/tid-format | Datum och tid då batch-uppladdnings processen startades.   |
| completedTime   | sträng i UTC-datum/tid-format  | Datum och tid då batch-överföringen slutfördes.   |
| devicesStatus   | matris med [DeviceUploadDetails](#deviceuploaddetails) -resurser | En matris med objekt som anger status för varje enhets informations uppladdning. |
| dokumentattribut      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** beskriver statusen för en överföring av information om en enhet.

| Egenskap         | Typ                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | sträng                  | En GUID-formaterad sträng som är associerad med enheten. |
| serialNumber     | sträng                  | Serie numret som är unikt för enheten. |
| productKey       | sträng                  | Produkt nyckeln som är unik för enheten. |
| status           | sträng                  | Status för enhets informations uppladdning: "pågår", "slutfört", "slutfört \_ med \_ fel". |
| errorCode        | sträng                  | Fel koden för HTTP-status returneras om enhets uppladdningen Miss lyckas. |
| errorDescription | sträng                  | HTTP-fel beskrivningen om enhets uppladdningen Miss lyckas. |
| dokumentattribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** representerar en samling enheter.

| Egenskap     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | sträng                                                         | En GUID-formaterad sträng som är associerad med gruppens enheter. |
| createdBy    | sträng                                                         | Namnet på den klient som skapade samlingen.                   |
| creationDate | sträng i UTC-datum/tid-format                                 | De data och den tidpunkt då samlingen skapades.                    |
| deviceCount  | antal                                                         | Antalet enheter i samlingen.                              |
| devicesLink  | [Operationsföljdslänkkod](utility-resources.md#link)                              | En länk till de enheter som ingår i den här batchen.                        |
| dokumentattribut   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** innehåller den information som krävs för att skapa en enhets batch och fylla den med enheter.

| Egenskap     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | sträng                                                         | En GUID-formaterad sträng som är associerad med gruppens enheter. |
| devices      | matris med [enhets](#device) objekt                             | Varje-objekt anger en enhet. Följande kombinationer av fält för att identifiera en enhet godkänns: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, endast hardwareHash, productKey, serialNumber + oemManufacturerName + modelName. |
| dokumentattribut   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** innehåller den information som krävs för att uppdatera en lista över enheter med en princip.

| Egenskap     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | matris med [enhets](#device) objekt                             | Varje-objekt anger en enhet. Följande egenskaper krävs: ID, principer. |
| dokumentattribut   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata.                                              |
