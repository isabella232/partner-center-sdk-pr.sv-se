---
title: Få en kunds kompetens
description: Lär dig hur du använder asynkron verifiering för att få en kund kvalificering via API för partner Center. Partner kan använda detta för att validera utbildnings kunder.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 2c860d4a35104131197e06d4712f4ef41ba0008e
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711922"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="3de5e-104">Få en kund kvalificering asynkront</span><span class="sxs-lookup"><span data-stu-id="3de5e-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="3de5e-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="3de5e-105">**Applies To**</span></span>

- <span data-ttu-id="3de5e-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="3de5e-106">Partner Center</span></span>

<span data-ttu-id="3de5e-107">Så här får du en kunds kvalifikationer asynkront.</span><span class="sxs-lookup"><span data-stu-id="3de5e-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3de5e-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3de5e-108">Prerequisites</span></span>

- <span data-ttu-id="3de5e-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3de5e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3de5e-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3de5e-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3de5e-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3de5e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3de5e-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="3de5e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3de5e-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="3de5e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3de5e-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="3de5e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3de5e-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="3de5e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3de5e-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3de5e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="3de5e-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3de5e-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3de5e-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="3de5e-118">Request syntax</span></span>

| <span data-ttu-id="3de5e-119">Metod</span><span class="sxs-lookup"><span data-stu-id="3de5e-119">Method</span></span>  | <span data-ttu-id="3de5e-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3de5e-120">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3de5e-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="3de5e-121">**GET**</span></span> | <span data-ttu-id="3de5e-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="3de5e-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3de5e-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="3de5e-123">URI parameter</span></span>

<span data-ttu-id="3de5e-124">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta all kvalificering.</span><span class="sxs-lookup"><span data-stu-id="3de5e-124">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="3de5e-125">Namn</span><span class="sxs-lookup"><span data-stu-id="3de5e-125">Name</span></span>               | <span data-ttu-id="3de5e-126">Typ</span><span class="sxs-lookup"><span data-stu-id="3de5e-126">Type</span></span>   | <span data-ttu-id="3de5e-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3de5e-127">Required</span></span> | <span data-ttu-id="3de5e-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3de5e-128">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="3de5e-129">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="3de5e-129">**customer-tenant-id**</span></span> | <span data-ttu-id="3de5e-130">sträng</span><span class="sxs-lookup"><span data-stu-id="3de5e-130">string</span></span> | <span data-ttu-id="3de5e-131">Ja</span><span class="sxs-lookup"><span data-stu-id="3de5e-131">Yes</span></span>      | <span data-ttu-id="3de5e-132">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="3de5e-132">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3de5e-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3de5e-133">Request headers</span></span>

<span data-ttu-id="3de5e-134">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3de5e-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3de5e-135">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3de5e-135">Request body</span></span>

<span data-ttu-id="3de5e-136">Inga.</span><span class="sxs-lookup"><span data-stu-id="3de5e-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3de5e-137">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3de5e-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="3de5e-138">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3de5e-138">REST response</span></span>

<span data-ttu-id="3de5e-139">Om det lyckas returnerar den här metoden en samling kvalifikationer i svars texten.</span><span class="sxs-lookup"><span data-stu-id="3de5e-139">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="3de5e-140">Nedan visas exempel på **Get** -anrop på en kund med **utbildnings** kompetensen.</span><span class="sxs-lookup"><span data-stu-id="3de5e-140">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3de5e-141">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3de5e-141">Response success and error codes</span></span>

<span data-ttu-id="3de5e-142">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="3de5e-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3de5e-143">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3de5e-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3de5e-144">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3de5e-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="3de5e-145">Svars exempel</span><span class="sxs-lookup"><span data-stu-id="3de5e-145">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="3de5e-146">Godkända</span><span class="sxs-lookup"><span data-stu-id="3de5e-146">Approved</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Approved",
        }
    ]
}

```

#### <a name="in-review"></a><span data-ttu-id="3de5e-147">Under granskning</span><span class="sxs-lookup"><span data-stu-id="3de5e-147">In Review</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "InReview",
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

#### <a name="denied"></a><span data-ttu-id="3de5e-148">Nekad</span><span class="sxs-lookup"><span data-stu-id="3de5e-148">Denied</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Denied",
            "vettingReason": "Not an Education Customer", // example Vetting Reason
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

## <a name="related-articles"></a><span data-ttu-id="3de5e-149">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="3de5e-149">Related articles</span></span>

- [<span data-ttu-id="3de5e-150">Uppdatera en kunds kvalificeringar</span><span class="sxs-lookup"><span data-stu-id="3de5e-150">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)