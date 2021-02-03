---
title: Snabbstartsguide för butiksbyggare för CSP-kunder
description: Skapa en online-Marketplace för att sälja CSP-erbjudanden (Cloud Solution Provider) med hjälp av CSP Customer butik Builder.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 83ae0c789f95485ec3eb272434e57421a8f93fb6
ms.sourcegitcommit: 970031473b2e8cd3d08c6c097949c057a51df3ef
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505330"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>Snabbstartsguide för butiksbyggare för CSP-kunder

**Gäller för:**

- Partnercenter

Skapa en online-Marketplace för att sälja CSP-erbjudanden (Cloud Solution Provider) med hjälp av CSP Customer butik Builder.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Introduktion till CSP Customer butik Builder

Med CSP Customer butik Builder kan partners enkelt skapa en online-marknadsplats för att sälja CSP-erbjudanden till sina kunder. De flesta partner och små försäljnings organisationer vill fokusera på försäljning i stället för att utveckla en online-marknadsplats. Partner Center SDK-exempelprogrammet kräver program utvecklings kunskaper för att skapa och distribuera en webbplats. Med CSP Customer butik Builder kan du snabbt och enkelt skapa en egen webbplats. Du kan också hämta webbplatsen som exempel kod eller distribuera direkt till din Azure-prenumeration med en klar till en Transact-webbplats.

Den här webbplatsen ägs fullt ut, stöds och underhålls av partner och Microsoft samlar inte in data eller telemetri från webbplatsen. CSP Customer butik Builder skapar en webbplats för partnern som är helt kompatibel med [betalnings kortet bransch data säkerhets standard](https://www.pcisecuritystandards.org/) (PCI DSS).

CSP Customer butik Builder-koden omfattas av licensen som är tillgänglig i [partner Center SDK-licensavtalet](/legal/partner-center/eula-partner-center-sdk).

>[!NOTE]
>Du ansvarar för butik webbplats hantering, underhåll och eventuella problem som kan uppstå när webbplatser skapas. Läs och förstå villkoren i [partner Center SDK-licensavtalet](/legal/partner-center/eula-partner-center-sdk).

Mer information finns även i följande artiklar: [CSP-kund Web butik](csp-customer-web-storefront.md) och [konsolen test app](console-test-app.md).

## <a name="considerations"></a>Överväganden

CSP Customer butik Builder är avsett som ett snabbt sätt att skapa en webbplats. Tänk på följande när du planerar:

- När Microsoft och partner Center har distribuerats underhåller inte Microsoft och partner Center en kopia av partner webbplatsen eller någon information som lagts till i CSP Customer butik Builder.

- Partner Center kan bara distribuera en CSP-kund butik-webbplats till en partners Azure-prenumerationer.

- Den här webbplatsen, när den har distribuerats, ägs helt och hanteras av partnern. Microsoft har inte åtkomst till den här webbplatsen eller data som är relaterade till webbplatsen. Partner är ansvariga för underhåll och hantering av webbplatsen. Microsoft kommer inte att tillhandahålla någon Live-webbplats eller annat stöd som är relaterat till CSP Customer butik Builder eller någon webbplats som skapats med hjälp av CSP-butik Builder.

- Partner Center kan inte komma åt eller uppgradera den här webbplatsen direkt med nya eller ändrade SDK-eller API-funktioner. Nya funktioner eller förbättringar måste ägas, utvecklas och hanteras av partners, inklusive att lägga till nya partner Center-eller API-funktioner.

- Detta CSP Customer butik Builder ger för närvarande möjlighet att konfigurera betalning till ett PayPal Pro/PayU Money-konto (för Indien). Om partners behöver ändra betalnings processorn måste de ändra koden för att stöda betalnings metoden.

- All betalningsrelaterad information som lagts till i CSP Customer butik Builder lagras eller underhålls inte i Partner Center.

- PayPal-betalningskonfiguration kommer att fungera i alla geografiska områden där PayPal är tillgängligt. PayPal-tillgänglighet och support kontrol leras bara av PayPal och kan när som helst tas ur drift av PayPal.

- PayU-betalningskonfiguration fungerar för närvarande endast i Indien. PayU-tillgänglighet och support kontrol leras bara av PayU och kan tas ur drift när som helst av PayU.

- Läs och förstå villkoren i [partner Center SDK-licensavtalet](/legal/partner-center/eula-partner-center-sdk).

## <a name="using-the-csp-customer-storefront-builder"></a>Använda CSP Customer butik Builder

CSP-partner administratörer på Partner Center kan distribuera en CSP-kund butik direkt från Partner Center. Med minimal ansträngning kan en ny webbplats distribueras på partnerns klient organisation. När de har distribuerats kan partner använda webbplatsen för att konfigurera varumärkes-, erbjudanden-och betalningsrelaterad information och sedan dela URL-adressen för webbplatsen till kunderna.

Processen för att skapa en butik webbplats är att:

1. [Distribuera webbplatsen](#deploy)

2. [Konfigurera butik](#configure)

3. [Transact på butik](#transact)

### <a name="deploy"></a>Distribuera

Distributions alternativ:

- Hämta [butik exempel kod för partner Center](https://github.com/Microsoft/Partner-Center-Storefront) från GitHub
- Integrera med Azure för att distribuera den konfigurerade webbplatsen
- Distribuera på en befintlig prenumeration eller ta med din egen prenumeration

### <a name="configure"></a>Konfigurera

Det krävs inga utvecklings kunskaper för att anpassa en butik.

Logga in med dina partner Center admin-autentiseringsuppgifter för att konfigurera:

- **Varumärke**: företags namn, logo typ, kontakter med mera.

- **Erbjudanden**: Visa alla CSP-erbjudanden. Du kan välja vilka erbjudanden dina kunder kan visa och köpa. Du kan också anpassa erbjudande informationen och lägga till ditt pris.

- **PayPal-betalnings konfiguration**: Lägg till din PayPal-betalnings konto information. Om du inte har ett PayPal-konto kan du besöka [https://www.paypal.com](https://www.paypal.com) och skapa ett nytt konto. Det här kontot kommer att användas för PayPal för att kreditera de betalningar som kunderna har gjort. *Microsoft ansvarar inte för förhållandet mellan partner och PayPal. Användningen av PayPal kan kräva att partner eller partner kunder accepterar ytterligare villkor.*

- (*För Indien*) **PayU-betalnings konfiguration**: Lägg till information om betalnings konto för PayU Money. Om du inte har något konto för PayU Money kan du besöka [https://www.payumoney.com/](https://www.payumoney.com/) och skapa ett nytt konto. Det här kontot kommer att användas för PayU för att kreditera de betalningar som kunderna har gjort. *Microsoft ansvarar inte för förhållandet mellan partner och PayU. Användningen av PayU kan kräva att partnern eller partner kunder samtycker till ytterligare villkor.*

### <a name="transact"></a>Transaktion

- Efter distributionen kan kunderna köpa och Transact direkt.

- Kunder kan köpa direkt från partner portalen som är integrerad med partner Center SDK.

#### <a name="customer-countries"></a>Kund länder

Kunder kan tillhöra följande länder:

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
| IO           | Polen         |
| PT           | Portugal       |
| RO           | Rumänien        |
| SK           | Slovakien       |
| SL           | Slovenien       |
| ES           | Spanien          |
| SE           | Sverige         |
| CH           | Schweiz    |
| GB           | Storbritannien |
| USA           | USA  |

## <a name="partner-experience-scenarios"></a>Scenarier för partner upplevelser

### <a name="deployment-scenario"></a>Distributionsscenario

Så här distribuerar du en utökad eller anpassad CSP-kund butik:

- Hämta [partner Center butik exempel kod](https://github.com/Microsoft/Partner-Center-Storefront) för att göra ytterligare anpassningar.

- Använd Microsoft Visual Studio 2015 (eller senare) för att utveckla.

- Utveckla ytterligare ändringar och förbättringar (inklusive auktoriseringar, certifieringar, manifest ändringar och andra objekt).

### <a name="configuration-scenario"></a>Konfigurationsscenario

- Den nyligen skapade webbplatsen är länkad till en partner klient organisation och har åtkomst till alla administratörs konton för den här partnerns klient organisation.

  - Partner kan logga in på den nya webbplatsen med sina autentiseringsuppgifter för partner Center-administratören.

- Butik-programmet stöder för närvarande franska, spanska, nederländska, tyska, japanska och engelska. (Engelska fungerar som reserv språk.)

  - Butik konfigurerar språket genom att använda partnerns standard språk från partnerns profil i Partner Center. Detta språk används för att konfigurera valutor, datum format och lokaliserade erbjudanden i lagrings platsen.

- Partner kan konfigurera anpassning, erbjudanden och PayPal-eller PayU (för Indien) betalnings information.

- Partner kan uppdatera företagets namn, företags logo typ, sidhuvud avbildning, Sälj-och support kontakter med mera.

- Partner kan se alla CSP-erbjudanden som är tillgängliga utifrån deras territorium.

  - Partner kan välja vilka erbjudanden de vill visa för alla sina kunder.

  - En CSP-partner kan välja ett eller flera erbjudanden och uppdatera namn, kvantitet, funktions beskrivning och pris.
  - Priset är det årliga priset. Kunderna prenumererar varje år.

- Partner kan när som helst konfigurera för hands godkända transaktioner för (a) alla aktuella och framtida kunder eller (b) vissa kunder.

  - För hands godkända kunder behöver inte betala på portalen när de lägger till nya prenumerationer, köpa ytterligare licenser till befintliga prenumerationer eller förnya en prenumeration.

  - Kunder som godkänts i förväg omdirigeras inte till PayPal eller PayU (för Indien) för betalning under dessa transaktioner.

  - I förväg godkända kund transaktioner kan en partner utföra faktureringen offline och fakturera till sina för hands godkända kunder.

- En CSP-partner kan mata in sin PayPal-kontoinformation som PayPal-klient-ID och hemlighet. En CSP-partner kan också välja om de vill testa med ett begränsat läge eller ett Live-konto.

  - Partner kan hitta den här informationen om [https://developer.paypal.com/](https://developer.paypal.com/) i **mina appar & autentiseringsuppgifter**. Du kan också hämta den här informationen från en aktuell app eller genom att skapa en ny app i PayPal.
  - Skapa ett nytt PayPal-konto om du inte redan har ett. Det här kontot kommer att användas för PayPal för att kreditera de betalningar som kunderna har gjort.

    - Information om hur du öppnar ett PayPal-företags konto finns i [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - Information om hur du skapar ett PayPal sandbox-konto finns i [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (För Indien) en CSP-partner kan mata in sin PayU Money-konto information, till exempel PayU-klient-ID och lösen ord. Partner kan hitta mer information om [https://developer.payumoney.com/](https://developer.payumoney.com/) .

  - Skapa ett nytt PayU Money-konto om du inte redan har ett. Om du vill öppna ett PayU Money-konto går du till [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . Det här kontot kommer att användas för PayU för att kreditera de betalningar som kunderna har gjort.

## <a name="customer-experience-scenarios"></a>Kund upplevelse scenarier

### <a name="new-customer-sign-up-scenario"></a>Nytt kund registrerings scenario

- Som standard är webbplatsen allmänt tillgänglig och visar partnerns katalog på Start sidan.

- Kunder kan nu tillhöra ett stort antal [kund länder](#customer-countries).

- Den europeiska fri handels sammanslutningen (EFTA)-länderna, Nordamerika, Japan, Indien, Australien och nya Zeeland-regioner har marker ATS.
  - Den här funktionen använder stöd för regional auktorisering i Partner Center SDK.

- Kunder kan välja ett erbjudande från katalogen att köpa.
  - De kan lägga till kund namn, adress och domän relaterad information.

- Kunderna dirigeras till utcheckningen PayPal eller PayU (för Indien). Kunder kan tillhandahålla betalning med hjälp av antingen:
  - Deras befintliga PayPal-eller PayU-konto (för Indien)
  - Finansierings instrument som stöds i sitt land av PayPal eller PayU (för Indien). Dessa kan omfatta kredit kort, betalkort och bank konton i förekommande fall.

- En kund klient organisation skapas för den här kunden. Efter att du har skapat klient organisations ordningen tillhandahåller kunderna kontots användar namn, lösen ord och prenumerations information.
  - Kunder kan spara användar namn och lösen ord för att förbli inloggade för ytterligare köp.
  - Varje prenumeration har köpts för ett år och kunderna kan förnya under 30 dagar innan prenumerationens slutdatum.

### <a name="view-prior-purchases-scenario"></a>Visa tidigare inköps scenario

- Kunden loggar in med kundens användar namn och lösen ord och går till avsnittet **mina beställningar** .

- Kunder kan gå till sidan **mina beställningar** där de kan visa köpta prenumerationer och göra uppdateringar om det behövs.

- Kunder kan gå till sidan **Mina prenumerationer** där de kan se alla prenumerationer (licensbaserade och användnings), inklusive de som finns i Partner Center.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Lägg till licenser i befintliga prenumerations scenario

- Från avsnittet **mina beställningar** kan kunder lägga till fler licenser i befintliga prenumerationer. Kunder kan lägga till fler licenser när som helst under ett prenumerations år.

- Varje tillagd licens ändrar inte slutdatum för prenumerationen. Priset för prenumerationen ändras dock baserat på det datum då du lägger till licensen och där datumet infaller under året. Priserna beräknas per dag för att bara debiteras för de återstående dagarna på året.

### <a name="add-more-subscriptions-scenario"></a>Lägg till fler prenumerations scenario

- Kunder kan köpa valfritt antal prenumerationer när som helst från avsnittet **Lägg till prenumerationer** under **mina beställningar**.

- En kund kan välja en prenumeration, lägga till en kvantitet och betala för att slutföra transaktionen och börja använda prenumerationen direkt. Om en kund är en för hands godkänd kund är prenumerationen tillgänglig för användning omedelbart och en faktura skickas till kunden för betalning.

### <a name="renew-subscription-scenario"></a>Förnya prenumerations scenario

- En kund kan förnya en prenumeration under de senaste 30 dagarna innan prenumerationens slutdatum.

- Detta är endast tillgängligt under de senaste 30 dagarna.

- Om de inte förnyas under de senaste 30 dagarna tas prenumerationen bort från listan över prenumerationer för den här kund klienten.

- Det går inte att uppdatera antalet under förnyelsen.

### <a name="payments-scenario"></a>Betalnings scenario

- Om kunden är för hands godkänd för transaktioner av administratören, visas inte betalnings upplevelsen för ovanstående scenarier. Partnern kan istället skicka fakturan för betalning till den förgodkännde kunden.

- För alla nya inköp kan du lägga till fler licenser, lägga till prenumerationer och förnya. En kund kan betala en partner med hjälp av den här webbplatsen via PayPal eller PayU (för Indien).

- Den här webbplatsen är integrerad med PayPal eller PayU (för Indien) och gör det möjligt för partner att acceptera betalningar från sina kunder. PayPal eller PayU (för Indien) krediterar detta belopp i en partners konto. PayPal eller PayU (för Indien) bank konto hantering är utanför den här webbplatsen och hanteras på PayPal.com respektive PayUmoney.com.

- Detta är beroende av partner som konfigurerar sina PayPal-orPayU (för Indien) betalnings konfiguration på PayPal.com eller PayUmoney.com. Microsoft sparar inte den här informationen eller faktiska betalnings transaktioner som beror på användningen av det här alternativet.

### <a name="prorated-pricing-scenario"></a>Proportionellt pris scenario

- Den här webbplatsen stöder proportionell prissättning i fall när kunder lägger till fler licenser till en befintlig prenumeration.

- Varje prenumeration upphör att gälla efter ett år och kan inte ändras efter att prenumerationen har köpts.

- Prenumerationens slutdatum ändras inte genom att ytterligare licenser läggs till. Kunderna debiteras för det återstående antalet dagar fram till slutdatumet. Om till exempel en prenumerations kostnad på dagen är $365 och du lägger till en licens på dag två, blir priset för den nya licensen $364. Om du lägger till en licens på 10 dagar senare blir priset $354.
