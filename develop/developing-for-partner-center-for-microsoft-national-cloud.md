---
title: Utveckla för PartnerCenter för Microsoft National Clouds
description: Partnercenter-SDK skillnader när du utvecklar för Partner Center för Microsoft National Clouds.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d38a35fb88b4835716e429aeed731a0d55d9a669
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906450"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Utveckla för PartnerCenter för Microsoft National Clouds

**Gäller för:** PartnerCenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Partnercenter har en uppsättning SDK-dokumentation. Vissa funktioner kanske dock inte är tillgängliga i versionerna av Partner Center for Microsoft National Clouds.

Utvecklare måste överväga ändringar i SDK för följande versioner av Partnercenter:

- [Partnercenter drivs av 21Vianet](#partner-center-operated-by-21vianet)
- [Partnercenter för Microsoft Cloud Tyskland](#partner-center-for-microsoft-cloud-germany)
- [Välkommen till Partnercenter för Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

Varje Partnercenter-SDK listar tillämpliga Partner Center-versioner. Varje hanterad referensartikel innehåller också en lista över tillämpliga Partner Center-versioner i **avsnittet** Krav.

## <a name="partner-center-operated-by-21vianet"></a>Partnercenter drivs av 21Vianet

Skillnaderna för partner mellan *Partner Center och* *Partnercenter som drivs av 21Vianet* är:

- Du kan inte programmässigt återställa ett lösenord för en kundanvändare eller en fullständig partneranvändare.

- Prenumerationer på Azure är inte tillgängliga.

- Du kan inte hantera licenserna för kundens användare. I stället måste kunderna använda administrationscentret Office 365 för att hantera sina licenser.

- Alla supportbegäranden hanteras via Partnercenter som drivs av 21Vianet. Tjänstbegäranden och tjänstuppdateringar gäller inte.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Partnercenter för Microsoft Cloud Tyskland

> [!IMPORTANT]
> Baserat på kundutvecklingen kommer vår molnstrategi för Tyskland att fokusera på leverans av de nya molnregionerna i Tyskland som är konsekventa med vårt globala molnerbjudande. Med det här fokuset kommer vi inte längre att ta emot nya kunder eller distribuera nya tjänster från det aktuella tillgängliga Microsoft Cloud Tyskland. Befintliga kunder kan fortsätta att använda de aktuella molntjänsterna som är tillgängliga idag, vilket vi kommer att underhålla med nödvändiga säkerhetsuppdateringar.
>
> Framöver har nya kunder möjlighet att använda de europeiska regioner som för närvarande är tillgängliga eller de nya regionerna i Tyskland när de blir tillgängliga. Mer information finns i [Microsoft för att leverera molntjänster från nya datacenter i Tyskland.](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/)

Skillnaderna för partner mellan *Partner Center och* Partner Center för Microsoft Cloud *Tyskland* är:

- Partner kan inte skapa användare för kundens organisation eller tilldela roller.
  - Partner kan läsa fält, men kan inte skriva eller uppdatera dem.
  - Partner måste manuellt skapa eller uppdatera sina kunders användare i Office 365 administrationscenter eller via Azure Portal. Se [Azure Active Directory dokumentation.](/azure/active-directory/)

- Du kan inte hantera licenser för dina kundanvändare med hjälp av Partnercenter för Microsoft Cloud Tyskland-portalen eller API:er. I stället måste du använda administrationscentret Office 365 Azure Active Group license management (kommer snart) för att hantera sina licenser.
  - (Valfritt) Du kan använda Azure AD Graph API. Se [Tilldela licenser till en användare.](/graph/api/user-assignlicense) För Partner Center för Microsoft Cloud Tyskland måste du använda slutpunkten Graph stället `https://graph.cloudapi.de` för `https://graph.windows.net` .

- Du kan inte programmässigt återställa ett lösenord för en kundanvändare eller en fullständig partneranvändare. Använd Office 365 administrationscenter eller Azure Portal. Se [Återställa lösenordet för en användare i Azure Active Directory](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). För steg 1 måste du logga in på Azure Portal Microsoft Cloud Tyskland.

- Utvecklare måste registrera sina app-ID manuellt för att integrera Partner Center API/SDK-funktioner i sin app för Partner Center för Microsoft Cloud Tyskland. Mer information finns i [Registrera appinformation för Partner Center for Microsoft National Cloud.](create-apps-for-partner-center-for-microsoft-national-clouds.md)

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Välkommen till Partnercenter för Microsoft Cloud for US Government

Skillnaderna för partner mellan *Partnercenter och* *Partnercenter för Microsoft Cloud for US Government* är:

- Office 365 prenumerationer är för närvarande inte tillgängliga för Partnercenter för Microsoft Cloud for US Government.

- Befintliga partner som stöder Microsoft Cloud for US Government måste skapa nya konton i Partnercenter för Microsoft Cloud for US Government.

- Microsoft Cloud for US Government kunder måste göra en kontakt med en enda partner.
  - Relationen mellan flera kanaler och flera partner och begärande med en befintlig kund Microsoft Cloud for US Government om scenarierna inte gäller. Den här begränsningen beror Office 365 inte är tillgänglig för närvarande.

- Partner kan inte skapa användare för kundens organisation eller tilldela roller.
  - Partner kan läsa fält, men kan inte skriva eller uppdatera dem. Partner måste manuellt skapa eller uppdatera sina kunders användare i Azure Portal. Se [Azure Active Directory dokumentation.](/azure/active-directory/)

- Du kan inte programmässigt återställa ett lösenord för en kundanvändare eller en fullständig partneranvändare. Använd Azure-portalen. Se [Återställa lösenordet för en användare i Azure Active Directory](/azure/active-directory/active-directory-users-reset-password-azure-portal). För steg 1 måste du logga in på Azure Portal för Microsoft Cloud for US Government.

- REST-slutpunkter för Partnercenter för Microsoft Cloud for US Government är samma som för Partnercenter: `https://api.partnercenter.microsoft.com` .

- Utvecklare måste registrera sina app-ID manuellt för att integrera Partner Center API/SDK-funktioner i sin app för Partnercenter för Microsoft Cloud for US Government. Mer information finns i [Registrera appinformation för Partner Center for Microsoft National Cloud.](create-apps-for-partner-center-for-microsoft-national-clouds.md)
