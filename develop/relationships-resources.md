---
title: Relationer resurser
description: Beskriver resurser som är relaterade till relationer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768877"
---
# <a name="relationships-resources"></a>Relationer resurser

**Gäller för**

- Partnercenter

Beskriver resurser som är relaterade till relationer.

## <a name="partnerrelationship"></a>PartnerRelationship

Representerar en relation mellan två partner.

| Egenskap         | Typ                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | sträng                                                         | Partner-ID. Partner-ID: t anger klient-ID för den partner som finns på mottagar sidan i relationen. |
| location         | sträng                                                         | Partnerns plats.                                                                                                                   |
| mpnId            | sträng                                                         | Partnerns Microsoft Partner Network-ID (MPN).                                                                                 |
| name             | sträng                                                         | Namnet på partnern.                                                                                                                       |
| relationshipType | sträng                                                         | Typ av relation.                                                                                                                      |
| state            | sträng                                                         | Status för relationen (till exempel `active` ).                                                                                                 |
| dokumentattribut       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Tillhandahåller URL: en som en kund kan upprätta en relation med en partner till.

| Egenskap   | Typ                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | sträng                                                         | URL för Relations förfrågan. |
| dokumentattribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.      |
