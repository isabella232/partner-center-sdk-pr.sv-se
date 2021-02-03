---
title: Hämta länkar för fakturauppskattning
description: Du kan hämta en samling med uppskattnings Länkar för att skicka information om rad objekt i frågor.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 10801cdb1f9d4f50a1f8fc86c2d0eaf8610ed68c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769018"
---
# <a name="get-invoice-estimate-links"></a>Hämta länkar för fakturauppskattning

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan få uppskattnings Länkar för att få hjälp med att fråga efter information om ej fakturerade avstämnings rads objekt.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett faktura-ID. Detta identifierar fakturan som rad artiklarna ska hämtas för.

## <a name="c"></a>C\#

Följande exempel kod visar hur du kan få uppskattnings Länkar för att fråga ej fakturerade rad artiklar för en specifik valuta. Svaret innehåller uppskattnings Länkar för varje period (till exempel aktuell och föregående månad).

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

Ett liknande exempel finns i följande avsnitt:

- Exempel: [konsol test app](console-test-app.md)
- Projekt: **SDK-exempel för partner Center**
- Klass: **GetEstimatesLinks.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/estimates/Links? CurrencyCode = {CURRENCYCODE} http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande URI och frågeparameter när du skapar begäran.

| Namn                   | Typ   | Obligatorisk | Beskrivning                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| currencyCode           | sträng | Yes      | Valuta koden för de ej fakturerade rad artiklarna.                    |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svaret Länkar för att hämta ej fakturerade uppskattningar.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 80EAA055-B5D3-4D88-BFE8-924A3F706462
MS-RequestId: 1b18689e-3fe3-4fdb-d09e-39d13941390b
X-Locale: en-US
X-SourceFiles: =?UTF-8?B?RDpcU291cmNlc1xSUEUuUGFydG5lci5TZXJ2aWNlLkJpbGxpbmdTZXJ2aWNlXHYxLjFcV2ViQXBpc1xCaWxsaW5nU2VydmljZS5WMi5XZWJcdjFcaW52b2ljZXNcZXN0aW1hdGVzXGxpbmtz?=
X-Powered-By: ASP.NET
Date: Thu, 14 Mar 2019 18:15:06 GMT
Content-Length: 1857

{
  "totalCount": 4,
  "items": [
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    }
  ],
  "attributes": {
    "objectType": "Collection"
 }
}
```
