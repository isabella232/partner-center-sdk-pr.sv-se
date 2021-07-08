---
title: Hämta partnerns aktuella kontosaldo
description: Hämtar partnerns aktuella kontosaldo. En sammanfattning av saldot och de totala avgifterna för en faktura för både återkommande och engångsavgifter.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a04ab63482ec9d06e2fe47d2b6ce1bc6a5fd5f27
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548506"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="45904-104">Hämta partnerns aktuella kontosaldo</span><span class="sxs-lookup"><span data-stu-id="45904-104">Get the partner's current account balance</span></span>

<span data-ttu-id="45904-105">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="45904-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="45904-106">Hämtar partnerns aktuella kontosaldo.</span><span class="sxs-lookup"><span data-stu-id="45904-106">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="45904-107">En sammanfattning av saldot och de totala avgifterna för en faktura för både återkommande och engångsavgifter.</span><span class="sxs-lookup"><span data-stu-id="45904-107">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45904-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="45904-108">Prerequisites</span></span>

- <span data-ttu-id="45904-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="45904-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="45904-110">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="45904-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="45904-111">C\#</span><span class="sxs-lookup"><span data-stu-id="45904-111">C\#</span></span>

<span data-ttu-id="45904-112">Om du vill hämta ditt kontosaldo använder **du samlingen IAggregatePartner.Invoices** och anropar sedan **egenskapen** Sammanfattning.</span><span class="sxs-lookup"><span data-stu-id="45904-112">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="45904-113">Anropa sedan **funktionen Get** och anropa slutligen egenskapen **BalanceAmount.**</span><span class="sxs-lookup"><span data-stu-id="45904-113">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="45904-114">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="45904-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="45904-115">**Project:** PartnerSDK.FeatureSample-klass: GetInvoiceSummary.cs </span><span class="sxs-lookup"><span data-stu-id="45904-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="45904-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="45904-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="45904-117">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="45904-117">Request syntax</span></span>

| <span data-ttu-id="45904-118">Metod</span><span class="sxs-lookup"><span data-stu-id="45904-118">Method</span></span>  | <span data-ttu-id="45904-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="45904-119">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="45904-120">**Få**</span><span class="sxs-lookup"><span data-stu-id="45904-120">**GET**</span></span> | <span data-ttu-id="45904-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="45904-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="45904-122">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="45904-122">Request headers</span></span>

<span data-ttu-id="45904-123">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="45904-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="45904-124">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="45904-124">Request body</span></span>

<span data-ttu-id="45904-125">Ingen</span><span class="sxs-lookup"><span data-stu-id="45904-125">None</span></span>

### <a name="request-example"></a><span data-ttu-id="45904-126">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="45904-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="45904-127">REST-svar</span><span class="sxs-lookup"><span data-stu-id="45904-127">REST response</span></span>

<span data-ttu-id="45904-128">Om det lyckas returnerar den här [metoden en InvoiceSummary-resurs](invoice-resources.md#invoicesummary) i svaret.</span><span class="sxs-lookup"><span data-stu-id="45904-128">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="45904-129">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="45904-129">Response success and error codes</span></span>

<span data-ttu-id="45904-130">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="45904-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="45904-131">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="45904-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="45904-132">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="45904-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="45904-133">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="45904-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "balanceAmount": 751094.39,
    "currencyCode": "USD",
    "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
```
