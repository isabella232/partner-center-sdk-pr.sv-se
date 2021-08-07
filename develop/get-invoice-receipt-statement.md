---
title: Hämta kvittoutdrag för faktura
description: Hämtar ett fakturakvittoutdrag med faktura-ID och kvitto-ID.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed47eadb377a94363b46cbc5508e5377cee005007698df9077d085705c7b9d08
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990740"
---
# <a name="get-invoice-receipt-statement"></a>Hämta kvittoutdrag för faktura

Hämtar ett fakturakvittoutdrag med faktura-ID och kvitto-ID.

> [!IMPORTANT]
> Den här funktionen gäller endast skattekvitton för Taiwan.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.

- Ett giltigt faktura-ID och motsvarande kvitto-ID.

## <a name="c"></a>C\#

Om du vill få ett fakturakvittoutdrag per ID börjar du med Partnercenter-SDK v1.12.0, använder **din IPartner.Invoices-samling** och anropar **metoden ById()** med hjälp av faktura-ID:t. Anropa sedan samlingen **Kvitton** och anropa **ById()** och anropa sedan metoderna **Documents()** och **Statement()** för att komma åt fakturakvittoutdraget. Anropa slutligen metoderna **Get()** eller **GetAsync().**

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
| invoice-id | sträng | Yes      | Värdet är ett faktura-ID som gör att återförsäljaren kan filtrera resultatet för en viss faktura. |
| receipt-id | sträng | Yes      | Värdet är ett kvitto-id som gör att återförsäljaren kan filtrera kvittona för en viss faktura. |

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

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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
