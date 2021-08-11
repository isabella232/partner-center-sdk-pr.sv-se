---
title: Partnercenter – språk och nationella inställningar som stöds
description: Lista över iso2- och ISO3-språk som stöds för Partnercenter.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 6f2e1d50fa0f2ace2e94f4dbb5681e2164241ee57a85249136a55fce20893fbb
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997591"
---
# <a name="partner-center-supported-languages-and-locales"></a>Partnercenter – språk och nationella inställningar som stöds

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Vissa Partner Center-API:er kräver ett värde som anger språk, land eller region. Till exempel kräver [Partner Center REST-huvudet](headers.md) X-Locale ett värde ofta i formatet "language-country" ("en-US" anger "Engelska - USA").

I partnercenter-hanterade API:er, klassen [CountryValidationRules/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) och [OfferCategory.Locale/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode/dotnet /api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode) eller [CustomerBillingProfile.Culture/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) kräver strängvärden som anger ett språk eller land/region (i form av en ISO2-språkkod eller ISO3-lands-/regionkod), en språkversion, eller en kultur (ett språk-ID kombinerat med en lands-/regionskod).

I följande tabell visas de landskoder för kulturer och ISO (International Standards Organization) som stöds i Partner Center-API:erna.

| Land/region                           | ISO Alpha 2-landskod | ISO Alpha 3-landskod | Kultur som stöds                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afghanistan                              | AF                       | Afg                      | ps-AF/en-US                         |
| Åland                            | Ax                       | Ala                      | sv-SE/en-US                         |
| Albanien                                  | AL                       | Alb                      | sq-AL/en-US                         |
| Algeriet                                  | DZ                       | Dza                      | ar-DZ/en-US                         |
| Amerikanska Samoa                           | AS                       | ASM                      | sv-SE                                 |
| Andorra                                  | AD                       | AND                      | ca-ES/en-US                         |
| Angola                                   | AO                       | Sedan                      | pt-PT/en-US                         |
| Anguilla                                 | AI                       | Aia                      | sv-SE                                 |
| Antarktis                               | Aq                       | Ata                      | sv-SE                                 |
| Antigua och Barbuda                      | AG                       | Atg                      | sv-SE                                 |
| Argentina                                | AR                       | ARG                      | es-AR/en-US                         |
| Armenien                                  | AM                       | ARM                      | hy-AM/en-US                         |
| Aruba                                    | Aw                       | Abw                      | nl-NL/en-US                         |
| Australien                                | AU                       | Aus                      | en-AU/en-US                         |
| Österrike                                  | AT                       | Ht                      | de-AT/en-US                         |
| Azerbajdzjan                               | AZ                       | AZE                      | az-Latn-AZ / en-US                    |
| Bahamas                                  | BS                       | Bhs                      | en-GB/en-US                         |
| Bahrain                                  | BH                       | Bhr                      | ar-BF/en-US                         |
| Bangladesh                               | BD                       | BGD                      | bn-BD/en-US                         |
| Barbados                                 | BB                       | Brb                      | en-GB/en-US                         |
| Vitryssland                                  | BY                       | BLR                      | be-BY/en-US                         |
| Belgien                                  | BE                       | Bel                      | fr-BE/nl-BE/en-US                 |
| Belize                                   | BZ                       | BLZ                      | en-BZ/en-US                         |
| Benin                                    | BJ                       | Ben                      | fr-FR / en-US                         |
| Bermuda                                  | Bm                       | Bmu                      | en-GB/en-US                         |
| Bhutan                                   | BT                       | Btn                      | sv-SE                                 |
| Bolivia                                  | BO                       | Bol                      | es-BO/en-US                         |
| Bonaire                                  | Bq                       | Bes                      | nl-NL/en-US                         |
| Bosnien och Hercegovina                   | BA                       | BIH                      | bs-Latn-BA / en-US                    |
| Botswana                                 | BW                       | Bwa                      | en-GB/en-US                         |
| Bouvetön                            | Bv                       | Bvt                      | nb-NO/en-US                         |
| Brasilien                                   | BR                       | Bh                      | pt-BR/en-US                         |
| Brittiska territoriet i Indiska Oceanen           | I/O                       | Sakernas Internet                      | sv-SE                                 |
| Brittiska Jungfruöarna                   | VG                       | VGB                      | sv-SE                                 |
| Brunei                                   | BN                       | Brn                      | ms-BN /en-US                         |
| Bulgarien                                 | BG                       | Bgr                      | bg-BG /en-US                         |
| Burkina Faso                             | BF                       | Bfa                      | fr-FR / en-US                         |
| Burundi                                  | BI                       | BDI                      | fr-FR / en-US                         |
| Cabo Verde                               | CV                       | Cpv                      | pt-CV/en-US                         |
| Kambodja                                 | KH                       | Khm                      | km-KH/en-US                         |
| Kamerun                                 | CM                       | Cmr                      | fr-FR / en-US                         |
| Kanada                                   | CA                       | Kan                      | fr-CA/en-US                         |
| Caymanöarna                           | KY                       | Cym                      | en-GB/en-US                         |
| Centralafrikanska Republiken                 | CF                       | Caf                      | fr-FR / en-US                         |
| Tchad                                     | TD                       | Tcd                      | fr-FR / en-US                         |
| Chile                                    | CL                       | Chl                      | es-CL/en-US                         |
| Kina                                    | CN                       | CHN                      | zh-CN /en-US                         |
| Julön                         | CX                       | CXR                      | sv-SE                                 |
| Kokosöarna                  | CC                       | Cck                      | sv-SE                                 |
| Colombia                                 | CO                       | Överste                      | es-CO/en-US                         |
| Komorerna                                  | Km                       | Com                      | fr-FR/en-US                         |
| Kongo                                    | Cg                       | Kugge                      | fr-FR/en-US                         |
| Kongo (DR)                              | CD                       | COD                      | fr-FR/en-US                         |
| Cooköarna                             | Ck                       | Cok                      | sv-SE                                 |
| Costa Rica                               | CR                       | Cri                      | es-CR/en-US                         |
| Côte d'Ivoire                            | CI                       | Civ                      | fr-FR/en-US                         |
| Kroatien                                  | HR                       | Hrv                      | hr-HR/en-US                         |
| Curaçao                                  | Cw                       | CUW                      | nl-NL/en-US                         |
| Cypern                                   | CY                       | Cyp                      | el-GR/en-US                         |
| Tjeckien                                  | CZ                       | Cze                      | cs-ZAR/en-US                         |
| Danmark                                  | DK                       | Dnk                      | da-DK/en-US                         |
| Djibouti                                 | Dj                       | Dji                      | fr-FR/en-US                         |
| Dominica                                 | DM                       | DMA                      | sv-SE                                 |
| Dominikanska republiken                       | DO                       | Dom                      | es-DO/en-US                         |
| Ecuador                                  | EC                       | Ecu                      | es-EC/en-US                         |
| Egypten                                    | EG                       | EGY                      | ar-EG/en-US                         |
| El Salvador                              | SV                       | Slv                      | es-SV/en-US                         |
| Ekvatorialguinea                        | Gq                       | GNQ                      | es-ES/en-US                         |
| Eritrea                                  | ER                       | Eri                      | ar-SA/en-US                         |
| Estland                                  | EE                       | Est                      | et-EE/en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | sv-SE                                 |
| Etiopien                                 | ET                       | Eth                      | am-ET/en-US                         |
| Falklandsöarna                         | Fk                       | FLK                      | sv-SE                                 |
| Färöarna                            | Fo                       | Tillbaka                      | fo-FO/en-US                         |
| Fiji                                     | FJ                       | FJI                      | en-GB/en-US                         |
| Finland                                  | FI                       | FIN                      | fi-FI / sv-FI / en-US                 |
| Frankrike                                   | FR                       | FRA                      | fr-FR / en-US                         |
| Franska Guyana                            | GF                       | GUF                      | fr-FR / en-US                         |
| Franska Polynesien                         | PF                       | PYF                      | fr-FR / en-US                         |
| Franska sydterritorierna              | Tf                       | Atf                      | fr-FR / en-US                         |
| Gabon                                    | Allmän tillgänglighet (GA)                       | Gab                      | fr-FR / en-US                         |
| Gambia                                   | GM                       | GMB                      | sv-SE                                 |
| Georgia                                  | GE                       | Geo                      | ka-GE/en-US                         |
| Tyskland                                  | DE                       | DEU                      | de-DE/en-US                         |
| Ghana                                    | GH                       | GHA                      | en-GB/en-US                         |
| Gibraltar                                | Gi                       | Gib                      | sv-SE                                 |
| Grekland                                   | GR                       | GRC                      | el-GR/en-US                         |
| Grönland                                | Gl                       | Grl                      | da-DK/en-US                         |
| Grenada                                  | KANT                       | Grd                      | sv-SE                                 |
| Guadeloupe                               | GP                       | Glp                      | fr-FR / en-US                         |
| Guam                                     | GU                       | Tuggummi                      | sv-SE                                 |
| Guatemala                                | GT                       | Gtm                      | es-GT/ en-US                         |
| Guernsey                                 | Gg                       | GGY                      | sv-SE                                 |
| Guinea                                   | GN                       | Gin                      | fr-FR / en-US                         |
| Guinea-Bissau                            | Gw                       | Gnb                      | pt-PT/en-US                         |
| Guyana                                   | GY                       | Kille                      | sv-SE                                 |
| Haiti                                    | HT                       | Hti                      | fr-FR / en-US                         |
| Heard- och McDonaldöarna        | Hm                       | Hmd                      | sv-SE                                 |
| Honduras                                 | HN                       | Hnd                      | es-HN / en-US                         |
| Folkrepubliken Kinas särskilda administrativa region Hongkong                            | HK                       | Hkg                      | zh-HK /en-US                         |
| Ungern                                  | HU                       | HUN                      | hu-HU/en-US                         |
| Island                                  | IS                       | Isl                      | is-IS/en-US                         |
| Indien                                    | IN                       | IND                      | en-IN/hi-IN/en-US                 |
| Indonesien                                | ID                       | Idn                      | id-ID/en-US                         |
| Irak                                     | IQ                       | Irq                      | ar-IQ/en-US                         |
| Irland                                  | IE                       | Irl                      | en-IE/en-US                         |
| Isle of Man                              | Snabbmeddelanden                       | Imn                      | sv-SE                                 |
| Israel                                   | IL                       | ISR                      | he-IL/en-US                         |
| Italien                                    | IT                       | ITA                      | it-IT/en-US                         |
| Jamaica                                  | JM                       | Sylt                      | en-JM/en-US                         |
| Jan Mayen                                | Xj                       | XJA                      | nb-NO/en-US                         |
| Japan                                    | JP                       | JPN                      | ja-JP/en-US                         |
| Jersey                                   | Je                       | Jey                      | sv-SE                                 |
| Jordanien                                   | JO                       | Jor                      | ar-JO/en-US                         |
| Kazakstan                               | KZ                       | Kaz                      | kk-KZ/en-US                         |
| Kenya                                    | KE                       | Ken                      | sw-KE/en-US                         |
| Kiribati                                 | KI                       | Kir                      | sv-SE                                 |
| Korea                                    | KR                       | KOR                      | ko-KR/en-US                         |
| Kosovo                                   | Xk                       | XKS                      | sv-SE                                 |
| Kuwait                                   | KW                       | KVT                      | ar-KW/en-US                         |
| Kirgizistan                               | KG                       | KGZ                      | ky-KG/en-US                         |
| Laos                                     | LA                       | Lao                      | lo-LA/en-US                         |
| Lettland                                   | LV                       | Lva                      | lv-LV/en-US                         |
| Libanon                                  | LB                       | LBN                      | ar-LB/en-US                         |
| Lesotho                                  | LS                       | Lso                      | sv-SE                                 |
| Liberia                                  | LR                       | LBR                      | sv-SE                                 |
| Libyen                                    | LY                       | Lby                      | ar-LY/en-US                         |
| Liechtenstein                            | LI                       | Ligger                      | de-LI/en-US                         |
| Litauen                                | LT                       | Ltu                      | lt-LT/en-US                         |
| Luxemburg                               | LU                       | Lux                      | de-LU / fr-LU / en-US                 |
| Folkrepubliken Kinas särskilda administrativa region Macao                                | MO                       | Mac                      | zh-MO/en-US                         |
| F.d. f.d. f.d. f.                          | MK                       | Mkd                      | mk-MK/en-US                         |
| Madagaskar                               | MG                       | Millennieutvecklingsmålen                      | fr-FR/en-US                         |
| Malawi                                   | MW                       | MWI                      | sv-SE                                 |
| Malaysia                                 | MY                       | Mys                      | en-MY/en-US                         |
| Maldiverna                                 | MV                       | MDV                      | dv-MV/en-US                         |
| Mali                                     | ML                       | MLI                      | fr-FR/en-US                         |
| Malta                                    | MT                       | Mlt                      | mt-MT/en-US                         |
| Marshallöarna                         | MH                       | Mhl                      | sv-SE                                 |
| Martinique                               | MQ                       | MTQ                      | fr-FR/en-US                         |
| Mauretanien                               | MR                       | Mrt                      | ar-SA/en-US                         |
| Mauritius                                | Mu                       | MUS                      | en-GB/en-US                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR/en-US                         |
| Mexico                                   | MX                       | Mex                      | es-MX/en-US                         |
| Mikronesien                               | FM                       | Mikronesien                      | sv-SE                                 |
| Moldavien                                  | MD                       | Mda                      | ro-RO/en-US                         |
| Monaco                                   | MC                       | Mco                      | fr-MC/en-US                         |
| Mongoliet                                 | MN                       | Mng                      | mn-MN/en-US                         |
| Montenegro                               | ME                       | Mne                      | sr-Latn-ME/en-US                    |
| Montserrat                               | MS                       | Msr                      | sv-SE                                 |
| Marocko                                  | MA                       | Mar                      | ar-MA/en-US                         |
| Moçambique                               | MZ                       | Moz                      | pt-PT                                 |
| Myanmar                                  | MM                       | Mmr                      | sv-SE                                 |
| Namibia                                  | NA                       | Nam                      | en-GB/en-US                         |
| Nauru                                    | NR                       | NRU                      | sv-SE                                 |
| Nepal                                    | NP                       | Npl                      | ne-NP/en-US                         |
| Bonaire, Curaçao, Saba, Sint Eustatius och Sint Maarten                     | En                       | Antillerna                      | sv-SE                                 |
| Nederländerna                         | NL                       | NLD                      | nl-NL/en-US                         |
| Nya Kaledonien                            | NC                       | NCL                      | fr-FR/en-US                         |
| Nya Zeeland                              | NZ                       | Nzl                      | en-NZ/en-US                         |
| Nicaragua                                | NI                       | NIC                      | es-NI/en-US                         |
| Niger                                    | NE                       | NER                      | fr-FR/en-US                         |
| Nigeria                                  | NG                       | Nga                      | ha-Latn-NG/en-US                    |
| Niue                                     | NU                       | Niu                      | sv-SE                                 |
| Norfolkön                           | Nf                       | NFK                      | sv-SE                                 |
| Nordmarianerna                 | MP                       | MNP                      | sv-SE                                 |
| Norge                                   | NO                       | NOR                      | nb-NO/en-US                         |
| Oman                                     | OM                       | Omn                      | ar-OM/en-US                         |
| Pakistan                                 | PK                       | Pak                      | your-PK/en-US                         |
| Palau                                    | PW                       | PLW                      | sv-SE                                 |
| Palestinska myndigheten                    | PS                       | Pse                      | ar-SA/en-US                         |
| Panama                                   | PA                       | PAN                      | es-PA/en-US                         |
| Papua Nya Guinea                         | Sida                       | PNG                      | sv-SE                                 |
| Paraguay                                 | PY                       | Bända                      | es-PY/en-US                         |
| Peru                                     | PE                       | PER                      | es-PE/en-US                         |
| Filippinerna                              | PH                       | Phl                      | en-PH/en-US                         |
| Pitcairn                         | Pn                       | PCN                      | sv-SE                                 |
| Polen                                   | PL                       | Pol                      | pl-PL/en-US                         |
| Portugal                                 | PT                       | Prt                      | pt-PT/en-US                         |
| Puerto Rico                              | PR                       | Pri                      | es-PR/en-US                         |
| Qatar                                    | QA                       | QAT                      | ar-QA/en-US                         |
| Réunion                                  | RE                       | Reu                      | fr-FR/en-US                         |
| Rumänien                                  | RO                       | Rou                      | ro-RO/en-US                         |
| Ryssland                                   | RU                       | RUS                      | ru-RU/en-US                         |
| Rwanda                                   | RW                       | RWA                      | rw-RW/en-US                         |
| Saba                                     | Xs                       | XSA                      | nl-NL/en-US                         |
| Saint Kitts och Nevis                    | KN                       | Kna                      | en-GB/en-US                         |
| Saint Lucia                              | Lc                       | Lca                      | sv-SE                                 |
| Saint Martin                             | Mf                       | Maf                      | fr-FR/en-US                         |
| Saint-Pierre och Miquelon                | PM                       | Spm                      | fr-FR/en-US                         |
| Saint Vincent och Grenadinerna         | VC                       | VCT                      | sv-SE                                 |
| Saint-Barthélemy                         | BL                       | Blm                      | fr-FR/en-US                         |
| Samoa                                    | WS                       | Wsm                      | sv-SE                                 |
| San Marino                               | Sm                       | Smr                      | it-IT/en-US                         |
| Séo Tomé och Prñncipe                    | ST                       | Stp                      | pt-PT/en-US                         |
| Saudiarabien                             | SA                       | Sau                      | ar-SA/en-US                         |
| Senegal                                  | SN                       | Senatorn                      | wo-SN/en-US                         |
| Serbien                                   | RS                       | Srb                      | sr-Latn-RS / sr-Cyrl-RS / en-US       |
| Seychellerna                               | SC                       | SYC                      | sv-SE                                 |
| Sierra Leone                             | SL                       | Sle                      | sv-SE                                 |
| Singapore                                | SG                       | Stabilitets                      | en-SG / zh-SG / en-US                 |
| Sint Eustatius                           | Xe                       | XSE                      | nl-NL/en-US                         |
| Sint Maarten                             | Sx                       | Sxm                      | sv-SE                                 |
| Slovakien                                 | SK                       | Svk                      | sk-SK/en-US                         |
| Slovenien                                 | SI                       | Svn                      | sl-SI/en-US                         |
| Solomonöarna                          | Sb                       | Slb                      | sv-SE                                 |
| Somalia                                  | SO                       | SOM                      | ar-SA/en-US                         |
| Sydafrika                             | ZA                       | ZAF                      | en-ZA/en-US                         |
| Sydgeorgien och Sydsandwichöarna | Gs                       | Sgs                      | sv-SE                                 |
| Sydsudan                              | SS                       | SSD                      | sv-SE                                 |
| Spanien                                    | ES                       | Esp                      | es-ES / ca-ES / eu-ES /färd-ES / en-US |
| Sri Lanka                                | LK                       | LKA                      | si-LK /en-US                         |
| StDirigering, Ascension, Tristan da Cunha   | SH                       | Shn                      | sv-SE                                 |
| Surinam                                 | SR                       | Sur                      | nl-NL                                 |
| Svalbard                                 | Sj                       | KANT                      | nb-NO/en-US                         |
| Sverige                                   | SE                       | S                      | sv-SE / en-US                         |
| Schweiz                              | CH                       | Che                      | de-CH / fr-CH / it-CH / en-US         |
| Taiwan                                   | TW                       | TWN                      | zh-TW /en-US                         |
| Tadzjikistan                               | Tj                       | TJK                      | tg-Cyrl-TJ /en-US                    |
| Tanzania                                 | TZ                       | TZA                      | en-GB/en-US                         |
| Thailand                                 | TH                       | Tha                      | th-TH/en-US                         |
| Timor-Leste                              | TL                       | TLS                      | pt-PT/en-US                         |
| Togo                                     | TG                       | Tgo                      | fr-FR/en-US                         |
| Tokelau                                  | Tk                       | TKL                      | sv-SE                                 |
| Tonga                                    | TO                       | TON                      | sv-SE                                 |
| Trinidad och Tobago                      | TT                       | Tför                      | en-TT/en-US                         |
| Tunisien                                  | TN                       | Tun                      | ar-TN/en-US                         |
| Turkiet                                   | TR                       | TUR                      | tr-TR/en-US                         |
| Turkmenistan                             | TM                       | Tkm                      | tk-TM/en-US                         |
| Turks- och Caicosöarna                 | TC                       | Tca                      | sv-SE                                 |
| Tuvalu                                   | TV                       | TUV                      | sv-SE                                 |
| Uganda                                   | UG                       | Uga                      | en-GB/en-US                         |
| Ukraina                                  | UA                       | Ukr                      | uk-UA/en-US                         |
| Förenade Arabemiraten                     | AE                       | Är                      | ar-AE/en-US                         |
| Storbritannien                           | GB                       | Gbr                      | en-GB/en-US                         |
| U.S. Outlying Islands                    | UM                       | Umi                      | sv-SE                                 |
| Amerikanska Jungfruöarna                      | VI                       | Vir                      | sv-SE                                 |
| USA                            | USA                       | USA                      | en-US/es-US                         |
| Uruguay                                  | UY                       | Ury                      | es-UY/en-US                         |
| Uzbekistan                               | UZ                       | UZB                      | uz-Latn-CUS / en-US                    |
| Vanuatu                                  | Vu                       | VUT                      | sv-SE                                 |
| Vatikanstaten                             | VA                       | Moms                      | it-IT/en-US                         |
| Venezuela                                | VE                       | VEN                      | es-VE/en-US                         |
| Vietnam                                  | VN                       | Vnm                      | vi-VN/en-US                         |
| Wallis ochUna                        | WF                       | Wlf                      | fr-FR/en-US                         |
| Jemen                                    | Ni                       | YEM                      | ar-YE/en-US                         |
| Zambia                                   | ZM                       | ZMB                      | en-GB/en-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW/en-US                         |

