---
title: Hämta en kunds prenumerationers överföringsberättigande
description: Hur du hämtar en samling av en kunds prenumerationer som är berättigade/icke-berättigade för överföring.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: fe8af76d1e1456754dec79291ec0853fb253d108
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446300"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="d36e7-103">Hämta en kunds prenumerationers överföringsberättigande</span><span class="sxs-lookup"><span data-stu-id="d36e7-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="d36e7-104">Så här hämtar du en samling av en kunds prenumerationer som är berättigade/inte berättigade till överföring.</span><span class="sxs-lookup"><span data-stu-id="d36e7-104">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d36e7-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d36e7-105">Prerequisites</span></span>

- <span data-ttu-id="d36e7-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d36e7-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d36e7-107">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d36e7-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d36e7-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d36e7-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d36e7-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d36e7-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d36e7-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="d36e7-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d36e7-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="d36e7-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d36e7-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="d36e7-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d36e7-113">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d36e7-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="d36e7-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d36e7-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d36e7-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="d36e7-115">Request syntax</span></span>

| <span data-ttu-id="d36e7-116">Metod</span><span class="sxs-lookup"><span data-stu-id="d36e7-116">Method</span></span>  | <span data-ttu-id="d36e7-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d36e7-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d36e7-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="d36e7-118">**GET**</span></span> | <span data-ttu-id="d36e7-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d36e7-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d36e7-120">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d36e7-120">URI parameter</span></span>

<span data-ttu-id="d36e7-121">I den här tabellen visas den frågeparameter som krävs för att hämta alla prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="d36e7-121">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="d36e7-122">Namn</span><span class="sxs-lookup"><span data-stu-id="d36e7-122">Name</span></span>               | <span data-ttu-id="d36e7-123">Typ</span><span class="sxs-lookup"><span data-stu-id="d36e7-123">Type</span></span>   | <span data-ttu-id="d36e7-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d36e7-124">Required</span></span> | <span data-ttu-id="d36e7-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d36e7-125">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="d36e7-126">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="d36e7-126">customer-tenant-id</span></span> | <span data-ttu-id="d36e7-127">sträng</span><span class="sxs-lookup"><span data-stu-id="d36e7-127">string</span></span> | <span data-ttu-id="d36e7-128">Ja</span><span class="sxs-lookup"><span data-stu-id="d36e7-128">Yes</span></span>      | <span data-ttu-id="d36e7-129">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="d36e7-129">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="d36e7-130">överföringstyp</span><span class="sxs-lookup"><span data-stu-id="d36e7-130">transfer-type</span></span>      | <span data-ttu-id="d36e7-131">sträng</span><span class="sxs-lookup"><span data-stu-id="d36e7-131">string</span></span> | <span data-ttu-id="d36e7-132">Ja</span><span class="sxs-lookup"><span data-stu-id="d36e7-132">Yes</span></span>      | <span data-ttu-id="d36e7-133">Den typ av överföring som är avsedd.</span><span class="sxs-lookup"><span data-stu-id="d36e7-133">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="d36e7-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d36e7-134">Request headers</span></span>

<span data-ttu-id="d36e7-135">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d36e7-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d36e7-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d36e7-136">Request body</span></span>

<span data-ttu-id="d36e7-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="d36e7-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d36e7-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d36e7-138">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d36e7-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d36e7-139">REST response</span></span>

<span data-ttu-id="d36e7-140">Om det lyckas returnerar den här metoden en samling [TransferEligibility-resurser](transfer-eligibility-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="d36e7-140">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d36e7-141">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d36e7-141">Response success and error codes</span></span>

<span data-ttu-id="d36e7-142">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="d36e7-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d36e7-143">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d36e7-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d36e7-144">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d36e7-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d36e7-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d36e7-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
Date: Tue, 24 Mar 2020 23:43:25 GMT

[
  {
    "id": "548FA265-5F40-4765-9A6B-47826F72A4BF",
    "isEligible": false,
    "reason": "Subscription: 548FA265-5F40-4765-9A6B-47826F72A4BF is in state: Deleted"
  },
  {
    "id": "E2A3AEB3-70A7-42E3-930C-7519EEDDC45A",
    "isEligible": false,
    "reason": "Subscription: E2A3AEB3-70A7-42E3-930C-7519EEDDC45A is in state: Suspended"
  },
  {
    "id": "4B600A9A-DF56-4564-A75A-6CC6D2D0C9F9",
    "isEligible": false,
    "reason": "subscription is already part of another transfer request id : 31a06eac-c527-458a-a6b4-0de197a45996"
  },
  {
    "id": "D3350F46-AA29-4F6F-95A0-E3011988915C",
    "isEligible": true
  }
  {
    "id": "E82B2F4A-736A-4E2B-955C-C1A4C56C0171",
    "isEligible": true
  }
]
```
