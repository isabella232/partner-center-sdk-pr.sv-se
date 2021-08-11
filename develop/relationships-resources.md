---
title: Relationsresurser
description: Beskriver resurser relaterade till relationer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bbbc973679ae80c3ad6b9d67945c6fbcb087789484939b67f8d8a6b538ce7d37
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997098"
---
# <a name="relationships-resources"></a>Relationsresurser

Beskriver resurser relaterade till relationer.

## <a name="partnerrelationship"></a>PartnerRelationship

Representerar en relation mellan två partner.

| Egenskap         | Typ                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | sträng                                                         | Partneridentifieraren. Partneridentifieraren anger klientorganisations-ID för den partner som finns på mottagarsidan (från) i relationen. |
| location         | sträng                                                         | Platsen för partnern.                                                                                                                   |
| mpnId            | sträng                                                         | Partnerns Microsoft Partner Network (MPN).                                                                                 |
| name             | sträng                                                         | Namnet på partnern.                                                                                                                       |
| relationshipType | sträng                                                         | Typ av relation.                                                                                                                      |
| state            | sträng                                                         | Tillståndet för relationen (till exempel `active` ).                                                                                                 |
| Attribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Anger den URL som en kund kan upprätta en relation med en partner.

| Egenskap   | Typ                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | sträng                                                         | URL:en för relationsbegäran. |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.      |
