---
title: Gransknings åtgärder för partner Center-aktivitet
description: Lär dig mer om typen av API-gransknings åtgärder för partner Center som du kan använda för att hämta en post för partner Center-aktivitet.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 019bebe40c43f6ee1c2ac7da381a86ca190702d4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97769993"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>Gransknings åtgärder som är tillgängliga via partner Center API som visar en post för partner Center-aktivitet

API: er för partner Center tillhandahåller gransknings funktioner så att du kan hämta en post för partner Center-aktivitet.

Du kan hämta gransknings poster för de senaste 30 dagarna från det aktuella datumet eller för ett datum intervall som anges genom att inkludera start datumet och/eller slutdatumet. Observera dock att data tillgänglighet för aktivitets loggen för prestanda orsaker är begränsad till föregående 90 dagar. Begär Anden med ett start datum som är större än 90 dagar före det aktuella datumet får ett felaktigt undantag för begäran (felkod: 400) och ett lämpligt meddelande.

## <a name="retrieve-audit-records"></a>Hämta gransknings poster

Få detaljerade historiska gransknings poster för åtgärder som utförs av en partner användare eller ett program:

- [Hämta en post för Partnercenter-aktivitet](get-a-record-of-partner-center-activity-by-user.md)
- [Granska resurser](auditing-resources.md)