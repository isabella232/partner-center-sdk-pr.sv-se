---
title: Partnercenteranalys
description: Dokumentation om det offentliga API:et för Partnercenter Analytics.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9028d5e2bdeb2637e35133b2c6dda739e0024ccc2838368a5276b1482af78d7f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997846"
---
# <a name="partner-center-analytics---resources"></a>Partnercenter-analys – resurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Med Analytics-API:et kan du programmatiskt komma åt data som presenteras i användarupplevelsen.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) De här scenarierna stöder autentisering endast med användarautentiseringsuppgifter.

## <a name="csp-program-azure-usage-analytics"></a>CSP-program: Azure-användningsanalys

Följande scenario visar hur du använder Analytics-API:et för att hämta all användningsanalysinformation i Partnercenter Azure.

- [Hämta all information om Azure-användningsanalys](get-all-azure-usage-analytics.md)

Det här scenariot returnerar din analysinformation i en samling [Azure-användningsresurser.](#azure-usage-resource)

## <a name="azure-usage-resource"></a>Azure-användningsresurs

Representerar alla analytiska data för Azure-användning.

| Egenskap | Typ | Description |
|----------|------|-------------|
| CustomerTenantId | sträng | Kundens klientorganisations-ID. |
| customerName | sträng | Kundens namn. |
| subscriptionId | sträng | Prenumerationsidentifieraren. |
| subscriptionName | sträng | Prenumerationens namn. |
| usageDate | sträng | Användningsdatum. |
| resourceLocation | sträng | Platsen för datacentret, till exempel Europa, västra. |
| meterCategory | sträng | Mätarkategori, till exempel datahantering. |
| meterSubcategory | sträng | Mätarunderkategorin, till exempel geo-redundant. |
| meterUnit | sträng | Mätarenheten, till exempel gigabyte eller timmar. |
| reservationOrderId | sträng | Reservationsbeställningen för en reserverad Azure VM-instans. |
| reservationId | sträng | Reserverade instanser under en specifik RI-beställning. |
| serviceType | sträng | Anger typ av virtuell dator. Till exempel Standard_E4s_v3. |
| quantity | long | Anger de tal som används i mätarenheten. |

## <a name="csp-program-indirect-resellers-analytics"></a>CSP-program: analys av indirekta återförsäljare

Följande scenario visar hur du använder Analytics-API:et för att hämta all analysinformation om indirekta återförsäljare i Partnercenter.

- [Hämta all analysinformation för indirekta återförsäljare](get-all-indirect-resellers-analytics.md)

Det här scenariot returnerar din analysinformation i en samling [indirekta återförsäljares](#indirect-resellers-resource) resurser.

## <a name="indirect-resellers-resource"></a>Resurs för indirekta återförsäljare

Representerar alla analytiska data för indirekta återförsäljare.

| Egenskap | Typ | Description |
|----------|------|-------------|
| partnerTenantId | sträng | Klientorganisations-ID för den partner som du vill hämta indirekta återförsäljares data för. |
| id | sträng | Id för indirekt återförsäljare. |
| name | sträng | Namnet på den partner som du vill hämta indirekta återförsäljares data för. |
| Marknaden | sträng | Partnerns marknad som du vill hämta data om indirekta återförsäljare för. |
| firstSubscriptionCreationDate | sträng i UTC-datum/tid-format | Skapandedatumet för den första prenumerationen baserat på vilken du vill hämta data för indirekta återförsäljare. |
| latestSubscriptionCreationDate | sträng i UTC-datum/tid-format | Skapandedatumet för den senaste prenumerationen. |
| firstSubscriptionEndDate | sträng i UTC-datum/tid-format | Första gången någon prenumeration avslutades. |
| latestSubscriptionEndDate | sträng i UTC-datum/tid-format | Senaste datum då en prenumeration avslutades. |
| firstSubscriptionSuspendedDate | sträng i UTC-datum/tid-format | Första gången någon prenumeration pausas. |
| latestSubscriptionSuspendedDate | sträng i UTC-datum/tid-format | Senaste datum då en prenumeration pausades. |
| firstSubscriptionDeprovisionedDate | sträng i UTC-datum/tid-format | Första gången någon prenumeration avetableades. |
| latestSubscriptionDeprovisionedDate | sträng i UTC-datum/tid-format | Senaste datum då en prenumeration avetableades. |
| subscriptionCount | double | Prenumerationsantal för alla återförsäljare med mervärde |
| licenseCount | double | Licensantal för alla återförsäljare med mervärde |
| indirectResellerCount | double | Antal indirekta återförsäljare |

## <a name="csp-program-subscription-analytics"></a>CSP-program: prenumerationsanalys

Följande scenarier visar hur du använder Analytics-API:et för att hämta all prenumerationsanalysinformation i Partnercenter, filtrera den med en sökfråga eller gruppera den efter datum eller villkor.

- [Hämta all information om prenumerationsanalys](get-all-subscription-analytics.md)
- [Hämta information om prenumerationsanalys filtrerad efter en sökfråga](get-subscription-analytics-by-search-query.md)
- [Hämta information om prenumerationsanalys grupperad efter datum eller perioder](get-subscription-analytics-grouped-by-dates-or-terms.md)

Alla dessa scenarier returnerar din analysinformation i en samling [prenumerationsresurser.](#subscription-resource)

## <a name="subscription-resource"></a>Prenumerationsresurs

Representerar alla analysdata för en prenumeration.

|         Egenskap          |              Typ              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             sträng             |                                              En GUID-formaterad sträng som identifierar kundens klientorganisation.                                              |
|       customerName        |             sträng             |                                                               Namnet på kunden.                                                                |
|      customerMarket       |             sträng             |                                                 Land/region som kunden gör affärer i.                                                 |
|            id             |             sträng             |                                                              Prenumerationsidentifieraren.                                                              |
|          status           |             sträng             |                                          Prenumerationsstatus: "ACTIVE", "SUSPENDED" eller "DEPROVISIONED".                                           |
|        Productname        |             sträng             |                                                                Namnet på produkten.                                                                |
|     subscriptionType      |             sträng             |       Prenumerationstyp. **Obs!** Det här fältet är case-sensitive. Värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Ett värde som anger om prenumerationen förnyas automatiskt.                                          |
|         partnerId         |             sträng             | ID Microsoft Partner Network (MPN). För en direktåterförsäljare är den här parametern MPN-ID för partnern. För en indirekt återförsäljare är den här parametern MPN-ID:t för den indirekta återförsäljaren. |
|       friendlyName        |             sträng             |                                                             Namnet på prenumerationen.                                                              |
|        partnerName        |             sträng             |                                              Namnet på den partner som prenumerationen köptes för                                               |
|       providerName        |             sträng             |            När prenumerationstransaktionen är för den indirekta återförsäljaren är providernamnet den indirekta leverantör som köpte prenumerationen.             |
|    effectiveStartDate     | sträng i UTC-datum/tid-format |                                                           Det datum då prenumerationen startar.                                                            |
|     commitmentEndDate     | sträng i UTC-datum/tid-format |                                                            Det datum då prenumerationen upphör.                                                             |
|    currentStateEndDate    | sträng i UTC-datum/tid-format |                                           Det datum då prenumerationens aktuella status ändras.                                            |
| trialToDateConversionDate | sträng i UTC-datum/tid-format |                                 Det datum då prenumerationen konverteras från utvärderingsversion till betald. Standardvärdet är null.                                 |
|      trialStartDate       | sträng i UTC-datum/tid-format |                                Det datum då utvärderingsperioden för prenumerationen startade. Standardvärdet är null.                                 |
|       trialEndDate        | sträng i UTC-datum/tid-format |                                  Det datum då utvärderingsperioden för prenumerationen upphör. Standardvärdet är null.                                  |
|       lastUsageDate       | sträng i UTC-datum/tid-format |                                        Det datum då prenumerationen senast användes. Standardvärdet är null.                                        |
|     deprovisionedDate     | sträng i UTC-datum/tid-format |                                      Det datum då prenumerationen avetableades. Standardvärdet är null.                                      |
|      lastRenewalDate      | sträng i UTC-datum/tid-format |                                       Det datum då prenumerationen senast förnyades. Standardvärdet är null.                                       |
|       licenseCount        |             antal             |                                                             Det totala antalet licenser.                                                              |
|     subscriptionCount     |             antal             |                        Antalet prenumerationer. Obs! Det här värdet visas bara som svar på en sammansättningsfråga.                         |

## <a name="search-analytics"></a>Sökanalys

> [!NOTE]
> CSP-programmedlemskap krävs inte för att få sökanalys.

I följande scenario visas hur du använder Analytics-API:et för att hämta all sökanalysinformation i Partnercenter.

- [Hämta all information om sökanalys](get-all-search-analytics.md)

Det här scenariot returnerar din analysinformation i en samling [sökresurser.](#search-resource)

## <a name="search-resource"></a>Sök resurs

Representerar alla analytiska data för en sökning.

| Egenskap | Typ | Description |
|----------|------|-------------|
| companyName | sträng | Faktureringsföretagets namn. |
| contactButtonClicked | Boolesk | Anger om du klickade på kontaktknappen. |
| keywordCountry | sträng | Landet som anges i sökningen. |
| detailsViewed | Boolesk | Anger om sökinformationen visades. |
| keywordIndustryFocus | sträng | Branschen att söka inom, till exempel sjukvård. |
| mpnId | sträng | ID Microsoft Partner Network (MPN). För en direktåterförsäljare är den här parametern MPN-ID för partnern. För en indirekt återförsäljare blir den här parametern MPN-ID:t för den indirekta återförsäljaren. |
| partnerMarket | sträng | Språk för att se var partnern utför sin verksamhet. |
| keywordProduct | sträng | Den produkt som anges i sökningen. |
| referralSubmitted | Boolesk | Anger om en referens har skickats. |
| searchDate | sträng i UTC-datum/tid-format | Datum då sökfrågan uppstod. |
| keywordSearchText | sträng | Den text som anges i sökningen. |
| searchResultPageViews | long | Antal gånger som partnern kom upp i sökresultatet. En del av ett svar endast på aggregering.
| contactClicks | long | Antal gånger som kontaktknappen klickades. En del av ett svar endast på aggregering.
| referralCount | long | Antal referenser som genererats från sökningen. En del av ett svar endast på aggregering.
| profileViews | long | Antal gånger som partnerprofilen visades. En del av ett svar endast på aggregering.

## <a name="referrals-analytics"></a>Referensanalys

> [!NOTE]
> CSP-programmedlemskap krävs inte för att få referensanalys.

Följande scenario visar hur du använder Analytics-API:et för att hämta all referensanalysinformation i Partnercenter.

- [Hämta all information om hänvisningsanalys](get-all-referrals-analytics.md)

Det här scenariot returnerar din analysinformation i en samling [referensresurser.](#referrals-resource)

> [!NOTE]
> Referensanalys är inte tillgängligt för Partnercenter som drivs av 21Vianet.

## <a name="referrals-resource"></a>Referensresurs

Representerar alla analytiska data för en referens.

| Egenskap | Typ | Description |
|----------|------|-------------|
| id | sträng | Kundens klientorganisations-ID.  |
| status | sträng | Anger om hänvisningen ledde till en kund.  |
| customerMarket | sträng | Landet/regionen som kunden gör affärer i. |
| customerName | sträng | Namnet på kunden. |
| customerOrgSize | sträng | Ett intervall som anger antalet anställda i kundens organisation. Till exempel "10to50employees". |
| acceptedDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen godkändes. |
| acknowledgedDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen bekräftades. |
| archivedDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen arkiverades. |
| declinedDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen avvisades. |
| expiredDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen upphörde att gälla. |
| lostDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen förlorades. |
| missedDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen missades. |
| createdDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen skapades. |
| skippedDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen överhoppades. |
| wonDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen vanns. |
| partnerMarket | sträng |  Land/region som partnern gör affärer i. |
