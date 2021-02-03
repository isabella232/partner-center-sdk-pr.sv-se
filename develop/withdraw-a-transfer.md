---
title: Återkalla en överföring
description: Så här drar du tillbaka en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a9e1e2a33d21fc1338a36b8ac96b528e70b61c86
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768703"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="333a8-103">Återkalla en överföring</span><span class="sxs-lookup"><span data-stu-id="333a8-103">Withdraw a transfer</span></span>

<span data-ttu-id="333a8-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="333a8-104">**Applies to:**</span></span>

- <span data-ttu-id="333a8-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="333a8-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="333a8-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="333a8-106">Prerequisites</span></span>

- <span data-ttu-id="333a8-107">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="333a8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="333a8-108">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="333a8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="333a8-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="333a8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="333a8-110">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="333a8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="333a8-111">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="333a8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="333a8-112">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="333a8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="333a8-113">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="333a8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="333a8-114">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="333a8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="333a8-115">En överförings identifierare för en befintlig överföring.</span><span class="sxs-lookup"><span data-stu-id="333a8-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="333a8-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="333a8-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="333a8-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="333a8-117">Request syntax</span></span>

| <span data-ttu-id="333a8-118">Metod</span><span class="sxs-lookup"><span data-stu-id="333a8-118">Method</span></span>    | <span data-ttu-id="333a8-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="333a8-119">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="333a8-120">**TA bort**</span><span class="sxs-lookup"><span data-stu-id="333a8-120">**DELETE**</span></span>| <span data-ttu-id="333a8-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="333a8-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="333a8-122">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="333a8-122">URI parameter</span></span>

<span data-ttu-id="333a8-123">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="333a8-123">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="333a8-124">Namn</span><span class="sxs-lookup"><span data-stu-id="333a8-124">Name</span></span>            | <span data-ttu-id="333a8-125">Typ</span><span class="sxs-lookup"><span data-stu-id="333a8-125">Type</span></span>     | <span data-ttu-id="333a8-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="333a8-126">Required</span></span> | <span data-ttu-id="333a8-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="333a8-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="333a8-128">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="333a8-128">**customer-id**</span></span> | <span data-ttu-id="333a8-129">sträng</span><span class="sxs-lookup"><span data-stu-id="333a8-129">string</span></span>   | <span data-ttu-id="333a8-130">Yes</span><span class="sxs-lookup"><span data-stu-id="333a8-130">Yes</span></span>      | <span data-ttu-id="333a8-131">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="333a8-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="333a8-132">**överförings-ID**</span><span class="sxs-lookup"><span data-stu-id="333a8-132">**transfer-id**</span></span> | <span data-ttu-id="333a8-133">sträng</span><span class="sxs-lookup"><span data-stu-id="333a8-133">string</span></span>   | <span data-ttu-id="333a8-134">Yes</span><span class="sxs-lookup"><span data-stu-id="333a8-134">Yes</span></span>      | <span data-ttu-id="333a8-135">Ett GUID-formaterat överförings-ID som identifierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="333a8-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="333a8-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="333a8-136">Request headers</span></span>

<span data-ttu-id="333a8-137">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="333a8-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="333a8-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="333a8-138">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="333a8-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="333a8-139">REST response</span></span>

<span data-ttu-id="333a8-140">Om det lyckas returnerar den här metoden inget innehåll (204).</span><span class="sxs-lookup"><span data-stu-id="333a8-140">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="333a8-141">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="333a8-141">Response success and error codes</span></span>

<span data-ttu-id="333a8-142">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="333a8-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="333a8-143">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="333a8-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="333a8-144">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="333a8-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="333a8-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="333a8-145">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
