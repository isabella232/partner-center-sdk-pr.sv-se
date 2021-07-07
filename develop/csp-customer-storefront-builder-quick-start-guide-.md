---
title: Snabbstartsguide för butiksbyggare för CSP-kunder
description: Skapa en marknadsplats online för att sälja erbjudanden för molnlösningsleverantörer (CSP) med hjälp av CSP Customer Storefront Builder.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8550492c7a4201a955c7b051b453103628612f3e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973357"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>Snabbstartsguide för butiksbyggare för CSP-kunder

Skapa en marknadsplats online för att sälja erbjudanden för molnlösningsleverantörer (CSP) med hjälp av CSP Customer Storefront Builder.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Introduktion till CSP Customer Storefront Builder

CSP Customer Storefront Builder hjälper partner att enkelt skapa en onlinemarknadsplats för att sälja CSP-erbjudanden till sina kunder. De flesta partner och små säljorganisationer vill fokusera på att sälja i stället för att utveckla en marknadsplats online. Exempelappen Partnercenter-SDK kräver kunskaper i programvaruutveckling för att skapa och distribuera en webbplats. Med CSP Customer Storefront Builder kan du snabbt och enkelt skapa din egen webbplats. Du kan också ladda ned webbplatsen som exempelkod eller distribuera direkt till din Azure-prenumeration med en Ready to Transact-webbplats.

Den här webbplatsen är helt ägd, stöds och underhålls av partner och Microsoft samlar inte in några data eller telemetri från webbplatsen. CSP Customer Storefront Builder skapar en webbplats för partnern som är helt kompatibel med [Payment Card Industry Data Security Standard](https://www.pcisecuritystandards.org/) (PCI DSS).

CSP Customer Storefront Builder-koden är föremål för den licens som är tillgänglig [i Partnercenter-SDK EULA](/legal/partner-center/eula-partner-center-sdk).

>[!NOTE]
>Du ansvarar för butikswebbplatshantering, underhåll och eventuella problem som kan uppstå när webbplatsen skapas. Läs och förstå termerna i [Partnercenter-SDK EULA](/legal/partner-center/eula-partner-center-sdk).

Mer information finns också i följande artiklar: [CSP customer web storefront and](csp-customer-web-storefront.md) [console test app](console-test-app.md).

## <a name="considerations"></a>Överväganden

CSP Customer Storefront Builder är avsett som ett snabbt sätt att skapa en webbplats. Tänk på följande när du planerar:

- När de har distribuerats behåller Microsoft och Partner Center inte en kopia av partnerwebbplatsen eller någon information som läggs till i CSP Customer Storefront Builder.

- Partnercenter kan bara distribuera en CSP Customer Storefront-webbplats till en partners Azure-prenumerationer.

- Den här webbplatsen, när den har distribuerats, är helt ägd och hanteras av partnern. Microsoft har inte åtkomst till den här webbplatsen eller data som är relaterade till webbplatsen. Partner ansvarar för underhåll och hantering av webbplatsen. Microsoft tillhandahåller inte någon live-webbplats eller annan support som rör CSP Customer Storefront Builder eller någon webbplats som skapats med hjälp av CSP Customer Storefront Builder.

- PartnerCenter kan inte direkt komma åt eller uppgradera den här webbplatsen med nya eller ändrade SDK- eller API-funktioner. Alla nya funktioner eller förbättringar måste ägas, utvecklas och hanteras av partner, inklusive att lägga till nya Partnercenter-SDK api-funktioner.

- Detta CSP Customer Storefront Builder ger för närvarande möjlighet att konfigurera betalning till ett PayPal Pro-/PayU Money-konto (för Indien). Om partner behöver ändra betalningsprocessorn måste de ändra koden för att stödja den betalningsmetod som de föredrar.

- Betalningsrelaterad information som läggs till i CSP Customer Storefront Builder lagras eller underhålls inte i Partnercenter.

- PayPal betalningskonfigurationen fungerar i alla geografiska områden där PayPal är tillgänglig. PayPal tillgänglighet och support styrs endast av PayPal och kan när som helst avbrytas av PayPal.

- Betalningskonfigurationen för PayU fungerar för närvarande endast i Indien. PayU:s tillgänglighet och support styrs endast av PayU och kan när som helst upphöra av PayU.

- Läs och förstå termerna i [Partnercenter-SDK EULA](/legal/partner-center/eula-partner-center-sdk).

## <a name="using-the-csp-customer-storefront-builder"></a>Använda CSP Customer Storefront Builder

CSP-partneradministratörer på Partnercenter kan distribuera en CSP Customer Storefront direkt från Partnercenter. Med minimal ansträngning kan en ny webbplats distribueras på partnerns klientorganisation. När de har distribuerats kan partner använda webbplatsen för att konfigurera varumärke, erbjudanden och betalningsrelaterad information och sedan dela webbadressen med kunder.

Processen för att skapa en butikswebbplats är att:

1. [Distribuera webbplatsen](#deploy)

2. [Konfigurera butiken](#configure)

3. [Transact i butiken](#transact)

### <a name="deploy"></a>Distribuera

Distributionsalternativ:

- Ladda ned [exempelkoden för Partnercenter-butiken](https://github.com/Microsoft/Partner-Center-Storefront) från GitHub
- Integrera med Azure för att distribuera den konfigurerade webbplatsen
- Distribuera på en befintlig prenumeration eller ta med din egen prenumeration

### <a name="configure"></a>Konfigurera

Inga utvecklingskunskaper krävs för att anpassa en butik.

Logga in med dina administratörsautentiseringsuppgifter för Partnercenter för att konfigurera:

- **Profilering:** företagsnamn, logotyp, kontakter med mera.

- **Erbjudanden:** Visa alla CSP-erbjudanden. Du kan välja vilka erbjudanden som dina kunder kan visa och köpa. Du kan också anpassa erbjudandeinformation och lägga till ditt pris.

- **PayPal: Lägg** till din PayPal information om ditt betalningskonto. Om du inte har ett PayPal konto kan du gå till [https://www.paypal.com](https://www.paypal.com) och skapa ett nytt konto. Det här kontot används för att PayPal kreditera de betalningar som görs av kunder. *Microsoft ansvarar inte för relationen mellan partner och PayPal. Användning av PayPal kan kräva att partnern eller partnerns kunder godkänner ytterligare villkor.*

- (*För Indien*) **Betalningskonfiguration för PayU:** Lägg till information om ditt PayU Money-betalningskonto. Om du inte har något PayU Money-konto kan du gå till [https://www.payumoney.com/](https://www.payumoney.com/) och skapa ett nytt konto. Det här kontot används för PayU för att kreditera de betalningar som görs av kunder. *Microsoft ansvarar inte för relationen mellan partner och PayU. Användning av PayU kan kräva att partnerns eller partnerns kunder godkänner ytterligare villkor.*

### <a name="transact"></a>Transaktion

- Efter distributionen kan kunder köpa och handla direkt.

- Kunder kan köpa direkt från partnerportalen som är integrerad med Partnercenter-SDK.

#### <a name="customer-countries"></a>Kund länder

Kunder kan tillhöra dessa länder:

| Landskod | Landsnamn   |
|--------------|----------------|
| AU           | Australien      |
| AT           | Österrike        |
| BE           | Belgien        |
| BG           | Bulgarien       |
| CA           | Kanada         |
| HR           | Kroatien        |
| CY           | Cypern         |
| CZ           | Tjeckien |
| DK           | Danmark        |
| EE           | Estland        |
| FI           | Finland        |
| FR           | Frankrike         |
| DE           | Tyskland        |
| GR           | Grekland         |
| HU           | Ungern        |
| IS           | Island        |
| IN           | Indien          |
| IE           | Irland        |
| IT           | Italien          |
| JP           | Japan          |
| LV           | Lettland         |
| LI           | Liechtenstein  |
| LT           | Litauen      |
| LU           | Luxemburg     |
| MT           | Malta          |
| MC           | Monaco         |
| NL           | Nederländerna    |
| NZ           | Nya Zeeland    |
| NO           | Norge         |
| Po           | Polen         |
| PT           | Portugal       |
| RO           | Rumänien        |
| SK           | Slovakien       |
| SL           | Slovenien       |
| ES           | Spanien          |
| SE           | Sverige         |
| CH           | Schweiz    |
| GB           | Storbritannien |
| USA           | USA  |

## <a name="partner-experience-scenarios"></a>Partnerupplevelsescenarier

### <a name="deployment-scenario"></a>Distributionsscenario

Så här distribuerar du en förbättrad eller anpassad CSP Customer Storefront:

- Ladda ned [exempelkoden i Partnercenter-butiken](https://github.com/Microsoft/Partner-Center-Storefront) för att göra ytterligare anpassningar.

- Använd Microsoft Visual Studio 2015 (eller senare) för att utveckla.

- Skapa för ytterligare ändringar och förbättringar (inklusive auktoriseringar, certifieringar, manifeständringar och andra objekt).

### <a name="configuration-scenario"></a>Konfigurationsscenario

- Den nyligen skapade webbplatsen är länkad till en partnerklientorganisation och har åtkomst till alla administratörskonton för den här partnerklientorganisationen.

  - Partner kan logga in på den nya webbplatsen med sina administratörsautentiseringsuppgifter för Partnercenter.

- Butiksprogrammet stöder för närvarande franska, spanska, nederländska, tyska, japanska och engelska. (Engelska fungerar som reservspråk.)

  - Butiken konfigurerar språkinställningarna med hjälp av partnerns standardspråk från partnerns profil i Partnercenter. Detta språk används för att konfigurera valutor, datumformat och lokaliserade erbjudanden på lagringsplatsen.

- Partner kan konfigurera varumärke, erbjudanden och PayPal betalningsinformation för PayU (för Indien).

- Partner kan uppdatera företagets namn, företagslogotyp, rubrikbild, sälj- och supportkontakter med mera.

- Partner kan se alla CSP-erbjudanden som är tillgängliga baserat på deras område.

  - Partner kan välja vilka erbjudanden de vill visa för alla sina kunder.

  - En CSP-partner kan välja ett eller flera erbjudanden och uppdatera namn, kvantitet, funktionsbeskrivning och pris.
  - Priset är det årliga priset. Kunder prenumererar varje år.

- Partner kan när som helst konfigurera förhandsgodkända transaktioner för (a) alla aktuella och framtida kunder ELLER (b) specifika kunder.

  - Förhandsgodkända kunder behöver inte betala på portalen när de lägger till nya prenumerationer, köper ytterligare licenser till befintliga prenumerationer eller förnyar en prenumeration.

  - Förhandsgodkända kunder omdirigeras inte till PayPal payU (för Indien) för betalning under dessa transaktioner.

  - Med förhandsgodkända kundtransaktioner kan en partner utföra offlinefakturering och fakturering till sina förhandsgodkända kunder.

- En CSP-partner kan ange PayPal kontoinformation, till exempel PayPal klient-ID och hemlighet. En CSP-partner kan också välja om de vill testa med en sandbox-miljö eller ett live-konto.

  - Partner hittar den här informationen i [https://developer.paypal.com/](https://developer.paypal.com/) mina appar och & **autentiseringsuppgifter.** Du kan också hämta den här informationen från en aktuell app eller genom att skapa en ny app i PayPal.
  - Skapa ett PayPal konto om du inte redan har ett. Det här kontot används för att PayPal kreditera betalningar som görs av kunder.

    - Information om hur du PayPal ett företagskonto finns i [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - Information om hur du skapar PayPal sandbox-konto finns i [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (För Indien) kan en CSP-partner ange kontoinformation för PayU Money, till exempel PayU-klient-ID och lösenord. Partner kan hitta mer information om [https://developer.payumoney.com/](https://developer.payumoney.com/) .

  - Skapa ett nytt PayU Money-konto om du inte redan har ett. Om du vill öppna ett PayU Money-konto går du till [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . Det här kontot används för PayU för att kreditera betalningar som görs av kunder.

## <a name="customer-experience-scenarios"></a>Kundupplevelsescenarier

### <a name="new-customer-sign-up-scenario"></a>Scenario för ny kunds registrering

- Som standard är webbplatsen offentligt tillgänglig och visar partnerkatalogen på startsidan.

- Kunder kan nu tillhöra ett stort antal [kund länder](#customer-countries).

- Fokus har varit på regionerna European Free Trade Association (EFTA), Nordamerika, Japan, Indien, Australien och Nya Zeeland.
  - Den här funktionen använder det regionala auktoriseringsstödet i Partnercenter-SDK.

- Kunder kan välja ett erbjudande från katalogen att köpa.
  - De kan lägga till kundnamn, adress och domänrelaterad information.

- Kunderna dirigeras till utcheckningsupplevelsen PayPal PayU (för Indien). Kunder kan betala med hjälp av antingen:
  - Deras befintliga PayPal eller PayU-konto (för Indien)
  - Bidragsinstrument som stöds i deras land av PayPal PayU (för Indien). Dessa kan omfatta kreditkort, debetkort och bankkonton efter vad som är tillämpligt.

- En kundklient skapas för den här kunden. När klientbeställningen har skapats får kunderna kontoinformation om användarnamn, lösenord och prenumeration.
  - Kunder kan spara användarnamnet och lösenordet för att vara inloggade för ytterligare köp.
  - Varje prenumeration köps för ett år och kunder kan förnya inom 30 dagar före prenumerationens slutdatum.

### <a name="view-prior-purchases-scenario"></a>Visa tidigare köpscenario

- Kunden loggar in med kundens klientorganisations användarnamn och lösenord och går till **avsnittet Mina** beställningar.

- Kunder kan navigera till sidan **Mina beställningar** där de kan visa köpta prenumerationer och göra uppdateringar om det behövs.

- Kunder kan navigera till **sidan Mina** prenumerationer där de kan visa alla prenumerationer (licensbaserade och användningsbaserade), inklusive de som finns i Partnercenter.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Lägga till licenser i ett befintligt prenumerationsscenario

- I avsnittet **Mina beställningar** kan kunder lägga till fler licenser till befintliga prenumerationer. Kunder kan lägga till fler licenser när som helst under ett prenumerationsår.

- Varje tillagd licens ändrar inte slutdatumet för prenumerationen. Priset för prenumerationen ändras dock baserat på det datum då du lägger till licensen och var datumet är under året. Prissättningen prorreras dagligen till att endast debiteras för de återstående dagarna på året.

### <a name="add-more-subscriptions-scenario"></a>Lägg till fler prenumerationsscenario

- Kunder kan när som helst köpa val av antal prenumerationer i avsnittet **Lägg till** prenumerationer under **Mina beställningar.**

- En kund kan välja en prenumeration, lägga till en kvantitet och betala för att slutföra transaktionen och börja använda prenumerationen direkt. Om en kund är en förhandsgodkänd kund är prenumerationen tillgänglig för användning omedelbart och en faktura skickas till kunden för betalning.

### <a name="renew-subscription-scenario"></a>Förnya prenumerationsscenario

- En kund kan förnya en prenumeration under de senaste 30 dagarna före prenumerationens slutdatum.

- Detta är endast tillgängligt under de senaste 30 dagarna.

- Om prenumerationen inte förnyats under de senaste 30 dagarna tas den bort från listan över prenumerationer för den här kundklientorganisationen.

- Du kan inte uppdatera kvantiteten under förnyelsen.

### <a name="payments-scenario"></a>Betalningsscenario

- Om kunden har förhandsgodkänd för transaktioner av administratören visas inte betalningsupplevelsen för ovanstående scenarier. Partnern kan i stället skicka fakturan för betalning till den förhandsgodkända kunden.

- För alla nya köp kan du lägga till fler licenser, lägga till prenumerationer och förnya. En kund kan betala en partner med hjälp av den här webbplatsen via PayPal eller PayU (för Indien).

- Den här webbplatsen är integrerad med PayPal eller PayU (för Indien) och gör att partner kan acceptera betalningar från sina kunder. PayPal eller PayU (för Indien) krediterar det här beloppet på en partners konto. PayPal eller PayU -kontohantering (för Indien) utanför den här webbplatsen och hanteras på PayPal.com eller PayUmoney.com respektive.

- Detta är beroende av att partner konfigurerar sin PayPal ellerbetalningskonfiguration (för Indien) på PayPal.com eller PayUmoney.com. Microsoft sparar inte den här informationen eller faktiska betalningstransaktioner som är resultatet av användningen av det här alternativet.

### <a name="prorated-pricing-scenario"></a>Scenario med prisprorerat pris

- Den här webbplatsen har stöd för prorated prissättning i fall när kunder lägger till fler licenser i en befintlig prenumeration.

- Varje prenumeration går ut efter ett år och kan inte ändras efter att prenumerationen har köpts.

- Slutdatumet för prenumerationen ändras inte genom att ytterligare licenser läggs till. Kunder debiteras för återstående antal dagar fram till slutdatumet. Om prenumerationskostnaden till exempel är 365 USD på dag ett och du lägger till en licens till dag två blir priset för den nya licensen 364 USD. Om du lägger till ytterligare en licens 10 dagar senare blir priset 354 USD.
