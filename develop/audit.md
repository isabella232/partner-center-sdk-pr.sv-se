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
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a><span data-ttu-id="ed6f5-103">Gransknings åtgärder som är tillgängliga via partner Center API som visar en post för partner Center-aktivitet</span><span class="sxs-lookup"><span data-stu-id="ed6f5-103">Audit operations available via Partner Center API that show a record of Partner Center activity</span></span>

<span data-ttu-id="ed6f5-104">API: er för partner Center tillhandahåller gransknings funktioner så att du kan hämta en post för partner Center-aktivitet.</span><span class="sxs-lookup"><span data-stu-id="ed6f5-104">The Partner Center APIs provide auditing features so you can get a record of Partner Center activity.</span></span>

<span data-ttu-id="ed6f5-105">Du kan hämta gransknings poster för de senaste 30 dagarna från det aktuella datumet eller för ett datum intervall som anges genom att inkludera start datumet och/eller slutdatumet.</span><span class="sxs-lookup"><span data-stu-id="ed6f5-105">You can retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="ed6f5-106">Observera dock att data tillgänglighet för aktivitets loggen för prestanda orsaker är begränsad till föregående 90 dagar.</span><span class="sxs-lookup"><span data-stu-id="ed6f5-106">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="ed6f5-107">Begär Anden med ett start datum som är större än 90 dagar före det aktuella datumet får ett felaktigt undantag för begäran (felkod: 400) och ett lämpligt meddelande.</span><span class="sxs-lookup"><span data-stu-id="ed6f5-107">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="retrieve-audit-records"></a><span data-ttu-id="ed6f5-108">Hämta gransknings poster</span><span class="sxs-lookup"><span data-stu-id="ed6f5-108">Retrieve audit records</span></span>

<span data-ttu-id="ed6f5-109">Få detaljerade historiska gransknings poster för åtgärder som utförs av en partner användare eller ett program:</span><span class="sxs-lookup"><span data-stu-id="ed6f5-109">Get detailed historical audit records of operations performed by a partner user or application:</span></span>

- [<span data-ttu-id="ed6f5-110">Hämta en post för Partnercenter-aktivitet</span><span class="sxs-lookup"><span data-stu-id="ed6f5-110">Get a record of Partner Center activity</span></span>](get-a-record-of-partner-center-activity-by-user.md)
- [<span data-ttu-id="ed6f5-111">Granska resurser</span><span class="sxs-lookup"><span data-stu-id="ed6f5-111">Auditing resources</span></span>](auditing-resources.md)