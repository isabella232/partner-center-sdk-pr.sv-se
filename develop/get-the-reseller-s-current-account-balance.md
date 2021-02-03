---
title: Hämta partnerns aktuella kontosaldo
description: Hämtar partnerns aktuella konto saldo. En sammanfattning av saldot och den totala kostnaden för en faktura för både återkommande och engångs kostnader.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 110da433faa6ff4d3d068c6d68a6f497f4a2721a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769045"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="cfcaa-104">Hämta partnerns aktuella kontosaldo</span><span class="sxs-lookup"><span data-stu-id="cfcaa-104">Get the partner's current account balance</span></span>

<span data-ttu-id="cfcaa-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="cfcaa-105">**Applies To**</span></span>

- <span data-ttu-id="cfcaa-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="cfcaa-106">Partner Center</span></span>
- <span data-ttu-id="cfcaa-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cfcaa-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cfcaa-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="cfcaa-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cfcaa-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cfcaa-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cfcaa-110">Hämtar partnerns aktuella konto saldo.</span><span class="sxs-lookup"><span data-stu-id="cfcaa-110">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="cfcaa-111">En sammanfattning av saldot och den totala kostnaden för en faktura för både återkommande och engångs kostnader.</span><span class="sxs-lookup"><span data-stu-id="cfcaa-111">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfcaa-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cfcaa-112">Prerequisites</span></span>

- <span data-ttu-id="cfcaa-113">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cfcaa-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cfcaa-114">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cfcaa-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="cfcaa-115">C\#</span><span class="sxs-lookup"><span data-stu-id="cfcaa-115">C\#</span></span>

<span data-ttu-id="cfcaa-116">Om du vill hämta ditt kontosaldo använder du din **IAggregatePartner. fakturor** -samling och anropar sedan **sammanfattnings** egenskapen.</span><span class="sxs-lookup"><span data-stu-id="cfcaa-116">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="cfcaa-117">Anropa sedan funktionen **Get** och anropa slutligen egenskapen **BalanceAmount** .</span><span class="sxs-lookup"><span data-stu-id="cfcaa-117">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="cfcaa-118">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cfcaa-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cfcaa-119">**Projekt**: PartnerSDK. FeatureSample- **klass**: GetInvoiceSummary.CS</span><span class="sxs-lookup"><span data-stu-id="cfcaa-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cfcaa-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cfcaa-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cfcaa-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="cfcaa-121">Request syntax</span></span>

| <span data-ttu-id="cfcaa-122">Metod</span><span class="sxs-lookup"><span data-stu-id="cfcaa-122">Method</span></span>  | <span data-ttu-id="cfcaa-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cfcaa-123">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="cfcaa-124">**TA**</span><span class="sxs-lookup"><span data-stu-id="cfcaa-124">**GET**</span></span> | <span data-ttu-id="cfcaa-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/Summary http/1.1</span><span class="sxs-lookup"><span data-stu-id="cfcaa-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="cfcaa-126">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cfcaa-126">Request headers</span></span>

<span data-ttu-id="cfcaa-127">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cfcaa-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cfcaa-128">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cfcaa-128">Request body</span></span>

<span data-ttu-id="cfcaa-129">Inget</span><span class="sxs-lookup"><span data-stu-id="cfcaa-129">None</span></span>

### <a name="request-example"></a><span data-ttu-id="cfcaa-130">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cfcaa-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="cfcaa-131">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cfcaa-131">REST response</span></span>

<span data-ttu-id="cfcaa-132">Om det lyckas returnerar den här metoden en [InvoiceSummary](invoice-resources.md#invoicesummary) -resurs i svaret.</span><span class="sxs-lookup"><span data-stu-id="cfcaa-132">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cfcaa-133">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cfcaa-133">Response success and error codes</span></span>

<span data-ttu-id="cfcaa-134">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="cfcaa-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cfcaa-135">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cfcaa-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cfcaa-136">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cfcaa-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cfcaa-137">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cfcaa-137">Response example</span></span>

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
