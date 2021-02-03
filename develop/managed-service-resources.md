---
title: Hanterade tjänst resurser
description: Hanterade tjänster är tjänster som en partner har delegerat administratörs privilegier för. Partner kan ge support för och fil tjänst begär Anden för de hanterade tjänsternas räkning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768862"
---
# <a name="managed-service-resources"></a>Hanterade tjänst resurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hanterade tjänster är tjänster som en partner har delegerat administratörs privilegier för. Partner kan ge support för och fil tjänst begär Anden för de hanterade tjänsternas räkning.

## <a name="managedservice"></a>ManagedService

Beskriver en hanterad tjänst.

| Egenskap   | Typ                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | sträng              | ID för hanterad tjänst.                                  |
| Name       | sträng              | Namnet på den hanterade tjänsten.                         |
| Namn  | sträng              | Namnet på den grupp som tjänsten tillhör.      |
| Länkar      | ManagedServiceLinks | Resurs länkarna som motsvarar den hanterade tjänsten. |
| Attribut | ResourceAttributes  | De metadata-attribut som motsvarar avtalet.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Innehåller de länkar som tillåter partnern med delegerade administratörs behörigheter att tillhandahålla stöd för tjänsten.

| Egenskap      | Typ | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Länk | Admin-tjänstens URI.      |
| ServiceHealth | Länk | URI för tjänste hälsa.     |
| ServiceTicket | Länk | URI för tjänst biljett.     |
| Själv          | Länk | Själv URI.               |
| Nästa          | Länk | Nästa sida med objekt.     |
| Föregående      | Länk | Föregående sida med objekt. |

