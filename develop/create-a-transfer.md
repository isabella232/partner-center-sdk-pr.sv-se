---
title: Skapa en överföring
description: Så här skapar du en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d459a0a96912ab27f312bc73af16af2d4fdb518c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973714"
---
# <a name="create-a-transfer"></a>Skapa en överföring

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1                    |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökvägsparameter för att identifiera kunden.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-ID** | sträng   | Ja      | Ett GUID-formaterat kund-ID som identifierar kunden.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs [transferEntity-egenskaperna](transfer-entity-resources.md) i begärandetexten.

| Egenskap              | Typ          | Obligatorisk  | Beskrivning                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | sträng        | No    | En transferEntity-identifierare som anges när transferEntity har skapats.                               |
| createdTime           | DateTime      | Inga    | Det datum då transferEntity skapades i datum/tid-format. Tillämpas när transferEntity har skapats.      |
| lastModifiedTime      | DateTime      | Inga    | Det datum då transferEntity senast uppdaterades, i datum/tid-format. Tillämpas när transferEntity har skapats. |
| lastModifiedUser      | sträng        | No    | Den användare som senast uppdaterade transferEntity. Tillämpas när transferEntity har skapats.                          |
| customerName          | sträng        | No    | Valfritt. Namnet på den kund vars prenumerationer överförs.                                              |
| customerTenantId      | sträng        | No    | Ett GUID-formaterat kund-ID som identifierar kunden. Tillämpas när transferEntity har skapats.         |
| partnertenantid       | sträng        | No    | Ett GUID-formaterat partner-ID som identifierar partnern.                                                                   |
| sourcePartnerName     | sträng        | No    | Valfritt. Namnet på den partnerorganisation som initierar överföringen.                                           |
| sourcePartnerTenantId | sträng        | Ja   | Ett GUID-formaterat partner-ID som identifierar den partner som initierar överföringen.                                           |
| targetPartnerName     | sträng        | No    | Valfritt. Namnet på den partnerorganisation som överföringen är riktad mot.                                         |
| targetPartnerTenantId | sträng        | Ja   | Ett GUID-formaterat partner-ID som identifierar den partner som överföringen är riktad mot.                                  |
| lineItems             | Matris med objekt | Ja| En matris med [TransferLineItem-resurser.](transfer-entity-resources.md#transferlineitem)                                   |
| status                | sträng        | No    | Status för transferEntity. Möjliga värden är "Aktiv" (kan tas bort/skickas) och "Slutförd" (har redan slutförts). Tillämpas när transferEntity har skapats.|

I den här tabellen beskrivs [transferLineItem-egenskaperna](transfer-entity-resources.md#transferlineitem) i begärandetexten.

|      Egenskap       |            Typ             | Obligatorisk | Beskrivning                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | sträng                     | No       | En unik identifierare för ett överföringsradsobjekt. Tillämpas när transferEntity har skapats.|
| subscriptionId       | sträng                     | Ja      | Prenumerationsidentifieraren.                                                                         |
| quantity             | int                        | Inga       | Antalet licenser eller instanser.                                                                 |
| billingCycle         | Objekt                     | Inga       | Den typ av faktureringsperiod som angetts för den aktuella perioden.                                                |
| friendlyName         | sträng                     | No       | Valfritt. Det egna namnet för det objekt som definierats av partnern för att undvika tvetydighet.                |
| partnerIdOnRecord    | sträng                     | No       | PartnerId på post (MPN-ID) för köpet som inträffar när överföringen godkänns.              |
| offerId              | sträng                     | No       | Erbjudandeidentifieraren.                                                                                |
| addonItems           | Lista över **TransferLineItem-objekt** | Inga | En samling transferEntity-radobjekt för addons som ska överföras tillsammans med basprenumerationen som överförs. Tillämpas när transferEntity har skapats.|
| transferError        | sträng                     | No       | Tillämpas efter överföringEntity godkänns om det finns ett fel.                                        |
| status               | sträng                     | No       | Status för lineitem i transferEntity.                                                    |

### <a name="request-example"></a>Exempel på begäran

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den [ifyllda TransferEnity-resursen](transfer-entity-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
