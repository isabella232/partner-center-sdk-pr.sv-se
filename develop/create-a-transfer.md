---
title: Skapa en överföring
description: Så här skapar du en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768829"
---
# <a name="create-a-transfer"></a>Skapa en överföring

**Gäller för:**

- Partnercenter

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/transfers http/1.1                    |

### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parameter för att identifiera kunden.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-ID** | sträng   | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs egenskaperna för [TransferEntity](transfer-entity-resources.md) i begär ande texten.

| Egenskap              | Typ          | Obligatorisk  | Beskrivning                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | sträng        | No    | En transferEntity-identifierare som anges när transferEntity har skapats.                               |
| createdTime           | DateTime      | No    | Datumet då transferEntity skapades, i datum-/tids format. Används när transferEntity har skapats.      |
| lastModifiedTime      | DateTime      | No    | Datumet då transferEntity senast uppdaterades, i datum-/tids format. Används när transferEntity har skapats. |
| lastModifiedUser      | sträng        | No    | Användaren som senast uppdaterade transferEntity. Används när transferEntity har skapats.                          |
| customerName          | sträng        | No    | Valfritt. Namnet på kunden vars prenumerationer överförs.                                              |
| customerTenantId      | sträng        | No    | Ett GUID-formaterat kund-ID som identifierar kunden. Används när transferEntity har skapats.         |
| partnertenantid       | sträng        | No    | Ett GUID-formaterat partner-ID som identifierar partnern.                                                                   |
| sourcePartnerName     | sträng        | No    | Valfritt. Namnet på partnerns organisation som initierar överföringen.                                           |
| sourcePartnerTenantId | sträng        | Yes   | Ett GUID-formaterat partner-ID som identifierar den partner som initierar överföringen.                                           |
| targetPartnerName     | sträng        | No    | Valfritt. Namnet på partnerns organisation som överföringen riktas mot.                                         |
| targetPartnerTenantId | sträng        | Yes   | Ett GUID-formaterat partner-ID som identifierar den partner som överföringen riktas mot.                                  |
| Rad objekt             | Objekt mat ris | Yes| En matris med [TransferLineItem](transfer-entity-resources.md#transferlineitem) -resurser.                                   |
| status                | sträng        | No    | Status för transferEntity. Möjliga värden är "aktiva" (kan tas bort/skickas) och "slutfört" (har redan slutförts). Används när transferEntity har skapats.|

I den här tabellen beskrivs egenskaperna för [TransferLineItem](transfer-entity-resources.md#transferlineitem) i begär ande texten.

|      Egenskap       |            Typ             | Obligatorisk | Beskrivning                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | sträng                     | No       | En unik identifierare för ett överförings rads objekt. Används när transferEntity har skapats.|
| subscriptionId       | sträng                     | Yes      | Prenumerations-ID.                                                                         |
| quantity             | int                        | No       | Antalet licenser eller instanser.                                                                 |
| billingCycle         | Objekt                     | No       | Typ av fakturerings cykel som angetts för den aktuella perioden.                                                |
| friendlyName         | sträng                     | No       | Valfritt. Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.                |
| partnerIdOnRecord    | sträng                     | No       | Partner on Record (MPNID) på köpet som inträffar när överföringen godkänns.              |
| offerId              | sträng                     | No       | Erbjudande-ID.                                                                                |
| addonItems           | Lista över **TransferLineItem** -objekt | No | En samling transferEntity rad objekt för tillägg som ska överföras tillsammans med den bas prenumeration som överförs. Används när transferEntity har skapats.|
| transferError        | sträng                     | No       | Tillämpas efter att transferEntity accepterats i händelse av ett fel.                                        |
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

Om det lyckas returnerar den här metoden den ifyllda [TransferEnity](transfer-entity-resources.md) -resursen i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

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
