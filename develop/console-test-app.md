---
title: Konsoltestapp
description: 'Den här konsolens testapp innehåller exempel kod för alla scenarier som stöds av API: er för partner Center. Du kan också använda den för testning.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769180"
---
# <a name="console-test-app"></a>Konsoltestapp

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

-Test-appen finns i C# och Java innehåller exempel koder för alla scenarier som stöds av API: er för partner Center. Du kan också använda den för testning.

## <a name="get-the-code"></a>Hämta koden

Hämta exempel koden för konsolens test app.

## <a name="net"></a>.NET

[Hämta exempel koden](https://go.microsoft.com/fwlink/p/?LinkId=746682) och ändra den efter behov.

> [!IMPORTANT]
> Innan du skapar programmet uppdaterar du värdena i *App.config* -filen så att den återspeglar den Azure AD-autentiseringsinformation som du skapade i [partner Center-autentisering](partner-center-authentication.md). Mer specifikt bör du använda konto inställningarna för integration i begränsat läge vid tidig utveckling eller för testning i produktion.

Under **ScenarioSettings** i *App.config* -filen kan du ange parametrar som ska skickas automatiskt till de scenarier som du kör.

För att ändra listan över scenarier som körs, kommentera ut rader i **IPartnerScenario \[ \] mainScenarios** eller i en enskild metod för att **Hämta scenarier** i *program.cs* -filen.

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Hämta exempel koden](https://go.microsoft.com/fwlink/p/?LinkId=2026887) och ändra den efter behov.

> [!IMPORTANT]
> Innan du skapar programmet uppdaterar du värdena i *SamplesConfigurations.jspå* filen för att avspegla den Azure AD-autentiseringsinformation som du skapade i [partner Center-autentisering](partner-center-authentication.md). Mer specifikt bör du använda konto inställningarna för integration i begränsat läge vid tidig utveckling eller för testning i produktion.

Under **ScenarioSettings** i *SamplesConfiguration.jspå* fil kan du ange parametrar som ska skickas automatiskt till de scenarier som du kör.

För att ändra listan över scenarier som körs, kommentera ut rader i **IPartnerScenario \[ \] mainScenarios** eller i en enskild metod för att **Hämta scenarier** i filen *program. java* .

## <a name="what-to-change"></a>Ändra

Använd följande listor för att avgöra vad som ska ändras eller inte ändras i exempel koden.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

Ändra inte för **PartnerServiceSettings**:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Alla de här inställningarna krävs för att exempel-API-anropen ska fungera korrekt.

### <a name="userauthentication"></a>UserAuthentication

För **UserAuthentication** är du tvungen att ändra:

- **ApplicationId** (ditt Azure Active Directory program-ID används för inloggning)
- **Användar namn** (ditt Active Directory-användarnamn)
- **Lösen ord** (ditt Active Directory-lösenord).

Ändra inte:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

För **AppAuthentication** är du tvungen att ändra:

- **ApplicationId** (ditt Active Directory-program-ID som används för program inloggning)
- **ApplicationSecret** (din Active Directory-programhemlighet som används för program inloggning)
- **Domän** (din Active Directory-domän som programmet finns på)

### <a name="scenariosettings"></a>ScenarioSettings

Ändra inte för **ScenarioSettings**:

- **CustomerDomainSuffix** (domänsuffix som används för att skapa en ny kund)

Valfria inställningar. Om detta lämnas tomt måste den här informationen anges när du kör ett scenario där det behövs):

- **CustomerIdToDelete** (ID för den kund som används för borttagning)
- **DefaultCustomerId** (kund-ID: t som ska användas i kundrelaterade scenarier)
- **DefaultInvoiceID** (faktura-ID som ska användas i faktura scenarier)
- **PartnerMpnId** (partner MPN-ID som ska användas i indirekta partner scenarier)
- **DefaultServiceRequestId** (ID för tjänst förfrågan som ska användas i scenarier med tjänstbegäran)
- **DefaultSupportTopicID** (ID för support avsnittet som ska användas i tjänst begär ande scenarier)
- **DefaultOfferID** (erbjudande-ID som ska användas i erbjudande scenarier)
- **DefaultOrderID** (order-ID som ska användas i ordnings scenarier)
- **DefaultSubscriptionID** (PRENUMERATIONS-ID som ska användas i prenumerations scenarier)

Valfritt att ändra. Alla de här inställningarna anger mängden poster per sida vid hämtning av växlat innehåll:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
