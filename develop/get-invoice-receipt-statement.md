---
title: Hämta kvittoutdrag för faktura
description: Hämtar en faktura kvitto instruktion med hjälp av faktura-ID och kvitto-ID.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768712"
---
# <a name="get-invoice-receipt-statement"></a>Hämta kvittoutdrag för faktura

**Gäller för**

- Partnercenter

Hämtar en faktura kvitto instruktion med hjälp av faktura-ID och kvitto-ID.

> [!IMPORTANT]
> Den här funktionen kan bara användas på Taiwans skatte kvitton.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett giltigt faktura-ID och ett motsvarande kvitto-ID.

## <a name="c"></a>C\#

Om du vill hämta en faktura kvitto policy per ID, som börjar med partner Center SDK v-1.12.0, använder du din **IPartner. fakturor** -samling och anropar metoden **ById ()** med faktura-ID: t och anropar sedan **insamlings** **-och** anrops-ID: **t och** anropar **ById (** ) för att få åtkomst till instruktionen för faktura kvittot. Anropa slutligen metoderna **Get ()** eller **GetAsync ()** .

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample- **klass**: GetInvoiceReceiptStatement.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/Receipts/{Receipt-ID}/Documents/Statement http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att hämta instruktionen för faktura kvittot.

| Namn       | Typ   | Obligatorisk | Beskrivning                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| faktura-ID | sträng | Yes      | Värdet är ett faktura-ID som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik faktura. |
| kvitto-ID | sträng | Yes      | Värdet är ett ID för inleverans som gör det möjligt för åter försäljaren att filtrera kvittona för en specifik faktura. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inget

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en PDF-ström i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

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
