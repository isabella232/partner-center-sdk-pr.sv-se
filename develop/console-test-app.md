---
title: Konsoltestapp
description: Den här konsoltestappen innehåller exempelkod för alla scenarier som stöds av Partner Center-API:erna. Du kan också använda den för testning.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974037"
---
# <a name="console-test-app"></a>Konsoltestapp

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Konsoltestappen finns i C# och Java. Den innehåller exempelkoder för alla scenarier som stöds av Partner Center-API:erna. Du kan också använda den för testning.

## <a name="get-the-code"></a>Hämta koden

Ladda ned exempelkoden för konsoltestappen.

## <a name="net"></a>.NET

[Ladda ned exempelkoden](https://go.microsoft.com/fwlink/p/?LinkId=746682) och ändra den efter behov.

> [!IMPORTANT]
> Innan du skapar programmet uppdaterar du värdena i filen *App.config* för att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering](partner-center-authentication.md). Mer specifikt bör du använda inställningarna för sandbox-integrationskontot under tidig utveckling eller för testning i produktion.

Under **ScenarioInställningar** i *App.config* kan du ange parametrar som skickas automatiskt till de scenarier som du kör.

Om du vill ändra listan över scenarier som körs kommenterar du ut rader **i IPartnerScenario \[ \] mainScenarios** eller i en enskild **metod** för att hämta scenarier som finns *i filen Program.cs.*

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Ladda ned exempelkoden](https://go.microsoft.com/fwlink/p/?LinkId=2026887) och ändra den efter behov.

> [!IMPORTANT]
> Innan du skapar programmet uppdaterar du värdena i filen *SamplesConfigurations.jsför* att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering .](partner-center-authentication.md) Mer specifikt bör du använda inställningarna för sandbox-integrationskontot under tidig utveckling eller för testning i produktion.

Under **ScenarioInställningar i** SamplesConfiguration.js *på* filen kan du ange parametrar som skickas automatiskt till de scenarier som du kör.

Om du vill ändra listan över scenarier som körs kommenterar du ut rader **i IPartnerScenario \[ \] mainScenarios** eller i en enskild **metod** för att hämta scenarier som finns i *filen Program.java.*

## <a name="what-to-change"></a>Vad som ska ändras

Använd följande listor för att avgöra vad som ska ändras eller inte ändras i exempelkoden.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

För **PartnerServiceSettings** ändrar du inte:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Alla dessa inställningar är nödvändiga för att exempel-API-anropen ska fungera korrekt.

### <a name="userauthentication"></a>UserAuthentication

För **UserAuthentication** måste du ändra:

- **ApplicationId** (ditt Azure Active Directory-ID som används för inloggning)
- **UserName** (ditt active directory-användarnamn)
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

- **CustomerDomainSuffix** (domänsuffixet som används när du skapar en ny kund)

Valfria inställningar. Om den lämnas tom måste den här informationen matas in när du kör ett scenario där det behövs):

- **CustomerIdToDelete** (ID:t för kunden som användes för borttagning)
- **DefaultCustomerId** (det kund-ID som ska användas i kundrelaterade scenarier)
- **DefaultInvoiceID (det** faktura-ID som ska användas i fakturascenarier)
- **PartnerMpnId** (partnerns MPN-ID som ska användas i indirekta partnerscenarier)
- **DefaultServiceRequestId (det** tjänstbegärande-ID som ska användas i scenarier med tjänstbegäran)
- **DefaultSupportTopicID** (supportämnes-ID som ska användas i scenarier med tjänstbegäran)
- **DefaultOfferID (det** erbjudande-ID som ska användas i erbjudandescenarier)
- **DefaultOrderID** (order-ID:t som ska användas i ordningsscenarier)
- **DefaultSubscriptionID** (prenumerations-ID:t som ska användas i prenumerationsscenarier)

Valfritt att ändra. Alla dessa inställningar anger hur många poster per sida som ska hämtas vid hämtning av sidindelade innehåll:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
