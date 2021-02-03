---
title: Prenumerations resurser
description: Prenumerations resurser kan ge ytterligare information om prenumerationer under hela livs cykeln, till exempel support, åter betalningar, Azure-rättigheter.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd835e46e99b1fcb1e0b0e694ad73b1dca1240c9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768964"
---
# <a name="subscription-resources"></a>Prenumerations resurser

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

En prenumeration låter en kund använda en tjänst under en viss tids period. Alla fält gäller inte för alla prenumerationer. Många fält gäller bara vid vissa tidpunkter i livs cykeln, till exempel om en prenumeration har pausats eller avbrutits.

## <a name="subscription"></a>Prenumeration

>[!NOTE]
>**Prenumerations** resursen har en hastighets begränsning på 500 förfrågningar per minut per klient-ID.

**Prenumerations** resursen representerar livs cykeln för en prenumeration och innehåller egenskaper som definierar tillstånden under prenumerationens livs cykel.

| Egenskap             | Typ                                                          | Description                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sträng                                                        | Prenumerations-ID.                                                                                                                                                  |
| offerId              | sträng                                                        | Erbjudande-ID.                                                                                                                                                         |
| entitlementId        | sträng                                                        | Rättighets identifieraren (ett Azure-prenumerations-ID).                                                                                                                        |
| offerName            | sträng                                                        | Namnet på erbjudandet.                                                                                                                                                               |
| friendlyName         | sträng                                                        | Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate.                                                                                           |
| quantity             | antal                                                        | Antalet. Om till exempel licensbaserade fakturerings inställningar anges, anges den här egenskapen till licens antalet.                                                            |
| unitType             | sträng                                                        | De enheter som definierar antalet för prenumerationen.                                                                                                                             |
| parentSubscriptionId | sträng                                                        | Hämtar eller anger den överordnade prenumerations-ID: n.                                                                                                                              |
| creationDate         | sträng                                                        | Hämtar eller anger skapande datumet i datum-/tids format.                                                                                                                          |
| effectiveStartDate   | sträng i UTC-datum/tid-format                                | Hämtar eller anger det effektiva start datumet för den här prenumerationen i datum-/tids format. Den används för att återställa en migrerad prenumerations datum eller att justera den mot en annan.                |
| commitmentEndDate    | sträng i UTC-datum/tid-format                                | Slutdatumet för den här prenumerationen i datum-/tids format. För prenumerationer som inte kan förnyas automatiskt representerar detta ett datum som är långt bort i framtiden.       |
| status               | sträng                                                        | Prenumerations status: "ingen", "aktiv", "väntar", "pausad" eller "borttagen".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Hämtar ett värde som anger om prenumerationen förnyas automatiskt.                                                                                                    |
| billingType          | sträng                                                        | Anger hur prenumerationen faktureras: "ingen", "användning" eller "licens".                                                                                                      |
| billingCycle         | sträng                                                        | Anger med vilken frekvens partnern faktureras för den här ordern. De värden som stöds är medlems namnen som finns i [**BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Hämtar eller anger ett värde som anger om prenumerationen har köpbara-tillägg.                                                                                             |
| isTrial              | boolean                                                       | Ett värde som anger om detta är en utvärderings prenumeration.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Ett värde som anger om detta är en Microsoft-produkt.                                                                                                                       |
| publisherName        | sträng                                                        | Utgivar namnet.                                                                                                                                                           |
| åtgärder              | matris med strängar                                              | Hämtar eller anger de åtgärder som tillåts. Möjliga värden: "redigera", "Avbryt"                                                                                                  |
| Partner            | sträng                                                        | MPN-ID för åter försäljaren av posten som används i den indirekta partner modellen.                                                                                                     |
| suspensionReasons    | matris med strängar                                              | Skrivskyddad. Om prenumerationen har pausats, anger varför.                                                                                                                  |
| contractType         | sträng                                                        | Skrivskyddad. Typ av kontrakt: "prenumeration", "productKey" eller "redemptionCode".                                                                                           |
| refundOptions        | matris med [RefundOption](#refundoption) -resurser   | Skrivskyddad. Den uppsättning med åter betalnings alternativ som är tillgängliga för den här prenumerationen.                                                                                              |
| Länkar                | [SubscriptionLinks](#subscriptionlinks)                       | Hämtar eller anger prenumerations länkar.                                                                                                                                          |
| orderId              | sträng                                                        | ID: t för den ordning som användes för att starta prenumerationen.                                                                                                                |
| termDuration         | sträng                                                        | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är **P1M** (1 månad), **P1Y** (1 år) och **P3Y** (3 år).                                                        |
| dokumentattribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar prenumerationen.                                                                                                                    |
| renewalTermDuration  | sträng                                                        | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är **P1M** (1 månad) och **P1Y** (1 år).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

**SubscriptionLinks** -resursen beskriver den samling länkar som är kopplade till en prenumerations resurs.

| Egenskap           | Typ                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Operationsföljdslänkkod](utility-resources.md#link) | Hämtar eller anger erbjudandet.               |
| parentSubscription | [Operationsföljdslänkkod](utility-resources.md#link) | Hämtar eller anger den överordnade prenumerationen. |
| produkt            | [Operationsföljdslänkkod](utility-resources.md#link) | Hämtar produkten som är associerad med prenumerationen. |
| sku                | [Operationsföljdslänkkod](utility-resources.md#link) | Hämtar produkt-SKU: n som är associerad med prenumerationen. |
| availability       | [Operationsföljdslänkkod](utility-resources.md#link) | Hämtar den produkt-SKU-tillgänglighet som är associerad med prenumerationen. |
| activationLinks    | [Operationsföljdslänkkod](utility-resources.md#link) | Hämtar listan över aktiverings länkar som är associerade med prenumerationen. |
| ständiga               | [Operationsföljdslänkkod](utility-resources.md#link) | Själv URI.                         |
| nästa               | [Operationsföljdslänkkod](utility-resources.md#link) | Nästa sida med objekt.               |
| ursprungliga           | [Operationsföljdslänkkod](utility-resources.md#link) | Föregående sida med objekt.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

**SubscriptionProvisioningStatus** -resursen innehåller information om etablerings statusen för en prenumeration.

| Egenskap   | Typ                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | sträng                                                         | En GUID-formaterad sträng som identifierar produkt-SKU: n.             |
| status     | sträng                                                         | Anger etablerings status: "lyckades", "väntar" eller "misslyckades". |
| quantity   | antal                                                         | Tillhandahåller antalet prenumerationer efter etableringen.               |
| endDate    | sträng i UTC-datum/tid-format                                 | Slutdatum för prenumerationen.                                    |
| dokumentattribut | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

**SubscriptionRegistrationStatus** -resursen beskriver den samling länkar som är kopplade till en prenumerations resurs.

| Egenskap           | Typ                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | sträng                             | Prenumerations-ID.                                                          |
| status             | sträng                             | Anger registrerings status: "registrerad", "registrering" eller "notregistered".    |

## <a name="supportcontact"></a>SupportContact

**SupportContact** -resursen representerar en support kontakt för en kunds prenumeration.

| Egenskap        | Typ                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | sträng                                                         | En GUID-formaterad sträng som anger support kontaktens klient-ID. |
| supportMpnId    | sträng                                                         | Kontaktens Microsoft Partner Network-ID (MPN).                       |
| name            | sträng                                                         | Namnet på support kontakten.                                                |
| Länkar           | [ResourceLinks](utility-resources.md#resourcelinks)            | Länkarna för support kontakten.                                              |
| dokumentattribut      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attribut för metadata. Innehåller "objectType": "SupportContact".              |

## <a name="registersubscription"></a>RegisterSubscription

**RegisterSubscription** -resursen returnerar en länk som kan användas för att fråga om registrerings status för en prenumeration. Registrerings statusen returneras i svars texten av en lyckad begäran om att registrera en Azure-prenumeration.

| Egenskap                | Typ                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | objekt                             | Returnerar HTTP-statuskod 202 "accepterad", med ett plats huvud som innehåller en länk för att fråga om registrerings status. Till exempel `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

**RefundOption** -resursen representerar ett möjligt åter betalnings alternativ för prenumerationen.

| Egenskap          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | sträng | Typ av åter betalning. De värden som stöds är "delvis" och "fullständig" |
| expiresAfter      | sträng i UTC-datum/tid-format | Tidsstämpeln när det här alternativet upphör att gälla. Om värdet är null innebär det att det inte har något förfallo datum. |

## <a name="azureentitlement"></a>AzureEntitlement

**AzureEntitlement** -resursen representerar Azure-rättigheterna för prenumerationen.

| Egenskap          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | sträng | Rättighets identifieraren |
| friendlyName      | sträng | Det egna namnet på rättigheten. |
| status | sträng | Status för rättigheten. |
| subscriptionId | sträng | Prenumerations-ID som rättigheten tillhör. |
