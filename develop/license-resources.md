---
title: Licens resurser
description: Beskriver resurser som är relaterade till licenser.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 681f53ec73122a4861e6f1a2f96560336481a068
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769486"
---
# <a name="license-resources"></a>Licens resurser

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Beskriver resurser som är relaterade till licenser.

## <a name="license"></a>Licens

Beskriver en användar licens.

>[!NOTE]
>Stöds inte på Partner Center som drivs av 21Vianet.

| Egenskap     | Typ                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | matris med ServicePlan-resurser                                 | Samlingen av tjänste planer som motsvarar licensen |
| productSKU   | ProductSku                                                     | SKU för den produkt som motsvarar licensen.        |
| dokumentattribut   | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar licensen.          |

## <a name="licenseupdate"></a>LicenseUpdate

Innehåller information som används för att tilldela eller ta bort licenser från en användare.

| Egenskap         | Typ                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | objekt mat ris                                               | Matris med [LicenseAssignment](#licenseassignment) -objekt. |
| licensesToRemove | matris med strängar                                               | Produkt-SKU-identifierare för de licenser som ska tas bort.    |
| licenseWarnings  | objekt mat ris                                               | Matris med [LicenseWarning](#licensewarning) -objekt.       |
| dokumentattribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.                                  |

## <a name="licenseassignment"></a>LicenseAssignment

Innehåller information som krävs för en licens uppdaterings åtgärd.

| Egenskap      | Typ             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | matris med strängar | Service plans-ID: n som ska undantas från tillgängligheten till användaren. |
| skuId         | sträng           | Produkt-SKU-identifieraren för licensen.                                |

## <a name="licensewarning"></a>LicenseWarning

Innehåller varnings information som inträffat under en licens uppdaterings åtgärd.

| Egenskap     | Typ             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| kod         | sträng           | Varnings koden.                                   |
| meddelande      | sträng           | Varnings meddelandet.                                |
| servicePlans | matris med strängar | De tjänst Plans namn som är associerade med varningen. |

## <a name="productsku"></a>ProductSku

Beskriver produkt information.

| Egenskap       | Typ             | Description                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | sträng           | Produkt-ID.                             |
| name           | sträng           | Användarens huvud-ID.                      |
| skuPartNumber  | sträng           | SKU-delens nummer namn för produkten. Till exempel, för Office 365 plan E3, är det här värdet `EnterprisePack` . Den här egenskapen kan användas i stället för ID om ID: t inte är tillgängligt.                |
| targetType     | sträng           | Mål typen för produkten. Den här egenskapen anger om produkten är tillämplig för en `User` eller en `Tenant` .                                                                    |
| licenseGroupId | sträng           | Identifierar via ett grupp-ID den myndighet eller tjänst som hanterar productSku-licensen. Produkter är åtskiljda under licens grupper för bättre hanterbarhet.<br/><br/>                                                                                     `group1` – Alla produkter vars licenser kan hanteras av Azure Active Directory (AAD).<br/><br/>                                            `group2` -Minecraft produkt licenser.                                         |

## <a name="serviceplan"></a>ServicePlan

Identifierar en distributions bara tjänst inom en produkt-SKU. En produkt kan ha många tjänste planer.

| Egenskap         | Typ   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | sträng | Service plan-identifieraren.                                                                                      |
| displayName      | sträng | Det lokaliserade visnings namnet för service planen.                                                                  |
| serviceName      | sträng | Tjänstens namn.                                                                                                 |
| capabilityStatus | sträng | Service planens status för service planen.                                                                      |
| targetType       | sträng | Mål typen för service planen. Den här egenskapen anger om produkten är tillämplig för en "användare" eller "klient". |

## <a name="subscribedsku"></a>SubscribedSku

Beskriver en registrerad produkt som ägs av en klient.

| Egenskap         | Typ                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | heltal                                                        | Antalet enheter som är tillgängliga för tilldelning. Det här värdet beräknas som totalt antal enheter-förbrukade enheter. |
| activeUnits      | heltal                                                        | Antalet enheter som är aktiva för tilldelning.                                                        |
| consumedUnits    | heltal                                                        | Antalet förbrukade enheter.                                                                     |
| suspendedUnits   | heltal                                                        | Antalet inaktiverade enheter.                                                                    |
| totalUnits       | heltal                                                        | Det totala antalet enheter. Det här värdet beräknas som summan av de aktiva och varnings enheterna.         |
| warningUnits     | heltal                                                        | Antalet varnings enheter.                                                                      |
| productSku       | ProductSku                                                     | Produkt-SKU: n.                                                                                  |
| servicePlans     | matris med ServicePlan-resurser                                 | Insamling av Service planer för en produkt.                                                     |
| capabilityStatus | sträng                                                         | SKU-status för en produkt.                                                                      |
| dokumentattribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar resursen.                                            |
