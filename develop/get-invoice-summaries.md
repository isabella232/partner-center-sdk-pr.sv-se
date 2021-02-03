---
title: Hämta fakturasammanfattningar
description: Du kan använda en faktura sammanfattnings resurs för varje valuta typ för att Visa saldot och det totala antalet avgifter för både återkommande och engångs kostnader.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 82cd669117db72e1819d941f48f8ea69b2eddaec
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768715"
---
# <a name="get-invoice-summaries"></a><span data-ttu-id="4ecc3-103">Hämta fakturasammanfattningar</span><span class="sxs-lookup"><span data-stu-id="4ecc3-103">Get invoice summaries</span></span>

<span data-ttu-id="4ecc3-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="4ecc3-104">**Applies to:**</span></span>

- <span data-ttu-id="4ecc3-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="4ecc3-105">Partner Center</span></span>
- <span data-ttu-id="4ecc3-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="4ecc3-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4ecc3-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="4ecc3-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4ecc3-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4ecc3-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4ecc3-109">Du kan använda **InvoiceSummaries** för att hämta en faktura sammanfattning som visar saldot och den totala kostnaden för både återkommande och engångs kostnader.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-109">You can use the **InvoiceSummaries** to retrieve an invoice summary which shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="4ecc3-110">**InvoiceSummaries** -resursen innehåller en faktura översikt för varje valuta typ.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-110">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ecc3-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="4ecc3-111">Prerequisites</span></span>

- <span data-ttu-id="4ecc3-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4ecc3-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4ecc3-113">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4ecc3-114">Ett giltigt faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-114">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="4ecc3-115">C\#</span><span class="sxs-lookup"><span data-stu-id="4ecc3-115">C\#</span></span>

<span data-ttu-id="4ecc3-116">Hämta en [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) -samling som innehåller en [**InvoiceSummary**](invoice-resources.md#invoicesummary) för varje valuta typ:</span><span class="sxs-lookup"><span data-stu-id="4ecc3-116">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="4ecc3-117">Använd din **IAggregatePartner. fakturor** -samling för att anropa **sammanfattnings** egenskapen.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-117">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="4ecc3-118">Anropa metoden **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="4ecc3-118">Call the **Get()** method.</span></span>
3. <span data-ttu-id="4ecc3-119">För att få en individuell [**InvoiceSummary**](invoice-resources.md#invoicesummary)kan du komma åt egenskapen **BalanceAmount** för denna medlem i samlingen.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-119">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="4ecc3-120">Mer information finns i följande exempel kod:</span><span class="sxs-lookup"><span data-stu-id="4ecc3-120">For more information, see the following example code:</span></span>

- <span data-ttu-id="4ecc3-121">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4ecc3-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4ecc3-122">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="4ecc3-122">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="4ecc3-123">Klass: **GetInvoiceSummaries.cs**</span><span class="sxs-lookup"><span data-stu-id="4ecc3-123">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="4ecc3-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="4ecc3-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4ecc3-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="4ecc3-125">Request syntax</span></span>

| <span data-ttu-id="4ecc3-126">Metod</span><span class="sxs-lookup"><span data-stu-id="4ecc3-126">Method</span></span>  | <span data-ttu-id="4ecc3-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="4ecc3-127">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="4ecc3-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="4ecc3-128">**GET**</span></span> | <span data-ttu-id="4ecc3-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/Summaries http/1.1</span><span class="sxs-lookup"><span data-stu-id="4ecc3-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="4ecc3-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="4ecc3-130">URI parameter</span></span>

<span data-ttu-id="4ecc3-131">Inga.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-131">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="4ecc3-132">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="4ecc3-132">Request headers</span></span>

<span data-ttu-id="4ecc3-133">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4ecc3-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4ecc3-134">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="4ecc3-134">Request body</span></span>

<span data-ttu-id="4ecc3-135">Inga.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4ecc3-136">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="4ecc3-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="4ecc3-137">REST-svar</span><span class="sxs-lookup"><span data-stu-id="4ecc3-137">REST response</span></span>

<span data-ttu-id="4ecc3-138">Om det lyckas returnerar den här metoden en [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-138">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4ecc3-139">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="4ecc3-139">Response success and error codes</span></span>

<span data-ttu-id="4ecc3-140">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4ecc3-141">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="4ecc3-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4ecc3-142">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4ecc3-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4ecc3-143">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="4ecc3-143">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "totalCount": 3,
    "items": [
        {
            "balanceAmount": 751094.39,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
            "lastPaymentDate": "2017-01-01T12:00:00Z",
            "lastPaymentAmount": 1000,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "Recurring",
                    "summary": {
                        "balanceAmount": 202955.87,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2017-02-27T00:00:00Z",
                        "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
                        "lastPaymentDate": "2017-01-01T12:00:00Z",
                        "lastPaymentAmount": 1000,
                        "latestInvoiceDate": "0001-01-01T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                },
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 548138.52,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1230.33,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1230.33,
                        "currencyCode": "CHF",
                        "currencySymbol": "CHF",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1001.12,
            "currencyCode": "EUR",
            "currencySymbol": "€",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1001.12,
                        "currencyCode": "EUR",
                        "currencySymbol": "€",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/summaries",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
