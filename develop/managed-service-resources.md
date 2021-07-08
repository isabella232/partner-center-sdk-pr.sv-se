---
title: Hanterade tjänstresurser
description: Hanterade tjänster är tjänster som en partner har delegerat administratörsbehörighet till. Partner kan ge stöd för begäranden om filtjänster och för deras hanterade tjänster.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548132"
---
# <a name="managed-service-resources"></a>Hanterade tjänstresurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Hanterade tjänster är tjänster som en partner har delegerat administratörsbehörighet till. Partner kan ge stöd för begäranden om filtjänster och för deras hanterade tjänster.

## <a name="managedservice"></a>ManagedService

Beskriver en hanterad tjänst.

| Egenskap   | Typ                | Beskrivning                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | sträng              | Det hanterade tjänst-ID:t.                                  |
| Name       | sträng              | Namnet på den hanterade tjänsten.                         |
| Gruppnamn  | sträng              | Namnet på den grupp som tjänsten tillhör.      |
| Länkar      | ManagedServiceLinks | Resursen länkar som motsvarar den hanterade tjänsten. |
| Attribut | ResourceAttributes  | Metadataattributen som motsvarar avtalet.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Innehåller länkarna som gör att partnern med delegerade administratörsbehörigheter kan ge stöd för tjänsten.

| Egenskap      | Typ | Beskrivning                 |
|---------------|------|-----------------------------|
| AdminService  | Länk | Administratörstjänstens URI.      |
| ServiceHealth | Länk | Tjänstens hälso-URI.     |
| ServiceTicket | Länk | URI för tjänstbiljett.     |
| Själv          | Länk | Själv-URI.               |
| Nästa          | Länk | Nästa sida med objekt.     |
| Föregående      | Länk | Föregående sida med objekt. |

