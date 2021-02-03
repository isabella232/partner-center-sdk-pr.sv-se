---
title: Hämta en nedladdnings länk för Microsofts kund avtals mall
description: Hämta en länk för att hämta en länk till Microsofts kund avtals mall.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8c794d264ad64a42fa6ca823ddfc3841248c01cd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769174"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Hämta en nedladdnings länk för Microsofts kund avtals mall

**Gäller för:**

- Partnercenter

**AgreementDocument** -resursen stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*. Den här resursen gäller inte för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Den här artikeln beskriver hur du hämtar en länk för att ladda ned Microsofts kund avtals mall, baserat på kundens land och språk.

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1,14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md). Det här scenariot stöder endast app + användarautentisering.

- Kundens land som Microsofts kund avtals mall gäller.

- Språket som Microsofts kundavtals mall ska vara lokaliserad till.

> [!IMPORTANT]
>
> - Microsofts kund avtal är landsspecifika. När du begär att en länk för att ladda ned Microsofts kund avtals mall, måste du ange rätt land baserat på kundens plats. eller en lista över länder som stöds finns i [listan över länder och språk som stöds](#list-of-supported-countries-and-languages).
>
> - För vissa länder finns Microsofts kund avtal på flera språk. För bästa kund upplevelse väljer du det språk som bäst matchar kundens behov. En lista över språk som stöds finns i [listan över länder och språk som stöds](#list-of-supported-countries-and-languages).
> - Den här metoden stöds endast med Microsofts kund avtal.

## <a name="net"></a>.NET

Hämta en länk för att hämta Microsofts kund avtals mall:

1. Hämta avtals metadata för Microsofts kund avtal. Du måste skaffa **templateId** till Microsofts kund avtal. Mer information finns i [Hämta avtals-metadata för Microsofts kund avtal](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Använd samlingen IAggregatePartner. AgreementTemplates.

3. Anropa metoden **ById** och ange **templateId** för Microsofts kund avtal.

4. Hämta **dokument** egenskapen.

5. Anropa metoden **ByCountry** och ange kundens land som avtals mal len gäller. Frågan används som standard för *oss* om metoden inte har angetts. En lista över lands koder som stöds finns i [listan över länder och språk som stöds](#list-of-supported-countries-and-languages). Den här metoden är Skift läges **känslig**.

6. Anropa metoden **ByLanguage** och ange språket som avtals mal len ska lokaliseras i. Frågan får en standard till *en-US* om metoden inte har angetts eller om den angivna lands koden inte stöds för det angivna landet. En lista över språk koder som stöds finns i [lista över länder och språk som stöds](#list-of-supported-countries-and-languages).

7. Anropa metoden **Get** eller **GetAsync** .

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Ett fullständigt exempel finns i [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.

## <a name="rest-request"></a>REST-begäran

Hämta en länk för att hämta Microsofts kund avtals mall:

1. Hämta avtals metadata för Microsofts kund avtal. Du måste skaffa **templateId** till Microsofts kund avtal. Mer information finns i [Hämta avtals-metadata för Microsofts kund avtal](get-customer-agreement-metadata.md).

2. Skapa en REST-begäran för att hämta en [ **AgreementDocument** -resurs](./agreement-document-resources.md). Ett exempel finns i exempel på [syntax för begäran](#request-syntax) . Du måste ange följande information:

    - **TemplateId** för Microsofts kund avtal.
    - Landet som Microsofts kund avtals mall gäller för.
    - Språket som Microsofts kundavtals mall ska vara lokaliserad till.

### <a name="request-syntax"></a>Syntax för begäran

Använd följande syntax för begäran för den här resursen:

| Metod | URI för förfrågan |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{Agreement-Template-ID}/Document? språk = {language} &land = {Country} http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Du kan använda följande URI-parametrar med din begäran:

| Namn                   | Typ   | Obligatorisk | Beskrivning                                 |
|------------------------|--------|----------|---------------------------------------------|
| avtal – mall-ID  | sträng | Yes      | Unikt ID för avtals typen. Du kan hämta templateId för Microsofts kund avtal genom att hämta avtals-metadata för Microsofts kund avtal. Mer information finns i [Hämta avtals-metadata för Microsofts kund avtal](./get-customer-agreement-metadata.md). Den här parametern är **SKIFT läges känslig**.|
| land                | sträng | No       | Anger det land som avtals mal len gäller. Frågan får standardvärdet för *oss* om parametern inte anges. En lista över lands koder som stöds finns i [listan över länder och språk som stöds](#list-of-supported-countries-and-languages).|
| language               | sträng | No       | Anger det språk som avtals mal len ska vara lokaliserad för. Frågan är som standard *en-US* om parametern inte anges eller om den landskod som anges in't stöds för det land som anges. En lista över lands koder som stöds finns i [listan över länder och språk som stöds](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en [ **AgreementDocument** -resurs](./agreement-document-resources.md) i svars texten.

Resursen har en **downloadUri** -egenskap som innehåller en URL-sträng som kan användas för att ladda ned avtals mal len. En annan länk returneras varje gången du skapar en fråga. Den här länken upphör att gälla efter fem minuter.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.

Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>Lista över länder och språk som stöds

> [!IMPORTANT]
> Lands kods egenskapen är Skift läges känslig. Se till att du använder rätt Skift läge som anges i tabellen nedan.

| Land                   | Landskod   | Språk koder som stöds |
|------------------------|--------|----------|
| Åland | AX | sv-SE |
| Afghanistan | AF | sv-SE |
| Albanien | AL | sv-SE |
| Algeriet | DZ | en-US, fr-FR, en-US |
| Amerikanska Samoa | AS | sv-SE |
| Andorra | AD | sv-SE |
| Angola | AO | en-US, pt-PT |
| Anguilla | AI | sv-SE |
| Antarktis | AQ | sv-SE |
| Antigua och Barbuda | AG | sv-SE |
| Argentina | AR | en-US, es-ES |
| Armenien | AM | sv-SE |
| Aruba | AW | sv-SE |
| Australien | AU | sv-SE |
| Österrike | AT | en-US, de-DE |
| Azerbajdzjan | AZ | sv-SE |
| Bahamas | BS | sv-SE |
| Bahrain | BH | en-US, AR-SA |
| Bangladesh | BD | sv-SE |
| Barbados | BB | sv-SE |
| Vitryssland | BY | en-US, ru-RU |
| Belgien | BE | en-US, nl-NL |
| Belize | BZ | en-US, es-ES |
| Benin | BJ | sv-SE |
| Bermuda | BM | sv-SE |
| Bhutan | BT | sv-SE |
| Bolivia | BO | en-US, es-ES |
| Bonaire | BQ | sv-SE |
| Bosnien och Hercegovina | BA | sv-SE |
| Botswana | BW | sv-SE |
| Bouvetön | BV | sv-SE |
| Brasilien | BR | en-US, pt-BR |
| Brittiska territoriet i Indiska Oceanen | I/O | sv-SE |
| Brittiska Jungfruöarna | VG | sv-SE |
| Brunei | BN | sv-SE |
| Bulgarien | BG | en-US, BG-BG |
| Burkina Faso | BF | sv-SE |
| Burundi | BI | sv-SE |
| Côte d'Ivoire | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, pt-PT |
| Kambodja | KH | sv-SE |
| Kamerun | CM | en-US, fr-FR |
| Kanada | CA | en-US, fr-FR |
| Caymanöarna | KY | en-US, en-US |
| Centralafrikanska Republiken | CF | sv-SE |
| Tchad | TD | sv-SE |
| Chile | CL | en-US, es-ES |
| Julön | CX | sv-SE |
| Kokosöarna | CC | sv-SE |
| Colombia | CO | en-US, es-ES |
| Komorerna | METER | sv-SE |
| Kongo (DR) | CD | sv-SE |
| Kongo | 0,05 | sv-SE |
| Cooköarna | CK | sv-SE |
| Costa Rica | CR | en-US, es-ES |
| Kroatien | HR | en-US, HR-HR |
| Curaçao | FELAKTIG | sv-SE |
| Cypern | CY | sv-SE |
| Czechia | CZ | en-US, CS-CZ |
| Danmark | DK | en-US, da-DK |
| Djibouti | DJ | sv-SE |
| Dominica | DM | sv-SE |
| Dominikanska republiken | DO | en-US, es-ES |
| Ecuador | EC | sv-SE |
| Egypten | EG | en-US, AR-SA |
| El Salvador | SV | en-US, es-ES |
| Ekvatorialguinea | GQ | sv-SE |
| Eritrea | ER | sv-SE |
| Estland | EE | en-US, et-EE |
| eSwatini | SZ | sv-SE |
| Etiopien | ET | sv-SE |
| Falklandsöarna | FK | sv-SE |
| Färöarna | DETALJERADE | sv-SE |
| Fiji | FJ | sv-SE |
| Finland | FI | en-US, fi-FI |
| Frankrike | FR | en-US, fr-FR |
| Franska Guyana | GF | en-US, fr-FR  |
| Franska Polynesien | PF | sv-SE |
| Franska sydterritorierna | TF | sv-SE |
| Gabon | Allmän tillgänglighet (GA) | sv-SE |
| Gambia | GM | sv-SE |
| Georgia | GE | sv-SE |
| Tyskland | DE | en-US, de-DE |
| Ghana | GH | sv-SE |
| Gibraltar | ETER | sv-SE |
| Grekland | GR | en-US, El-GR |
| Grönland | HUVUD | sv-SE |
| Grenada | GD | sv-SE |
| Guadeloupe | GP | sv-SE |
| Guam | GU | sv-SE |
| Guatemala | GT | en-US, es-ES |
| Guernsey | GG | sv-SE |
| Guinea | GN | sv-SE |
| Guinea-Bissau | GW | sv-SE |
| Guyana | GY | sv-SE |
| Haiti | HT | sv-SE |
| Heard- och McDonaldöarna | IGNERINGSALGORITM | sv-SE |
| Honduras | HN | en-US, es-ES |
| Folkrepubliken Kinas särskilda administrativa region Hongkong | HK | en-US, zh-HK |
| Ungern | HU | en-US, hu – HU |
| Island | IS | sv-SE |
| Indien | IN | en-US, Hi-IN |
| Indonesien | ID | en-US, ID-ID |
| Irak | IQ | en-US, AR-SA |
| Irland | IE | sv-SE |
| Isle of Man | Snabbmeddelanden | sv-SE |
| Israel | IL | en-US, he-IL |
| Italien | IT | en-US, IT – IT |
| Jamaica | JM | sv-SE |
| Jan Mayen | XJ | sv-SE |
| Japan | JP | en-US, ja-JP |
| Jersey | JE | sv-SE |
| Jordanien | JO | en-US, AR-SA |
| Kazakstan | KZ | en-US, KK – KZ |
| Kenya | KE | sv-SE |
| Kiribati | KI | sv-SE |
| Korea | KR | en-US, ko-KR |
| Kosovo | XK | sv-SE |
| Kuwait | KW | en-US, AR-SA |
| Kirgizistan | KG | en-US, ru-RU |
| Laos | LA | sv-SE |
| Lettland | LV | en-US, LV-LV |
| Libanon | LB | en-US, AR-SA |
| Lesotho | LS | sv-SE |
| Liberia | LR | sv-SE |
| Libyen | LY | en-US, AR-SA |
| Liechtenstein | LI | en-US, de-DE |
| Litauen | LT | en-US, lt-LT |
| Luxemburg | LU | en-US, fr-FR |
| Folkrepubliken Kinas särskilda administrativa region Macao | MO | en-US, zh-HK |
| F.d. jugoslaviska republiken Makedonien | MK | sv-SE |
| Madagaskar | MG | sv-SE |
| Malawi | MW | sv-SE |
| Malaysia | MY | en-US, MS-MY |
| Maldiverna | MV | sv-SE |
| Mali | ML | sv-SE |
| Malta | MT | sv-SE |
| Marshallöarna | MH | sv-SE |
| Martinique | MQ | sv-SE |
| Mauretanien | MR | sv-SE |
| Mauritius | MK | en-US, AR-SA |
| Mayotte | YT | sv-SE |
| Mexico | MX | en-US, es-ES |
| Mikronesien | FM | sv-SE |
| Moldavien | MD | en-US, RO-RO |
| Monaco | MC | en-US, fr-FR |
| Mongoliet | MN | sv-SE |
| Montenegro | ME | sv-SE |
| Montserrat | MS | sv-SE |
| Marocko | MA | en-US, fr-FR, en-US |
| Moçambique | MZ | sv-SE |
| Myanmar | MM | sv-SE |
| Namibia | NA | sv-SE |
| Nauru | NR | sv-SE |
| Nepal | NP | sv-SE |
| Nederländerna | NL | en-US, nl-NL |
| Nya Kaledonien | NC | sv-SE |
| Nya Zeeland | NZ | sv-SE |
| Nicaragua | NI | en-US, es-ES |
| Niger | NE | sv-SE |
| Nigeria | NG | sv-SE |
| Niue | NU | sv-SE |
| Norfolkön | NF | sv-SE |
| Nordmarianerna | MP | sv-SE |
| Norge | NO | en-US, NB – nej |
| Oman | OM | en-US, AR-SA |
| Pakistan | PK | sv-SE |
| Palau | PW | sv-SE |
| Palestinska myndigheten | PS | sv-SE |
| Panama | PA | en-US, es-ES |
| Papua Nya Guinea | P1500 | sv-SE |
| Paraguay | PY | en-US, es-ES |
| Peru | PE | en-US, es-ES |
| Filippinerna | PH | sv-SE |
| Pitcairn | PN | sv-SE |
| Polen | PL | en-US, pl-PL |
| Portugal | PT | en-US, pt-PT |
| Puerto Rico | PR | en-US, en-US |
| Qatar | QA | en-US, AR-SA |
| Réunion | RE | sv-SE |
| Rumänien | RO | en-US, RO-RO |
| Ryssland | RU | en-US, ru-RU |
| Rwanda | RW | en-US, fr-FR |
| São Tomé och Príncipe | ST | en-US, fr-FR |
| Saba | X | sv-SE |
| Saint-Barthélemy | BL | sv-SE |
| Saint Kitts och Nevis | KN | sv-SE |
| Saint Lucia | LC | en-US, en-US |
| Saint Martin | MF | en-US, en-US |
| Saint-Pierre och Miquelon | PM | sv-SE |
| Saint Vincent och Grenadinerna | VC | sv-SE |
| Samoa | WS | sv-SE |
| San Marino | SM | sv-SE |
| Saudiarabien | SA | sv-SE |
| Senegal | SN | en-US, fr-FR |
| Serbien | RS | en-US, SR-latn-RS, en-US |
| Seychellerna | SC | sv-SE |
| Sierra Leone | SL | sv-SE |
| Singapore | SG | en-US, zh-SG |
| Sint Eustatius | XE | sv-SE |
| Sint Maarten | NÄTVERKSANSLUTNING | en-US, en-US |
| Slovakien | SK | en-US, sk-SK |
| Slovenien | SI | en-US, SL-SI |
| Solomonöarna | SA | sv-SE |
| Somalia | SO | sv-SE |
| Sydafrika | ZA | sv-SE |
| Sydgeorgien och Sydsandwichöarna | GS | sv-SE |
| Sydsudan | SS | sv-SE |
| Spanien | ES | en-US, es-ES, en-US, en-US |
| Sri Lanka | LK | sv-SE |
| Saint Helena, Ascension, Tristan da Cunha | SH | sv-SE |
| Surinam | SR | sv-SE |
| Svalbard | SJ | sv-SE |
| Sverige | SE | en-US, sa-SE |
| Schweiz | CH | en-US, fr-FR, en-US, en-US |
| Taiwan | TW | en-US, zh-HK |
| Tadzjikistan | TJ | sv-SE |
| Tanzania | TZ | sv-SE |
| Thailand | TH | en-US, Th |
| Timor-Leste | TL | sv-SE |
| Togo | TG | sv-SE |
| Tokelau | TK | sv-SE |
| Tonga | TO | sv-SE |
| Trinidad och Tobago | TT | sv-SE |
| Tunisien | TN | en-US, fr-FR, en-US |
| Turkiet | TR | en-US, tr-TR |
| Turkmenistan | TM | sv-SE |
| Turks- och Caicosöarna | TC | sv-SE |
| Tuvalu | TV | sv-SE |
| Amerikanska öar | UM | sv-SE |
| Amerikanska jungfru öarna | VI | sv-SE |
| Uganda | UG | sv-SE |
| Ukraina | UA | en-US, Storbritannien-UA |
| Förenade Arabemiraten | AE | en-US, AR-SA |
| Storbritannien | GB | sv-SE |
| USA | USA | sv-SE |
| Uruguay | UY | en-US, es-ES |
| Uzbekistan | UZ | en-US, ru-RU |
| Vanuatu | ANTECKNING | sv-SE |
| Vatikanstaten | VA | sv-SE |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi – VN |
| Wallis och Futuna | WF | sv-SE |
| Jemen | CHANSEN | en-US, AR-SA |
| Zambia | ZM | sv-SE |
| Zimbabwe | ZW | sv-SE |
