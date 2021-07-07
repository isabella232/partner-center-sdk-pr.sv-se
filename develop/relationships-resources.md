---
title: Relationsresurser
description: Beskriver resurser relaterade till relationer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dba1e99a6c97c759e3c61cde1e7565faa2ef4d1
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445739"
---
# <a name="relationships-resources"></a>Relationsresurser

Beskriver resurser relaterade till relationer.

## <a name="partnerrelationship"></a>PartnerRelationship

Representerar en relation mellan två partner.

| Egenskap         | Typ                                                           | Beskrivning                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | sträng                                                         | Partneridentifieraren. Partneridentifieraren anger klientorganisations-ID:t för den partner som finns på mottagarens (från) sida av relationen. |
| location         | sträng                                                         | Platsen för partnern.                                                                                                                   |
| mpnId            | sträng                                                         | Partnerns Microsoft Partner Network (MPN).                                                                                 |
| name             | sträng                                                         | Namnet på partnern.                                                                                                                       |
| relationshipType | sträng                                                         | Typen av relation.                                                                                                                      |
| state            | sträng                                                         | Tillståndet för relationen (till exempel `active` ).                                                                                                 |
| Attribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Anger den URL som en kund kan använda för att upprätta en relation med en partner.

| Egenskap   | Typ                                                           | Beskrivning                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | sträng                                                         | URL:en för relationsbegäran. |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.      |
