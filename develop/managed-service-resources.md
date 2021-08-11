---
title: Hanterade tjänstresurser
description: Hanterade tjänster är tjänster som en partner har delegerat administratörsbehörighet till. Partner kan ge stöd för begäranden om filtjänster och för deras hanterade tjänster.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066c9f2a0d5ca8d03553508c2b471ca49735406a5a0566bf48b0773385c129f7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994395"
---
# <a name="managed-service-resources"></a>Hanterade tjänstresurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Hanterade tjänster är tjänster som en partner har delegerat administratörsbehörighet till. Partner kan ge stöd för begäranden om filtjänster och för deras hanterade tjänster.

## <a name="managedservice"></a>ManagedService

Beskriver en hanterad tjänst.

| Egenskap   | Typ                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | sträng              | Det hanterade tjänst-ID:t.                                  |
| Name       | sträng              | Namnet på den hanterade tjänsten.                         |
| Gruppnamn  | sträng              | Namnet på den grupp som tjänsten tillhör.      |
| Länkar      | ManagedServiceLinks | Resursen länkar som motsvarar den hanterade tjänsten. |
| Attribut | ResourceAttributes  | Metadataattributen som motsvarar avtalet.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Innehåller länkarna som gör att partnern med delegerade administratörsbehörigheter kan ge stöd för tjänsten.

| Egenskap      | Typ | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Länk | Administratörstjänstens URI.      |
| ServiceHealth | Länk | Tjänstens hälso-URI.     |
| ServiceTicket | Länk | URI för tjänstbiljett.     |
| Själv          | Länk | Själv-URI.               |
| Nästa          | Länk | Nästa sida med objekt.     |
| Föregående      | Länk | Föregående sida med objekt. |

