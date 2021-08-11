---
title: Utveckla för PartnerCenter för Microsoft National Clouds
description: Partnercenter-SDK skillnader när du utvecklar för Partner Center för Microsoft National Clouds.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8b9b3c3b9a1a1173cf8f3e79f60e629e3d34ea13ecce2e7a2c74924bde2b7d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994871"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Utveckla för PartnerCenter för Microsoft National Clouds

**Gäller för:** PartnerCenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Partnercenter har en uppsättning SDK-dokumentation. Vissa funktioner kanske dock inte är tillgängliga i versionerna av Partner Center for Microsoft National Clouds.

Utvecklare måste överväga ändringar i SDK för följande versioner av PartnerCenter:

- [Partnercenter drivs av 21Vianet](#partner-center-operated-by-21vianet)
- [Partnercenter för Microsoft Cloud Tyskland](#partner-center-for-microsoft-cloud-germany)
- [Välkommen till Partnercenter för Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

Varje Partnercenter-SDK innehåller en lista över tillämpliga Partner Center-versioner. Varje hanterad referensartikel innehåller också en lista över tillämpliga Partner Center-versioner i **avsnittet** Krav.

## <a name="partner-center-operated-by-21vianet"></a>Partnercenter drivs av 21Vianet

Skillnaderna för partner mellan *Partner Center och* *Partnercenter som drivs av 21Vianet* är:

- Du kan inte programmässigt återställa ett lösenord för en kundanvändare eller en fullständig partneranvändare.

- Prenumerationer på Azure är inte tillgängliga.

- Du kan inte hantera licenser för kundens användare. I stället måste dina kunder använda Office 365 administrationscenter för att hantera sina licenser.

- Alla supportbegäranden hanteras via Partnercenter som drivs av 21Vianet. Tjänstbegäranden och tjänstuppdateringar gäller inte.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Partnercenter för Microsoft Cloud Tyskland

> [!IMPORTANT]
> Baserat på utvecklingen av kundernas behov kommer vår molnstrategi för Tyskland att fokusera på leverans av de nya molnregionerna i Tyskland som är konsekventa med vårt globala molnerbjudande. Det innebär att vi inte längre kommer att ta emot nya kunder eller distribuera nya tjänster från Microsoft Cloud Germany, som är tillgängligt för närvarande. Befintliga kunder kan fortsätta att använda de aktuella molntjänsterna som är tillgängliga idag, och vi kommer att underhålla dessa med nödvändiga säkerhetsuppdateringar.
>
> Framöver har nya kunder möjlighet att använda de tillgängliga europeiska regionerna eller de nya regionerna i Tyskland när de blir tillgängliga. Mer information finns i avsnittet om att [Microsoft ska leverera molntjänster från nya datacenter i Tyskland](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

Skillnaderna för partner mellan *Partner Center* och Partner Center for Microsoft *Cloud Tyskland* är:

- Partner kan inte skapa användare för kundens organisation eller tilldela roller.
  - Partner kan läsa fält, men kan inte skriva eller uppdatera dem.
  - Partner måste manuellt skapa eller uppdatera sina kunders användare i Office 365 administrationscenter eller via Azure Portal. Se [Azure Active Directory dokumentation](/azure/active-directory/).

- Du kan inte hantera licenser för dina kunders användare med hjälp av Partnercenter för Microsoft Cloud Tyskland-portalen eller API:er. I stället måste du använda administrationscentret Office 365 Azure Active Group license management (kommer snart) för att hantera deras licenser.
  - (Valfritt) Du kan använda Azure AD Graph API. Se [Tilldela licenser till en användare.](/graph/api/user-assignlicense) För Partner Center för Microsoft Cloud Tyskland måste du använda slutpunkten Graph stället `https://graph.cloudapi.de` för `https://graph.windows.net` .

- Du kan inte programmässigt återställa ett lösenord för en kundanvändare eller en fullständig partneranvändare. Använd Office 365 administrationscenter eller Azure Portal. Se [Återställa lösenordet för en användare i Azure Active Directory](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). För steg 1 måste du logga in på Azure Portal för Microsoft Cloud Tyskland.

- Utvecklare måste registrera sina app-ID manuellt för att integrera Partner Center API/SDK-funktioner i sin app för Partner Center för Microsoft Cloud Tyskland. Mer information finns i [Registrera appinformation för Partner center för Microsoft National Cloud.](create-apps-for-partner-center-for-microsoft-national-clouds.md)

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Välkommen till Partnercenter för Microsoft Cloud for US Government

Skillnaderna för partner mellan *Partner Center* och *Partnercenter för Microsoft Cloud for US Government* är:

- Office 365 prenumerationer är för närvarande inte tillgängliga för Partnercenter för Microsoft Cloud for US Government.

- Befintliga partner som stöder Microsoft Cloud for US Government måste skapa nya konton i Partnercenter för Microsoft Cloud for US Government.

- Microsoft Cloud for US Government kunder måste göra en överträdelse med en enda partner.
  - Multichannel och multipartner och begäranderelation med en befintlig kund Microsoft Cloud for US Government gäller inte. Den här begränsningen beror Office 365 inte är tillgänglig för närvarande.

- Partner kan inte skapa användare för kundens organisation eller tilldela roller.
  - Partner kan läsa fält, men kan inte skriva eller uppdatera dem. Partner måste manuellt skapa eller uppdatera sina kunders användare i Azure Portal. Se [Azure Active Directory dokumentation](/azure/active-directory/).

- Du kan inte programmässigt återställa ett lösenord för en kundanvändare eller en fullständig partneranvändare. Använd Azure-portalen. Se [Återställa lösenordet för en användare i Azure Active Directory](/azure/active-directory/active-directory-users-reset-password-azure-portal). För steg 1 måste du logga in på Azure Portal för Microsoft Cloud for US Government.

- REST-slutpunkter för Partnercenter för Microsoft Cloud for US Government är samma som för PartnerCenter: `https://api.partnercenter.microsoft.com` .

- Utvecklare måste registrera sina app-ID manuellt för att integrera Partner Center API/SDK-funktioner i sin app för Partnercenter för Microsoft Cloud for US Government. Mer information finns i [Registrera appinformation för Partner center för Microsoft National Cloud.](create-apps-for-partner-center-for-microsoft-national-clouds.md)
