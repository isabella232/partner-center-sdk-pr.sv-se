---
title: Hämta fakturasammanfattningar
description: Du kan använda en resurs för fakturasammanfattningar för varje valutatyp för att visa saldot och de totala avgifterna för både återkommande och engångsavgifter.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: fb6ff839c56c7b0b77a9904abf05d95ca0500b00
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549118"
---
# <a name="get-invoice-summaries"></a><span data-ttu-id="189c7-103">Hämta fakturasammanfattningar</span><span class="sxs-lookup"><span data-stu-id="189c7-103">Get invoice summaries</span></span>

<span data-ttu-id="189c7-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="189c7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="189c7-105">Du kan använda **InvoiceSummaries för att** hämta en fakturasammanfattning som visar saldot och de totala avgifterna för både återkommande och engångsavgifter.</span><span class="sxs-lookup"><span data-stu-id="189c7-105">You can use the **InvoiceSummaries** to retrieve an invoice summary that shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="189c7-106">Resursen **InvoiceSummaries** innehåller en fakturasammanfattning för varje valutatyp.</span><span class="sxs-lookup"><span data-stu-id="189c7-106">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="189c7-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="189c7-107">Prerequisites</span></span>

- <span data-ttu-id="189c7-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="189c7-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="189c7-109">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="189c7-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="189c7-110">En giltig fakturaidentifierare.</span><span class="sxs-lookup"><span data-stu-id="189c7-110">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="189c7-111">C\#</span><span class="sxs-lookup"><span data-stu-id="189c7-111">C\#</span></span>

<span data-ttu-id="189c7-112">Så här hämtar [**du en InvoiceSummaries-samling**](invoice-resources.md#invoicesummaries) som innehåller [**en InvoiceSummary**](invoice-resources.md#invoicesummary) för varje valutatyp:</span><span class="sxs-lookup"><span data-stu-id="189c7-112">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="189c7-113">Använd din **IAggregatePartner.Invoices-samling** för att anropa **egenskapen Sammanfattningar.**</span><span class="sxs-lookup"><span data-stu-id="189c7-113">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="189c7-114">Anropa **metoden Get().**</span><span class="sxs-lookup"><span data-stu-id="189c7-114">Call the **Get()** method.</span></span>
3. <span data-ttu-id="189c7-115">Om du vill hämta saldot för en [**enskild InvoiceSummary**](invoice-resources.md#invoicesummary)får du åtkomst till **egenskapen BalanceAmount** för den medlemmen i samlingen.</span><span class="sxs-lookup"><span data-stu-id="189c7-115">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="189c7-116">Mer information finns i följande exempelkod:</span><span class="sxs-lookup"><span data-stu-id="189c7-116">For more information, see the following example code:</span></span>

- <span data-ttu-id="189c7-117">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="189c7-117">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="189c7-118">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="189c7-118">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="189c7-119">Klass: **GetInvoiceSummaries.cs**</span><span class="sxs-lookup"><span data-stu-id="189c7-119">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="189c7-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="189c7-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="189c7-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="189c7-121">Request syntax</span></span>

| <span data-ttu-id="189c7-122">Metod</span><span class="sxs-lookup"><span data-stu-id="189c7-122">Method</span></span>  | <span data-ttu-id="189c7-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="189c7-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="189c7-124">**Få**</span><span class="sxs-lookup"><span data-stu-id="189c7-124">**GET**</span></span> | <span data-ttu-id="189c7-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="189c7-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="189c7-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="189c7-126">URI parameter</span></span>

<span data-ttu-id="189c7-127">Inga.</span><span class="sxs-lookup"><span data-stu-id="189c7-127">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="189c7-128">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="189c7-128">Request headers</span></span>

<span data-ttu-id="189c7-129">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="189c7-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="189c7-130">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="189c7-130">Request body</span></span>

<span data-ttu-id="189c7-131">Inga.</span><span class="sxs-lookup"><span data-stu-id="189c7-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="189c7-132">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="189c7-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="189c7-133">REST-svar</span><span class="sxs-lookup"><span data-stu-id="189c7-133">REST response</span></span>

<span data-ttu-id="189c7-134">Om det lyckas returnerar den här metoden [**en InvoiceSummaries-resurs**](invoice-resources.md#invoicesummaries) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="189c7-134">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="189c7-135">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="189c7-135">Response success and error codes</span></span>

<span data-ttu-id="189c7-136">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="189c7-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="189c7-137">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="189c7-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="189c7-138">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="189c7-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="189c7-139">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="189c7-139">Response example</span></span>

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
