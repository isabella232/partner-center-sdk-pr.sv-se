---
title: Dra tillbaka en överföring
description: Hur du drar tillbaka en skapad överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3c15cf09b4e466e178c7afb5f9d324fe1199418e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445212"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="c728e-103">Dra tillbaka en överföring</span><span class="sxs-lookup"><span data-stu-id="c728e-103">Withdraw a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c728e-104">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c728e-104">Prerequisites</span></span>

- <span data-ttu-id="c728e-105">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c728e-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c728e-106">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="c728e-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c728e-107">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c728e-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c728e-108">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="c728e-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c728e-109">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="c728e-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c728e-110">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="c728e-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c728e-111">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="c728e-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c728e-112">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c728e-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c728e-113">En överföringsidentifierare för en befintlig överföring.</span><span class="sxs-lookup"><span data-stu-id="c728e-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c728e-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c728e-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c728e-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="c728e-115">Request syntax</span></span>

| <span data-ttu-id="c728e-116">Metod</span><span class="sxs-lookup"><span data-stu-id="c728e-116">Method</span></span>    | <span data-ttu-id="c728e-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c728e-117">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c728e-118">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="c728e-118">**DELETE**</span></span>| <span data-ttu-id="c728e-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c728e-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="c728e-120">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="c728e-120">URI parameter</span></span>

<span data-ttu-id="c728e-121">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="c728e-121">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="c728e-122">Namn</span><span class="sxs-lookup"><span data-stu-id="c728e-122">Name</span></span>            | <span data-ttu-id="c728e-123">Typ</span><span class="sxs-lookup"><span data-stu-id="c728e-123">Type</span></span>     | <span data-ttu-id="c728e-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c728e-124">Required</span></span> | <span data-ttu-id="c728e-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c728e-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="c728e-126">**kund-id**</span><span class="sxs-lookup"><span data-stu-id="c728e-126">**customer-id**</span></span> | <span data-ttu-id="c728e-127">sträng</span><span class="sxs-lookup"><span data-stu-id="c728e-127">string</span></span>   | <span data-ttu-id="c728e-128">Ja</span><span class="sxs-lookup"><span data-stu-id="c728e-128">Yes</span></span>      | <span data-ttu-id="c728e-129">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="c728e-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="c728e-130">**transfer-id**</span><span class="sxs-lookup"><span data-stu-id="c728e-130">**transfer-id**</span></span> | <span data-ttu-id="c728e-131">sträng</span><span class="sxs-lookup"><span data-stu-id="c728e-131">string</span></span>   | <span data-ttu-id="c728e-132">Ja</span><span class="sxs-lookup"><span data-stu-id="c728e-132">Yes</span></span>      | <span data-ttu-id="c728e-133">Ett GUID-formaterat överförings-ID som identifierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="c728e-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="c728e-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c728e-134">Request headers</span></span>

<span data-ttu-id="c728e-135">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c728e-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="c728e-136">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="c728e-136">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="c728e-137">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c728e-137">REST response</span></span>

<span data-ttu-id="c728e-138">Om det lyckas returnerar den här metoden Inget innehåll (204).</span><span class="sxs-lookup"><span data-stu-id="c728e-138">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c728e-139">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c728e-139">Response success and error codes</span></span>

<span data-ttu-id="c728e-140">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="c728e-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c728e-141">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c728e-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c728e-142">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c728e-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c728e-143">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="c728e-143">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
