---
title: Hämta en kunds prenumerationers överföringsberättigande
description: Hämta en samling av en kunds prenumerationer som är berättigade/ineligibile för överföring.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 43086a32fa0dbbdecf65aac167c687f26fc4c2c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768742"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="ca199-103">Hämta en kunds prenumerationers överföringsberättigande</span><span class="sxs-lookup"><span data-stu-id="ca199-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="ca199-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="ca199-104">**Applies To**</span></span>

- <span data-ttu-id="ca199-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="ca199-105">Partner Center</span></span>

<span data-ttu-id="ca199-106">Hämta en samling av en kunds prenumerationer som är berättigade/inberättigade för överföring.</span><span class="sxs-lookup"><span data-stu-id="ca199-106">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca199-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ca199-107">Prerequisites</span></span>

- <span data-ttu-id="ca199-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ca199-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ca199-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ca199-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ca199-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ca199-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ca199-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="ca199-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ca199-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="ca199-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ca199-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="ca199-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ca199-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="ca199-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ca199-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ca199-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="ca199-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ca199-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ca199-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="ca199-117">Request syntax</span></span>

| <span data-ttu-id="ca199-118">Metod</span><span class="sxs-lookup"><span data-stu-id="ca199-118">Method</span></span>  | <span data-ttu-id="ca199-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ca199-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ca199-120">**TA**</span><span class="sxs-lookup"><span data-stu-id="ca199-120">**GET**</span></span> | <span data-ttu-id="ca199-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/transferseligibility? transferType = {transfer-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="ca199-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ca199-122">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ca199-122">URI parameter</span></span>

<span data-ttu-id="ca199-123">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta alla prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="ca199-123">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="ca199-124">Namn</span><span class="sxs-lookup"><span data-stu-id="ca199-124">Name</span></span>               | <span data-ttu-id="ca199-125">Typ</span><span class="sxs-lookup"><span data-stu-id="ca199-125">Type</span></span>   | <span data-ttu-id="ca199-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ca199-126">Required</span></span> | <span data-ttu-id="ca199-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ca199-127">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="ca199-128">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="ca199-128">customer-tenant-id</span></span> | <span data-ttu-id="ca199-129">sträng</span><span class="sxs-lookup"><span data-stu-id="ca199-129">string</span></span> | <span data-ttu-id="ca199-130">Yes</span><span class="sxs-lookup"><span data-stu-id="ca199-130">Yes</span></span>      | <span data-ttu-id="ca199-131">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="ca199-131">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="ca199-132">överförings typ</span><span class="sxs-lookup"><span data-stu-id="ca199-132">transfer-type</span></span>      | <span data-ttu-id="ca199-133">sträng</span><span class="sxs-lookup"><span data-stu-id="ca199-133">string</span></span> | <span data-ttu-id="ca199-134">Yes</span><span class="sxs-lookup"><span data-stu-id="ca199-134">Yes</span></span>      | <span data-ttu-id="ca199-135">Den typ av överföring som är avsedd.</span><span class="sxs-lookup"><span data-stu-id="ca199-135">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="ca199-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ca199-136">Request headers</span></span>

<span data-ttu-id="ca199-137">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ca199-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ca199-138">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ca199-138">Request body</span></span>

<span data-ttu-id="ca199-139">Inga.</span><span class="sxs-lookup"><span data-stu-id="ca199-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ca199-140">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ca199-140">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="ca199-141">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ca199-141">REST response</span></span>

<span data-ttu-id="ca199-142">Om det lyckas returnerar den här metoden en samling [TransferEligibility](transfer-eligibility-resources.md) -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="ca199-142">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ca199-143">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ca199-143">Response success and error codes</span></span>

<span data-ttu-id="ca199-144">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="ca199-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ca199-145">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ca199-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ca199-146">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ca199-146">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ca199-147">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ca199-147">Response example</span></span>

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
