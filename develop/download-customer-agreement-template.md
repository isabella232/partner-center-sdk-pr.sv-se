---
title: Hämta en nedladdningslänk för Microsoft-kundavtal mallen
description: Hämta en nedladdningslänk för Microsoft-kundavtal mall.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: fccb9e3d4a837f3e8043f8c7ae1e3911d819afd7
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906527"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Hämta en nedladdningslänk för Microsoft-kundavtal mallen

**Gäller för:** Partnercenter

**Gäller inte för:** Partner Center som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**AgreementDocument-resursen** stöds för närvarande endast av PartnerCenter i Det offentliga Microsoft-molnet.

Den här artikeln beskriver hur du hämtar en länk för Microsoft-kundavtal mallen, baserat på kundens land och språk.

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1.14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](./partner-center-authentication.md). Det här scenariot stöder endast app- och användarautentisering.

- Kundens land som mallen Microsoft-kundavtal gäller.

- Det språk som mallen Microsoft-kundavtal ska lokaliseras till.

> [!IMPORTANT]
>
> - Den Microsoft-kundavtal är landsspecifik. När du begär en länk för att Microsoft-kundavtal mallen måste du ange rätt land baserat på kundens plats. eller lista över länder som stöds, se [Lista över länder och språk som stöds.](#list-of-supported-countries-and-languages)
>
> - För vissa länder är Microsoft-kundavtal tillgängliga på flera språk. För bästa kundupplevelse väljer du det språk som bäst matchar kundens behov. En lista över språk som stöds finns i [Lista över länder och språk som stöds.](#list-of-supported-countries-and-languages)
> - Den här metoden stöds endast med Microsoft-kundavtal.

## <a name="net"></a>.NET

Så här hämtar du en länk för att Microsoft-kundavtal mallen:

1. Hämta avtalets metadata för Microsoft-kundavtal. Du måste hämta **templateId för** Microsoft-kundavtal. Mer information finns i Hämta [avtalsmetadata för Microsoft-kundavtal](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Använd samlingen IAggregatePartner.AgreementTemplates.

3. Anropa **metoden ById** och ange **templateId för** Microsoft-kundavtal.

4. Hämta **egenskapen** Document.

5. Anropa **metoden ByCountry** och ange kundens land som avtalsmallen gäller för. Frågan är som standard *USA* om metoden inte har angetts. En lista över landskoder som stöds finns i [Lista över länder och språk som stöds.](#list-of-supported-countries-and-languages) Den här metoden är **fallkänslig**.

6. Anropa **metoden ByLanguage** och ange det språk som avtalsmallen ska lokaliseras till. Frågan är som standard *en-US* om metoden inte har angetts eller om den angivna landskoden inte stöds för det angivna landet. En lista över språkkoder som stöds finns i [Lista över länder och språk som stöds.](#list-of-supported-countries-and-languages)

7. Anropa metoden **Get** eller **GetAsync.**

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Ett komplett exempel finns i klassen [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>REST-begäran

Så här hämtar du en länk för att Microsoft-kundavtal mallen:

1. Hämta avtalets metadata för Microsoft-kundavtal. Du måste hämta **templateId för** Microsoft-kundavtal. Mer information finns i Hämta [avtalsmetadata för Microsoft-kundavtal](get-customer-agreement-metadata.md).

2. Skapa en REST-begäran för att hämta [ **en AgreementDocument-resurs**](./agreement-document-resources.md). Ett exempel finns i exemplet med [syntax för begäran.](#request-syntax) Du måste ange följande information:

    - **TemplateId för** Microsoft-kundavtal.
    - Det land som mallen Microsoft-kundavtal gäller för.
    - Det språk som mallen Microsoft-kundavtal ska lokaliseras till.

### <a name="request-syntax"></a>Begärandesyntax

Använd följande begärandesyntax för den här resursen:

| Metod | URI för förfrågan |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Du kan använda följande URI-parametrar med din begäran:

| Namn                   | Typ   | Obligatorisk | Beskrivning                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | sträng | Ja      | Unik identifierare för avtalstypen. Du kan hämta templateId för Microsoft-kundavtal genom att hämta avtalets metadata för Microsoft-kundavtal. Mer information finns i Hämta [avtalsmetadata för Microsoft-kundavtal](./get-customer-agreement-metadata.md). Den här parametern **är fallkänslig**.|
| land                | sträng | No       | Anger det land som avtalsmallen gäller för. Frågan är som standard *USA* om parametern inte har angetts. En lista över landskoder som stöds finns i [Lista över länder och språk som stöds.](#list-of-supported-countries-and-languages)|
| language               | sträng | No       | Anger det språk som avtalsmallen ska lokaliseras till. Frågan är som standard *en-US* om parametern inte har angetts eller om landskoden som anges i inte stöds för det angivna landet. En lista över landskoder som stöds finns i [Lista över länder och språk som stöds.](#list-of-supported-countries-and-languages)|

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas returnerar den här metoden [ **en AgreementDocument-resurs**](./agreement-document-resources.md) i svarstexten.

Resursen har en **downloadUri-egenskap** som innehåller en URL-sträng som kan användas för att ladda ned avtalsmallen. En annan länk returneras varje gång du gör en fråga. Den här länken upphör att gälla efter fem minuter.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.

Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
> Landskodegenskapen är fallkänslig. Se till att använda rätt hölje som anges i tabellen nedan.

| Land                   | Landskod   | Språkkod som stöds |
|------------------------|--------|----------|
| Åland | Ax | sv-SE |
| Afghanistan | AF | sv-SE |
| Albanien | AL | sv-SE |
| Algeriet | DZ | en-US, fr-FR, en-US |
| Amerikanska Samoa | AS | sv-SE |
| Andorra | AD | sv-SE |
| Angola | AO | en-US, pt-PT |
| Anguilla | AI | sv-SE |
| Antarktis | Aq | sv-SE |
| Antigua och Barbuda | AG | sv-SE |
| Argentina | AR | en-US, es-ES |
| Armenien | AM | sv-SE |
| Aruba | Aw | sv-SE |
| Australien | AU | sv-SE |
| Österrike | AT | en-US, de-DE |
| Azerbajdzjan | AZ | sv-SE |
| Bahamas | BS | sv-SE |
| Bahrain | BH | en-US, ar-SA |
| Bangladesh | BD | sv-SE |
| Barbados | BB | sv-SE |
| Vitryssland | BY | en-US, ru-RU |
| Belgien | BE | en-US, nl-NL |
| Belize | BZ | en-US, es-ES |
| Benin | BJ | sv-SE |
| Bermuda | Bm | sv-SE |
| Bhutan | BT | sv-SE |
| Bolivia | BO | en-US, es-ES |
| Bonaire | Bq | sv-SE |
| Bosnien och Hercegovina | BA | sv-SE |
| Botswana | BW | sv-SE |
| Bouvetön | Bv | sv-SE |
| Brasilien | BR | en-US, pt-BR |
| Brittiska territoriet i Indiska Oceanen | I/O | sv-SE |
| Brittiska Jungfruöarna | VG | sv-SE |
| Brunei | BN | sv-SE |
| Bulgarien | BG | en-US, bg-BG |
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
| Komorerna | Km | sv-SE |
| Kongo (DR) | CD | sv-SE |
| Kongo | Cg | sv-SE |
| Cooköarna | Ck | sv-SE |
| Costa Rica | CR | en-US, es-ES |
| Kroatien | HR | en-US, hr-HR |
| Curaçao | Cw | sv-SE |
| Cypern | CY | sv-SE |
| Tjeckien | CZ | en-US, cs-ZAR |
| Danmark | DK | en-US, da-DK |
| Djibouti | Dj | sv-SE |
| Dominica | DM | sv-SE |
| Dominikanska republiken | DO | en-US, es-ES |
| Ecuador | EC | sv-SE |
| Egypten | EG | en-US, ar-SA |
| El Salvador | SV | en-US, es-ES |
| Ekvatorialguinea | Gq | sv-SE |
| Eritrea | ER | sv-SE |
| Estland | EE | en-US, et-EE |
| eSwatini | SZ | sv-SE |
| Etiopien | ET | sv-SE |
| Falklandsöarna | Fk | sv-SE |
| Färöarna | Fo | sv-SE |
| Fiji | FJ | sv-SE |
| Finland | FI | en-US, fi-FI |
| Frankrike | FR | en-US, fr-FR |
| Franska Guyana | GF | en-US, fr-FR  |
| Franska Polynesien | PF | sv-SE |
| Franska sydterritorierna | Tf | sv-SE |
| Gabon | Allmän tillgänglighet (GA) | sv-SE |
| Gambia | GM | sv-SE |
| Georgia | GE | sv-SE |
| Tyskland | DE | en-US, de-DE |
| Ghana | GH | sv-SE |
| Gibraltar | Gi | sv-SE |
| Grekland | GR | en-US, el-GR |
| Grönland | Gl | sv-SE |
| Grenada | DDR | sv-SE |
| Guadeloupe | GP | sv-SE |
| Guam | GU | sv-SE |
| Guatemala | GT | en-US, es-ES |
| Guernsey | Gg | sv-SE |
| Guinea | GN | sv-SE |
| Guinea-Bissau | Gw | sv-SE |
| Guyana | GY | sv-SE |
| Haiti | HT | sv-SE |
| Heard- och McDonaldöarna | Hm | sv-SE |
| Honduras | HN | en-US, es-ES |
| Folkrepubliken Kinas särskilda administrativa region Hongkong | HK | en-US, zh-HK |
| Ungern | HU | en-US, hu-HU |
| Island | IS | sv-SE |
| Indien | IN | en-US, hi-IN |
| Indonesien | ID | en-US, id-ID |
| Irak | IQ | en-US, ar-SA |
| Irland | IE | sv-SE |
| Isle of Man | Snabbmeddelanden | sv-SE |
| Israel | IL | en-US, he-IL |
| Italien | IT | en-US, it-IT |
| Jamaica | JM | sv-SE |
| Jan Mayen | Xj | sv-SE |
| Japan | JP | en-US, ja-JP |
| Jersey | Je | sv-SE |
| Jordanien | JO | en-US, ar-SA |
| Kazakstan | KZ | en-US, kk-KZ |
| Kenya | KE | sv-SE |
| Kiribati | KI | sv-SE |
| Korea | KR | en-US, ko-KR |
| Kosovo | Xk | sv-SE |
| Kuwait | KW | en-US, ar-SA |
| Kirgizistan | KG | en-US, ru-RU |
| Laos | LA | sv-SE |
| Lettland | LV | en-US, lv-LV |
| Libanon | LB | en-US, ar-SA |
| Lesotho | LS | sv-SE |
| Liberia | LR | sv-SE |
| Libyen | LY | en-US, ar-SA |
| Liechtenstein | LI | en-US, de-DE |
| Litauen | LT | en-US, lt-LT |
| Luxemburg | LU | en-US, fr-FR |
| Folkrepubliken Kinas särskilda administrativa region Macao | MO | en-US, zh-HK |
| F.d. f.d. f.d. f. | MK | sv-SE |
| Madagaskar | MG | sv-SE |
| Malawi | MW | sv-SE |
| Malaysia | MY | en-US, ms-MY |
| Maldiverna | MV | sv-SE |
| Mali | ML | sv-SE |
| Malta | MT | sv-SE |
| Marshallöarna | MH | sv-SE |
| Martinique | MQ | sv-SE |
| Mauretanien | MR | sv-SE |
| Mauritius | Mu | en-US, ar-SA |
| Mayotte | YT | sv-SE |
| Mexico | MX | en-US, es-ES |
| Mikronesien | FM | sv-SE |
| Moldavien | MD | en-US, ro-RO |
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
| Norfolkön | Nf | sv-SE |
| Nordmarianerna | MP | sv-SE |
| Norge | NO | en-US, nb-NO |
| Oman | OM | en-US, ar-SA |
| Pakistan | PK | sv-SE |
| Palau | PW | sv-SE |
| Palestinska myndigheten | PS | sv-SE |
| Panama | PA | en-US, es-ES |
| Papua Nya Guinea | Sida | sv-SE |
| Paraguay | PY | en-US, es-ES |
| Peru | PE | en-US, es-ES |
| Filippinerna | PH | sv-SE |
| Pitcairn | Pn | sv-SE |
| Polen | PL | en-US, pl-PL |
| Portugal | PT | en-US, pt-PT |
| Puerto Rico | PR | en-US, en-US |
| Qatar | QA | en-US, ar-SA |
| Réunion | RE | sv-SE |
| Rumänien | RO | en-US, ro-RO |
| Ryssland | RU | en-US, ru-RU |
| Rwanda | RW | en-US, fr-FR |
| Séo Tomé och Prñncipe | ST | en-US, fr-FR |
| Saba | Xs | sv-SE |
| Saint-Barthélemy | BL | sv-SE |
| Saint Kitts och Nevis | KN | sv-SE |
| Saint Lucia | Lc | en-US, en-US |
| Saint Martin | Mf | en-US, en-US |
| Saint-Pierre och Miquelon | PM | sv-SE |
| Saint Vincent och Grenadinerna | VC | sv-SE |
| Samoa | WS | sv-SE |
| San Marino | Sm | sv-SE |
| Saudiarabien | SA | sv-SE |
| Senegal | SN | en-US, fr-FR |
| Serbien | RS | en-US, sr-Latn-RS, en-US |
| Seychellerna | SC | sv-SE |
| Sierra Leone | SL | sv-SE |
| Singapore | SG | en-US, zh-SG |
| Sint Eustatius | Xe | sv-SE |
| Sint Maarten | Sx | en-US, en-US |
| Slovakien | SK | en-US, sk-SK |
| Slovenien | SI | en-US, sl-SI |
| Solomonöarna | Sb | sv-SE |
| Somalia | SO | sv-SE |
| Sydafrika | ZA | sv-SE |
| Sydgeorgien och Sydsandwichöarna | Gs | sv-SE |
| Sydsudan | SS | sv-SE |
| Spanien | ES | en-US, es-ES, en-US, en-US |
| Sri Lanka | LK | sv-SE |
| StDirigering, Ascension, Tristan da Cunha | SH | sv-SE |
| Surinam | SR | sv-SE |
| Svalbard | Sj | sv-SE |
| Sverige | SE | sv-SE |
| Schweiz | CH | en-US, fr-FR, en-US, en-US |
| Taiwan | TW | en-US, zh-HK |
| Tadzjikistan | Tj | sv-SE |
| Tanzania | TZ | sv-SE |
| Thailand | TH | en-US, th-TH |
| Timor-Leste | TL | sv-SE |
| Togo | TG | sv-SE |
| Tokelau | Tk | sv-SE |
| Tonga | TO | sv-SE |
| Trinidad och Tobago | TT | sv-SE |
| Tunisien | TN | en-US, fr-FR, en-US |
| Turkiet | TR | en-US, tr-TR |
| Turkmenistan | TM | sv-SE |
| Turks- och Caicosöarna | TC | sv-SE |
| Tuvalu | TV | sv-SE |
| U.S. Outlying Islands | UM | sv-SE |
| Amerikanska Jungfruöarna | VI | sv-SE |
| Uganda | UG | sv-SE |
| Ukraina | UA | en-US, uk-UA |
| Förenade Arabemiraten | AE | en-US, ar-SA |
| Storbritannien | GB | sv-SE |
| USA | USA | sv-SE |
| Uruguay | UY | en-US, es-ES |
| Uzbekistan | UZ | en-US, ru-RU |
| Vanuatu | Vu | sv-SE |
| Vatikanstaten | VA | sv-SE |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis och Spanuna | WF | sv-SE |
| Jemen | Ni | en-US, ar-SA |
| Zambia | ZM | sv-SE |
| Zimbabwe | ZW | sv-SE |
