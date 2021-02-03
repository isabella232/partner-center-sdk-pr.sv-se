---
title: Partnercenteranalys
description: Dokumentation om offentlig API för partner Center Analytics.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4b14ee929f3020079f409be8817e077673d3219f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768847"
---
# <a name="partner-center-analytics---resources"></a>Partnercenter-analys – resurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Med analys-API: et kan du få program mässig åtkomst till data som presenteras i användar upplevelsen.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Dessa scenarier stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="csp-program-azure-usage-analytics"></a>CSP-program: Azure användnings analys

Följande scenario visar hur du använder analys-API: t för att hämta all information om användnings analys i Partner Center Azure.

- [Hämta all information om Azure-användningsanalys](get-all-azure-usage-analytics.md)

Det här scenariot returnerar analys informationen i en samling [Azures användnings](#azure-usage-resource) resurser.

## <a name="azure-usage-resource"></a>Azure Usage-resurs

Representerar alla analys data för Azure-användning.

| Egenskap | Typ | Description |
|----------|------|-------------|
| CustomerTenantId | sträng | Kundens klient-ID. |
| customerName | sträng | Kundens namn. |
| subscriptionId | sträng | Prenumerations-ID. |
| subscriptionName | sträng | Prenumerationens namn. |
| usageDate | sträng | Användnings datum. |
| resourceLocation | sträng | Platsen för data centret, västra Europa, till exempel. |
| meterCategory | sträng | I mätar kategorin, data hantering, till exempel. |
| meterSubcategory | sträng | Under kategori för mätning, till exempel Geo-redundant. |
| meterUnit | sträng | Mätar enheten, till exempel gigabyte eller timmar. |
| reservationOrderId | sträng | Reservations ordningen för en reserverad Azure VM-instans. |
| reservationId | sträng | Reserverade instanser under en speciell RI-ordning. |
| serviceType | sträng | Anger typen av virtuell dator. Till exempel Standard_E4s_v3. |
| quantity | long | Anger de siffror som används i mätar enheten. |

## <a name="csp-program-indirect-resellers-analytics"></a>CSP-program: indirekt åter försäljare Analytics

Följande scenario visar hur du använder analys-API: t för att hämta all information om dina partner Centers indirekta åter försäljare.

- [Hämta all analysinformation för indirekta återförsäljare](get-all-indirect-resellers-analytics.md)

Det här scenariot returnerar analys informationen i en samling med [indirekta åter försäljar](#indirect-resellers-resource) resurser.

## <a name="indirect-resellers-resource"></a>Indirekt åter försäljare resurs

Representerar alla analys data för indirekta åter försäljare.

| Egenskap | Typ | Description |
|----------|------|-------------|
| partnerTenantId | sträng | Klient-ID för den partner som du vill hämta indirekta data om åter försäljare för. |
| id | sträng | ID för indirekt åter försäljare. |
| name | sträng | Namnet på den partner som du vill hämta data om indirekta åter försäljare för. |
| telefonförsäljning | sträng | Marknaden för den partner som du vill hämta data om indirekta åter försäljare för. |
| firstSubscriptionCreationDate | sträng i UTC-datum/tid-format | Skapande datumet för den första prenumerationen som du vill hämta indirekta åter försäljar data från. |
| latestSubscriptionCreationDate | sträng i UTC-datum/tid-format | Skapande datumet för den senaste prenumerationen. |
| firstSubscriptionEndDate | sträng i UTC-datum/tid-format | Första gången en prenumeration avslutades. |
| latestSubscriptionEndDate | sträng i UTC-datum/tid-format | Senaste datum när en prenumeration avslutades. |
| firstSubscriptionSuspendedDate | sträng i UTC-datum/tid-format | Första gången en prenumeration pausades. |
| latestSubscriptionSuspendedDate | sträng i UTC-datum/tid-format | Senaste datum när en prenumeration pausades. |
| firstSubscriptionDeprovisionedDate | sträng i UTC-datum/tid-format | Första gången en prenumeration har avetablerats. |
| latestSubscriptionDeprovisionedDate | sträng i UTC-datum/tid-format | Senaste datum när en prenumeration har avetablerats. |
| subscriptionCount | double | Prenumerations antal för alla mervärdes åter försäljare |
| licenseCount | double | Licens antal för alla mervärdes åter försäljare |
| indirectResellerCount | double | Antal indirekta åter försäljare |

## <a name="csp-program-subscription-analytics"></a>CSP-program: prenumerations analys

Följande scenarier visar hur du använder analys-API: t för att hämta all information om din partner analys för partner Center, filtrera den med en Sök fråga eller gruppera den efter datum eller villkor.

- [Hämta all information om prenumerationsanalys](get-all-subscription-analytics.md)
- [Hämta information om prenumerationsanalys filtrerad efter en sökfråga](get-subscription-analytics-by-search-query.md)
- [Hämta information om prenumerationsanalys grupperad efter datum eller perioder](get-subscription-analytics-grouped-by-dates-or-terms.md)

Alla de här scenarierna returnerar analys informationen i en samling [prenumerations](#subscription-resource) resurser.

## <a name="subscription-resource"></a>Prenumerations resurs

Representerar alla analys data för en prenumeration.

|         Egenskap          |              Typ              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             sträng             |                                              En GUID-formaterad sträng som identifierar kundens klient organisation.                                              |
|       customerName        |             sträng             |                                                               Namnet på kunden.                                                                |
|      customerMarket       |             sträng             |                                                 Landet/regionen som kunden gör affärer med.                                                 |
|            id             |             sträng             |                                                              Prenumerations-ID.                                                              |
|          status           |             sträng             |                                          Prenumerationens status: "aktiv", "inaktive rad" eller "deetablerat".                                           |
|        Namn        |             sträng             |                                                                Produktens namn.                                                                |
|     subscriptionType      |             sträng             |       Prenumerations typ. **Obs!** det här fältet är Skift läges känsligt. De värden som stöds är: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Ett värde som anger om prenumerationen förnyas automatiskt.                                          |
|         Partner         |             sträng             | MPN-ID. För en direkt åter försäljare är den här parametern MPN-ID för partnern. För en indirekt åter försäljare är den här parametern MPN-ID: t för den indirekta åter försäljaren. |
|       friendlyName        |             sträng             |                                                             Namnet på prenumerationen.                                                              |
|        partnerName        |             sträng             |                                              Namnet på partnern som prenumerationen köptes för                                               |
|       providerName        |             sträng             |            När prenumerations transaktionen är för den indirekta åter försäljaren är Providerns namn den indirekta providern som köpte prenumerationen.             |
|    effectiveStartDate     | sträng i UTC-datum/tid-format |                                                           Det datum då prenumerationen startar.                                                            |
|     commitmentEndDate     | sträng i UTC-datum/tid-format |                                                            Det datum då prenumerationen slutar.                                                             |
|    currentStateEndDate    | sträng i UTC-datum/tid-format |                                           Det datum då prenumerationens aktuella status kommer att ändras.                                            |
| trialToPaidConversionDate | sträng i UTC-datum/tid-format |                                 Det datum då prenumerationen konverteras från utvärderings versionen till betald. Standardvärdet är null.                                 |
|      trialStartDate       | sträng i UTC-datum/tid-format |                                Det datum då utvärderings perioden för prenumerationen startades. Standardvärdet är null.                                 |
|       trialEndDate        | sträng i UTC-datum/tid-format |                                  Det datum då utvärderings perioden för prenumerationen upphör. Standardvärdet är null.                                  |
|       lastUsageDate       | sträng i UTC-datum/tid-format |                                        Det datum då prenumerationen senast användes. Standardvärdet är null.                                        |
|     deprovisionedDate     | sträng i UTC-datum/tid-format |                                      Det datum då prenumerationen avetablerades. Standardvärdet är null.                                      |
|      lastRenewalDate      | sträng i UTC-datum/tid-format |                                       Det datum då prenumerationen senast förnyades är standardvärdet null.                                       |
|       licenseCount        |             antal             |                                                             Det totala antalet licenser.                                                              |
|     subscriptionCount     |             antal             |                        Antalet prenumerationer. Obs! det här värdet visas bara i svaret på en agg regerings fråga.                         |

## <a name="search-analytics"></a>Sök analys

> [!NOTE]
> Det krävs inget medlemskap i CSP-programmet för att hämta Sök analys.

Följande scenario visar hur du använder analys-API: n för att hämta all information om din partner Center search Analytics-information.

- [Hämta all information om sökanalys](get-all-search-analytics.md)

Det här scenariot returnerar analys informationen i en samling [Sök](#search-resource) resurser.

## <a name="search-resource"></a>Sök resurs

Representerar alla analys data för en sökning.

| Egenskap | Typ | Description |
|----------|------|-------------|
| companyName | sträng | Fakturerings företagets namn. |
| contactButtonClicked | Boolesk | Anger om kontakt knappen klickade. |
| keywordCountry | sträng | Det land som anges i sökningen. |
| detailsViewed | Boolesk | Anger om Sök information har visats. |
| keywordIndustryFocus | sträng | Branschen att söka inom, t. ex. sjukvård. |
| mpnId | sträng | Microsoft Partner Network-ID (MPN). För en direkt åter försäljare är den här parametern MPN-ID för partnern. För en indirekt åter försäljare är den här parametern MPN-ID: t för den indirekta åter försäljaren. |
| partnerMarket | sträng | Nationella inställningar där partnern genomför verksamhet. |
| keywordProduct | sträng | Den produkt som anges i sökningen. |
| referralSubmitted | Boolesk | Anger om en hänvisning har skickats. |
| searchDate | sträng i UTC-datum/tid-format | Datum när Sök frågan utfördes. |
| keywordSearchText | sträng | Texten som anges i sökningen. |
| searchResultPageViews | long | Antal gånger som partnern kommer upp i Sök resultatet. Ingår endast i ett svar på agg regering.
| contactClicks | long | Antal gånger som kontakt knappen klickade. Ingår endast i ett svar på agg regering.
| referralCount | long | Antalet referenser som genererats från sökningen. Ingår endast i ett svar på agg regering.
| profileViews | long | Antal gånger som partner profilen visades. Ingår endast i ett svar på agg regering.

## <a name="referrals-analytics"></a>Referens analys

> [!NOTE]
> Det krävs inget medlemskap i CSP-programmet för att få hänvisningar till analyser.

Följande scenario visar hur du använder analys-API: t för att hämta all information om dina partner Centers referensinformations analyser.

- [Hämta all information om hänvisningsanalys](get-all-referrals-analytics.md)

Det här scenariot returnerar analys informationen i en samling av [referenser](#referrals-resource) till resurser.

> [!NOTE]
> Referral Analytics är inte tillgängligt för partner Center som drivs av 21Vianet.

## <a name="referrals-resource"></a>Referens resurs

Representerar alla analys data för en hänvisning.

| Egenskap | Typ | Description |
|----------|------|-------------|
| id | sträng | Kundens klient-ID.  |
| status | sträng | Anger om hänvisningen ledde till en kund.  |
| customerMarket | sträng | Landet/regionen som kunden gör affärer med. |
| customerName | sträng | Namnet på kunden. |
| customerOrgSize | sträng | Ett intervall som visar antalet anställda i kundens organisation. Till exempel "10to50employees". |
| acceptedDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen godkändes. |
| acknowledgedDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen bekräftades. |
| archivedDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen arkiverades. |
| declinedDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen nekades. |
| expiredDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen upphörde att gälla. |
| lostDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen bröts. |
| missedDate | sträng i UTC-datum/tid-format | Det datum då hänvisningen missades. |
| createdDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen skapades. |
| skippedDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen hoppades över. |
| wonDate | sträng i UTC-datum/tid-format | Datumet då hänvisningen vanns. |
| partnerMarket | sträng |  Landet/regionen som partnern gör affärer med. |
