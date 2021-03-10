---
title: Partnercenter – språk och nationella inställningar som stöds
description: Lista över ISO2 och ISO3 som stöds för partner Center.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: d486eed96586eb2577577eac44fa9e866479e825
ms.sourcegitcommit: 9bc35836b389fdf083b278128a2e9ec994919f1c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/10/2021
ms.locfileid: "102532846"
---
# <a name="partner-center-supported-languages-and-locales"></a>Partnercenter – språk och nationella inställningar som stöds

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Vissa API: er för partner Center kräver ett värde som anger språk, land eller region. Till exempel kräver [partner Center rest-huvudet](headers.md) X-locale ett värde ofta i formatet "språk land" ("en-US" indikerar "engelska-USA").

I Partner Center Managed API: erna [CountryValidationRules/dotNet/API/Microsoft. Store. Partnercenter. Models. CountryValidationRules. CountryValidationRules) och klassen [OfferCategory. locale/dotNet/API/Microsoft. Store. Partnercenter. Models. OfferCategory. locale), [ServiceRequest. CountryCode/dotNet/API/Microsoft. Store. Partnercenter. Models. servicerequests. ServiceRequest. CountryCode) eller [CustomerBillingProfile. Culture/dotNet/API/Microsoft. Store. Partnercenter. Models. Customers. CustomerBillingProfile. Culture) kräver sträng värden som anger ett språk eller land/region (i form av en ISO2 språkkod eller ISO3 landskod), ett språk eller en kultur (ett språk-ID kombinerat med en landskod).

I följande tabell visas de språk koder för kulturer och International Standards Organization (ISO) som stöds i API: er för partner Center.

| Land/region                           | ISO alpha 2 landkod | ISO alpha 3 landkod | Kultur (er) som stöds                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afghanistan                              | AF                       | AFG                      | PS-AF/en-US                         |
| Åland                            | AX                       | ALA                      | sa-SE/en-US                         |
| Albanien                                  | AL                       | ALB                      | kv-AL/en-US                         |
| Algeriet                                  | DZ                       | DZA                      | ar-DZ/en-US                         |
| Amerikanska Samoa                           | AS                       | ASM                      | sv-SE                                 |
| Andorra                                  | AD                       | AND                      | ca-ES/en-US                         |
| Angola                                   | AO                       | SEN                      | pt-PT/en-US                         |
| Anguilla                                 | AI                       | AIA                      | sv-SE                                 |
| Antarktis                               | AQ                       | ATA                      | sv-SE                                 |
| Antigua och Barbuda                      | AG                       | ATG                      | sv-SE                                 |
| Argentina                                | AR                       | ARG                      | ES-AR/en-US                         |
| Armenien                                  | AM                       | ARM                      | hy – FM/en – US                         |
| Aruba                                    | AW                       | ABW                      | nl-NL/en-US                         |
| Australien                                | AU                       | ÖSTRA                      | en-AU/en-US                         |
| Österrike                                  | AT                       | AUT                      | de-på/en – US                         |
| Azerbajdzjan                               | AZ                       | AZE                      | AZ-latn-AZ/en-US                    |
| Bahamas                                  | BS                       | BHS                      | en-GB/en-US                         |
| Bahrain                                  | BH                       | BHR                      | ar-BH/en-US                         |
| Bangladesh                               | BD                       | BGD                      | BN – BD/en-US                         |
| Barbados                                 | BB                       | BRB                      | en-GB/en-US                         |
| Vitryssland                                  | BY                       | BLR                      | måste vara av/en-US                         |
| Belgien                                  | BE                       | BEL                      | fr-är/nl-är/en-US                 |
| Belize                                   | BZ                       | BLZ                      | en-BZ/en-US                         |
| Benin                                    | BJ                       | BEN                      | fr-FR/en-US                         |
| Bermuda                                  | BM                       | BMU                      | en-GB/en-US                         |
| Bhutan                                   | BT                       | BTN                      | sv-SE                                 |
| Bolivia                                  | BO                       | BOL                      | ES-BO/en – US                         |
| Bonaire                                  | BQ                       | BES                      | nl-NL/en-US                         |
| Bosnien och Hercegovina                   | BA                       | BIH                      | BS-latn – BA/en-US                    |
| Botswana                                 | BW                       | BWA                      | en-GB/en-US                         |
| Bouvetön                            | BV                       | BVT                      | NB-NO/en – US                         |
| Brasilien                                   | BR                       | BRA                      | pt-BR/en – US                         |
| Brittiska territoriet i Indiska Oceanen           | I/O                       | Sakernas Internet                      | sv-SE                                 |
| Brittiska Jungfruöarna                   | VG                       | VGB                      | sv-SE                                 |
| Brunei                                   | BN                       | BRN                      | MS-BN/en-US                         |
| Bulgarien                                 | BG                       | BGR                      | BG-BG/en-US                         |
| Burkina Faso                             | BF                       | BFA                      | fr-FR/en-US                         |
| Burundi                                  | BI                       | BDI                      | fr-FR/en-US                         |
| Cabo Verde                               | CV                       | CPV                      | PT-CV/en-US                         |
| Kambodja                                 | KH                       | KHM                      | km – KH/sv-US                         |
| Kamerun                                 | CM                       | CMR                      | fr-FR/en-US                         |
| Kanada                                   | CA                       | SKRIVA                      | fr-CA/en-US                         |
| Caymanöarna                           | KY                       | CYM                      | en-GB/en-US                         |
| Centralafrikanska Republiken                 | CF                       | CAF                      | fr-FR/en-US                         |
| Tchad                                     | TD                       | TCD                      | fr-FR/en-US                         |
| Chile                                    | CL                       | CHL                      | ES-CL/en – US                         |
| Kina                                    | CN                       | CHN                      | zh-CN/en-US                         |
| Julön                         | CX                       | CXR                      | sv-SE                                 |
| Kokosöarna                  | CC                       | CCK                      | sv-SE                                 |
| Colombia                                 | CO                       | COL                      | ES-CO/sv-US                         |
| Komorerna                                  | METER                       | COM                      | fr-FR/en-US                         |
| Kongo                                    | 0,05                       | KUGG HJULS                      | fr-FR/en-US                         |
| Kongo (DR)                              | CD                       | COD                      | fr-FR/en-US                         |
| Cooköarna                             | CK                       | COK                      | sv-SE                                 |
| Costa Rica                               | CR                       | CRI                      | ES – CR/en – US                         |
| Côte d'Ivoire                            | CI                       | CIV                      | fr-FR/en-US                         |
| Kroatien                                  | HR                       | HRV                      | HR – HR/en – US                         |
| Curaçao                                  | FELAKTIG                       | CUW                      | nl-NL/en-US                         |
| Cypern                                   | CY                       | CYP                      | El-GR/en-US                         |
| Czechia                                  | CZ                       | CZE                      | CS-CZ/en-US                         |
| Danmark                                  | DK                       | DNK                      | da-DK/en-US                         |
| Djibouti                                 | DJ                       | DJI                      | fr-FR/en-US                         |
| Dominica                                 | DM                       | DMA                      | sv-SE                                 |
| Dominikanska republiken                       | DO                       | SAMLA                      | ES-gör/en-US                         |
| Ecuador                                  | EC                       | MOTVÄRDE                      | ES-EC/en – US                         |
| Egypten                                    | EG                       | EGY                      | ar-tex/en-US                         |
| El Salvador                              | SV                       | SLV                      | ES – sa/en – US                         |
| Ekvatorialguinea                        | GQ                       | GNQ                      | es-ES/en-US                         |
| Eritrea                                  | ER                       | ERI                      | ar-SA/en-US                         |
| Estland                                  | EE                       | EST                      | et-EE/en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | sv-SE                                 |
| Etiopien                                 | ET                       | ETH                      | am-ET/en-US                         |
| Falklandsöarna                         | FK                       | FLK                      | sv-SE                                 |
| Färöarna                            | DETALJERADE                       | IMPORTERAS                      | FO-FO/sv – USA                         |
| Fiji                                     | FJ                       | FJI                      | en-GB/en-US                         |
| Finland                                  | FI                       | FIN                      | fi-FI/sa-FI/en-US                 |
| Frankrike                                   | FR                       | FRA                      | fr-FR/en-US                         |
| Franska Guyana                            | GF                       | GUF                      | fr-FR/en-US                         |
| Franska Polynesien                         | PF                       | PYF                      | fr-FR/en-US                         |
| Franska sydterritorierna              | TF                       | ATF                      | fr-FR/en-US                         |
| Gabon                                    | Allmän tillgänglighet (GA)                       | GAB                      | fr-FR/en-US                         |
| Gambia                                   | GM                       | GMB                      | sv-SE                                 |
| Georgia                                  | GE                       | GEOGRAFISKA                      | ka-GE en-US                         |
| Tyskland                                  | DE                       | DEU                      | de/DE/en – US                         |
| Ghana                                    | GH                       | GHA                      | en-GB/en-US                         |
| Gibraltar                                | ETER                       | GIB                      | sv-SE                                 |
| Grekland                                   | GR                       | GRC                      | El-GR/en-US                         |
| Grönland                                | HUVUD                       | GRL                      | da-DK/en-US                         |
| Grenada                                  | GD                       | GRD                      | sv-SE                                 |
| Guadeloupe                               | GP                       | LABORATORIESED                      | fr-FR/en-US                         |
| Guam                                     | GU                       | Arabic                      | sv-SE                                 |
| Guatemala                                | GT                       | GTM                      | ES-GT/en-US                         |
| Guernsey                                 | GG                       | GGY                      | sv-SE                                 |
| Guinea                                   | GN                       | GIN                      | fr-FR/en-US                         |
| Guinea-Bissau                            | GW                       | GNB                      | pt-PT/en-US                         |
| Guyana                                   | GY                       | GUY                      | sv-SE                                 |
| Haiti                                    | HT                       | HTI                      | fr-FR/en-US                         |
| Heard- och McDonaldöarna        | IGNERINGSALGORITM                       | HMD                      | sv-SE                                 |
| Honduras                                 | HN                       | HND                      | ES-HN/en – US                         |
| Folkrepubliken Kinas särskilda administrativa region Hongkong                            | HK                       | HKG                      | zh-HK/en-US                         |
| Ungern                                  | HU                       | HUN                      | hu – HU/en – USA                         |
| Island                                  | IS                       | ISL                      | är-är/en-US                         |
| Indien                                    | IN                       | IND                      | a-IN/Hi-IN/an-US                 |
| Indonesien                                | ID                       | IDN                      | ID-ID/en-US                         |
| Irak                                     | IQ                       | PLATSHÅLLARE                      | ar-SWEETIQ/en-US                         |
| Irland                                  | IE                       | IRL                      | en-IE/en-US                         |
| Isle of Man                              | Snabbmeddelanden                       | IMN                      | sv-SE                                 |
| Israel                                   | IL                       | ISR                      | He-IL/en-US                         |
| Italien                                    | IT                       | ITA                      | IT – IT/en – US                         |
| Jamaica                                  | JM                       | FACK                      | en-JM/en-US                         |
| Jan Mayen                                | XJ                       | XJA                      | NB-NO/en – US                         |
| Japan                                    | JP                       | JPN                      | ja-JP/en-US                         |
| Jersey                                   | JE                       | JEY                      | sv-SE                                 |
| Jordanien                                   | JO                       | JOR                      | ar-JO/en-US                         |
| Kazakstan                               | KZ                       | KAZ                      | KK – KZ/en-US                         |
| Kenya                                    | KE                       | KEN                      | SW-KE/en-US                         |
| Kiribati                                 | KI                       | KIR                      | sv-SE                                 |
| Korea                                    | KR                       | KOR                      | ko-KR/en – US                         |
| Kosovo                                   | XK                       | XKS                      | sv-SE                                 |
| Kuwait                                   | KW                       | KWT                      | ar-KW/en – US                         |
| Kirgizistan                               | KG                       | KGZ                      | Ky – KG/en – US                         |
| Laos                                     | LA                       | Laos                      | Lo-LA/en-US                         |
| Lettland                                   | LV                       | LVA                      | LV-LV/en-US                         |
| Libanon                                  | LB                       | LBN                      | ar-LB/en-US                         |
| Lesotho                                  | LS                       | LSO                      | sv-SE                                 |
| Liberia                                  | LR                       | LBR                      | sv-SE                                 |
| Libyen                                    | LY                       | LBY                      | ar-LY/en-US                         |
| Liechtenstein                            | LI                       | FINNS                      | de-LI/sv-US                         |
| Litauen                                | LT                       | LTU                      | lt-LT/sv-se                         |
| Luxemburg                               | LU                       | LUX                      | de-LU/fr-LU/en-US                 |
| Folkrepubliken Kinas särskilda administrativa region Macao                                | MO                       | OS                      | zh – MO/en – USA                         |
| F.d. jugoslaviska republiken Makedonien                          | MK                       | MKD                      | MK-MK/en-US                         |
| Madagaskar                               | MG                       | MDG                      | fr-FR/en-US                         |
| Malawi                                   | MW                       | MWI                      | sv-SE                                 |
| Malaysia                                 | MY                       | MYS                      | en-MY/en-US                         |
| Maldiverna                                 | MV                       | MDV                      | DV-MV/en-US                         |
| Mali                                     | ML                       | MLI                      | fr-FR/en-US                         |
| Malta                                    | MT                       | MLT                      | MT-MT/en-US                         |
| Marshallöarna                         | MH                       | MHL                      | sv-SE                                 |
| Martinique                               | MQ                       | MTQ                      | fr-FR/en-US                         |
| Mauretanien                               | MR                       | MRT                      | ar-SA/en-US                         |
| Mauritius                                | MK                       | MUS                      | en-GB/en-US                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR/en-US                         |
| Mexico                                   | MX                       | MEX                      | ES-MX/en-US                         |
| Mikronesien                               | FM                       | FSM                      | sv-SE                                 |
| Moldavien                                  | MD                       | MDA                      | RO-RO/en-US                         |
| Monaco                                   | MC                       | MCO                      | fr-MC/en-US                         |
| Mongoliet                                 | MN                       | MNG                      | mn-MN/sv-US                         |
| Montenegro                               | ME                       | MNE                      | SR-latn – mig/en-US                    |
| Montserrat                               | MS                       | MSR                      | sv-SE                                 |
| Marocko                                  | MA                       | Mar                      | ar-MA/en-US                         |
| Moçambique                               | MZ                       | MOZ                      | pt-PT                                 |
| Myanmar                                  | MM                       | MMR                      | sv-SE                                 |
| Namibia                                  | NA                       | Vietnam                      | en-GB/en-US                         |
| Nauru                                    | NR                       | NRU                      | sv-SE                                 |
| Nepal                                    | NP                       | NPL                      | Ne-NP/en-US                         |
| Bonaire, Curaçao, Saba, Sint Eustatius och Sint Maarten                     | DEN                       | ANT                      | sv-SE                                 |
| Nederländerna                         | NL                       | NLD                      | nl-NL/en-US                         |
| Nya Kaledonien                            | NC                       | NCL                      | fr-FR/en-US                         |
| Nya Zeeland                              | NZ                       | NZL                      | en-NZ/en-US                         |
| Nicaragua                                | NI                       | NIC                      | ES-NI/en – US                         |
| Niger                                    | NE                       | NER                      | fr-FR/en-US                         |
| Nigeria                                  | NG                       | NGA                      | ha-latn – NG/en-US                    |
| Niue                                     | NU                       | NIU                      | sv-SE                                 |
| Norfolkön                           | NF                       | NFK                      | sv-SE                                 |
| Nordmarianerna                 | MP                       | MNP                      | sv-SE                                 |
| Norge                                   | NO                       | NOR                      | NB-NO/en – US                         |
| Oman                                     | OM                       | OMN                      | ar-OM/en-US                         |
| Pakistan                                 | PK                       | PAK                      | din-PK/en-US                         |
| Palau                                    | PW                       | PLW                      | sv-SE                                 |
| Palestinska myndigheten                    | PS                       | PSE                      | ar-SA/en-US                         |
| Panama                                   | PA                       | PAN                      | ES-PA/en-US                         |
| Papua Nya Guinea                         | P1500                       | PNG                      | sv-SE                                 |
| Paraguay                                 | PY                       | PRY                      | ES-PY/en-US                         |
| Peru                                     | PE                       | PER                      | ES-PE/en-US                         |
| Filippinerna                              | PH                       | PHL                      | en-PH/en-US                         |
| Pitcairn                         | PN                       | PCN                      | sv-SE                                 |
| Polen                                   | PL                       | POL                      | PL-PL/en-US                         |
| Portugal                                 | PT                       | PRT                      | pt-PT/en-US                         |
| Puerto Rico                              | PR                       | PRI                      | ES-PR/en – US                         |
| Qatar                                    | QA                       | QAT                      | ar-frågor/en-US                         |
| Réunion                                  | RE                       | REU                      | fr-FR/en-US                         |
| Rumänien                                  | RO                       | ROU                      | RO-RO/en-US                         |
| Ryssland                                   | RU                       | RUS                      | ru-RU/en-US                         |
| Rwanda                                   | RW                       | RWA                      | RW-RW/en-US                         |
| Saba                                     | X                       | XSA                      | nl-NL/en-US                         |
| Saint Kitts och Nevis                    | KN                       | KNA                      | en-GB/en-US                         |
| Saint Lucia                              | LC                       | LCA                      | sv-SE                                 |
| Saint Martin                             | MF                       | MAF                      | fr-FR/en-US                         |
| Saint-Pierre och Miquelon                | PM                       | SPM                      | fr-FR/en-US                         |
| Saint Vincent och Grenadinerna         | VC                       | VCT                      | sv-SE                                 |
| Saint-Barthélemy                         | BL                       | BLM                      | fr-FR/en-US                         |
| Samoa                                    | WS                       | WSM                      | sv-SE                                 |
| San Marino                               | SM                       | SMR                      | IT – IT/en – US                         |
| São Tomé och Príncipe                    | ST                       | STP                      | pt-PT/en-US                         |
| Saudiarabien                             | SA                       | SAU                      | ar-SA/en-US                         |
| Senegal                                  | SN                       | AVSÄN                      | vå – SN/en-US                         |
| Serbien                                   | RS                       | SRB                      | SR-latn-RS/sr-cyrl-RS/en-US       |
| Seychellerna                               | SC                       | SYC                      | sv-SE                                 |
| Sierra Leone                             | SL                       | SLE                      | sv-SE                                 |
| Singapore                                | SG                       | SGP                      | en-TG/zh-SG/en-US                 |
| Sint Eustatius                           | XE                       | XSE                      | nl-NL/en-US                         |
| Sint Maarten                             | NÄTVERKSANSLUTNING                       | SXM                      | sv-SE                                 |
| Slovakien                                 | SK                       | SVK                      | sk-SK/en-US                         |
| Slovenien                                 | SI                       | SVN                      | SL-SI/en-US                         |
| Solomonöarna                          | SA                       | SLB                      | sv-SE                                 |
| Somalia                                  | SO                       | RAPPORTERAT                      | ar-SA/en-US                         |
| Sydafrika                             | ZA                       | ZAF                      | en-ZA/en-US                         |
| Sydgeorgien och Sydsandwichöarna | GS                       | SGS                      | sv-SE                                 |
| Sydsudan                              | SS                       | SSD                      | sv-SE                                 |
| Spanien                                    | ES                       | ESP                      | es-ES/ca-ES/EU-ES/gl-ES/en-US |
| Sri Lanka                                | LK                       | LKA                      | Si-LK/en – US                         |
| Saint Helena, Ascension, Tristan da Cunha   | SH                       | SHN                      | sv-SE                                 |
| Surinam                                 | SR                       | SUR                      | nl-NL                                 |
| Svalbard                                 | SJ                       | SJM                      | NB-NO/en – US                         |
| Sverige                                   | SE                       | Sverige                      | sa-SE/en-US                         |
| Schweiz                              | CH                       | CACHELAGRA                      | on-CH/fr-CH/IT-CH/an-US         |
| Taiwan                                   | TW                       | TWN                      | zh-TW/sv-USA                         |
| Tadzjikistan                               | TJ                       | TJK                      | TG-cyrl-TJ/en-US                    |
| Tanzania                                 | TZ                       | TZA                      | en-GB/en-US                         |
| Thailand                                 | TH                       | THA                      | Th/sv – USA                         |
| Timor-Leste                              | TL                       | TLS                      | pt-PT/en-US                         |
| Togo                                     | TG                       | TGO                      | fr-FR/en-US                         |
| Tokelau                                  | TK                       | TKL                      | sv-SE                                 |
| Tonga                                    | TO                       | TON                      | sv-SE                                 |
| Trinidad och Tobago                      | TT                       | PÅSKYNDA                      | en-TT/en-US                         |
| Tunisien                                  | TN                       | TUN                      | ar-TN/en-US                         |
| Turkiet                                   | TR                       | TUR                      | TR-TR/en-US                         |
| Turkmenistan                             | TM                       | TKM                      | TK-TM/en-US                         |
| Turks- och Caicosöarna                 | TC                       | TCA                      | sv-SE                                 |
| Tuvalu                                   | TV                       | TUV                      | sv-SE                                 |
| Uganda                                   | UG                       | UGA                      | en-GB/en-US                         |
| Ukraina                                  | UA                       | UKR                      | Storbritannien – UA/en-US                         |
| Förenade Arabemiraten                     | AE                       | TILLHANDAHÅLLS                      | ar-AE/en-US                         |
| Storbritannien                           | GB                       | GBR                      | en-GB/en-US                         |
| Amerikanska öar                    | UM                       | UMI                      | sv-SE                                 |
| Amerikanska jungfru öarna                      | VI                       | VIR                      | sv-SE                                 |
| USA                            | USA                       | USA                      | en-US/es – USA                         |
| Uruguay                                  | UY                       | URY                      | ES-UY/en – US                         |
| Uzbekistan                               | UZ                       | UZB                      | uz-latn-UZ/en-US                    |
| Vanuatu                                  | ANTECKNING                       | VUT                      | sv-SE                                 |
| Vatikanstaten                             | VA                       | LANDKODEN                      | IT – IT/en – US                         |
| Venezuela                                | VE                       | VEN                      | ES-VE/en – USA                         |
| Vietnam                                  | VN                       | VNM                      | Vi-VN/en – US                         |
| Wallis och Futuna                        | WF                       | WLF                      | fr-FR/en-US                         |
| Jemen                                    | CHANSEN                       | YEM                      | ar-julen/en-US                         |
| Zambia                                   | ZM                       | ZMB                      | en-GB/en-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW/en-US                         |

