---
title: Hämta faktura efter ID
description: Hämtar en viss faktura med faktura-ID:t.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c888786a6b6ca941629bb7aac95227021c37a7fc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549169"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="f1fbf-103">Hämta faktura efter ID</span><span class="sxs-lookup"><span data-stu-id="f1fbf-103">Get invoice by ID</span></span>

<span data-ttu-id="f1fbf-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f1fbf-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f1fbf-105">Hämtar en viss faktura med faktura-ID:t.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-105">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1fbf-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f1fbf-106">Prerequisites</span></span>

- <span data-ttu-id="f1fbf-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f1fbf-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f1fbf-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f1fbf-109">Ett giltigt faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-109">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="f1fbf-110">C\#</span><span class="sxs-lookup"><span data-stu-id="f1fbf-110">C\#</span></span>

<span data-ttu-id="f1fbf-111">Så här hämtar du en faktura efter ID:</span><span class="sxs-lookup"><span data-stu-id="f1fbf-111">To get an invoice by ID:</span></span>

1. <span data-ttu-id="f1fbf-112">Använd samlingen **IPartner.Invoices** och anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="f1fbf-112">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="f1fbf-113">Anropa **metoderna Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="f1fbf-113">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="f1fbf-114">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f1fbf-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f1fbf-115">**Project:** PartnerSDK.FeatureSample-klass: GetInvoice.cs </span><span class="sxs-lookup"><span data-stu-id="f1fbf-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f1fbf-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f1fbf-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f1fbf-117">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="f1fbf-117">Request syntax</span></span>

| <span data-ttu-id="f1fbf-118">Metod</span><span class="sxs-lookup"><span data-stu-id="f1fbf-118">Method</span></span>  | <span data-ttu-id="f1fbf-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f1fbf-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="f1fbf-120">**Få**</span><span class="sxs-lookup"><span data-stu-id="f1fbf-120">**GET**</span></span> | <span data-ttu-id="f1fbf-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f1fbf-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="f1fbf-122">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="f1fbf-122">URI parameter</span></span>

<span data-ttu-id="f1fbf-123">Använd följande frågeparameter för att hämta fakturan.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-123">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="f1fbf-124">Namn</span><span class="sxs-lookup"><span data-stu-id="f1fbf-124">Name</span></span>           | <span data-ttu-id="f1fbf-125">Typ</span><span class="sxs-lookup"><span data-stu-id="f1fbf-125">Type</span></span>       | <span data-ttu-id="f1fbf-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="f1fbf-126">Required</span></span> | <span data-ttu-id="f1fbf-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="f1fbf-127">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f1fbf-128">**faktura-id**</span><span class="sxs-lookup"><span data-stu-id="f1fbf-128">**invoice-id**</span></span> | <span data-ttu-id="f1fbf-129">**sträng**</span><span class="sxs-lookup"><span data-stu-id="f1fbf-129">**string**</span></span> | <span data-ttu-id="f1fbf-130">Ja</span><span class="sxs-lookup"><span data-stu-id="f1fbf-130">Yes</span></span>      | <span data-ttu-id="f1fbf-131">Värdet är ett **faktura-ID som** gör att återförsäljaren kan filtrera resultatet för en viss faktura.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-131">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f1fbf-132">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f1fbf-132">Request headers</span></span>

<span data-ttu-id="f1fbf-133">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f1fbf-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f1fbf-134">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f1fbf-134">Request body</span></span>

<span data-ttu-id="f1fbf-135">Ingen</span><span class="sxs-lookup"><span data-stu-id="f1fbf-135">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f1fbf-136">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f1fbf-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="f1fbf-137">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f1fbf-137">REST response</span></span>

<span data-ttu-id="f1fbf-138">Om det lyckas returnerar den här metoden [en fakturaresurs](invoice-resources.md#invoice) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-138">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f1fbf-139">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f1fbf-139">Response success and error codes</span></span>

<span data-ttu-id="f1fbf-140">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f1fbf-141">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f1fbf-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f1fbf-142">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f1fbf-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f1fbf-143">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f1fbf-143">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 676
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
Date: Thu, 24 Mar 2016 05:22:14 GMT

{
    "id": "G000024135",
    "invoiceDate": "2018-02-08T22:40:37.5897767Z",
    "billingPeriodStartDate": "2018-02-01T22:40:37.5897767Z",
    "billingPeriodEndDate": "2018-02-28T22:40:37.5897767Z",
    "totalCharges": 2076.63,
    "paidAmount": 0,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "pdfDownloadLink": "/invoices/G000024135/documents/statement",
    "taxReceipts": [
        {
            "id": "123456",
            "taxReceiptPdfDownloadLink": "/invoices/G000024135/receipts/123456/documents/statement"
        }
    ],
    "invoiceDetails": [
        {
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024135/lineitems/OneTime/BillingLineItems",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceDetail"
            }
        }
    ],
    "documentType": "invoice",
    "invoiceType": "OneTime",
    "links": {
        "self": {
            "uri": "/invoices/OneTime-G000024135",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Invoice"
    }
}
```
