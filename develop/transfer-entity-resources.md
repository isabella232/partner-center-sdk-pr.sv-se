---
title: TransferEntity-resurser
description: En partner skapar en överföring när en kund vill att deras prenumeration med partnern ska överföras till en annan partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3103c0e9f8e6850336d663a5a38274ce7391e30edd433d08f44071de31b5fc5e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990213"
---
# <a name="transferentity-resources"></a>TransferEntity-resurser

En partner skapar en överföring när en kund vill att deras prenumeration med partnern ska överföras till en annan partner.

## <a name="transferentity"></a>TransferEntity

Beskriver en transferEntity.

| Egenskap              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | En transferEntity-identifierare som anges när transferEntity har skapats.                               |
| createdTime           | DateTime         | Det datum då transferEntity skapades i datum/tid-format. Tillämpas när transferEntity har skapats.      |
| lastModifiedTime      | DateTime         | Det datum då transferEntity senast uppdaterades, i datum/tid-format. Tillämpas när transferEntity har skapats. |
| lastModifiedUser      | sträng           | Den användare som senast uppdaterade transferEntity. Tillämpas när transferEntity har skapats.                          |
| customerName          | sträng           | Valfritt. Namnet på den kund vars prenumerationer överförs.                                              |
| customerTenantId      | sträng           | Ett GUID-formaterat kund-ID som identifierar kunden. Tillämpas när transferEntity har skapats.         |
| partnertenantid       | sträng           | Ett GUID-formaterat partner-ID som identifierar partnern.                                                                   |
| sourcePartnerName     | sträng           | Valfritt. Namnet på den partnerorganisation som initierar överföringen.                                           |
| sourcePartnerTenantId | sträng           | Ett GUID-formaterat partner-ID som identifierar den partner som initierar överföringen.                                           |
| targetPartnerName     | sträng           | Valfritt. Namnet på den partnerorganisation som överföringen är riktad mot.                                         |
| targetPartnerTenantId | sträng           | Ett GUID-formaterat partner-ID som identifierar den partner som överföringen är riktad mot.                                  |
| lineItems             | Matris med objekt | En matris med [TransferLineItem-resurser.](#transferlineitem)                                                   |
| status                | sträng           | Status för transferEntity. Möjliga värden är "Aktiv" (kan tas bort/skickas) och "Slutförd" (har redan slutförts). Tillämpas när transferEntity har skapats.|

## <a name="transferlineitem"></a>TransferLineItem

Representerar ett objekt som finns i en transferEntity.

| Egenskap             | Typ                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | sträng                           | En unik identifierare för ett överföringsradsobjekt. Tillämpas när transferEntity har skapats.   |
| subscriptionId       | sträng                           | Prenumerationsidentifieraren.                                                                            |
| quantity             | int                              | Antalet licenser eller instanser.                                                                    |
| billingCycle         | Objekt                           | Den typ av faktureringsperiod som angetts för den aktuella perioden.                                                   |
| friendlyName         | sträng                           | Valfritt. Det egna namnet för objektet som definierats av partnern för att undvika tvetydighet.                   |
| partnerIdOnRecord    | sträng                           | PartnerId on Record (MPNID) för köpet som sker när överföringen godkänns.                 |
| offerId              | sträng                           | Erbjudandeidentifieraren.    |
| addonItems           | Lista över **TransferLineItem-objekt** | En samling transferEntity-radobjekt för addoner som ska överföras tillsammans med basprenumerationen som överförs. Tillämpas när transferEntity har skapats.|
| transferError        | sträng                           | Tillämpas efter att transferEntity har godkänts i händelse av ett fel.                |
| status               | sträng           | Status för lineitem i transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Representerar resultatet av en överförings accept.

| Egenskap          | Typ                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| beställningar            | Lista över [orderobjekt.](order-resources.md#order)    | Samlingen med beställningar.          |
| transferErrors    | Lista över [TransferError-objekt.](#transfererror)      | Insamling av överföringsfel. |

## <a name="transfererror"></a>TransferError

Representerar ett fel som inträffar när en överföring godkänns.

| Egenskap          | Typ   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | sträng | Ordergruppens ID för ordern med felet . |
| kod              | int    | Felkoden.                                 |
| beskrivning       | sträng | Beskrivning av felet.                   |
| lineItems         | Lista över **TransferLineItem-objekt** | En samling transferEntity-radobjekt som ingår i överföringsfelet.|

## <a name="transfererrorcode"></a>TransferErrorCode

En [Enum/dotnet/api/system.enum) med värden som anger en typ av orderfel.

| Värde | Position | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Partnertoken saknas i begäranskontext. |
| InvalidInput | 800002 | Ogiltiga indata för begäran. |
| ServiceException | 800003 | Oväntat tjänstfel. |
| InvalidOfferId | 800004 | Ogiltigt erbjudande-ID. |
| CreateOrderError | 800005 | Det går inte att skapa ordern. |
| MpnIdNotFound | 800015 | MPN-ID:t hittades inte. |
| NotValidIndirectResellerMpnId | 800016 | MPN-ID är inte en giltig indirekt återförsäljare. |
| TransferIdNotFound | 900100   | Överföringsbegäran hittades inte.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | Överföringsbegäran pågår redan.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Överföringsbegäran har redan slutförts.|
| TransferCreateOrderError | 900103 | Överföringsordningen lyckas inte.|
| TransferProcessedByAnotherRequest | 900104 | Överföringen bearbetas av en annan begäran.|