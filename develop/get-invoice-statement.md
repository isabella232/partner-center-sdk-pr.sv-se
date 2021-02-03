---
title: Hämta fakturautdrag
description: Hämtar en faktura instruktion med hjälp av faktura-ID.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 42e5201919eea5644da463dfe2584c8d55002083
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769015"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="44031-103">Hämta fakturautdrag</span><span class="sxs-lookup"><span data-stu-id="44031-103">Get invoice statement</span></span>

<span data-ttu-id="44031-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="44031-104">**Applies To**</span></span>

- <span data-ttu-id="44031-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="44031-105">Partner Center</span></span>
- <span data-ttu-id="44031-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="44031-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="44031-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="44031-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="44031-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44031-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="44031-109">Hämtar en faktura instruktion med hjälp av faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="44031-109">Retrieves an invoice statement using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44031-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="44031-110">Prerequisites</span></span>

- <span data-ttu-id="44031-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="44031-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44031-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="44031-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="44031-113">Ett giltigt faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="44031-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="44031-114">C\#</span><span class="sxs-lookup"><span data-stu-id="44031-114">C\#</span></span>

<span data-ttu-id="44031-115">Om du vill hämta en faktura rapport per ID använder du din **IPartner. fakturor** -samling och anropar metoden **ById ()** med faktura-ID: t och anropar sedan metoderna **Documents ()** och **statement ()** för att få åtkomst till faktura utdraget.</span><span class="sxs-lookup"><span data-stu-id="44031-115">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="44031-116">Anropa slutligen metoderna **Get ()** eller **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="44031-116">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="44031-117">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="44031-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="44031-118">**Projekt**: PartnerSDK. FeatureSample- **klass**: GetInvoiceStatement.CS</span><span class="sxs-lookup"><span data-stu-id="44031-118">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="44031-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="44031-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44031-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="44031-120">Request syntax</span></span>

| <span data-ttu-id="44031-121">Metod</span><span class="sxs-lookup"><span data-stu-id="44031-121">Method</span></span>  | <span data-ttu-id="44031-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="44031-122">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44031-123">**TA**</span><span class="sxs-lookup"><span data-stu-id="44031-123">**GET**</span></span> | <span data-ttu-id="44031-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/Documents/Statement http/1.1</span><span class="sxs-lookup"><span data-stu-id="44031-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="44031-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="44031-125">URI parameter</span></span>

<span data-ttu-id="44031-126">Använd följande frågeparameter för att hämta faktura instruktionen.</span><span class="sxs-lookup"><span data-stu-id="44031-126">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="44031-127">Namn</span><span class="sxs-lookup"><span data-stu-id="44031-127">Name</span></span>       | <span data-ttu-id="44031-128">Typ</span><span class="sxs-lookup"><span data-stu-id="44031-128">Type</span></span>       | <span data-ttu-id="44031-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="44031-129">Required</span></span> | <span data-ttu-id="44031-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="44031-130">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44031-131">faktura-ID</span><span class="sxs-lookup"><span data-stu-id="44031-131">invoice-id</span></span> | <span data-ttu-id="44031-132">sträng</span><span class="sxs-lookup"><span data-stu-id="44031-132">string</span></span>     | <span data-ttu-id="44031-133">Yes</span><span class="sxs-lookup"><span data-stu-id="44031-133">Yes</span></span>      | <span data-ttu-id="44031-134">Värdet är ett faktura-ID som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik faktura.</span><span class="sxs-lookup"><span data-stu-id="44031-134">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="44031-135">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="44031-135">Request headers</span></span>

<span data-ttu-id="44031-136">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="44031-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44031-137">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="44031-137">Request body</span></span>

<span data-ttu-id="44031-138">Inget</span><span class="sxs-lookup"><span data-stu-id="44031-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="44031-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="44031-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="44031-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="44031-140">REST response</span></span>

<span data-ttu-id="44031-141">Om det lyckas returnerar den här metoden en [InvoiceStatement](invoice-resources.md#invoicestatement) -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="44031-141">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44031-142">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="44031-142">Response success and error codes</span></span>

<span data-ttu-id="44031-143">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="44031-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44031-144">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="44031-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44031-145">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="44031-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44031-146">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="44031-146">Response example</span></span>

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
