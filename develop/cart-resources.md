---
title: Kundvagnsresurser
description: En partner lägger en beställning i kundvagn när en kund vill köpa en prenumeration från en lista över erbjudanden.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c9372bb982528127f8870094e26465d004b1f05c75140f0ac729375f5d5f3302
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992185"
---
# <a name="cart-resources"></a>Kundvagnsresurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

En partner gör en beställning när en kund vill köpa en prenumeration från en lista över erbjudanden.

## <a name="cart"></a>Kundvagn

Beskriver en kundvagn.

| Egenskap              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | En kundvagnsidentifierare som anges när kundvagnen har skapats.                               |
| creationTimeStamp     | DateTime         | Datumet då kundvagnen skapades i datum/tid-format. Tillämpas när kundvagnen har skapats.      |
| lastModifiedTimeStamp | DateTime         | Datum då kundvagnen senast uppdaterades i datum/tid-format. Tillämpas när kundvagnen har skapats. |
| expirationTimeStamp   | DateTime         | Datumet då kundvagnen upphör att gälla i datum/tid-format. Tillämpas när kundvagnen har skapats.          |
| lastModifiedUser      | sträng           | Den användare som senast uppdaterade kundvagnen. Tillämpas när kundvagnen har skapats.                          |
| lineItems             | Matris med objekt | En matris med [CartLineItem-resurser.](#cartlineitem)                                                   |
| status                | sträng           | Kundvagnens status. Möjliga värden är "Aktiv" (kan uppdateras/skickas) och "Ordered" (har redan skickats). |

## <a name="cartlineitem"></a>CartLineItem

Representerar ett objekt som finns i en kundvagn.

| Egenskap             | Typ                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sträng                           | En unik identifierare för ett kundvagnsradsobjekt. Tillämpas när kundvagnen har skapats.                                                                   |
| catalogItemId        | sträng                           | Katalogobjektets identifierare.                                                                                                                          |
| friendlyName         | sträng                           | Valfritt. Det egna namnet för det objekt som definierats av partnern för att undvika tvetydighet.                                                                 |
| quantity             | int                              | Antalet licenser eller instanser.                                                                                                                  |
| currencyCode         | sträng                           | Valutakoden.                                                                                                                                    |
| billingCycle         | Objekt                           | Den typ av faktureringsperiod som angetts för den aktuella perioden.                                                                                                 |
| termDuration         | sträng                           | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (1 månad), P1Y (1 år) och P3Y (3 år).                                |
| deltagare         | Lista över objektsträngpar      | En samling PartnerId on Record (MPN ID) för köpet.                                                                                          |
| provisioningContext  | Ordlista<sträng, sträng>       | Ytterligare kontext som används vid etablering av det köpta objektet. Information om vilka värden som behövs för ett visst objekt finns i SKU:ns provisioningVariables-egenskap. |
| orderGroup           | sträng                           | En grupp som anger vilka objekt som kan skickas tillsammans i samma ordning.                                                                          |
| addonItems           | Lista över **CartLineItem-objekt** | En samling kundvagnsradsobjekt för addons. De här objekten köps mot basprenumerationen som är resultatet av rotkorgsartikelns köp. |
| fel                | Objekt                           | Tillämpas efter att kundvagnen har skapats om ett fel har uppstått.                                                                                                    |
| renewsTo             | Matris med objekt                 | En matris med [RenewsTo-resurser.](#renewsto)                                                                            |
| AttestationAccepted             | boolesk                 | Anger avtal om att erbjuda eller SKU-villkor. Krävs endast för erbjudanden eller SKU:er där SkuAttestationProperties eller OfferAttestationProperties enforceAttestation är True.                                                                            |

## <a name="renewsto"></a>RenewsTo

Representerar ett objekt som finns i en kundvagnsrad.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelseperiodens varaktighet. De aktuella värdena som stöds **är P1M** (1 månad) och **P1Y** (1 år). |

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

## <a name="carterror"></a>CartError

Representerar ett fel som inträffar när en kundvagn har skapats.

| Egenskap         | Typ                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CareErrorCode](#carterrorcode) | Typ av kundvagnsfel.                                                                       |
| errorDescription | sträng                                 | Felbeskrivningen, inklusive eventuella anteckningar om värden som stöds, standardvärden eller gränser. |


## <a name="carterrorcode"></a>CartErrorCode

Typer av kundvagnsfel.

| Name                             | Felkod   | Description
|----------------------------------|-------------|-----------------------------------------------------------------------------------------------|
| CurrencyIsNotSupported           | 10000   | Valuta stöds inte för den angivna marknaden  |
| CatalogItemIdIsNotValid          | 10001   | Katalogobjektets ID är inte giltigt  |
| QuotaNotAvailable                | 10002   | Det finns inte tillräckligt med tillgänglig kvot  |
| InventoryNotAvailable            | 10003   | Inventering är inte tillgängligt för valt erbjudande  |
| DeltagareIsNotSupportedForPartner  | 10004   | Det finns inte stöd för att ställa in deltagare för partner  |
| UnableToProcessCartLineItem      | 10006   | Det går inte att bearbeta kundvagnsradsobjektet.  |
| SubscriptionIsNotValid           | 10007   | Prenumerationen är inte giltig.  |
| SubscriptionIsNotEnabledForRI    | 10008   | Prenumerationen har inte aktiverats för RI-köp.  |
| SandboxLimitExceeded             | 10009   | Sandbox-gränsen har överskridits.  |
| InvalidInput                     | 10010   | Allmänna indata är inte giltiga.  |
| SubscriptionNotRegistered        | 10011   | Prenumerationen är inte giltig.  |
| AttestationNotAccepted           | 10012   | Attestation har inte godkänts.  |
| Okänt                          | 0   | Standardvärde   |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Representerar resultatet av en kundvagnsutcheckning.

| Egenskap    | Typ                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| beställningar      | Lista över [orderobjekt.](order-resources.md#order)         | Samlingen med beställningar.       |
| orderErrors | Lista över [OrderError-objekt.](#ordererror) | Samlingen med orderfel. |

## <a name="ordererror"></a>OrderError

Representerar ett fel som inträffar under en kundvagnsutcheckning när en order skapas.

| Egenskap     | Typ   | Description                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | sträng | Ordergruppens ID med felet . |
| kod         | int    | Felkoden.                                 |
| beskrivning  | sträng | Beskrivningen av felet.                   |
