---
title: Faktura resurser
description: 'Flera faktura relaterade resurser är tillgängliga via API: er för partner Center. Dessa resurser är relaterade till information om faktura och rad objekt.'
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd2caefe4ae18c81a31083d084f1e87da1288dd9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768904"
---
# <a name="invoice-resources"></a>Faktura resurser

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Följande faktura relaterade resurser är tillgängliga via API: er för partner Center.

## <a name="invoice"></a>Faktura

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| id | sträng | Faktura-ID. |
| invoiceDate | sträng i UTC-datum/tid-format | Datumet då fakturan genererades. |
| billingPeriodStartDate | sträng i UTC-datum/tid-format | Fakturerings periodens start datum i UTC. |
| billingPeriodEndDate | sträng i UTC-datum/tid-format   | Fakturerings periodens slutdatum i UTC. |
| totalCharges | antal | De totala kostnaderna. Innehåller avgifter för transaktioner och eventuella justeringar.     |
| paidAmount | antal  | Det belopp som betalas av partnern. Negativt om en betalning togs emot.  |
| currencyCode | sträng  | En kod som anger vilken valuta som används för alla faktura objekts belopp och total summor. |
| currencySymbol  | sträng | Valuta symbolen som används för alla faktura objekts belopp och total summor. |
| pdfDownloadLink | sträng  | En länk för att ladda ned fakturan i PDF-format. Den här länken returneras inte som en del av Sök resultaten och fylls bara i om fakturan nås av ID. Den här länken upphör att gälla om 30 minuter. |
| invoiceDetails  | matris med [InvoiceDetail](#invoicedetail) -objekt  | Faktura informationen.  |
| föreslå      | matris med [faktura](#invoice) objekt   | Ändringarna av den här fakturan.  |
| documentType    | sträng | Fakturans dokument typ: "kredit anmärkning", "faktura". |
| amendsOf        | sträng | Referens numret för dokumentet som det här dokumentet är en ändring i.  |
| invoiceType     | sträng  | Typ av faktura: "återkommande", "en \_ tid".   |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks)  | Resurs länkarna.  |
| dokumentattribut      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.  |

## <a name="invoicedetail"></a>InvoiceDetail

En faktura innehåller en samling av fakturerade artiklar, och varje objekt representeras av en InvoiceDetail-resurs.

| Egenskap            | Typ                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | sträng                                                         | Typ av faktura information: "ingen", "användnings \_ rads \_ objekt", "fakturerings \_ rad \_ objekt". |
| billingProvider     | sträng                                                         | Fakturerings leverantören: "ingen", "Office", "Azure" eller "Azure \_ data \_ Marketing".         |
| Länkar               | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna.                                                               |
| dokumentattribut          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Varje enskild avgift i en faktura representeras som en InvoiceLineItem.

| Egenskap            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | sträng                                                         | Typ av faktura rads objekt: "ingen", "användnings \_ rads \_ objekt", "fakturerings \_ rad \_ objekt". |
| billingProvider     | sträng                                                         | Fakturerings leverantören: "ingen", "Office", "Azure" eller "Azure \_ data \_ Marketing".            |
| dokumentattribut          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Beskriver en översikt över saldot och den totala kostnaden för en faktura.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | antal                                                         | Fakturans saldo. Detta är den totala mängden obetalda fakturor. |
| currencyCode             | sträng                                                         | En kod som anger valutan som används för saldobeloppet.       |
| currencySymbol           | sträng                                                         | Valuta symbolen som används.                                             |
| accountingDate           | sträng i UTC-datum/tid-format                                 | Det datum då saldobeloppet senast uppdaterades.                         |
| firstInvoiceCreationDate | sträng i UTC-datum/tid-format                                 | Datumet då den första fakturan för kunden skapades.              |
| lastPaymentDate          | sträng i UTC-datum/tid-format                                 | Datumet för den senaste betalningen.                                         |
| lastPaymentAmount        | antal                                                         | Den senaste Betalningens belopp.                                       |
| latestInvoiceDate        | sträng i UTC-datum/tid-format                                 | Datumet då den sista fakturan för kunden skapades.               |
| information                  | matris med [InvoiceSummaryDetail](#invoicesummarydetail) -objekt | Faktura sammanfattnings information.                                           |
| Länkar                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Resurs länkarna.                                                   |
| dokumentattribut               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Visar en sammanfattning av de enskilda detaljerna för en faktura typ (till exempel återkommande, en \_ tid).

| Egenskap            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | sträng                                                         | Typ av faktura: "återkommande", "en \_ tid".                                       |
| sammanfattning             | [InvoiceSummary](#invoicesummary) -objekt                       | Sammanfattningen av fakturan per faktura typ.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Representera en samling av typen [InvoiceSummary](#invoicesummary) som innehåller de enskilda detaljerna för en faktura typ per valuta.

| Egenskap            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | matris med [InvoiceSummary](#invoicesummary) -objekt             | Sammanfattningen av fakturan per faktura typ per valuta.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Representerar ett faktura fakturerings rads objekt för licensierade prenumerationer.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| debetbelopp                   | sträng                                                         | Hämtar eller anger den totala mängden. Total belopp = enhets pris * kvantitet.  |
| dokumentattribut               | sträng                                                         | Hämtar attributen.                                                  |
| billingCycleType         | sträng                                                         | Hämtar eller anger typen av fakturerings cykel.                                  |
| billingProvider          | sträng                                                         | Hämtar fakturerings leverantören.                                            |
| chargeEndDate            | sträng i UTC-datum/tid-format                                 | Hämtar eller anger fakturerings datum.                             |
| chargeStartDate          | sträng i UTC-datum/tid-format                                 | Hämtar eller anger avgiftens start datum.                           |
| chargeType               | sträng                                                         | Hämtar eller anger avgifts typen.                                      |
| currency                 | sträng                                                         | Hämtar eller anger valutan som används för det här rad objektet.                    |
| customerId               | sträng                                                         | Hämtar eller anger kundens unika identifierare i Microsofts fakturerings plattform.  |
| customerName             | sträng i UTC-datum/tid-format                                 | Hämtar eller anger kundens namn.                                       |
| Namn               | sträng                                                         | Hämtar eller anger domän namn.                                             |
| durableOfferId           | sträng                                                         | Hämtar eller anger den unika identifieraren för det beständiga erbjudandet.                     |
| invoiceLineItemType      | sträng                                                         | Hämtar typen av faktura rads objekt.                                   |
| mpnId                    | antal                                                         | Hämtar eller anger det MPN-ID som är kopplat till det här rad objektet. För direkt åter försäljare är detta MPN-ID: t för åter försäljaren. För indirekta åter försäljare är detta MPN-ID för mervärdes åter försäljaren (VAR).                                   |
| offerId                  | sträng                                                         | Hämtar eller anger unikt ID för erbjudandet.                             |
| offerName                | sträng                                                         | Hämtar eller anger namnet på erbjudandet.                                          |
| orderId                  | sträng                                                         | Hämtar eller anger den unika beställnings identifieraren.                             |
| Partner                | sträng                                                         | Hämtar eller anger partnerns ID för Azure Active Directory-klienten.            |
| quantity                 | antal                                                         | Hämtar eller anger antalet enheter som är kopplade till det här rad objektet.      |
| subscriptionDescription  | sträng                                                         | Hämtar eller anger prenumerations beskrivningen.                            |
| subscriptionEndDate      | sträng i UTC-datum/tid-format                                 | Hämtar eller anger det datum då prenumerationen upphör att gälla.                      |
| subscriptionId           | sträng                                                         | Hämtar eller anger prenumerationens unika identifierare.                      |
| subscriptionName         | sträng                                                         | Hämtar eller anger prenumerationens namn.                                   |
| subscriptionStartDate    | sträng i UTC-datum/tid-format                                 | Hämtar eller anger det datum då prenumerationen startar.                   |
| Delsumma                 | antal                                                         | Hämtar eller anger beloppet efter rabatt.                               |
| syndicationPartnerSubscriptionNumber | sträng                                             | Hämtar eller anger prenumerations numret för syndikerings partnern.             |
| Tax                      | antal                                                         | Hämtar eller anger de skatter som debiteras.                                       |
| tier2MpnId               | antal                                                         | Hämtar eller anger MPN-ID: t för nivå 2-partnern som är kopplad till det här rad objektet. |
| totalForCustomer         | antal                                                         | Hämtar eller anger det totala beloppet efter rabatt och skatt.                 |
| totalOtherDiscount       | antal                                                         | Hämtar eller anger rabatten som är kopplad till det här köpet.              |
| unitPrice                | antal                                                         | Hämtar eller anger enhets priset.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Representerar ett faktura fakturerings rads objekt för användnings prenumerationer.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| dokumentattribut               | sträng                                                         | Hämtar attributen.                                                  |
| billingCycleType         | sträng                                                         | Hämtar eller anger typen av fakturerings cykel.                                  |
| billingProvider          | sträng                                                         | Hämtar fakturerings leverantören.                                            |
| chargeEndDate            | sträng i UTC-datum/tid-format                                 | Hämtar eller anger fakturerings datum.                             |
| chargeStartDate          | sträng i UTC-datum/tid-format                                 | Hämtar eller anger avgiftens start datum.                           |
| chargeType               | sträng                                                         | Hämtar eller anger avgifts typen.                                      |
| consumedQuantity         | antal                                                         | Hämtar eller anger det totala antalet enheter som förbrukas.                                |
| consumptionDiscount      | sträng                                                         | Hämtar eller anger rabatten för förbrukning.                             |
| consumptionPrice         | sträng                                                         | Hämtar eller anger priset för Förbrukat antal.                          |
| currency                 | sträng                                                         | Hämtar eller anger valutan som är associerad med priserna.                 |
| customerName             | sträng                                                         | Hämtar eller anger kundens namn.                                       |
| customerId               | sträng                                                         | Hämtar eller anger kundens unika identifierare.                          |
| detailLineItemId         | antal                                                         | Hämtar eller anger informations radens objekt-ID. Identifierar rad objekt unikt för de fall där beräkningen skiljer sig från förbrukade enheter. Exempel: totalt förbrukat = 1338, 1024 debiteras med en kostnad, 314 är debiterad med en annan taxa.        |
| Namn               | sträng                                                         | Hämtar eller anger domän namn.                                             |
| includedQuantity         | antal                                                         | Hämtar eller anger de enheter som ingår i ordern.                         |
| invoiceLineItemType      | sträng                                                         | Hämtar typen av faktura rads objekt.                                   |
| invoiceNumber            | sträng                                                         | Hämtar eller anger faktura numret.                                      |
| listPrice                | antal                                                         | Hämtar eller anger priset för varje enhet.                                  |
| mpnId                    | antal                                                         | Hämtar eller anger det MPN-ID som är kopplat till det här rad objektet. För direkt åter försäljare är detta MPN-ID: t för åter försäljaren. För indirekta åter försäljare är detta MPN-ID för mervärdes åter försäljaren (VAR).                                   |
| orderId                  | sträng                                                         | Hämtar eller anger den unika beställnings identifieraren.                             |
| overageQuantity          | antal                                                         | Hämtar eller anger Förbrukat antal ovan tillåten användning.               |
| partnerBillableAccountId | sträng                                                         | Hämtar eller anger partnerns konto-ID.                         |
| Partner                | sträng                                                         | Hämtar eller anger partnerns ID för Azure Active Directory-klienten.            |
| partnerName              | sträng                                                         | Hämtar eller anger partnerns namn.                                      |
| postTaxEffectiveRate     | antal                                                         | Hämtar eller anger det effektiva priset efter skatt.                         |
| postTaxTotal             | antal                                                         | Hämtar eller anger den totala kostnaden efter skatt. Pretax avgifter + skatte belopp |
| preTaxCharges            | antal                                                         | Hämtar eller anger priset som debiteras före skatt.                          |
| preTaxEffectiveRate      | antal                                                         | Hämtar eller anger det effektiva priset före skatt.                        |
| region                   | sträng                                                         | Hämtar eller anger den region som är kopplad till resurs instansen.        |
| resourceGuid             | sträng                                                         | Hämtar eller anger resurs-ID.                                 |
| resourceName             | sträng                                                         | Hämtar eller anger resursens namn. Exempel: databas (GB/månad).         |
| serviceName              | sträng                                                         | Hämtar eller anger tjänstens namn. Exempel: Azure Data Service.           |
| serviceType              | sträng                                                         | Hämtar eller anger tjänst typen. Exempel: Azure SQL Azure DB.           |
| sku                      | sträng                                                         | Hämtar eller anger tjänstens SKU.                                         |
| subscriptionDescription  | sträng                                                         | Hämtar eller anger prenumerations beskrivningen.                            |
| subscriptionId           | sträng                                                         | Hämtar eller anger prenumerationens unika identifierare.                      |
| subscriptionName         | sträng                                                         | Hämtar eller anger prenumerationens namn.                                   |
| taxAmount                | antal                                                         | Hämtar eller anger skatte beloppet.                               |
| tier2MpnId               | antal                                                         | Hämtar eller anger MPN-ID: t för nivå 2-partnern som är kopplad till det här rad objektet. |
| unit                     | sträng                                                         | Hämtar eller anger mått enheten för Azure-användning.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Representerar de åtgärder som är tillgängliga för ett faktura uttryck i program/PDF.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | objekt                                                         | ByteArrayContent med contentType = Application/PDF.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Representerar ett faktura fakturerings rads objekt för licensierade prenumerationer.

| Egenskap | Typ | Description |
| --- | --- | --- |
| Partner | sträng | Hämtar eller anger partnerns klient-ID. |
| CustomerId | sträng | Hämtar eller anger kundens klient-ID. |
| CustomerName | sträng | Hämtar eller anger kundens namn. |
| CustomerDomainName | sträng | Hämtar eller anger kundens domän namn. |
| CustomerCountry | sträng | Hämtar eller anger kundens land. |
| InvoiceNumber | sträng | Hämtar eller anger faktura numret. |
| MpnId | sträng | Hämtar eller anger det MPN-ID som är kopplat till det här rad objektet. |
| ResellerMpnId | int | Hämtar eller anger den unika beställnings identifieraren. |
| OrderDate | DateTime | Hämtar eller anger datumet när ordern skapades. |
| ProductId | sträng | Hämtar eller anger produktens unika identifierare. |
| SkuId | sträng | Hämtar eller anger den unika SKU-identifieraren. |
| AvailabilityId | sträng | Hämtar eller anger unikt unikt ID för tillgänglighet. |
| ProductName | sträng | Hämtar eller anger produktens namn. |
| SkuName | sträng | Hämtar eller anger SKU-namnet. |
| ChargeType | sträng | Hämtar eller anger avgifts typen. |
| UnitPrice | decimal | Hämtar eller anger enhets priset. |
| EffectiveUnitPrice | decimal | Hämtar eller anger det effektiva enhets priset. |
| UnitType | sträng | Hämtar eller anger enhets typen. |
| Antal | int | Hämtar eller anger antalet enheter som är kopplade till det här rad objektet. |
| Delsumma | decimal | Hämtar eller anger beloppet efter rabatt. |
| TaxTotal | decimal | Hämtar eller anger de skatter som debiteras. |
| TotalForCustomer | decimal | Hämtar eller anger det totala beloppet efter rabatt och skatt. |
| Valuta | sträng | Hämtar eller anger valutan som används för det här rad objektet. |
| PublisherName | sträng | Hämtar eller anger utgivar namnet som är associerat med det här köpet. |
| PublisherId | sträng | Hämtar eller anger det utgivar-ID som är associerat med det här köpet. |
| SubscriptionDescription | sträng | Hämtar eller anger den prenumerations beskrivning som är associerad med det här köpet. |
| SubscriptionId | sträng | Hämtar eller anger det prenumerations-ID som är kopplat till det här köpet. |
| ChargeStartDate | DateTime | Hämtar eller anger det debiterings start datum som är kopplat till det här köpet. |
| ChargeEndDate | DateTime | Hämtar eller anger det sista debiterings datumet för köpet. |
| TermAndBillingCycle | sträng | Hämtar eller anger den period och den fakturerings cykel som är kopplad till det här köpet. |
| AlternateId | sträng | Hämtar eller anger alternativ-ID (offert-ID). |
| PriceAdjustmentDescription | sträng | Hämtar eller anger pris justerings beskrivningen. |
| DiscountDetails | sträng |  **Föråldrad**. Hämtar eller anger rabatt information som är associerad med det här köpet. |
| PricingCurrency | sträng | Hämtar eller anger pris valuta koden. |
| PCToBCExchangeRate | decimal | Hämtar eller anger pris valutan för fakturerings valutakursen. |
| PCToBCExchangeRateDate | DateTime | Hämtar eller anger det datum för valutakursen som pris nivån till fakturerings valuta för fakturerings kursen fastställdes för. |
| BillableQuantity | decimal | Hämtar eller anger de köpta enheterna. För varje design kolumn som heter som **BillableQuantity**. |
| MeterDescription | sträng | Hämtar eller anger mätar beskrivningen för förbruknings rads objekt. |
| ReservationOrderId | sträng | Hämtar eller anger reservations ordnings identifieraren för ett Azure RI-köp. |
| BillingFrequency | sträng | Hämtar eller anger fakturerings frekvensen. |
| InvoiceLineItemType | InvoiceLineItemType | Returnerar typen av faktura rads objekt. |
| BillingProvider | BillingProvider | Returnerar fakturerings leverantören. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Representerar ej fakturerade, rad artiklar för fakturerings utjämning för dagligt Beräknad användning.

| Egenskap | Typ | Description |
| --- | --- | --- |
| Partner | sträng | Hämtar eller anger partnerns klient-ID. |
| PartnerName | sträng | Hämtar eller anger partner namnet. |
| CustomerId | sträng | Hämtar eller anger klient-ID för den kund som användningen tillhör. |
| CustomerName | sträng | Hämtar eller anger namnet på det kund företag som användningen tillhör. |
| CustomerDomainName | sträng | Hämtar eller anger domän namnet för den kund som användningen tillhör. |
| InvoiceNumber | sträng | Hämtar eller anger ID för fakturan som används tillhör. |
| ProductId | sträng | Hämtar eller anger produktens unika identifierare. |
| SkuId | sträng | Hämtar eller anger den unika SKU-identifieraren. |
| AvailabilityId | sträng | Hämtar eller anger unikt unikt ID för tillgänglighet. |
| SkuName | sträng | Hämtar eller anger tjänstens SKU-namn. |
| ProductName | sträng | Hämtar eller anger produktens namn. |
| PublisherName | sträng | Hämtar eller anger utgivarens namn. |
| PublisherId | sträng | Hämtar eller anger utgivarens ID. |
| SubscriptionId | sträng | Hämtar eller anger prenumerations-ID. |
| SubscriptionDescription | sträng | Hämtar eller anger prenumerations beskrivningen. |
| ChargeStartDate | DateTime | Hämtar eller anger laddningens start datum. |
| ChargeEndDate | DateTime | Hämtar eller anger avgiftens slutdatum. |
| UsageDate | DateTime | Hämtar eller anger användnings datumet. |
| MeterType | sträng | Hämtar eller anger mätar typen. |
| MeterCategory | sträng | Hämtar eller anger mätar kategorin. |
| MeterId | sträng | Hämtar eller anger ett mätar-ID (GUID). |
| MeterSubCategory | sträng | Hämtar eller anger mätar under kategorin. |
| MeterName | sträng | Hämtar eller anger mätarens namn. |
| MeterRegion | sträng | Hämtar eller anger mätnings regionen. |
| UnitOfMeasure | sträng | Hämtar eller anger mått enheten. |
| ResourceLocation | sträng | Hämtar eller anger resursens plats. |
| ConsumedService | sträng | Hämtar eller anger namnet på den förbrukade tjänsten. |
| ResourceGroup | sträng | Hämtar eller anger namnet på resurs gruppen. |
| ResourceUri | sträng | Hämtar eller anger URI för den resurs instans som används. |
| Taggar | sträng | Hämtar eller anger kundens tillagda taggar. |
| AdditionalInfo | sträng | Hämtar eller anger tjänstspecifika metadata. Det kan till exempel vara en avbildningstyp för en virtuell dator. |
| ServiceInfo1 | sträng | Hämtar eller anger interna Azure-tjänstemetadata. |
| ServiceInfo2 | sträng | Hämtar eller anger tjänst information till exempel en avbildnings typ för en virtuell dator och ett ISP-namn för ExpressRoute. |
| CustomerCountry | sträng | Hämtar eller anger kundens land. |
| MpnId | sträng | Hämtar eller anger det MPN-ID som är kopplat till det här rad objektet. |
| ResellerMpnId | sträng | Hämtar eller anger åter försäljarens MPN-ID för nivå 2-partnern som är kopplad till det här rad objektet. |
| ChargeType | sträng | Hämtar eller anger avgifts typen. |
| UnitPrice | decimal | Hämtar eller anger priset för enheten. |
| Antal | decimal | Hämtar eller anger antalet användnings områden. |
| UnitType | sträng | Hämtar eller anger enhets typen (t. ex. 1 timme). |
| BillingPreTaxTotal | decimal | Hämtar eller anger den utökade kostnaden eller den totala kostnaden före skatt i lokal valuta för kunden eller fakturerings valutan. |
| BillingCurrency | sträng | Hämtar eller anger ISO-valutan som mätaren debiteras i i lokal valuta för kunden eller fakturerings valutan. |
| PricingPreTaxTotal | decimal | Hämtar eller anger den utökade kostnaden eller den totala kostnaden före skatt i USD eller katalog valuta som används för klassificering. |
| PricingCurrency | sträng | Hämtar eller anger ISO-valutan som mätaren debiteras i USD eller katalog valuta som används för klassificering. |
| EntitlementId | sträng | Hämtar eller anger behörighets-ID: t (Azure-prenumerationen). |
| EntitlementDescription | sträng | Hämtar eller anger beskrivningen av rättigheten (Azure-prenumerationen). |
| PCToBCExchangeRate | sträng | Hämtar eller anger pris valutan för fakturerings valutakursen. |
| PCToBCExchangeRateDate | DateTime | Hämtar eller anger pris valutan för fakturerings valutans datum. |
| EffectiveUnitPrice | decimal | Hämtar eller anger det effektiva enhets priset. |
| RateOfPartnerEarnedCredit | decimal | Hämtar eller anger frekvensen för intjänad kredit för partner. |
| hasPartnerEarnedCredit | boolesk | Hämtar eller anger den intjänade partner krediten. |
| InvoiceLineItemType | InvoiceLineItemType | Returnerar typen av faktura rads objekt. |
| BillingProvider | BillingProvider | Returnerar fakturerings leverantören. |
