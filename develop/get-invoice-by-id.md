---
title: Hämta faktura efter ID
description: Hämtar en faktura med hjälp av faktura-ID.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 17880265d06e8e5eaacc5470d83c49defd10ad51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768718"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="d2561-103">Hämta faktura efter ID</span><span class="sxs-lookup"><span data-stu-id="d2561-103">Get invoice by ID</span></span>

<span data-ttu-id="d2561-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="d2561-104">**Applies to:**</span></span>

- <span data-ttu-id="d2561-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d2561-105">Partner Center</span></span>
- <span data-ttu-id="d2561-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d2561-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d2561-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="d2561-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d2561-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d2561-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d2561-109">Hämtar en faktura med hjälp av faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="d2561-109">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2561-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d2561-110">Prerequisites</span></span>

- <span data-ttu-id="d2561-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d2561-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d2561-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d2561-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d2561-113">Ett giltigt faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="d2561-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="d2561-114">C\#</span><span class="sxs-lookup"><span data-stu-id="d2561-114">C\#</span></span>

<span data-ttu-id="d2561-115">Så här hämtar du en faktura efter ID:</span><span class="sxs-lookup"><span data-stu-id="d2561-115">To get an invoice by ID:</span></span>

1. <span data-ttu-id="d2561-116">Använd din **IPartner. fakturor** -samling och anropa **ById ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="d2561-116">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="d2561-117">Anropa metoderna **Get ()** eller **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="d2561-117">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="d2561-118">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d2561-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d2561-119">**Projekt**: PartnerSDK. FeatureSample- **klass**: GetInvoice.CS</span><span class="sxs-lookup"><span data-stu-id="d2561-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d2561-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d2561-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d2561-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d2561-121">Request syntax</span></span>

| <span data-ttu-id="d2561-122">Metod</span><span class="sxs-lookup"><span data-stu-id="d2561-122">Method</span></span>  | <span data-ttu-id="d2561-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d2561-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="d2561-124">**TA**</span><span class="sxs-lookup"><span data-stu-id="d2561-124">**GET**</span></span> | <span data-ttu-id="d2561-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d2561-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d2561-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d2561-126">URI parameter</span></span>

<span data-ttu-id="d2561-127">Använd följande frågeparameter för att hämta fakturan.</span><span class="sxs-lookup"><span data-stu-id="d2561-127">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="d2561-128">Namn</span><span class="sxs-lookup"><span data-stu-id="d2561-128">Name</span></span>           | <span data-ttu-id="d2561-129">Typ</span><span class="sxs-lookup"><span data-stu-id="d2561-129">Type</span></span>       | <span data-ttu-id="d2561-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d2561-130">Required</span></span> | <span data-ttu-id="d2561-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d2561-131">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2561-132">**faktura-ID**</span><span class="sxs-lookup"><span data-stu-id="d2561-132">**invoice-id**</span></span> | <span data-ttu-id="d2561-133">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="d2561-133">**string**</span></span> | <span data-ttu-id="d2561-134">Yes</span><span class="sxs-lookup"><span data-stu-id="d2561-134">Yes</span></span>      | <span data-ttu-id="d2561-135">Värdet är ett **faktura-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik faktura.</span><span class="sxs-lookup"><span data-stu-id="d2561-135">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d2561-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d2561-136">Request headers</span></span>

<span data-ttu-id="d2561-137">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d2561-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d2561-138">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d2561-138">Request body</span></span>

<span data-ttu-id="d2561-139">Inget</span><span class="sxs-lookup"><span data-stu-id="d2561-139">None</span></span>

### <a name="request-example"></a><span data-ttu-id="d2561-140">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d2561-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="d2561-141">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d2561-141">REST response</span></span>

<span data-ttu-id="d2561-142">Om det lyckas returnerar den här metoden en [faktura](invoice-resources.md#invoice) resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="d2561-142">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d2561-143">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d2561-143">Response success and error codes</span></span>

<span data-ttu-id="d2561-144">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d2561-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d2561-145">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d2561-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d2561-146">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d2561-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d2561-147">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d2561-147">Response example</span></span>

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
