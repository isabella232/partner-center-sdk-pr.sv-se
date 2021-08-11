---
title: Resurser för enhetsdistribution
description: Resurser som rör distribution av Partnercenter-enheter.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8e2429fea88a89873955d9af9253492934e40e5be1a1b7600446485d13f5bd7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994854"
---
# <a name="device-deployment-resources"></a>Resurser för enhetsdistribution

**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland

Följande resurser är relaterade till enhetsdistribution.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** innehåller information om en konfigurationsprincip.

| Egenskap             | Typ                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | sträng                                       | En GUID-formaterad sträng som identifierar principen.                                  |
| name                 | sträng                                       | Principens egna namn.                                                    |
| category             | sträng                                       | Kategorin .                                                                        |
| beskrivning          | sträng                                       | Principbeskrivningen.                                                              |
| devicesAssignedCount | antal                                       | Antalet enheter som är tilldelade till den här principen.                                       |
| policySettings       | matris med strängar                             | Principinställningarna: "none","remove \_ oem \_ preinstalls","oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration", "skip \_ eula".    |
| createdDate          | sträng i UTC-datum/tid-format               | Datum och tid då principen skapades.                                            |
| lastModifiedDate     | sträng i UTC-datum/tid-format               | Datum och tid då principen senast ändrades.                                      |
| Attribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                            |

## <a name="device"></a>Enhet

**Enheten** innehåller information om en enhet.

| Egenskap            | Typ                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | sträng                                                         | En GUID-formaterad sträng som identifierar enheten.                      |
| serialNumber        | sträng                                                         | Serienumret som är unikt associerat med enheten.                   |
| Produkt          | sträng                                                         | Produktnyckeln som är unikt associerad med enheten.                     |
| hardwareHash        | sträng                                                         | Den maskinvaruhash som är unikt associerad med enheten.                   |
| modelName           | sträng                                                         | Modellnamnet som är associerat med enheten.                               |
| oemManufacturerName | sträng                                                         | Namnet på den OEM-tillverkare som är associerad med enheten.             |
| policies            | matris med objekt                                               | Listan över principer som tilldelats enheten.                             |
| uploadedDate        | sträng i UTC-datum/tid-format                                 | Datum och tid då enhetsinformationen laddades upp.                      |
| allowedOperations   | matris med strängar                                               | Listan över HTTP-metoder som tillåts vid en enhetssynkronisering som GET, PATCH, DELETE. |
| Attribut          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** beskriver status för en enhets batchuppladdning av information om varje enhet i en lista över enheter.

| Egenskap        | Typ     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | sträng   | En GUID-formaterad sträng som är associerad med batchen med enheter som laddats upp. |
| status          | sträng   | Status för batchuppladdningen: "unknown","queued","processing","finished","finished \_ with \_ errors". |
| startedTime     | sträng i UTC-datum/tid-format | Datum och tid då batchuppladdningen startade.   |
| completedTime   | sträng i UTC-datum/tid-format  | Datum och tid då batchuppladdningen slutfördes.   |
| devicesStatus   | matris med [DeviceUploadDetails-resurser](#deviceuploaddetails) | En matris med objekt som anger status för varje uppladdning av enhetsinformation. |
| Attribut      | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** beskriver status för en uppladdning av information om en enhet.

| Egenskap         | Typ                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | sträng                  | En GUID-formaterad sträng som är associerad med enheten. |
| serialNumber     | sträng                  | Serienumret som är unikt associerat med enheten. |
| Produkt       | sträng                  | Produktnyckeln som är unikt associerad med enheten. |
| status           | sträng                  | Status för uppladdning av enhetsinformation: "pågår", "slutfört", \_ "slutfört \_ med fel". |
| errorCode        | sträng                  | HTTP-statusfelkoden returneras om enhetsuppladdningen misslyckas. |
| errorDescription | sträng                  | HTTP-felbeskrivningen om enhetsuppladdningen misslyckas. |
| Attribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** representerar en samling enheter.

| Egenskap     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | sträng                                                         | En GUID-formaterad sträng som är associerad med batchen med enheter. |
| createdBy    | sträng                                                         | Namnet på den klientorganisation som skapade samlingen.                   |
| creationDate | sträng i UTC-datum/tid-format                                 | Data och tid då samlingen skapades.                    |
| deviceCount  | antal                                                         | Antalet enheter i samlingen.                              |
| devicesLink  | [Länk](utility-resources.md#link)                              | En länk till de enheter som ingår i den här batchen.                        |
| Attribut   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest tillhandahåller** den information som krävs för att skapa en enhetsbatch och fylla den med enheter.

| Egenskap     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | sträng                                                         | En GUID-formaterad sträng som är associerad med batchen med enheter. |
| devices      | matris med [enhetsobjekt](#device)                             | Varje objekt anger en enhet. Följande kombinationer av fält för att identifiera en enhet accepteras: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| Attribut   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest innehåller** den information som krävs för att uppdatera en lista över enheter med en princip.

| Egenskap     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | matris med [enhetsobjekt](#device)                             | Varje objekt anger en enhet. Följande egenskaper krävs: Id, Principer. |
| Attribut   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen.                                              |
