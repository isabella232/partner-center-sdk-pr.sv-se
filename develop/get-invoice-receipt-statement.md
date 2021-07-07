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
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="57bdd-103">Hämta kvittoutdrag för faktura</span><span class="sxs-lookup"><span data-stu-id="57bdd-103">Get invoice receipt statement</span></span>

<span data-ttu-id="57bdd-104">Hämtar ett fakturakvittoutdrag med faktura-ID och kvitto-ID.</span><span class="sxs-lookup"><span data-stu-id="57bdd-104">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57bdd-105">Den här funktionen gäller endast skattekvitton för Taiwan.</span><span class="sxs-lookup"><span data-stu-id="57bdd-105">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57bdd-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="57bdd-106">Prerequisites</span></span>

- <span data-ttu-id="57bdd-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="57bdd-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="57bdd-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="57bdd-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="57bdd-109">Ett giltigt faktura-ID och motsvarande kvitto-ID.</span><span class="sxs-lookup"><span data-stu-id="57bdd-109">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="57bdd-110">C\#</span><span class="sxs-lookup"><span data-stu-id="57bdd-110">C\#</span></span>

<span data-ttu-id="57bdd-111">Om du vill hämta ett fakturakvittoutdrag efter ID börjar du med Partnercenter-SDK v1.12.0, använder **samlingen IPartner.Invoices** och anropar **Metoden ById()** med faktura-ID:t. Anropa sedan samlingen **Kvitton** och anropa **ById()** och anropa sedan metoderna **Documents()** och **Statement()** för att få åtkomst till fakturakvittoutdraget.</span><span class="sxs-lookup"><span data-stu-id="57bdd-111">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="57bdd-112">Anropa slutligen metoderna **Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="57bdd-112">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="57bdd-113">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="57bdd-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="57bdd-114">**Project:** PartnerSDK.FeatureSample-klass: GetInvoiceReceiptStatement.cs </span><span class="sxs-lookup"><span data-stu-id="57bdd-114">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="57bdd-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="57bdd-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="57bdd-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="57bdd-116">Request syntax</span></span>

| <span data-ttu-id="57bdd-117">Metod</span><span class="sxs-lookup"><span data-stu-id="57bdd-117">Method</span></span>  | <span data-ttu-id="57bdd-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="57bdd-118">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="57bdd-119">**Få**</span><span class="sxs-lookup"><span data-stu-id="57bdd-119">**GET**</span></span> | <span data-ttu-id="57bdd-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="57bdd-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="57bdd-121">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="57bdd-121">URI parameter</span></span>

<span data-ttu-id="57bdd-122">Använd följande frågeparameter för att hämta fakturakvittoutdraget.</span><span class="sxs-lookup"><span data-stu-id="57bdd-122">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="57bdd-123">Namn</span><span class="sxs-lookup"><span data-stu-id="57bdd-123">Name</span></span>       | <span data-ttu-id="57bdd-124">Typ</span><span class="sxs-lookup"><span data-stu-id="57bdd-124">Type</span></span>   | <span data-ttu-id="57bdd-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="57bdd-125">Required</span></span> | <span data-ttu-id="57bdd-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="57bdd-126">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="57bdd-127">faktura-id</span><span class="sxs-lookup"><span data-stu-id="57bdd-127">invoice-id</span></span> | <span data-ttu-id="57bdd-128">sträng</span><span class="sxs-lookup"><span data-stu-id="57bdd-128">string</span></span> | <span data-ttu-id="57bdd-129">Ja</span><span class="sxs-lookup"><span data-stu-id="57bdd-129">Yes</span></span>      | <span data-ttu-id="57bdd-130">Värdet är ett faktura-ID som gör att återförsäljaren kan filtrera resultatet för en viss faktura.</span><span class="sxs-lookup"><span data-stu-id="57bdd-130">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="57bdd-131">receipt-id</span><span class="sxs-lookup"><span data-stu-id="57bdd-131">receipt-id</span></span> | <span data-ttu-id="57bdd-132">sträng</span><span class="sxs-lookup"><span data-stu-id="57bdd-132">string</span></span> | <span data-ttu-id="57bdd-133">Ja</span><span class="sxs-lookup"><span data-stu-id="57bdd-133">Yes</span></span>      | <span data-ttu-id="57bdd-134">Värdet är ett kvitto-ID som gör att återförsäljaren kan filtrera kvittona för en viss faktura.</span><span class="sxs-lookup"><span data-stu-id="57bdd-134">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="57bdd-135">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="57bdd-135">Request headers</span></span>

<span data-ttu-id="57bdd-136">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="57bdd-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="57bdd-137">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="57bdd-137">Request body</span></span>

<span data-ttu-id="57bdd-138">Ingen</span><span class="sxs-lookup"><span data-stu-id="57bdd-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="57bdd-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="57bdd-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="57bdd-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="57bdd-140">REST response</span></span>

<span data-ttu-id="57bdd-141">Om det lyckas returnerar den här metoden en pdf-ström i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="57bdd-141">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="57bdd-142">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="57bdd-142">Response success and error codes</span></span>

<span data-ttu-id="57bdd-143">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="57bdd-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="57bdd-144">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="57bdd-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="57bdd-145">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="57bdd-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="57bdd-146">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="57bdd-146">Response example</span></span>

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
