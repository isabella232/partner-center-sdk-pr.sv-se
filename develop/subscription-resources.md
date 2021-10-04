---
title: Prenumerationsresurser
description: Prenumerationsresurser kan ge ytterligare information om prenumerationer under hela livscykeln, till exempel support, återbetalningar och Azure-rättigheter.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 461df9cdb909fc44be9069cb7eb4b41fa2a5f170
ms.sourcegitcommit: 3ee00d9fe9da6b9df0fb7027ae506e2abe722770
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/04/2021
ms.locfileid: "129417295"
---
# <a name="subscription-resources"></a>Prenumerationsresurser

**Gäller för:** Partner Center | Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Med en prenumeration kan en kund använda en tjänst under en viss tidsperiod. Alla fält gäller inte för alla prenumerationer. Många fält gäller endast vid vissa punkter i livscykeln, till exempel om en prenumeration pausas eller avbryts.

## <a name="subscription"></a>Prenumeration

>[!NOTE]
>**Prenumerationsresursen** har en hastighetsgräns på 500 begäranden per minut per klientorganisations-ID.

**Prenumerationsresursen** representerar livscykeln för en prenumeration och innehåller egenskaper som definierar tillstånden under prenumerationens livscykel.

| Egenskap             | Typ                                                          | Description                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sträng                                                        | Prenumerationsidentifieraren.                                                                                                                                                  |
| offerId              | sträng                                                        | Erbjudandeidentifieraren.                                                                                                                                                         |
| entitlementId        | sträng                                                        | Berättigandeidentifieraren (ett Prenumerations-ID för Azure).                                                                                                                        |
| offerName            | sträng                                                        | Erbjudandets namn.                                                                                                                                                               |
| friendlyName         | sträng                                                        | Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydighet.                                                                                           |
| quantity             | antal                                                        | Kvantitet. Om du till exempel använder licensbaserad fakturering anges den här egenskapen till licensantalet.                                                            |
| unitType             | sträng                                                        | Enheter som definierar kvantitet för prenumerationen.                                                                                                                             |
| parentSubscriptionId | sträng                                                        | Hämtar eller anger den överordnade prenumerationsidentifieraren.                                                                                                                              |
| creationDate         | sträng                                                        | Hämtar eller anger skapandedatum i datum/tid-format.                                                                                                                          |
| effectiveStartDate   | sträng i UTC-datum/tid-format                                | Hämtar eller anger det effektiva startdatumet för den här prenumerationen i datum/tid-format. Den används för att bakåt datera en migrerad prenumeration eller justera den med en annan.                |
| commitmentEndDate    | sträng i UTC-datum/tid-format                                | Slutdatumet för åtagandet för den här prenumerationen i datum/tid-format. För prenumerationer som inte förnyas automatiskt representerar detta ett datum långt bort i framtiden.       |
| status               | sträng                                                        | Prenumerationsstatus: "none", "active", "pending", "suspended", "expired" eller "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Hämtar ett värde som anger om prenumerationen förnyas automatiskt.                                                                                                    |
| billingType          | sträng                                                        | Anger hur prenumerationen faktureras: "none", "usage" eller "license".                                                                                                      |
| billingCycle         | sträng                                                        | Anger med vilken frekvens partnern faktureras för den här beställningen. Värden som stöds är de medlemsnamn som finns [**i BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Hämtar eller anger ett värde som anger om prenumerationen har köpbara tillägg.                                                                                             |
| isTrial              | boolean                                                       | Ett värde som anger om det här är en utvärderingsprenumeration.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Ett värde som anger om det här är en Microsoft-produkt.                                                                                                                       |
| publisherName        | sträng                                                        | Utgivarens namn.                                                                                                                                                           |
| åtgärder              | matris med strängar                                              | Hämtar eller anger de åtgärder som tillåts. Möjliga värden: "edit", "cancel"                                                                                                  |
| partnerId            | sträng                                                        | MPN-ID:t för den registrerande återförsäljaren, som används i den indirekta partnermodellen.                                                                                                     |
| suspendReasons    | matris med strängar                                              | Skrivskyddade. Om prenumerationen pausas anger varför.                                                                                                                  |
| contractType         | sträng                                                        | Skrivskyddade. Kontrakttypen: "subscription", "productKey" eller "redemptionCode".                                                                                           |
| refundOptions        | matris med [RefundOption-resurser](#refundoption)   | Skrivskyddade. Den uppsättning återbetalningsalternativ som är tillgängliga för den här prenumerationen.                                                                                              |
| Länkar                | [SubscriptionLinks](#subscriptionlinks)                       | Hämtar eller anger prenumerationslänkarna.                                                                                                                                          |
| Ordernr              | sträng                                                        | ID:t för ordern som gjordes för att påbörja prenumerationen.                                                                                                                |
| termDuration         | sträng                                                        | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds **är P1M** (1 månad), **P1Y** (1 år) och **P3Y** (3 år).                                                        |
| Attribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar prenumerationen.                                                                                                                    |
| renewalTermDuration  | sträng                                                        | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds **är P1M** (1 månad) och **P1Y** (1 år).                                                        |
| ProductType  | [ItemType](product-resources.md#itemtype)                             | Skrivskyddade. Den typ av produkt som prenumerationen är till för.     |
| consumptionType  | matris med [överanvändningsresurser](subscription-resources.md#overage)   | Hämtar eller anger överage för en viss kund.     |

## <a name="subscriptionlinks"></a>SubscriptionLinks

Resursen **SubscriptionLinks** beskriver samlingen med länkar som är kopplade till en prenumerationsresurs.

| Egenskap           | Typ                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Länk](utility-resources.md#link) | Hämtar eller anger erbjudandet.               |
| parentSubscription | [Länk](utility-resources.md#link) | Hämtar eller anger den överordnade prenumerationen. |
| produkt            | [Länk](utility-resources.md#link) | Hämtar produkten som är associerad med prenumerationen. |
| sku                | [Länk](utility-resources.md#link) | Hämtar produkt-SKU:n som är associerad med prenumerationen. |
| availability       | [Länk](utility-resources.md#link) | Hämtar den produkt-SKU-tillgänglighet som är associerad med prenumerationen. |
| activationLinks    | [Länk](utility-resources.md#link) | Hämtar listan över aktiveringslänkar som är associerade med prenumerationen. |
| Själv               | [Länk](utility-resources.md#link) | Själv-URI:en.                         |
| nästa               | [Länk](utility-resources.md#link) | Nästa sida med objekt.               |
| Tidigare           | [Länk](utility-resources.md#link) | Föregående sida med objekt.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

Resursen **SubscriptionProvisioningStatus** innehåller information om etableringsstatusen för en prenumeration.

| Egenskap   | Typ                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | sträng                                                         | En GUID-formaterad sträng som identifierar produktens SKU.             |
| status     | sträng                                                         | Anger etableringsstatus: "lyckades", "väntar" eller "misslyckades". |
| quantity   | antal                                                         | Anger prenumerationskvantiteten efter etableringen.               |
| endDate    | sträng i UTC-datum/tid-format                                 | Slutdatumet för prenumerationen.                                    |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

Resursen **SubscriptionRegistrationStatus** beskriver samlingen med länkar som är kopplade till en prenumerationsresurs.

| Egenskap           | Typ                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | sträng                             | Prenumerationsidentifieraren.                                                          |
| status             | sträng                             | Anger registreringsstatus: "registered", "registering" eller "notregistered".    |

## <a name="supportcontact"></a>SupportContact

**SupportContact-resursen** representerar en supportkontakt för en kunds prenumeration.

| Egenskap        | Typ                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | sträng                                                         | En GUID-formaterad sträng som anger supportkontaktens klientorganisations-ID. |
| supportMpnId    | sträng                                                         | Kontaktens ID Microsoft Partner Network (MPN).                       |
| name            | sträng                                                         | Namnet på supportkontakten.                                                |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks)            | Länkarna som är relaterade till supportkontakten.                                              |
| Attribut      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen. Innehåller "objectType": " SupportContact".              |

## <a name="overage"></a>Överanvändning

**Överförbrukningsresursen** representerar den överförbrukningsprenumeration som överförbrukning kan tilldelas, oavsett om den har tilldelats och tilldelats återförsäljaren.

| Egenskap        | Typ               | Description                                                                     |
|-----------------|--------------------|---------------------------------------------------------------------------------|
| azureEntitlementId | sträng       | En GUID-formaterad sträng som anger förbrukningsprenumerations-ID. |
| partnerId    | sträng            | ID Microsoft Partner Network (MPN) för återförsäljaren som är associerad med prenumerationen.        |
| typ    | sträng       | Typen av övergrupp, kan vara "PhoneServices"       |
| Översatsning            | boolean      | Ett värde som anger om överning har aktiverats.       |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks)            | Överage-relaterade länkar.                          |
| Attribut      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Metadataattributen. Innehåller "objectType": "Overage".  |



## <a name="registersubscription"></a>RegisterSubscription

**RegisterSubscription-resursen** returnerar en länk som kan användas för att fråga registreringsstatusen för en prenumeration. Registreringsstatusen returneras i svarstexten för en godkänd begäran om att registrera en Azure-prenumeration.

| Egenskap                | Typ                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | objekt                             | Returnerar HTTP-statuskod 202 "Accepted", med en platsrubrik som innehåller en länk för att fråga registreringsstatusen. Till exempel `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

Resursen **RefundOption** representerar ett möjligt återbetalningsalternativ för prenumerationen.

| Egenskap          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | sträng | Typ av återbetalning. De värden som stöds är "Partiell" och "Fullständig" |
| expiresAfter      | sträng i UTC-datum/tid-format | Tidsstämpeln när det här alternativet upphör att gälla. Om värdet är null innebär det att det inte har någon förfallotid. |

## <a name="azureentitlement"></a>AzureEntitlement

Resursen **AzureEntitlement** representerar Azure-rättigheterna för prenumerationen.

| Egenskap          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | sträng | Berättigandeidentifieraren |
| friendlyName      | sträng | Det egna namnet på rättigheten. |
| status | sträng | Status för rättigheten. |
| subscriptionId | sträng | Prenumerations-ID:t som rättigheten tillhör. |
