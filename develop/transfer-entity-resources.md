---
title: TransferEntity-resurser
description: En partner skapar en överföring när en kund vill att prenumerationen på partnern ska överföras till en annan partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96c43d255fcd31e6dc4de50baa0e19f5d8855685
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769219"
---
# <a name="transferentity-resources"></a>TransferEntity-resurser

**Gäller för:**

- Partnercenter

En partner skapar en överföring när en kund vill att prenumerationen på partnern ska överföras till en annan partner.

## <a name="transferentity"></a>TransferEntity

Beskriver en transferEntity.

| Egenskap              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | En transferEntity-identifierare som anges när transferEntity har skapats.                               |
| createdTime           | DateTime         | Datumet då transferEntity skapades, i datum-/tids format. Används när transferEntity har skapats.      |
| lastModifiedTime      | DateTime         | Datumet då transferEntity senast uppdaterades, i datum-/tids format. Används när transferEntity har skapats. |
| lastModifiedUser      | sträng           | Användaren som senast uppdaterade transferEntity. Används när transferEntity har skapats.                          |
| customerName          | sträng           | Valfritt. Namnet på kunden vars prenumerationer överförs.                                              |
| customerTenantId      | sträng           | Ett GUID-formaterat kund-ID som identifierar kunden. Används när transferEntity har skapats.         |
| partnertenantid       | sträng           | Ett GUID-formaterat partner-ID som identifierar partnern.                                                                   |
| sourcePartnerName     | sträng           | Valfritt. Namnet på partnerns organisation som initierar överföringen.                                           |
| sourcePartnerTenantId | sträng           | Ett GUID-formaterat partner-ID som identifierar den partner som initierar överföringen.                                           |
| targetPartnerName     | sträng           | Valfritt. Namnet på partnerns organisation som överföringen riktas mot.                                         |
| targetPartnerTenantId | sträng           | Ett GUID-formaterat partner-ID som identifierar den partner som överföringen riktas mot.                                  |
| Rad objekt             | Objekt mat ris | En matris med [TransferLineItem](#transferlineitem) -resurser.                                                   |
| status                | sträng           | Status för transferEntity. Möjliga värden är "aktiva" (kan tas bort/skickas) och "slutfört" (har redan slutförts). Används när transferEntity har skapats.|

## <a name="transferlineitem"></a>TransferLineItem

Representerar ett objekt som finns i en transferEntity.

| Egenskap             | Typ                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | sträng                           | En unik identifierare för ett överförings rads objekt. Används när transferEntity har skapats.   |
| subscriptionId       | sträng                           | Prenumerations-ID.                                                                            |
| quantity             | int                              | Antalet licenser eller instanser.                                                                    |
| billingCycle         | Objekt                           | Typ av fakturerings cykel som angetts för den aktuella perioden.                                                   |
| friendlyName         | sträng                           | Valfritt. Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.                   |
| partnerIdOnRecord    | sträng                           | Partner on Record (MPNID) på köpet som inträffar när överföringen godkänns.                 |
| offerId              | sträng                           | Erbjudande-ID.    |
| addonItems           | Lista över **TransferLineItem** -objekt | En samling transferEntity rad objekt för tillägg som ska överföras tillsammans med den bas prenumeration som överförs. Används när transferEntity har skapats.|
| transferError        | sträng                           | Tillämpas efter att transferEntity accepterats i händelse av ett fel.                |
| status               | sträng           | Status för lineitem i transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Visar resultatet av ett överförings godkännande.

| Egenskap          | Typ                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| beställningar            | Lista med [order](order-resources.md#order) objekt.    | Samlingen med beställningar.          |
| transferErrors    | Lista över [TransferError](#transfererror) -objekt.      | Insamling av överförings fel. |

## <a name="transfererror"></a>TransferError

Representerar ett fel som uppstår när en överföring godkänns.

| Egenskap          | Typ   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | sträng | Order grupp-ID: t för ordern med felet. |
| kod              | int    | Felkoden.                                 |
| beskrivning       | sträng | Beskrivningen av felet.                   |
| Rad objekt         | Lista över **TransferLineItem** -objekt | En samling transferEntity rad objekt som ingår i överförings felet.|

## <a name="transfererrorcode"></a>TransferErrorCode

En [Enum/dotNet/API/system. Enum) med värden som indikerar en typ av ordnings fel.

| Värde | Position | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Partner-token saknas i kontexten för begäran. |
| InvalidInput | 800002 | Ogiltig Indatatyp för begäran. |
| ServiceException | 800003 | Oväntat tjänst fel. |
| InvalidOfferId | 800004 | Ogiltigt erbjudande-ID. |
| CreateOrderError | 800005 | Create order misslyckades. |
| MpnIdNotFound | 800015 | Det gick inte att hitta MPN-ID. |
| NotValidIndirectResellerMpnId | 800016 | MPN-ID är inte en giltig indirekt åter försäljare. |
| TransferIdNotFound | 900100   | Överförings förfrågan hittades inte.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | Överföringsbegäran pågår redan.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Överföringsbegäran har redan slutförts.|
| TransferCreateOrderError | 900103 | Överförings ordningen är inte klar.|
| TransferProcessedByAnotherRequest | 900104 | Överföringen bearbetas av en annan begäran.|