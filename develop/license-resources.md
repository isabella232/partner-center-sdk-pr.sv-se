---
title: Licensresurser
description: Beskriver resurser relaterade till licenser.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 27d44f89ac89f365e77e073c425ca45ab3638c68
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548404"
---
# <a name="license-resources"></a>Licensresurser

**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Beskriver resurser relaterade till licenser.

## <a name="license"></a>Licens

Beskriver en användarlicens.

>[!NOTE]
>Stöds inte på Partner Center som drivs av 21Vianet.

| Egenskap     | Typ                                                           | Beskrivning                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | matris med ServicePlan-resurser                                 | En samling tjänstplaner som motsvarar licensen |
| productSKU   | ProductSku                                                     | SKU:n för den produkt som motsvarar licensen.        |
| Attribut   | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar licensen.          |

## <a name="licenseupdate"></a>LicenseUpdate

Innehåller information som används för att tilldela eller ta bort licenser från en användare.

| Egenskap         | Typ                                                           | Beskrivning                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | matris med objekt                                               | Matris med [LicenseAssignment-objekt.](#licenseassignment) |
| licensesToRemove | matris med strängar                                               | Produktens SKU-identifierare för de licenser som ska tas bort.    |
| licenseWarnings  | matris med objekt                                               | Matris med [LicenseWarning-objekt.](#licensewarning)       |
| Attribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                  |

## <a name="licenseassignment"></a>LicenseAssignment

Innehåller information som behövs för en licensuppdateringsåtgärd.

| Egenskap      | Typ             | Beskrivning                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | matris med strängar | De tjänstplansidentifierare som ska undantas från tillgängligheten för användaren. |
| skuId         | sträng           | Produktens SKU-identifierare för licensen.                                |

## <a name="licensewarning"></a>LicenseWarning

Innehåller varningsinformation som inträffade under en licensuppdateringsåtgärd.

| Egenskap     | Typ             | Beskrivning                                         |
|--------------|------------------|-----------------------------------------------------|
| kod         | sträng           | Varningskoden.                                   |
| meddelande      | sträng           | Varningsmeddelandet.                                |
| servicePlans | matris med strängar | De tjänstplannamn som är associerade med varningen. |

## <a name="productsku"></a>ProductSku

Beskriver produktinformation.

| Egenskap       | Typ             | Beskrivning                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | sträng           | Produktidentifieraren.                             |
| name           | sträng           | Användarens huvudnamnsidentifierare.                      |
| skuPartNumber  | sträng           | SKU-delens nummernamn för produkten. Till exempel, för Office 365 E3 är det här värdet `EnterprisePack` . Den här egenskapen kan användas i stället för ID om ID:t inte är tillgängligt.                |
| targetType     | sträng           | Måltypen för produkten. Den här egenskapen anger om produkten gäller för en `User` eller en `Tenant` .                                                                    |
| licenseGroupId | sträng           | Identifierar den utfärdare eller tjänst som hanterar productSku-licensen via en gruppidentifierare. Produkter är åtskilda under licensgrupper för bättre hanterbarhet.<br/><br/>                                                                                     `group1`– Alla produkter vars licenser kan hanteras av Azure Active Directory (AAD).<br/><br/>                                            `group2`– Minecraft produktlicenser.                                         |

## <a name="serviceplan"></a>ServicePlan

Identifierar en distribuerad tjänst i en produkt-SKU. En produkt kan ha många tjänstplaner.

| Egenskap         | Typ   | Beskrivning                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | sträng | Identifierare för tjänstplan.                                                                                      |
| displayName      | sträng | Det lokaliserade visningsnamnet för tjänstplanen.                                                                  |
| Tjänstnamn      | sträng | Tjänstens namn.                                                                                                 |
| capabilityStatus | sträng | Tjänstplanens status.                                                                      |
| targetType       | sträng | Måltypen för tjänstplanen. Den här egenskapen anger om produkten gäller för en "användare" eller en "klientorganisation". |

## <a name="subscribedsku"></a>SubscribedSku

Beskriver en prenumererad produkt som ägs av en klientorganisation.

| Egenskap         | Typ                                                           | Beskrivning                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | heltal                                                        | Antalet enheter som är tillgängliga för tilldelning. Det här värdet beräknas som totalt antal enheter – förbrukade enheter. |
| activeUnits      | heltal                                                        | Antalet enheter som är aktiva för tilldelning.                                                        |
| consumedUnits    | heltal                                                        | Antalet förbrukade enheter.                                                                     |
| suspendedUnits   | heltal                                                        | Antalet pausade enheter.                                                                    |
| totalUnits       | heltal                                                        | Det totala antalet enheter. Det här värdet beräknas som summan av de aktiva enheterna och varningsenheterna.         |
| warningUnits     | heltal                                                        | Antalet varningsenheter.                                                                      |
| productSku       | ProductSku                                                     | Produkt-SKU:n.                                                                                  |
| servicePlans     | matris med ServicePlan-resurser                                 | Insamling av tjänstplaner för en produkt.                                                     |
| capabilityStatus | sträng                                                         | SKU-status för en produkt.                                                                      |
| Attribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar resursen.                                            |
