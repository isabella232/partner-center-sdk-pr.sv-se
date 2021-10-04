---
title: Felkoder för Partner Center REST
description: Beskrivning av felkoder och lyckade svar från Partner Center-API:erna.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a26d8bebb79074df1bc962d061d3fd975e5e8e7f
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/02/2021
ms.locfileid: "129378769"
---
# <a name="partner-center-rest-error-codes"></a>Felkoder för Partner Center REST

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Rest-API:erna i Partnercenter returnerar ett JSON-objekt som innehåller en statuskod. Den här koden anger om din begäran lyckades eller varför den misslyckades.

## <a name="success-responses"></a>Lyckade svar

Statuskoden **2xx** anger att klientens begäran har tagits emot, förståtts och godkänts.

## <a name="http-status-codes"></a>HTTP-statuskoder

Följande **statuskoder för 4xx** **och 5xx** indikerar ett fel:

- 400: Felaktig begäran
- 401: Obehörig
- 403: Förbjudet
- 404: Hittades inte
- 405: Metoden tillåts inte
- 406: Inte acceptabelt
- 408: Tidsgräns för begäran
- 409: Konflikt, felkod
- 412: Förhandsvillkoret misslyckades
- 429: För många begäranden
- 500: Internt serverfel
- 501: Inte implementerat
- 502: Felaktig gateway
- 503: Tjänsten är inte tillgänglig
- 504: Gateway-timeout

## <a name="error-responses"></a>Felsvar

Svar med **statuskoden 4xx** eller **5xx** innehåller ett felmeddelande med information om feltillstånden för den koden.

I följande tabell och kodexempel beskrivs schemat för ett felsvar:

| Namn        | Typ   | Beskrivning                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| kod        | sträng | Returneras alltid. Anger vilken typ av fel som inträffade. Inte null.                                                                                  |
| beskrivning | sträng | Returneras alltid. Beskriver felet i detalj och innehåller felsökningsinformation. Icke-null, icke-tom. Maxlängden är 1 024 tecken. |
| data        | matris  | Returneras endast för vissa feltyper. En lista över felobjekt.                                                                                           |
| källa      | sträng | Returneras alltid. Källan till felet.                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
}
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```

## <a name="error-codes"></a>Felkoder

Följande är felkoder som returneras av API:erna:

| HTTP-status         | HTTP-felkod | Felkod | Beskrivning     |
|---------------------|-----------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OK | 200 | 400072 | Det här objektet är inte tillgängligt. [Läs mer](https://go.microsoft.com/fwlink/p/?linkid=2164140) |
| Inte implementerat      | 501       | 0          | Undantaget har inte definierats       |
| Behörighet saknas        | 401       | 400        | Åtkomst nekad         |
| NotFound      | 404       | 1000       | Hittades inte       |
| Förbjudet     | 403       | 2006       | Partnern är inte giltig för erbjudandet          |
| BadRequest          | 400       | 2012       | Det går inte att konvertera mellan Handels- Azure Active Directory prenumerations-ID:er.          |
| Förbjudet     | 403       | 2030       | Partnern har inte introducerats för försäljning i landet          |
| Förbjudet     | 403       | 2032       | Åtkomst nekad         |
| Förbjudet     | 403       | 2091       | Erbjudandet är inte längre tillgängligt för köp        |
| BadRequest          | 400       | 2100       | API:et för erbjudanden stöder inte objekt med {0} ID: t . Prova att använda API:erna Products och/eller SKU:er      |
| BadRequest          | 400       | 3000       | Ogiltig egenskap      |
| Förbjudet     | 403       | 20002      | {0}Partner-ID:t har ingen handelsrelation med kund-ID:t {1} .          |
| NotFound      | 404       | 20003      | Prenumeration med ID {0} hittades inte.     |
| BadRequest          | 400       | 27007      | Ogiltig kampanjkod         |
| BadRequest          | 400       | 60000      | Migreringen av kundlicensen misslyckades     |
| NotFound      | 404       | 60002      | Användarobjektets ID hittades inte       |
| NotFound      | 404       | 60003      | Klientorganisationen hittades inte      |
| BadRequest          | 400       | 2001       | Prenumerationskvantiteten kan inte ökas eller minskas medan prenumerationen pausas          |
| BadRequest          | 400       | 2002       | Prenumerationskvantiteten är inte inom den lägsta och högsta tillåtna kvantiteten     |
| BadRequest          | 400       | 2006       | Uppdateringar av prenumerationer för erbjudandet {0} är inte tillåtna     |
| BadRequest          | 400       | 2011       | Prenumeration med ID {0} och borttagna statusar kan inte uppdateras.         |
| BadRequest          | 400       | 2054       | Faktureringsperioden för en befintlig prenumeration kan inte uppdateras med åtgärden update-subscription. Använda åtgärden update-Order                |
| BadRequest          | 400       | 2055       | Etag är inte längre giltig     |
| BadRequest          | 400       | 2071       | MPN-ID:t är inte en giltig rådgivare     |
| NotFound      | 404       | 2072       | MPN-ID för indirekt leverantör är inte giltigt som Partner on Record          |
| Förbjudet     | 403       | 2085       | Erbjudandet är inte berättigat till köp               |
| BadRequest          | 400       | 4018       | Det går inte att bearbeta den här ordningen      |
| BadRequest          | 400       | 6000       | Det gick inte att ändra faktureringsperioden eftersom ordern innehåller en eller flera prenumerationer som inte är aktiva         |
| BadRequest          | 400       | 6001       | Det gick inte att ändra faktureringsperioden eftersom en av beställningens erbjudande-ID:er inte stöder faktureringsperioden     |
| Förbjudet     | 403       | 13605      | En partnerbekräftelse på kundens godkännande av Microsoft-kundavtal måste anges eller så måste kunden godkänna Microsoft-kundavtal i Microsoft Admin Center innan du kan slutföra köpet           |
| NotFound      | 404       | 20000      | Order-ID hittades inte          |
| BadRequest          | 400       | 27006      | Användningsgränsen har överskridits för erbjudande-ID      |
| Konflikt      | 409       | 27009      | Det går inte att aktivera en underordnad prenumeration om den överordnade prenumerationen inte är aktiv     |
| BadRequest          | 400       | 600002     | Organisationsregistrerings-ID-värdet stöds inte  <br/><br/>Det här felet uppstår om kundens företag/organisation inte finns i något av följande länder, men de försökte ange organizationRegistrationNumber.  Länder som påverkas:<br/><br/>– Det här (AM) <br/>– Det här (AZ)<br/>– Aadsen (BY)<br/>– Jusend (HU)<br/>– Förniska (KZ)<br/>– Kyrgyzstan (KG)<br/>– Skar (MD)<br/>– Ryssland (RU)<br/>–IstanIstan (TJ)<br/>–Istan (UZ)<br/>– Förnå (UA) |
| BadRequest          | 400       | 600049     | Organisationsregistrerings-ID-information saknas <br/><br/>Det här felet uppstår om kundens företag/organisation finns i något av följande länder och organizationRegistrationNumber inte har angetts. Länder som påverkas:<br/><br/>– Det här (AM) <br/>– Det här (AZ)<br/>– Aadsen (BY)<br/>– Jusend (HU)<br/>– Förniska (KZ)<br/>– Kyrgyzstan (KG)<br/>– Skar (MD)<br/>– Ryssland (RU)<br/>–IstanIstan (TJ)<br/>–Istan (UZ)<br/>– Förnå (UA)       |
| BadRequest          | 400       | 600050     | Organisationsregistrerings-ID-informationen är ogiltig och ska ha formatet \{ 0\} <br/><br/>Det här felet inträffar om organizationRegistrationNumber inte är giltigt för kundens företag. \{0 \} har det förväntade reguljära uttrycksformatet för felet. Exempel: `Organization registration ID information is invalid and should be of the format ^(\\d{7}|\\d{10})$`.          |
| BadRequest          | 400       | 600051     | Kundens telefonnummer saknas <br/><br/>Det här felet uppstår om kundens företag/organisation finns i något av följande länder, men billingProfile.defaultAddress.phoneNumber inte anges. Länder som påverkas:<br/><br/>– Det här (AM) <br/>– Det här (AZ)<br/>– Aadsen (BY)<br/>– Jusend (HU)<br/>– Förniska (KZ)<br/>– Kyrgyzstan (KG)<br/>– Skar (MD)<br/>– Ryssland (RU)<br/>–IstanIstan (TJ)<br/>–Istan (UZ)<br/>– Förnå (UA)       |
| Behörighet saknas        | 401       | 800001     | Partnertoken saknas i begärandekontext             |
| BadRequest          | 400       | 800002     | Ogiltiga begärandeindata       |
| InternalServerError | 500       | 800003     | Oväntat tjänstfel          |
| BadRequest          | 400       | 800004     | Ogiltigt erbjudande-ID      |
| InternalServerError | 500       | 800005     | Det går inte att skapa ordern          |
| NotFound      | 404       | 800007     | Det går inte att hämta etableringsinformation          |
| NotFound      | 404       | 800008     | Det går inte att hämta kundvagns-ID:t        |
| BadRequest          | 400       | 800009     | Fel i kundvagnsobjekt       |
| BadRequest          | 400       | 800010     | Inventering är inte tillgängligt för det här katalogobjektet     |
| BadRequest          | 400       | 800011     | Den här prenumerationen är inte en giltig Azure-prenumeration        |
| BadRequest          | 400       | 800012     | Den här prenumerationen är inte en aktiv prenumeration      |
| BadRequest          | 400       | 800013     | Den här prenumerationen har inte aktiverats för RI-köp     |
| Konflikt      | 409       | 800014     | En väntande justering begärs för den här ordern     |
| NotFound      | 404       | 800015     | MPN-ID hittades inte         |
| BadRequest          | 400       | 800016     | MPN-ID är inte en giltig indirekt återförsäljare              |
| BadRequest          | 400       | 800017     | Kvantiteten är inte tillgänglig för det här katalogobjektet        |
| BadRequest          | 400       | 800018     | Sandbox-gränsen har uppnåtts          |
| Förbjudet     | 403       | 800019     | Icke-sandbox-klienter tillåts inte avbryta inköp förutom programvaruprenumerationer och permanent programvara        |
| Förbjudet     | 403       | 800020     | Katalogobjektet är inte berättigat till köp.       |
| BadRequest          | 400       | 800021     | Den här prenumerationen är inte en giltig prenumeration        |
| BadRequest          | 400       | 800022     | Du kan vara berättigad till den här transaktionen. Kontakta supporten om du behöver hjälp          |
| Förbjudet     | 403       | 800023     | Du är inte berättigad till den här transaktionen eftersom din kreditrad inte når minimitröskelvärdet för det här köpet. Uppdatera din beställning (eller) kontakta supporten för hjälp       |
| BadRequest          | 400       | 800024     | Du är inte berättigad till den här transaktionen            |
| BadRequest          | 400       | 800025     | Du är inte berättigad till den här transaktionen eftersom din kreditrad inte når minimitröskelvärdet för det här köpet. Uppdatera din beställning (eller) kontakta supporten för hjälp       |
| BadRequest          | 400       | 800026     | Du är inte berättigad till den här transaktionen            |
| Förbjudet     | 403       | 800027     | Katalogobjektet är inte berättigat till att lägga till eller ta bort kvantitet      |
| Förbjudet     | 403       | 800028     | Den första köpperioden är inte längre tillgänglig för köp/uppdatering         |
| BadRequest          | 400       | 800029     | Tillägget är inte relaterat till den angivna överordnade prenumerationen         |
| BadRequest          | 400       | 800030     | Den här prenumerationen är inte registrerad     |
| InternalServerError | 500       | 800031     | Inköpssystemet stöds inte     |
| ExpectationFailed   | 417       | 800036     | Förvillkoret misslyckades        |
| NotFound      | 404       | 800037     | Tillgångs-ID hittades inte          |
| NotFound      | 404       | 800038     | Asset FutureBillingInfo hittades inte       |
| Förbjudet     | 403       | 800039     | Statusen för återförsäljarprogrammet är inte aktiv                |
| BadRequest          | 400       | 800040     | Tillgångsstatus kan inte ändras till {0} från {1}       |
| BadRequest          | 400       | 800041     | Det här objektet har redan aktiverats                 |
| BadRequest          | 400       | 800042     | Stöds inte         |
| Förbjudet     | 403       | 800043     | Åtkomst till prisinformation beviljas inte         |
| Konflikt      | 409       | 800060     | Din order pågår. Kontrollera orderhistoriken för de senaste beställningarna på några minuter           |
| BadRequest          | 400       | 800061     | Ordern kan inte avbrytas         |
| BadRequest          | 400       | 800062     | Du är inte berättigad till den här transaktionen            |
| BadRequest          | 400       | 800063     | Den här {0} ordern kan inte avbrytas. Använda PATCH /customers/ {1} /subscriptions/ för \<subscriptionId\> att pausa prenumerationer          |
| Konflikt      | 409       | 800064     | Kundvagnen {0} bearbetas av en annan begäran       |
| BadRequest          | 400       | 800065     | Det går inte att checka ut en redan skickad {0} kundvagn.      |
| Förbjudet     | 403       | 800066     | Det önskade antalet prenumerationer överskred det maximala antalet prenumerationer som tillåts per kund       |
| Förbjudet     | 403       | 800067     | Det önskade antalet platser överskred det maximala antalet tillåtna platser per prenumeration          |
| Förbjudet     | 403       | 800068     | Det önskade antalet prenumerationer överskred det maximala antalet Azure-prenumerationer som tillåts per partner        |
| Förbjudet     | 403       | 800069     | Kontroll av misslyckad orderhantering      |
| BadRequest          | 400       | 800070     | Erbjudandet är inte tillgängligt i det angivna landet      |
| BadRequest          | 400       | 800071     | Radartikelnumret ska vara från 0 till antalet radobjekt        |
| BadRequest          | 400       | 800071     | Radartikelnumret ska vara från 0 till antalet radobjekt        |
| BadRequest          | 400       | 800072     | Det går inte att ändra faktureringscykeln om prenumerationens SyncState inte har slutförts     |
| Förbjudet     | 403       | 800073     | Ditt kundkonto är under granskning. Kom tillbaka om några dagar. Ditt tålamod uppskattas under den här tiden. Läs mer på {0}              |
| Förbjudet     | 403       | 800074     | Ditt kundkonto är under granskning. Kom tillbaka om några dagar. Ditt tålamod uppskattas under den här tiden. Läs mer på {0}              |
| Förbjudet     | 403       | 800075     | är korrekt. Mer information finns i {0Kundkontot godkändes inte. Transaktioner för den här kunden tillåts inte. Verifiera kundkontoinformationen}        |
| NotFound      | 404       | 800076     | Det går inte att hitta prenumerationshistoriken          |
| Förbjudet     | 403       | 800077     | Det går inte att avbryta platsbaserad SaaS via korrigeringsordning. Använd korrigeringsprenumeration i stället.       |
| BadRequest          | 400       | 800078     | Det går inte att skapa överföringen med en ogiltig prenumeration       |
| BadRequest          | 400       | 800080     | Det går inte att ändra faktureringscykeln om prenumerationen inte är associerad med ett Mint-konto        |
| BadRequest          | 400       | 800081     | Det går inte att uppdatera en prenumeration innan den aktiveras          |
| BadRequest          | 400       | 800082     | som ska uppdateras. Försök igen efter att någon gångPrenumeration inte är klar      |
| InternalServerError | 500       | 800083     | Tillgänglighet har fler än ett alternativ för inkluderad kvantitet         |
| InternalServerError | 500       | 800084     | Varaktighet som inte stöds {0}          |
| BadRequest          | 400       | 800085     | Prenumerationens faktureringsperiod matchar inte den ursprungliga beställningsfaktureringsperioden        |
| BadRequest          | 400       | 800086     | Kundens klientorganisation har inte de taggar som krävs för erbjudandet        |
| InternalServerError | 500       | 800087     | Det är problem med radobjektet.                |
| Förbjudet     | 403       | 800088     | Det begärda {0} antalet platser överskred den återstående gränsen för {1} tillåtna platser per prenumeration för CatalogID – {2}       |
| Förbjudet     | 403       | 800089     | Det begärda antalet {0} tillgångar överskred den återstående gränsen för {1} tillåtna tillgångar per kund         |
| BadRequest          | 400       | 800090     | Det går inte att minska prenumerationskvantiteten            |
| BadRequest          | 400       | 800091     | Det går inte att uppdatera en prenumeration med inaktiverad status         |
| BadRequest          | 400       | 800092     | Det går inte att öka antalet platser för en prenumeration som köpts under Software Assurance program         |
| BadRequest          | 400       | 800093     | Prenumerationen är inte berättigad att förnyas automatiskt        |
| InternalServerError | 500       | 800094     | Uppdateringsprenumerationen har inte lyckats                |
| BadRequest          | 400       | 800095     | Det går inte att uppdatera platskvantiteten för den här prenumerationen      |
| BadRequest          | 400       | 800096     | Det går inte att uppdatera statusen för den här prenumerationen       |
| BadRequest          | 400       | 800097     | Det går inte att uppdatera faktureringsperioden för den här prenumerationen      |
| BadRequest          | 400       | 800098     | Det går inte att uppdatera partnerposten för den här prenumerationen        |
| NotFound      | 404       | 800111     | Azure-prenumerationen med det angivna rättighets-ID:t hittades inte.       |
| Förbjudet     | 403       | 800115     | Överage har redan tilldelats till en annan klientorganisation. Kontakta kunden för att lösa ägarskapsfrågor.       |
| Förbjudet     | 403       | 800114     | Du är inte berättigad att hantera över- eller överning för den här kunden.       |
| Förbjudet     | 403       | 800112     | Överlagring kan inte anges eftersom kunden har äldre Azure-prenumerationer.       |
| NotFound      | 404       | 900100     | Överföringsbegäran hittades inte        |
| Konflikt      | 409       | 900101     | Den här överföringen tillåts inte eftersom den {0} ursprungliga överföringen pågår         |
| BadRequest          | 400       | 900102     | Det går inte att bearbeta överföringsbegäran för {1} överföring {0}         |
| InternalServerError | 500       | 900103     | Överföringsordningen lyckades inte        |
| Konflikt      | 409       | 900104     | Överföringen {0} bearbetas av en annan begäran         |
| Förbjudet     | 403       | 900105     | Du har en eller flera Azure-prenumerationer i pausat tillstånd. Dessa kan inte övergå till Azure-planen          |
| NotFound      | 404       | 900106     | Ingen uppgraderingsbegäran hittades      |
| BadRequest          | 400       | 900107     | Det går inte att bearbeta Azure-uppgraderingen eftersom det inte gick att hitta katalogobjektet i Azure          |
| Förbjudet     | 403       | 900108     | Det går inte att bearbeta Azure-uppgraderingen eftersom kunden inte har några Azure-prenumerationer.      |
| Konflikt      | 409       | 900109     | Den här uppgraderingen är inte tillåten eftersom den {0} ursprungliga uppgraderingen pågår     |
| BadRequest          | 400       | 900110     | Det går inte att bearbeta uppgraderingsbegäran för slutförd uppgradering {0}     |
| BadRequest          | 400       | 900111     | Det angivna uppgraderings-ID:t tillhör inte kunden {0} . Kunden mappas till uppgraderings-ID:t {1}     |
| Konflikt      | 409       | 900112     | Det här köpet är inte tillåtet eftersom {0} uppgraderingsbegäran är i väntande tillstånd        |
| Konflikt      | 409       | 900113     | Det här köpet är inte tillåtet eftersom {0} uppgraderingsbegäran pågår       |
| Konflikt      | 409       | 900114     | Det här köpet är inte tillåtet eftersom uppgraderingsbegäran {0} misslyckades         |
| Förbjudet     | 403       | 900115     | Azure-planen kan inte flyttas till pausat tillstånd eftersom du har en eller flera Azure-prenumerationer i aktivt tillstånd        |
| BadRequest          | 400       | 900116     | Det går inte att skapa en order. Det finns en gräns för hur många Azure-planer som kan skapas under sandbox-konton      |
| BadRequest          | 400       | 900117     | Du har passerat {0} annulleringsfönstret för -day. Vi kan inte avbryta köpet               |
| BadRequest          | 400       | 900118     | Ogiltigt kund-ID         |
| Förbjudet     | 403       | 900119     | Det går inte att bearbeta Azure-uppgradering för Azure Partner Shared Services         |
| Förbjudet     | 403       | 900120     | Det går inte att bearbeta Azure-uppgradering      |
| Förbjudet     | 403       | 900121     | Det går inte att bearbeta ordern på grund av otillräcklig kreditgräns, kontakta ucmwrcsp@microsoft.com för ytterligare hjälp        |
| NotFound      | 404       | 900122     | Advisor-citattecken hittades inte     |
| Förbjudet     | 403       | 900123     | Microsoft-partneravtal har inte godkänts av den indirekta återförsäljaren         |
| Förbjudet     | 403       | 900124     | Ditt företag har inte godkänt Microsoft-partneravtal (MPA). Den globala administratören för CSP-kontot måste acceptera MPA för att återuppta de fullständiga transaktionsfunktionerna. Sök {0} efter din globala administratör och be dem signera MPA på instrumentpanelen för att återuppta fullständiga {1} transaktionsfunktioner          |
| BadRequest          | 400       | 900125     | Advisor-partnerinformation hittades inte i begärandekontexten     |
| BadRequest          | 400       | 900126     | Det går inte att parsa upp: {0} Mer information finns i {1}       |
| BadRequest          | 400       | 900127     | Den här åtgärden stöds inte i den här miljön        |
| BadRequest          | 400       | 900128     | En Azure-plan krävs för att köpa en SaaS-prenumeration med en förbrukningsdelade faktureringsplan                 |
| BadRequest          | 400       | 900129     | Det angivna Azure-plan-ID:t hittades inte eller så finns det inga aktiva Azure-prenumerationer under det. En Azure-plan med aktiva prenumerationer krävs för att köpa en SaaS-produkt med en förbrukningsdelade faktureringsplan         |
| Förbjudet     | 403       | 900130     | En eller flera Azure-prenumerationer har nyligen köpts. Dessa prenumerationer kan inte övergå just nu. Försök igen senare               |
| BadRequest          | 400       | 900131     | Den här överföringsbegäran kan inte initieras eftersom kunden har äldre Azure-prenumerationer              |
| BadRequest          | 400       | 900132     | Den här överföringsbegäran kan inte initieras eftersom Azure-planen inte är aktiv. Aktivera Azure-planen     |
| BadRequest          | 400       | 900133     | Den här överföringsbegäran kan inte initieras eftersom kunden inte har köpt Azure-plan       |
| BadRequest          | 400       | 900134     | Den här överföringsbegäran kan inte initieras eftersom Azure-planen inte kan rensas     |
| InternalServerError | 500       | 900135     | Det gick inte att initiera överföringsbegäran. Försök igen senare         |
| BadRequest          | 400       | 900136     | Överföringen kan inte initieras eftersom källpartnerns e-post/domäninformation saknas i begäran            |
| Förbjudet     | 403       | 900137     | Överföringen kan inte skapas som partner: inte {0} aktiverad för den här funktionen      |
| Förbjudet     | 403       | 900138     | Överföringen kan inte skapas som partner: {0} nationella {1} moln stöds inte         |
| Förbjudet     | 403       | 900139     | Överföringsbegäran kan inte godkännas. Be partnern att skapa överföring utan Azure-prenumerationer        |
| NotFound      | 404       | 900140     | Det går inte att Azure Active Directory prenumerationer för en kund med klientorganisations-ID {0} och källetablerings-ID{1}     |
| BadRequest          | 400       | 900141     | Den här åtgärden stöds inte         |
| BadRequest          | 400       | 900142     | Katalogobjektets ID finns inte      |
| BadRequest          | 400       | 900143     | Begäran kunde inte hämta alla tillgängligheter med productId: {0} , skuId: {1} för en kund med ID: {3}     |
| BadRequest          | 400       | 900144     | Etablerings-SKU-ID:t finns inte               |
| BadRequest          | 400       | 900145     | Den här begäran om överföring av faktureringsägarskap kan inte slutföras eftersom Azure-reservationer inte överförs med prenumerationer. Avbryt de Azure-reservationer som är associerade med prenumerationerna i ditt val och försök igen.         |
| BadRequest          | 400       | 900146     | Denna begäran om överföring av faktureringsägarskap kan inte slutföras eftersom marketplace-produkter från tredje part inte överförs med prenumerationer. Ta bort marketplace-produkter från tredje part från ditt val och försök igen.       |
| BadRequest          | 400       | 900147     | Ange en giltig domän som är associerad med den aktuella partnern       |
| BadRequest          | 400       | 900148     | Det gick inte att skapa överföringen på grund av att källpartnerinformationen matchade med den begärande partnern                |
| Förbjudet     | 403       | 900149     | {0} programstatusen är inte aktiv.       |
| Förbjudet     | 403       | 900150     | Den angivna rollen har inte behörighet att utföra den begärda åtgärden      |
| InternalServerError | 500       | 900192     | Något gick fel. Försök igen efter en stund.       |
| BadRequest          | 400       | 900203     | CatalogItemId: {0} kräver godkännande av attestation.        |
| BadRequest          | 400       | 600049     | Organisationsregistrerings-ID-information saknas. Det här felet uppstår om kundens företag/organisation finns i följande länder: Det här felet är Försent(AM), Förlamning(AZ), Förlamad(BY), Arhubb (HU), ALAM (Kyrgyzstan(KG),Ledar(MD), Ryssland (RU), Thernistan(TJ), Hubs (CUS), Uia),Men organizationRegistrationNumber skickas inte in.      |
| BadRequest          | 400       | 600050     | Organisationsregistrerings-ID-informationen är ogiltig och ska ha formatet `{0}` . Det här felet uppstår om organizationRegistrationNumber som skickas är ogiltigt för kundens företag. {0} kommer att ha det förväntade reguljära uttrycksformatet för felet. Exempel: Informationen för organisationsregistrerings-ID är ogiltig och ska ha formatet `^(\\d{7}|\\d{10})$`          |
| BadRequest          | 400       | 600051     | Kundens telefonnummer saknas. Det här felet uppstår om kundens företag/organisation finns i följande länder: Det här felet gäller för kunden: Det här felet är Förskansning(AM), Förlamning(BY), 16666(HU), Kyrgyzstan(KG),Ledar(MD), Ryssland (RU), Debitikistan(TJ), Hubs (UZ) Och BillingProfile.defaultAddress.phoneNumber skickas inte in.       |
| BadRequest          | 400       | 600002     | Värdet för organisationsregistrerings-ID stöds inte. Det här felet uppstår om kundens företag/organisation inte finns i följande länder: Det här felet: Förvekelse(AM), Förlamning(AZ), 12,1( HU), Kyrgyzstan(KG), Hubs(MD), Ryssland (RU), Uiikistan(TJ), Hubs(CUS) Eller Eller (UA), men de försökte ange organizationRegistrationNumber.       |
