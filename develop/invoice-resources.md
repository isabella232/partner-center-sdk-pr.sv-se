---
title: Fakturaresurser
description: Flera fakturarelaterade resurser är tillgängliga via Partner Center-API:erna. Dessa resurser är relaterade till information om faktura och radobjekt.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2e801dc3b082411e140b88cd495807b1381ef915e8f5f06803d64ca2cca1c6b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996554"
---
# <a name="invoice-resources"></a>Fakturaresurser

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Följande fakturarelaterade resurser är tillgängliga via Partner Center-API:erna.

## <a name="invoice"></a>Faktura

| Egenskap | Typ | Description |
| -------- | ---- | ----------- |
| id | sträng | Fakturaidentifieraren. |
| invoiceDate | sträng i UTC-datum/tid-format | Det datum då fakturan genererades. |
| billingPeriodStartDate | sträng i UTC-datum/tid-format | Startdatum för faktureringsperiod i UTC. |
| billingPeriodEndDate | sträng i UTC-datum/tid-format   | Slutdatum för faktureringsperiod i UTC. |
| totalCharges | antal | De totala avgifterna. Inkluderar avgifter för transaktioner och eventuella justeringar.     |
| paidAmount | antal  | Det belopp som betalas av partnern. Negativt om en betalning togs emot.  |
| currencyCode | sträng  | En kod som anger vilken valuta som används för alla fakturaobjektsbelopp och summor. |
| currencySymbol  | sträng | Valutasymbolen som används för alla fakturaobjektsbelopp och summor. |
| pdfDownloadLink | sträng  | En länk för att ladda ned fakturan i PDF-format. Den här länken returneras inte som en del av sökresultaten och fylls bara i om fakturan används av ID:t. Den här länken upphör att gälla automatiskt om 30 minuter. |
| invoiceDetails  | matris med [InvoiceDetail-objekt](#invoicedetail)  | Fakturainformation.  |
| Ändringsförslag      | matris med [fakturaobjekt](#invoice)   | Ändringarna av den här fakturan.  |
| documentType    | sträng | Dokumenttypen för fakturan: "Credit Note", "Invoice". |
| amendsOf        | sträng | Referensnumret för dokumentet som det här dokumentet är en ändring av.  |
| invoiceType     | sträng  | Typ av faktura: "återkommande", "en \_ gång".   |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks)  | Resurslänkarna.  |
| Attribut      | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.  |

## <a name="invoicedetail"></a>InvoiceDetail

En faktura innehåller en samling fakturerade objekt och varje objekt representeras av en InvoiceDetail-resurs.

| Egenskap            | Typ                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | sträng                                                         | Typ av fakturainformation: "none", "usage \_ line \_ items", "billing \_ line \_ items". |
| billingProvider     | sträng                                                         | Faktureringsleverantören: "none", "office", "azure" eller "azure \_ data \_ market".         |
| Länkar               | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurslänkarna.                                                               |
| Attribut          | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Varje enskild avgift inom en faktura representeras som en InvoiceLineItem.

| Egenskap            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | sträng                                                         | Typen av fakturarad: "none", "usage \_ line \_ items", "billing \_ line \_ items". |
| billingProvider     | sträng                                                         | Faktureringsleverantören: "none", "office", "azure" eller "azure \_ data \_ market".            |
| Attribut          | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Beskriver en sammanfattning av saldot och de totala avgifterna för en faktura.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | antal                                                         | Saldot på fakturan. Det här är den totala mängden obetalt fakturor. |
| currencyCode             | sträng                                                         | En kod som anger vilken valuta som används för saldobeloppet.       |
| currencySymbol           | sträng                                                         | Valutasymbolen som används.                                             |
| accountingDate           | sträng i UTC-datum/tid-format                                 | Det datum då saldobeloppet senast uppdaterades.                         |
| firstInvoiceCreationDate | sträng i UTC-datum/tid-format                                 | Det datum då den första fakturan för kunden skapades.              |
| lastPaymentDate          | sträng i UTC-datum/tid-format                                 | Datum för den senaste betalningen.                                         |
| lastPaymentAmount        | antal                                                         | Beloppet för den senaste betalningen.                                       |
| latestInvoiceDate        | sträng i UTC-datum/tid-format                                 | Det datum då den sista fakturan för kunden skapades.               |
| Detaljer                  | matris med [InvoiceSummaryDetail-objekt](#invoicesummarydetail) | Information om fakturasammanfattning.                                           |
| Länkar                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Resurslänkarna.                                                   |
| Attribut               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Representerar en sammanfattning av den enskilda informationen för en fakturatyp (till exempel återkommande, en \_ gång).

| Egenskap            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | sträng                                                         | Typ av faktura: "återkommande", "en \_ gång".                                       |
| sammanfattning             | [InvoiceSummary-objekt](#invoicesummary)                       | Sammanfattning av fakturan per fakturatyp.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Representerar en samling av typen [InvoiceSummary](#invoicesummary) som innehåller enskild information för en fakturatyp per valuta.

| Egenskap            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | matris med [InvoiceSummary-objekt](#invoicesummary)             | Sammanfattning av fakturan per fakturatyp per valuta.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Representerar ett fakturafaktureringsradobjekt för licensierade prenumerationer.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Belopp                   | sträng                                                         | Hämtar eller anger det totala beloppet. Totalt belopp = enhetspris * kvantitet.  |
| Attribut               | sträng                                                         | Hämtar attributen.                                                  |
| billingCycleType         | sträng                                                         | Hämtar eller anger faktureringscykeltypen.                                  |
| billingProvider          | sträng                                                         | Hämtar faktureringsleverantören.                                            |
| chargeEndDate            | sträng i UTC-datum/tid-format                                 | Hämtar eller anger slutdatumet för avgiften.                             |
| chargeStartDate          | sträng i UTC-datum/tid-format                                 | Hämtar eller anger startdatumet för avgiften.                           |
| chargeType               | sträng                                                         | Hämtar eller anger typen av avgift.                                      |
| currency                 | sträng                                                         | Hämtar eller anger valutan som används för det här radobjektet.                    |
| customerId               | sträng                                                         | Hämtar eller anger kundens unika identifierare på Microsofts faktureringsplattform.  |
| customerName             | sträng i UTC-datum/tid-format                                 | Hämtar eller anger kundnamnet.                                       |
| Domännamn               | sträng                                                         | Hämtar eller anger domännamn.                                             |
| durableOfferId           | sträng                                                         | Hämtar eller anger det hållbara erbjudandets unika identifierare.                     |
| invoiceLineItemType      | sträng                                                         | Hämtar typen av fakturaradspost.                                   |
| mpnId                    | antal                                                         | Hämtar eller anger det MPN-ID som är associerat med det här radobjektet. För direktåterförsäljare är detta återförsäljarens MPN-ID. För indirekta återförsäljare är detta MPN-ID:t för Value Added Reseller (VAR).                                   |
| offerId                  | sträng                                                         | Hämtar eller anger erbjudandets unika identifierare.                             |
| offerName                | sträng                                                         | Hämtar eller anger erbjudandets namn.                                          |
| Ordernr                  | sträng                                                         | Hämtar eller anger den unika orderidentifieraren.                             |
| partnerId                | sträng                                                         | Hämtar eller anger partnerns Klientorganisations-ID för Azure Active Directory.            |
| quantity                 | antal                                                         | Hämtar eller anger antalet enheter som är associerade med det här radobjektet.      |
| subscriptionDescription  | sträng                                                         | Hämtar eller anger prenumerationsbeskrivningen.                            |
| subscriptionEndDate      | sträng i UTC-datum/tid-format                                 | Hämtar eller anger det datum då prenumerationen upphör att gälla.                      |
| subscriptionId           | sträng                                                         | Hämtar eller anger prenumerationens unika identifierare.                      |
| subscriptionName         | sträng                                                         | Hämtar eller anger prenumerationens namn.                                   |
| subscriptionStartDate    | sträng i UTC-datum/tid-format                                 | Hämtar eller anger det datum då prenumerationen startar.                   |
| Delsumma                 | antal                                                         | Hämtar eller anger beloppet efter rabatten.                               |
| syndicationPartnerSubscriptionNumber | sträng                                             | Hämtar eller anger prenumerationsnumret för syndikeringspartnern.             |
| Skatt                      | antal                                                         | Hämtar eller anger de skatter som debiteras.                                       |
| tier2MpnId               | antal                                                         | Hämtar eller anger MPN-ID:t för den nivå 2-partner som är associerad med det här radobjektet. |
| totalForCustomer         | antal                                                         | Hämtar eller anger det totala beloppet efter rabatt och skatt.                 |
| totalOtherDiscount       | antal                                                         | Hämtar eller anger rabatten som är associerad med det här köpet.              |
| unitPrice                | antal                                                         | Hämtar eller anger enhetspriset.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Representerar ett fakturafaktureringsradobjekt för användningsbaserade prenumerationer.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Attribut               | sträng                                                         | Hämtar attributen.                                                  |
| billingCycleType         | sträng                                                         | Hämtar eller anger faktureringscykeltypen.                                  |
| billingProvider          | sträng                                                         | Hämtar faktureringsleverantören.                                            |
| chargeEndDate            | sträng i UTC-datum/tid-format                                 | Hämtar eller anger slutdatumet för avgiften.                             |
| chargeStartDate          | sträng i UTC-datum/tid-format                                 | Hämtar eller anger startdatumet för avgiften.                           |
| chargeType               | sträng                                                         | Hämtar eller anger typen av avgift.                                      |
| consumedQuantity         | antal                                                         | Hämtar eller anger det totala antalet förbrukade enheter.                                |
| consumptionDiscount      | sträng                                                         | Hämtar eller anger rabatten för förbrukning.                             |
| consumptionPrice         | sträng                                                         | Hämtar eller anger priset för förbrukad kvantitet.                          |
| currency                 | sträng                                                         | Hämtar eller anger valutan som är associerad med priserna.                 |
| customerName             | sträng                                                         | Hämtar eller anger kundnamnet.                                       |
| customerId               | sträng                                                         | Hämtar eller anger kundens unika identifierare.                          |
| detailLineItemId         | antal                                                         | Hämtar eller anger informationsradobjektets ID. Identifierar unikt radobjekten för fall där beräkningen skiljer sig för förbrukade enheter. Exempel: Totalt förbrukat = 1338, 1 024 debiteras med ett pris, 314 debiteras med ett annat pris.        |
| Domännamn               | sträng                                                         | Hämtar eller anger domännamn.                                             |
| includedQuantity         | antal                                                         | Hämtar eller anger de enheter som ingår i ordningen.                         |
| invoiceLineItemType      | sträng                                                         | Hämtar typen av fakturaradsobjekt.                                   |
| invoiceNumber            | sträng                                                         | Hämtar eller anger fakturanumret.                                      |
| listPrice                | antal                                                         | Hämtar eller anger priset för varje enhet.                                  |
| mpnId                    | antal                                                         | Hämtar eller anger det MPN-ID som är associerat med det här radobjektet. För direktåterförsäljare är detta MPN-ID:t för återförsäljaren. För indirekta återförsäljare är detta MPN-ID för Återförsäljare av mervärde (VAR).                                   |
| Ordernr                  | sträng                                                         | Hämtar eller anger den unika orderidentifieraren.                             |
| overageQuantity          | antal                                                         | Hämtar eller anger den kvantitet som förbrukas över tillåten användning.               |
| partnerBillableAccountId | sträng                                                         | Hämtar eller anger partnerns fakturerbara konto-ID.                         |
| partnerId                | sträng                                                         | Hämtar eller anger partnerns Klientorganisations-ID för Azure Active Directory.            |
| partnerName              | sträng                                                         | Hämtar eller anger partnerns namn.                                      |
| postTaxEffectiveRate     | antal                                                         | Hämtar eller anger det effektiva priset efter skatt.                         |
| postTaxTotal             | antal                                                         | Hämtar eller anger de totala avgifterna efter skatt. Avgifter före skatt + skattebelopp |
| preTaxCharges            | antal                                                         | Hämtar eller anger det pris som debiteras före skatter.                          |
| preTaxEffectiveRate      | antal                                                         | Hämtar eller anger det effektiva priset före skatter.                        |
| region                   | sträng                                                         | Hämtar eller anger den region som är associerad med resursinstansen.        |
| resourceGuid             | sträng                                                         | Hämtar eller anger resursidentifieraren.                                 |
| resourceName             | sträng                                                         | Hämtar eller anger resursnamnet. Exempel: Databas (GB/månad).         |
| Tjänstnamn              | sträng                                                         | Hämtar eller anger tjänstnamnet. Exempel: Azure Data Service.           |
| serviceType              | sträng                                                         | Hämtar eller anger tjänsttypen. Exempel: Azure SQL Azure DB.           |
| sku                      | sträng                                                         | Hämtar eller anger tjänstens SKU.                                         |
| subscriptionDescription  | sträng                                                         | Hämtar eller anger prenumerationsbeskrivningen.                            |
| subscriptionId           | sträng                                                         | Hämtar eller anger den unika identifieraren för prenumerationen.                      |
| subscriptionName         | sträng                                                         | Hämtar eller anger prenumerationsnamnet.                                   |
| taxAmount                | antal                                                         | Hämtar eller anger hur mycket skatt som debiteras.                               |
| tier2MpnId               | antal                                                         | Hämtar eller anger MPN-ID:t för den nivå 2-partner som är associerad med det här radobjektet. |
| unit                     | sträng                                                         | Hämtar eller anger måttenheten för Azure-användning.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Representerar de åtgärder som är tillgängliga på ett fakturautdrag i program/pdf.

| Egenskap                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | objekt                                                         | ByteArrayContent med contentType = application/pdf.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Representerar ett fakturafaktureringsradobjekt för licensierade prenumerationer.

| Egenskap | Typ | Description |
| --- | --- | --- |
| PartnerId | sträng | Hämtar eller anger partnerns klientorganisations-ID. |
| CustomerId | sträng | Hämtar eller anger kundens klientorganisations-ID. |
| CustomerName | sträng | Hämtar eller anger kundnamnet. |
| CustomerDomainName | sträng | Hämtar eller anger kundens domännamn. |
| CustomerCountry | sträng | Hämtar eller anger kundens land. |
| InvoiceNumber | sträng | Hämtar eller anger fakturanumret. |
| MpnId | sträng | Hämtar eller anger det MPN-ID som är associerat med det här radobjektet. |
| ResellerMpnId | int | Hämtar eller anger den unika orderidentifieraren. |
| OrderDate | DateTime | Hämtar eller anger datumet när ordern skapades. |
| ProductId | sträng | Hämtar eller anger den unika identifieraren för produkten. |
| SkuId | sträng | Hämtar eller anger den unika SKU-identifieraren. |
| AvailabilityId | sträng | Hämtar eller anger den unika identifieraren för tillgänglighet. |
| ProductName | sträng | Hämtar eller anger produktnamnet. |
| SkuName | sträng | Hämtar eller anger SKU-namnet. |
| ChargeType | sträng | Hämtar eller anger typen av avgift. |
| UnitPrice | decimal | Hämtar eller anger enhetspriset. |
| EffectiveUnitPrice | decimal | Hämtar eller anger det effektiva enhetspriset. |
| UnitType | sträng | Hämtar eller anger enhetstypen. |
| Kvantitet | int | Hämtar eller anger antalet enheter som är associerade med det här radobjektet. |
| Delsumma | decimal | Hämtar eller anger beloppet efter rabatten. |
| TaxTotal | decimal | Hämtar eller anger de skatter som debiteras. |
| TotalForCustomer | decimal | Hämtar eller anger det totala beloppet efter rabatt och skatt. |
| Valuta | sträng | Hämtar eller anger den valuta som används för det här radobjektet. |
| PublisherName | sträng | Hämtar eller anger det utgivarnamn som är associerat med köpet. |
| PublisherId | sträng | Hämtar eller anger det utgivar-ID som är associerat med köpet. |
| SubscriptionDescription | sträng | Hämtar eller anger prenumerationsbeskrivningen som är associerad med det här köpet. |
| SubscriptionId | sträng | Hämtar eller anger prenumerations-ID:t som är associerat med det här köpet. |
| ChargeStartDate | DateTime | Hämtar eller anger startdatumet för avgiften som är associerat med det här köpet. |
| ChargeEndDate | DateTime | Hämtar eller anger slutdatumet för avgiften som är associerat med det här köpet. |
| TermAndBillingCycle | sträng | Hämtar eller anger den period och faktureringsperiod som är associerad med det här köpet. |
| AlternateId | sträng | Hämtar eller anger alternativt ID (offert-ID). |
| PriceAdjustmentDescription | sträng | Hämtar eller anger beskrivningen av prisjusteringen. |
| CreditReasonCode | sträng | Hämtar eller anger kreditorsakskoden. |
| DiscountDetails | sträng |  **har föraktats.** Hämtar eller anger rabattinformation som är associerad med det här köpet. |
| PricingCurrency | sträng | Hämtar eller anger prisvalutakoden. |
| PCToBCExchangeRate | decimal | Hämtar eller anger prissättningsvalutan till faktureringsvalutakursen. |
| PCToBCExchangeRateDate | DateTime | Hämtar eller anger det datum då växelkursen för prissättningsvalutan till faktureringsvalutakursen fastställde. |
| BillableQuantity | decimal | Hämtar eller anger de köpta enheterna. För varje designkolumn med namnet **BillableQuantity**. |
| MeterDescription | sträng | Hämtar eller anger mätarbeskrivningen för förbrukningsradobjektet. |
| ReservationOrderId | sträng | Hämtar eller anger reservationsbeställningsidentifieraren för ett Azure RI-köp. |
| BillingFrequency | sträng | Hämtar eller anger faktureringsfrekvensen. |
| InvoiceLineItemType | InvoiceLineItemType | Returnerar typen av fakturaradsobjekt. |
| BillingProvider | BillingProvider | Returnerar faktureringsleverantören. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Representerar ej fakturerade, fakturerade avstämningsradsobjekt för daglig beräknad användning.

| Egenskap | Typ | Description |
| --- | --- | --- |
| PartnerId | sträng | Hämtar eller anger partnerns klientorganisations-ID. |
| PartnerName | sträng | Hämtar eller anger partnernamnet. |
| CustomerId | sträng | Hämtar eller anger klientorganisations-ID:t för den kund som användningen tillhör. |
| CustomerName | sträng | Hämtar eller anger namnet på det kundföretag som användningen tillhör. |
| CustomerDomainName | sträng | Hämtar eller anger domännamnet för den kund som användningen tillhör. |
| InvoiceNumber | sträng | Hämtar eller anger ID:t för den faktura som användningen tillhör. |
| ProductId | sträng | Hämtar eller anger den unika identifieraren för produkten. |
| SkuId | sträng | Hämtar eller anger den unika SKU-identifieraren. |
| AvailabilityId | sträng | Hämtar eller anger den unika identifieraren för tillgänglighet. |
| SkuName | sträng | Hämtar eller anger SKU-namnet för tjänsten. |
| ProductName | sträng | Hämtar eller anger namnet på produkten. |
| PublisherName | sträng | Hämtar eller anger namnet på utgivaren. |
| PublisherId | sträng | Hämtar eller anger utgivarens ID. |
| SubscriptionId | sträng | Hämtar eller anger prenumerations-ID:t. |
| SubscriptionDescription | sträng | Hämtar eller anger prenumerationsbeskrivningen. |
| ChargeStartDate | DateTime | Hämtar eller anger startdatumet för avgiften. |
| ChargeEndDate | DateTime | Hämtar eller anger slutdatumet för avgiften. |
| UsageDate | DateTime | Hämtar eller anger användningsdatum. |
| MeterType | sträng | Hämtar eller anger mätartypen. |
| MeterCategory | sträng | Hämtar eller anger mätarkategorin. |
| MeterId | sträng | Hämtar eller anger mätar-ID (GUID). |
| MeterSubCategory | sträng | Hämtar eller anger mätarens underkategori. |
| MeterName | sträng | Hämtar eller anger mätarnamnet. |
| MeterRegion | sträng | Hämtar eller anger mätarregionen. |
| UnitOfMeasure | sträng | Hämtar eller anger måttenheten. |
| ResourceLocation | sträng | Hämtar eller anger platsen för resursen. |
| ConsumedService | sträng | Hämtar eller anger namnet på den förbrukade tjänsten. |
| ResourceGroup | sträng | Hämtar eller anger namnet på resursgruppen. |
| ResourceUri | sträng | Hämtar eller anger URI för resursinstansen som användningen gäller. |
| Taggar | sträng | Hämtar eller anger att kunden har lagt till taggar. |
| AdditionalInfo | sträng | Hämtar eller anger tjänstspecifika metadata. Det kan till exempel vara en avbildningstyp för en virtuell dator. |
| ServiceInfo1 | sträng | Hämtar eller anger interna Metadata för Azure-tjänsten. |
| ServiceInfo2 | sträng | Hämtar eller anger tjänstinformation, till exempel en avbildningstyp för en virtuell dator och Internetleverantörens namn för ExpressRoute. |
| CustomerCountry | sträng | Hämtar eller anger kundens land. |
| MpnId | sträng | Hämtar eller anger det MPN-ID som är associerat med det här radobjektet. |
| ResellerMpnId | sträng | Hämtar eller anger MPN-ID:t för återförsäljaren för den nivå 2-partner som är associerad med det här radobjektet. |
| ChargeType | sträng | Hämtar eller anger typen av avgift. |
| UnitPrice | decimal | Hämtar eller anger priset för enheten. |
| Kvantitet | decimal | Hämtar eller anger mängden användning. |
| UnitType | sträng | Hämtar eller anger enhetstypen (till exempel 1 timme). |
| BillingPreTaxTotal | decimal | Hämtar eller anger den utökade kostnaden eller den totala kostnaden före skatt i lokal valuta för kunden eller faktureringsvalutan. |
| BillingCurrency | sträng | Hämtar eller anger ISO-valuta där mätaren debiteras i kundens eller faktureringsvalutans lokala valuta. |
| PricingPreTaxTotal | decimal | Hämtar eller anger den utökade kostnaden eller den totala kostnaden före skatt i USD eller katalogvaluta som används för klassificering. |
| PricingCurrency | sträng | Hämtar eller anger ISO-valuta där mätaren debiteras i USD eller katalogvalutan som används för klassificering. |
| EntitlementId | sträng | Hämtar eller anger berättigande-ID :t (Azure-prenumeration). |
| EntitlementDescription | sträng | Hämtar eller anger rättighetsbeskrivningen (Azure-prenumeration). |
| PCToBCExchangeRate | sträng | Hämtar eller anger prissättningsvalutan till växlingskursen för faktureringsvalutan. |
| PCToBCExchangeRateDate | DateTime | Hämtar eller anger prissättningsvalutan till faktureringsvalutakursens datum. |
| EffectiveUnitPrice | decimal | Hämtar eller anger det effektiva enhetspriset. |
| RateOfPartnerEarnedCredit | decimal | Hämtar eller anger priset för partner-intjänad kredit. |
| HasPartnerEarnedCredit | boolesk | Hämtar eller uppsättningar är partner-intjänad kredit som tillämpas. |
| RateOfCredit | decimal | Hämtar eller anger kreditfrekvensen för den angivna kredittypen. |
| CreditType | sträng | Hämtar eller anger typen av kredit. |
| InvoiceLineItemType | InvoiceLineItemType | Returnerar typen av fakturaradsobjekt. |
| BillingProvider | BillingProvider | Returnerar faktureringsleverantören. |
