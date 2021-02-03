---
title: Få en kunds kompetens
description: Lär dig hur du använder asynkron verifiering för att få en kund kvalificering via API för partner Center. Partner kan använda detta för att validera utbildnings kunder.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 9f9b9aaddde0d66caf9c7ef32e8fba6d5e3aba36
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770190"
---
# <a name="get-a-customers-qualifications-via-asynchronous-validation"></a><span data-ttu-id="95907-104">Få en kunds kompetens via asynkron verifiering</span><span class="sxs-lookup"><span data-stu-id="95907-104">Get a customer's qualifications via asynchronous validation</span></span>

<span data-ttu-id="95907-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="95907-105">**Applies To**</span></span>

- <span data-ttu-id="95907-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="95907-106">Partner Center</span></span>

<span data-ttu-id="95907-107">Lär dig hur du får en kunds kvalifikationer asynkront via API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="95907-107">Learn how to get a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="95907-108">Information om hur du gör detta synkront finns i [Skaffa en kunds kvalificering via synkron verifiering](get-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="95907-108">To learn how to do this synchronously, see [Get a customer's qualification via synchronous validation](get-customer-qualification-synchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95907-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="95907-109">Prerequisites</span></span>

- <span data-ttu-id="95907-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="95907-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95907-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="95907-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="95907-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95907-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="95907-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="95907-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="95907-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="95907-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="95907-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="95907-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="95907-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="95907-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="95907-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95907-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="95907-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="95907-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95907-119">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="95907-119">Request syntax</span></span>

| <span data-ttu-id="95907-120">Metod</span><span class="sxs-lookup"><span data-stu-id="95907-120">Method</span></span>  | <span data-ttu-id="95907-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="95907-121">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95907-122">**TA**</span><span class="sxs-lookup"><span data-stu-id="95907-122">**GET**</span></span> | <span data-ttu-id="95907-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="95907-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="95907-124">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="95907-124">URI parameter</span></span>

<span data-ttu-id="95907-125">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta all kvalificering.</span><span class="sxs-lookup"><span data-stu-id="95907-125">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="95907-126">Namn</span><span class="sxs-lookup"><span data-stu-id="95907-126">Name</span></span>               | <span data-ttu-id="95907-127">Typ</span><span class="sxs-lookup"><span data-stu-id="95907-127">Type</span></span>   | <span data-ttu-id="95907-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="95907-128">Required</span></span> | <span data-ttu-id="95907-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="95907-129">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="95907-130">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="95907-130">**customer-tenant-id**</span></span> | <span data-ttu-id="95907-131">sträng</span><span class="sxs-lookup"><span data-stu-id="95907-131">string</span></span> | <span data-ttu-id="95907-132">Yes</span><span class="sxs-lookup"><span data-stu-id="95907-132">Yes</span></span>      | <span data-ttu-id="95907-133">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="95907-133">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95907-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="95907-134">Request headers</span></span>

<span data-ttu-id="95907-135">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="95907-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95907-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="95907-136">Request body</span></span>

<span data-ttu-id="95907-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="95907-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="95907-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="95907-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="95907-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="95907-139">REST response</span></span>

<span data-ttu-id="95907-140">Om det lyckas returnerar den här metoden en samling kvalifikationer i svars texten.</span><span class="sxs-lookup"><span data-stu-id="95907-140">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="95907-141">Nedan visas exempel på **Get** -anrop på en kund med **utbildnings** kompetensen.</span><span class="sxs-lookup"><span data-stu-id="95907-141">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95907-142">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="95907-142">Response success and error codes</span></span>

<span data-ttu-id="95907-143">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="95907-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95907-144">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="95907-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="95907-145">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="95907-145">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="95907-146">Svars exempel</span><span class="sxs-lookup"><span data-stu-id="95907-146">Response examples</span></span>

<span data-ttu-id="95907-147">I det här avsnittet visas svar som du kan få när en kund `vettingStatus` är:</span><span class="sxs-lookup"><span data-stu-id="95907-147">This section shows responses you might receive when a customer's `vettingStatus` is:</span></span>

- <span data-ttu-id="95907-148">Godkända</span><span class="sxs-lookup"><span data-stu-id="95907-148">Approved</span></span>
- <span data-ttu-id="95907-149">Under granskning</span><span class="sxs-lookup"><span data-stu-id="95907-149">In Review</span></span>
- <span data-ttu-id="95907-150">Nekad</span><span class="sxs-lookup"><span data-stu-id="95907-150">Denied</span></span>

<span data-ttu-id="95907-151">**Godkänt** exempel:</span><span class="sxs-lookup"><span data-stu-id="95907-151">**Approved** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Approved",
    }
]

```

<span data-ttu-id="95907-152">**I gransknings** exempel:</span><span class="sxs-lookup"><span data-stu-id="95907-152">**In Review** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "InReview",
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

<span data-ttu-id="95907-153">**Nekat** exempel:</span><span class="sxs-lookup"><span data-stu-id="95907-153">**Denied** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Denied",
        "vettingReason": "Not an Education Customer", // example Vetting Reason
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="95907-154">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="95907-154">Related articles</span></span>

- [<span data-ttu-id="95907-155">Uppdatera en kunds kompetens</span><span class="sxs-lookup"><span data-stu-id="95907-155">Update a customer's qualifications</span></span>](update-a-customer-s-qualifications.md)