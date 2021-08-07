---
title: Konsoltestapp
description: Den här konsoltestappen innehåller exempelkod för alla scenarier som stöds av Partner Center-API:erna. Du kan också använda den för testning.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 53a014608303e432be251de0845857547170a5464a1952bb4fde9ff7beb8ae95
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991964"
---
# <a name="console-test-app"></a>Konsoltestapp

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Konsoltestappen finns i C# och Java. Den innehåller exempelkoder för alla scenarier som stöds av Partner Center-API:erna. Du kan också använda den för testning.

## <a name="get-the-code"></a>Hämta koden

Ladda ned exempelkoden för konsoltestappen.

## <a name="net"></a>.NET

[Ladda ned exempelkoden](https://go.microsoft.com/fwlink/p/?LinkId=746682) och ändra den efter behov.

> [!IMPORTANT]
> Innan du skapar programmet uppdaterar du värdena i filen *App.config* för att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering.](partner-center-authentication.md) Mer specifikt bör du använda inställningarna för sandbox-integreringskontot under tidig utveckling eller för testning i produktion.

Under **ScenarioInställningar** i *App.config* kan du ange parametrar som skickas automatiskt till de scenarier som du kör.

Om du vill ändra listan över scenarier som körs kommenterar du ut rader **i IPartnerScenario \[ \] mainScenarios** eller i en enskild **Metod** för att hämta scenarier som finns i *filen Program.cs.*

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Ladda ned exempelkoden](https://go.microsoft.com/fwlink/p/?LinkId=2026887) och ändra den efter behov.

> [!IMPORTANT]
> Innan du skapar programmet uppdaterar du värdena i filen *SamplesConfigurations.jsför* att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering.](partner-center-authentication.md) Mer specifikt bör du använda inställningarna för sandbox-integreringskontot under tidig utveckling eller för testning i produktion.

Under **ScenarioInställningar i** SamplesConfiguration.js *på* filen kan du ange parametrar som skickas automatiskt till de scenarier som du kör.

Om du vill ändra listan över scenarier som körs kommenterar du ut rader **i IPartnerScenario \[ \] mainScenarios** eller i en enskild Metod för **att** hämta scenarier som finns i *filen Program.java.*

## <a name="what-to-change"></a>Vad som ska ändras

Använd följande listor för att avgöra vad som ska ändras eller inte ändras i exempelkoden.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

För **PartnerServiceSettings** ändrar du inte:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Alla dessa inställningar är nödvändiga för att exempel-API-anrop ska fungera korrekt.

### <a name="userauthentication"></a>UserAuthentication

För **UserAuthentication** måste du ändra:

- **ApplicationId** (ditt Azure Active Directory-ID som används för inloggning)
- **UserName** (ditt Active Directory-användarnamn)
- **Lösenord** (ditt Active Directory-lösenord).

Ändra inte:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

För **AppAuthentication** måste du ändra:

- **ApplicationId** (ditt Active Directory-program-ID som används för programinloggning)
- **ApplicationSecret** (din Active Directory-programhemlighet som används för programinloggning)
- **Domän** (active directory-domänen där programmet finns)

### <a name="scenariosettings"></a>ScenarioInställningar

För **ScenarioSettings** ändrar du inte:

- **CustomerDomainSuffix** (domänsuffixet som används när en ny kund skapas)

Valfria inställningar. Om det lämnas tomt måste den här informationen matas in när du kör ett scenario där det behövs):

- **CustomerIdToDelete** (ID:t för den kund som användes för borttagning)
- **DefaultCustomerId** (det kund-ID som ska användas i kundrelaterade scenarier)
- **DefaultInvoiceID (det** faktura-ID som ska användas i fakturascenarier)
- **PartnerMpnId** (partnerns MPN-ID som ska användas i indirekta partnerscenarier)
- **DefaultServiceRequestId (det** tjänstbegärande-ID som ska användas i scenarier med tjänstbegäran)
- **DefaultSupportTopicID** (supportämnes-ID som ska användas i scenarier med tjänstbegäran)
- **DefaultOfferID (det** erbjudande-ID som ska användas i erbjudandescenarier)
- **DefaultOrderID** (det order-ID som ska användas i ordningsscenarier)
- **DefaultSubscriptionID (det** prenumerations-ID som ska användas i prenumerationsscenarier)

Valfritt att ändra. Alla dessa inställningar anger antalet poster per sida vid hämtning av sidindelade innehåll:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
