---
title: Granskningsåtgärder för Partnercenter-aktivitet
description: Lär dig mer om vilken typ av granskningsåtgärder i Partnercenter-API:et som du kan använda för att hämta en post för Partner center-aktivitet.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e8010bde75bee4c4954034d8f61f19b076d96349e4a05807e272ca88efbc2fa
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994276"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>Granskningsåtgärder som är tillgängliga via Partnercenter-API:et som visar en post för PartnerCenter-aktivitet

Partner Center-API:erna tillhandahåller granskningsfunktioner så att du kan få en post med PartnerCenter-aktivitet.

Du kan hämta granskningsposter för de senaste 30 dagarna från det aktuella datumet eller för ett datumintervall som anges genom att inkludera startdatumet och/eller slutdatumet. Observera dock att tillgängligheten för aktivitetsloggdata av prestandaskäl är begränsad till de senaste 90 dagarna. Begäranden med ett startdatum som är större än 90 dagar före det aktuella datumet får ett undantag för felaktig begäran (felkod: 400) och ett lämpligt meddelande.

## <a name="retrieve-audit-records"></a>Hämta granskningsposter

Hämta detaljerade historiska granskningsposter för åtgärder som utförs av en partneranvändare eller ett program:

- [Hämta en post för Partnercenter-aktivitet](get-a-record-of-partner-center-activity-by-user.md)
- [Granskningsresurser](auditing-resources.md)