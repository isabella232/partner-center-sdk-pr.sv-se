---
title: Avvisa en överföring
description: Så här avvisar du en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7862b017a494fcb8a503498c957ebc2cb5f4de9d3ede0aae625db53668e5477
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997217"
---
# <a name="reject-a-transfer"></a>Avvisa en överföring

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- En överföringsidentifierare för en befintlig överföring.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1                    |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökvägsparameter för att identifiera kunden och ange vilken överföring som ska godkännas.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-id** | sträng   | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden.             |
| **transfer-id** | sträng   | Yes      | Ett GUID-formaterat överförings-ID som identifierar överföringen.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs [TransferEntity-egenskaperna](transfer-entity-resources.md) i begärandetexten.

| Egenskap              | Typ          | Obligatorisk  | Beskrivning                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | sträng        | No    | En transferEntity-identifierare som anges när transferEntity har skapats.                               |
| status                | sträng        | No    | Status för transferEntity. Om du vill avvisa en överföring ska värdet anges som "avvisa"|

### <a name="request-example"></a>Exempel på begäran

```http
PATCH /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
Connection: keep-alive
Content-Length: 63

{"id":"ac4a9d22-ba07-444e-890f-cfe084eed498","status":"reject"}

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den [ifyllda TransferEntity-resursen](transfer-entity-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1069
Content-Type: application/json; charset=utf-8
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
X-Locale: en-US
Date: Fri, 27 Mar 2020 17:50:33 GMT

{
  "id": "ac4a9d22-ba07-444e-890f-cfe084eed498",
  "status": "Reject",
  "createdTime": "2020-03-25T22:05:25.1057725Z",
  "lastModifiedTime": "2020-03-27T17:50:32Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
      "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
      "billingCycle": "monthly",
      "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
      "quantity": 20,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "TransferEntity"
  }
}
```
