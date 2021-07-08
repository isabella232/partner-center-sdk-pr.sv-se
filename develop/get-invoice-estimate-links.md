---
title: Hämta länkar för fakturauppskattning
description: Du kan hämta en samling uppskattningslänkar till information om avstämningsradobjekt.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 719becd3fac5605c4ad48ab86d483ba7903d65d8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549152"
---
# <a name="get-invoice-estimate-links"></a><span data-ttu-id="df207-103">Hämta länkar för fakturauppskattning</span><span class="sxs-lookup"><span data-stu-id="df207-103">Get invoice estimate links</span></span>

<span data-ttu-id="df207-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="df207-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="df207-105">Du kan få uppskattningslänkar som hjälper dig att fråga efter information om ej fakturerade avstämningsradsobjekt.</span><span class="sxs-lookup"><span data-stu-id="df207-105">You can get estimate links to help query details for unbilled reconciliation line items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df207-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="df207-106">Prerequisites</span></span>

- <span data-ttu-id="df207-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="df207-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="df207-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="df207-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="df207-109">En fakturaidentifierare.</span><span class="sxs-lookup"><span data-stu-id="df207-109">An invoice identifier.</span></span> <span data-ttu-id="df207-110">Detta identifierar fakturan som radobjekten ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="df207-110">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="df207-111">C\#</span><span class="sxs-lookup"><span data-stu-id="df207-111">C\#</span></span>

<span data-ttu-id="df207-112">Följande exempelkod visar hur du kan hämta uppskattningslänkarna för att fråga efter ej fakturerade radobjekt för en viss valuta.</span><span class="sxs-lookup"><span data-stu-id="df207-112">The following example code shows how you can get the estimate links to query unbilled line items for a given currency.</span></span> <span data-ttu-id="df207-113">Svaret innehåller uppskattningslänkarna för varje period (till exempel aktuell och föregående månad).</span><span class="sxs-lookup"><span data-stu-id="df207-113">The response contains the estimate links for each period (for example, the current and previous month).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

<span data-ttu-id="df207-114">Ett liknande exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="df207-114">For a similar example, see the following:</span></span>

- <span data-ttu-id="df207-115">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="df207-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="df207-116">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="df207-116">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="df207-117">Klass: **GetEstimatesLinks.cs**</span><span class="sxs-lookup"><span data-stu-id="df207-117">Class: **GetEstimatesLinks.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="df207-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="df207-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="df207-119">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="df207-119">Request syntax</span></span>

| <span data-ttu-id="df207-120">Metod</span><span class="sxs-lookup"><span data-stu-id="df207-120">Method</span></span>  | <span data-ttu-id="df207-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="df207-121">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="df207-122">**Få**</span><span class="sxs-lookup"><span data-stu-id="df207-122">**GET**</span></span> | <span data-ttu-id="df207-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="df207-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="df207-124">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="df207-124">URI parameters</span></span>

<span data-ttu-id="df207-125">Använd följande URI och frågeparameter när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="df207-125">Use the following URI and query parameter when creating the request.</span></span>

| <span data-ttu-id="df207-126">Namn</span><span class="sxs-lookup"><span data-stu-id="df207-126">Name</span></span>                   | <span data-ttu-id="df207-127">Typ</span><span class="sxs-lookup"><span data-stu-id="df207-127">Type</span></span>   | <span data-ttu-id="df207-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="df207-128">Required</span></span> | <span data-ttu-id="df207-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="df207-129">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="df207-130">currencyCode</span><span class="sxs-lookup"><span data-stu-id="df207-130">currencyCode</span></span>           | <span data-ttu-id="df207-131">sträng</span><span class="sxs-lookup"><span data-stu-id="df207-131">string</span></span> | <span data-ttu-id="df207-132">Ja</span><span class="sxs-lookup"><span data-stu-id="df207-132">Yes</span></span>      | <span data-ttu-id="df207-133">Valutakoden för de ej fakturerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="df207-133">The currency code for the unbilled line items.</span></span>                    |

### <a name="request-headers"></a><span data-ttu-id="df207-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="df207-134">Request headers</span></span>

<span data-ttu-id="df207-135">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="df207-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="df207-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="df207-136">Request body</span></span>

<span data-ttu-id="df207-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="df207-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="df207-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="df207-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="df207-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="df207-139">REST response</span></span>

<span data-ttu-id="df207-140">Om det lyckas innehåller svaret länkar för att hämta ej fakturerade uppskattningar.</span><span class="sxs-lookup"><span data-stu-id="df207-140">If successful, the response contains the links to retrieve unbilled estimates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="df207-141">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="df207-141">Response success and error codes</span></span>

<span data-ttu-id="df207-142">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="df207-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="df207-143">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="df207-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="df207-144">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="df207-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="df207-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="df207-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 80EAA055-B5D3-4D88-BFE8-924A3F706462
MS-RequestId: 1b18689e-3fe3-4fdb-d09e-39d13941390b
X-Locale: en-US
X-SourceFiles: =?UTF-8?B?RDpcU291cmNlc1xSUEUuUGFydG5lci5TZXJ2aWNlLkJpbGxpbmdTZXJ2aWNlXHYxLjFcV2ViQXBpc1xCaWxsaW5nU2VydmljZS5WMi5XZWJcdjFcaW52b2ljZXNcZXN0aW1hdGVzXGxpbmtz?=
X-Powered-By: ASP.NET
Date: Thu, 14 Mar 2019 18:15:06 GMT
Content-Length: 1857

{
  "totalCount": 4,
  "items": [
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    }
  ],
  "attributes": {
    "objectType": "Collection"
 }
}
```
