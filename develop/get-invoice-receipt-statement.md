---
title: Hämta kvittoutdrag för faktura
description: Hämtar ett fakturakvittoutdrag med faktura-ID och kvitto-ID.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac4c8f0b881409dcad3560eefb82d4bb5e877a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446137"
---
# <a name="get-invoice-receipt-statement"></a>Hämta kvittoutdrag för faktura

Hämtar ett fakturakvittoutdrag med faktura-ID och kvitto-ID.

> [!IMPORTANT]
> Den här funktionen gäller endast skattekvitton för Taiwan.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.

- Ett giltigt faktura-ID och motsvarande kvitto-ID.

## <a name="c"></a>C\#

Om du vill hämta ett fakturakvittoutdrag efter ID börjar du med Partnercenter-SDK v1.12.0, använder **samlingen IPartner.Invoices** och anropar **Metoden ById()** med faktura-ID:t. Anropa sedan samlingen **Kvitton** och anropa **ById()** och anropa sedan metoderna **Documents()** och **Statement()** för att få åtkomst till fakturakvittoutdraget. Anropa slutligen metoderna **Get()** eller **GetAsync().**

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** PartnerSDK.FeatureSample-klass: GetInvoiceReceiptStatement.cs 

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att hämta fakturakvittoutdraget.

| Namn       | Typ   | Obligatorisk | Beskrivning                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| faktura-id | sträng | Ja      | Värdet är ett faktura-ID som gör att återförsäljaren kan filtrera resultatet för en viss faktura. |
| receipt-id | sträng | Ja      | Värdet är ett kvitto-ID som gör att återförsäljaren kan filtrera kvittona för en viss faktura. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en pdf-ström i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
