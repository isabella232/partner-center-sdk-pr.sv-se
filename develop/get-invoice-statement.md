---
title: Hämta fakturautdrag
description: Hämtar ett fakturautdrag med faktura-ID:t.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f0324916eb2efd9244530a53b1d7bb4abc0c8e6e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549135"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="dfc0b-103">Hämta fakturautdrag</span><span class="sxs-lookup"><span data-stu-id="dfc0b-103">Get invoice statement</span></span>

<span data-ttu-id="dfc0b-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="dfc0b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfc0b-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="dfc0b-105">Prerequisites</span></span>

- <span data-ttu-id="dfc0b-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dfc0b-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dfc0b-107">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="dfc0b-108">Ett giltigt faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-108">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="dfc0b-109">C\#</span><span class="sxs-lookup"><span data-stu-id="dfc0b-109">C\#</span></span>

<span data-ttu-id="dfc0b-110">Om du vill hämta ett fakturautdrag efter ID använder du **samlingen IPartner.Invoices** och anropar **Metoden ById()** med faktura-ID:t och anropar sedan metoderna **Documents()** **och Statement()** för att komma åt fakturautdraget.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-110">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="dfc0b-111">Anropa slutligen metoderna **Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="dfc0b-111">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="dfc0b-112">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="dfc0b-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="dfc0b-113">**Project:** PartnerSDK.FeatureSample-klass: GetInvoiceStatement.cs </span><span class="sxs-lookup"><span data-stu-id="dfc0b-113">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="dfc0b-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="dfc0b-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dfc0b-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="dfc0b-115">Request syntax</span></span>

| <span data-ttu-id="dfc0b-116">Metod</span><span class="sxs-lookup"><span data-stu-id="dfc0b-116">Method</span></span>  | <span data-ttu-id="dfc0b-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="dfc0b-117">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dfc0b-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="dfc0b-118">**GET**</span></span> | <span data-ttu-id="dfc0b-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="dfc0b-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="dfc0b-120">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="dfc0b-120">URI parameter</span></span>

<span data-ttu-id="dfc0b-121">Använd följande frågeparameter för att hämta fakturautdraget.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-121">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="dfc0b-122">Namn</span><span class="sxs-lookup"><span data-stu-id="dfc0b-122">Name</span></span>       | <span data-ttu-id="dfc0b-123">Typ</span><span class="sxs-lookup"><span data-stu-id="dfc0b-123">Type</span></span>       | <span data-ttu-id="dfc0b-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="dfc0b-124">Required</span></span> | <span data-ttu-id="dfc0b-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="dfc0b-125">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dfc0b-126">faktura-id</span><span class="sxs-lookup"><span data-stu-id="dfc0b-126">invoice-id</span></span> | <span data-ttu-id="dfc0b-127">sträng</span><span class="sxs-lookup"><span data-stu-id="dfc0b-127">string</span></span>     | <span data-ttu-id="dfc0b-128">Ja</span><span class="sxs-lookup"><span data-stu-id="dfc0b-128">Yes</span></span>      | <span data-ttu-id="dfc0b-129">Värdet är ett faktura-ID som gör att återförsäljaren kan filtrera resultatet för en viss faktura.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-129">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dfc0b-130">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="dfc0b-130">Request headers</span></span>

<span data-ttu-id="dfc0b-131">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dfc0b-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dfc0b-132">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="dfc0b-132">Request body</span></span>

<span data-ttu-id="dfc0b-133">Ingen</span><span class="sxs-lookup"><span data-stu-id="dfc0b-133">None</span></span>

### <a name="request-example"></a><span data-ttu-id="dfc0b-134">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="dfc0b-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="dfc0b-135">REST-svar</span><span class="sxs-lookup"><span data-stu-id="dfc0b-135">REST response</span></span>

<span data-ttu-id="dfc0b-136">Om det lyckas returnerar den här metoden [en InvoiceStatement-resurs](invoice-resources.md#invoicestatement) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-136">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dfc0b-137">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="dfc0b-137">Response success and error codes</span></span>

<span data-ttu-id="dfc0b-138">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dfc0b-139">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dfc0b-140">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="dfc0b-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dfc0b-141">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="dfc0b-141">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
