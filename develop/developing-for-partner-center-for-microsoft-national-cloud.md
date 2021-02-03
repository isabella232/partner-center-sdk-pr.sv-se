---
title: Utveckla för partner Center för Microsofts nationella moln
description: Skillnader i Partner Center SDK när du utvecklar för partner Center för Microsofts nationella moln.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7882846de0c591b21fe73345f560613f535d1788
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769411"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Utveckla för partner Center för Microsofts nationella moln

**Gäller för:**

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Partner Center har en uppsättning SDK-dokumentation. Vissa funktioner kanske inte är tillgängliga i versionerna av Partner Center för Microsofts nationella moln.

Utvecklare måste överväga ändringar i SDK för följande versioner av Partner Center:

- [Partner Center som drivs av 21Vianet](#partner-center-operated-by-21vianet)
- [Partnercenter för Microsoft Cloud Tyskland](#partner-center-for-microsoft-cloud-germany)
- [Välkommen till Partnercenter för Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

Varje SDK-artikel för partner Center listar tillämpliga Partner Center-versioner. Varje hanterad referens artikel visar också tillämpliga Partner Center-versioner i avsnittet **krav** .

## <a name="partner-center-operated-by-21vianet"></a>Partner Center som drivs av 21Vianet

Skillnaderna mellan *partner Center* och *partner Center som drivs av 21Vianet* är:

- Det går inte att program mässigt återställa ett lösen ord för en kund användare eller fullständig partner användare.

- Prenumerationer på Azure är inte tillgängliga.

- Du kan inte hantera licenserna för kundens användare. Kunderna måste i stället använda administrations centret för Office 365 för att hantera sina licenser.

- Alla support förfrågningar hanteras via partner Center som drivs av 21Vianet. Tjänst begär Anden och tjänst uppdateringar gäller inte.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Partnercenter för Microsoft Cloud Tyskland

> [!IMPORTANT]
> Efter utvecklingen av kundernas behov kommer vår moln strategi för Tyskland att fokuseras på leverans av nya moln regioner i Tyskland som är konsekvent med vårt globala moln erbjudande. I detta fokus kommer vi inte längre att acceptera nya kunder eller att distribuera nya tjänster från den för närvarande tillgängliga Microsoft Cloud Tyskland. Befintliga-kunder kan fortsätta att använda de aktuella moln tjänsterna som finns idag, som vi ska underhålla med nödvändiga säkerhets uppdateringar.
>
> Nya kunder kan fortsätta att använda de för närvarande tillgängliga europeiska regionerna eller de nya regionerna i Tyskland när de blir tillgängliga. Mer information finns i [Microsoft för att leverera moln tjänster från nya data Center i Tyskland](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

Skillnaderna mellan *partner Center* och *partner Center för Microsoft Cloud Tyskland* är:

- Partner kan inte skapa användare för kundens organisation eller tilldela roller.
  - Partner kan läsa fält, men kan inte skriva eller uppdatera dem.
  - Partners måste manuellt skapa eller uppdatera sina kunders användare i administrations centret för Office 365 eller via Azure Portal. Se [Azure Active Directory-dokumentationen](/azure/active-directory/).

- Du kan inte hantera licenser för kundens användare med hjälp av Partner Center för Microsoft Cloud Tyskland-portalen eller-API: er. I stället måste du använda administrations centret för Office 365 eller Azure Active Group License Management direkt (kommer snart) för att hantera sina licenser.
  - (Valfritt) du kan använda Azure AD-Graph API. Se [tilldela licenser till en användare](/graph/api/user-assignlicense). För partner Center för Microsoft Cloud Tyskland, se till att du använder diagrammets slut punkt `https://graph.cloudapi.de` i stället för `https://graph.windows.net` .

- Det går inte att program mässigt återställa ett lösen ord för en kund användare eller fullständig partner användare. Använd administrations centret för Office 365 eller Azure Portal. Se [återställa lösen ordet för en användare i Azure Active Directory](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). I steg 1 måste du logga in på Azure Portal för Microsoft Cloud Tyskland.

- Utvecklare måste registrera sitt app-ID manuellt för att integrera API/SDK-funktioner i appen för partner Center för Microsoft Cloud Tyskland. Mer information finns i [Registrera app-information för partner Center för Microsoft National Cloud](create-apps-for-partner-center-for-microsoft-national-clouds.md).

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Välkommen till Partnercenter för Microsoft Cloud for US Government

Skillnaderna mellan *partner Center* och *partner Center för Microsoft Cloud för amerikanska myndigheter* är:

- Office 365-prenumerationer är för närvarande inte tillgängliga för partner Center för Microsoft Cloud för amerikanska myndigheter.

- Befintliga partners som stöder Microsoft Cloud för amerikanska myndigheter måste skapa nya konton i Partner Center för Microsoft Cloud för amerikanska myndigheter.

- Microsoft Cloud för amerikanska myndighets Kunder måste Transact med en enda partner.
  - Multichannel och multipartner och begäran relation med en befintlig kund inom Microsoft Cloud för amerikanska myndighets scenarier gäller inte. Den här begränsningen beror på att Office 365 inte är tillgängligt för närvarande.

- Partner kan inte skapa användare för kundens organisation eller tilldela roller.
  - Partner kan läsa fält, men kan inte skriva eller uppdatera dem. Partners måste manuellt skapa eller uppdatera sina kunders användare i Azure Portal. Se [Azure Active Directory-dokumentationen](/azure/active-directory/).

- Det går inte att program mässigt återställa ett lösen ord för en kund användare eller fullständig partner användare. Använd Azure Portal. Se [återställa lösen ordet för en användare i Azure Active Directory](/azure/active-directory/active-directory-users-reset-password-azure-portal). I steg 1 måste du logga in på Azure Portal för Microsoft Cloud för amerikanska myndigheter.

- REST-slutpunkter för partner Center för Microsoft Cloud för amerikanska myndigheter är desamma som för partner Center: `https://api.partnercenter.microsoft.com` .

- Utvecklare måste registrera sitt app-ID manuellt för att integrera API/SDK-funktioner i appen för partner Center för Microsoft Cloud för amerikanska myndigheter. Mer information finns i [Registrera app-information för partner Center för Microsoft National Cloud](create-apps-for-partner-center-for-microsoft-national-clouds.md).
