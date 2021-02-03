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
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="ed4cf-103">Hämta kvittoutdrag för faktura</span><span class="sxs-lookup"><span data-stu-id="ed4cf-103">Get invoice receipt statement</span></span>

<span data-ttu-id="ed4cf-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="ed4cf-104">**Applies To**</span></span>

- <span data-ttu-id="ed4cf-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="ed4cf-105">Partner Center</span></span>

<span data-ttu-id="ed4cf-106">Hämtar en faktura kvitto instruktion med hjälp av faktura-ID och kvitto-ID.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-106">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed4cf-107">Den här funktionen kan bara användas på Taiwans skatte kvitton.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-107">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed4cf-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ed4cf-108">Prerequisites</span></span>

- <span data-ttu-id="ed4cf-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ed4cf-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ed4cf-110">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ed4cf-111">Ett giltigt faktura-ID och ett motsvarande kvitto-ID.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-111">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="ed4cf-112">C\#</span><span class="sxs-lookup"><span data-stu-id="ed4cf-112">C\#</span></span>

<span data-ttu-id="ed4cf-113">Om du vill hämta en faktura kvitto policy per ID, som börjar med partner Center SDK v-1.12.0, använder du din **IPartner. fakturor** -samling och anropar metoden **ById ()** med faktura-ID: t och anropar sedan **insamlings** **-och** anrops-ID: **t och** anropar **ById (** ) för att få åtkomst till instruktionen för faktura kvittot.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-113">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="ed4cf-114">Anropa slutligen metoderna **Get ()** eller **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="ed4cf-114">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="ed4cf-115">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ed4cf-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ed4cf-116">**Projekt**: PartnerSDK. FeatureSample- **klass**: GetInvoiceReceiptStatement.CS</span><span class="sxs-lookup"><span data-stu-id="ed4cf-116">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ed4cf-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ed4cf-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ed4cf-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="ed4cf-118">Request syntax</span></span>

| <span data-ttu-id="ed4cf-119">Metod</span><span class="sxs-lookup"><span data-stu-id="ed4cf-119">Method</span></span>  | <span data-ttu-id="ed4cf-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ed4cf-120">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ed4cf-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="ed4cf-121">**GET**</span></span> | <span data-ttu-id="ed4cf-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/Receipts/{Receipt-ID}/Documents/Statement http/1.1</span><span class="sxs-lookup"><span data-stu-id="ed4cf-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ed4cf-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ed4cf-123">URI parameter</span></span>

<span data-ttu-id="ed4cf-124">Använd följande frågeparameter för att hämta instruktionen för faktura kvittot.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-124">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="ed4cf-125">Namn</span><span class="sxs-lookup"><span data-stu-id="ed4cf-125">Name</span></span>       | <span data-ttu-id="ed4cf-126">Typ</span><span class="sxs-lookup"><span data-stu-id="ed4cf-126">Type</span></span>   | <span data-ttu-id="ed4cf-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ed4cf-127">Required</span></span> | <span data-ttu-id="ed4cf-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ed4cf-128">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ed4cf-129">faktura-ID</span><span class="sxs-lookup"><span data-stu-id="ed4cf-129">invoice-id</span></span> | <span data-ttu-id="ed4cf-130">sträng</span><span class="sxs-lookup"><span data-stu-id="ed4cf-130">string</span></span> | <span data-ttu-id="ed4cf-131">Yes</span><span class="sxs-lookup"><span data-stu-id="ed4cf-131">Yes</span></span>      | <span data-ttu-id="ed4cf-132">Värdet är ett faktura-ID som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik faktura.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-132">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="ed4cf-133">kvitto-ID</span><span class="sxs-lookup"><span data-stu-id="ed4cf-133">receipt-id</span></span> | <span data-ttu-id="ed4cf-134">sträng</span><span class="sxs-lookup"><span data-stu-id="ed4cf-134">string</span></span> | <span data-ttu-id="ed4cf-135">Yes</span><span class="sxs-lookup"><span data-stu-id="ed4cf-135">Yes</span></span>      | <span data-ttu-id="ed4cf-136">Värdet är ett ID för inleverans som gör det möjligt för åter försäljaren att filtrera kvittona för en specifik faktura.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-136">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ed4cf-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ed4cf-137">Request headers</span></span>

<span data-ttu-id="ed4cf-138">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ed4cf-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ed4cf-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ed4cf-139">Request body</span></span>

<span data-ttu-id="ed4cf-140">Inget</span><span class="sxs-lookup"><span data-stu-id="ed4cf-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="ed4cf-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ed4cf-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="ed4cf-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ed4cf-142">REST response</span></span>

<span data-ttu-id="ed4cf-143">Om det lyckas returnerar den här metoden en PDF-ström i svars texten.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-143">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ed4cf-144">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ed4cf-144">Response success and error codes</span></span>

<span data-ttu-id="ed4cf-145">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ed4cf-146">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ed4cf-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ed4cf-147">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ed4cf-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ed4cf-148">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ed4cf-148">Response example</span></span>

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
