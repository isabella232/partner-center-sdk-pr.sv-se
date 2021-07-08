---
title: Hämta en lista över tillgängliga för en SKU (efter kund)
description: Du kan hämta en samling tillgänglighet för en angiven produkt och SKU av kunden med hjälp av kunden, produkten och SKU-identifierarna.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b237bbd17a6108bbcb4e23529cf476a6b8306f68
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874558"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="0604c-103">Hämta en lista över tillgängliga för en SKU (efter kund)</span><span class="sxs-lookup"><span data-stu-id="0604c-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="0604c-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0604c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0604c-105">Du kan använda följande metoder för att få en samling tillgänglighet för en angiven produkt och SKU som är tillgänglig för en viss kund.</span><span class="sxs-lookup"><span data-stu-id="0604c-105">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0604c-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="0604c-106">Prerequisites</span></span>

- <span data-ttu-id="0604c-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0604c-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0604c-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="0604c-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0604c-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0604c-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0604c-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0604c-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0604c-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="0604c-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0604c-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="0604c-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0604c-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="0604c-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0604c-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0604c-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0604c-115">En produktidentifierare (**product-id**).</span><span class="sxs-lookup"><span data-stu-id="0604c-115">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="0604c-116">En SKU-identifierare (**sku-id**).</span><span class="sxs-lookup"><span data-stu-id="0604c-116">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="0604c-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="0604c-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0604c-118">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="0604c-118">Request syntax</span></span>

| <span data-ttu-id="0604c-119">Metod</span><span class="sxs-lookup"><span data-stu-id="0604c-119">Method</span></span> | <span data-ttu-id="0604c-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="0604c-120">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0604c-121">POST</span><span class="sxs-lookup"><span data-stu-id="0604c-121">POST</span></span>   | <span data-ttu-id="0604c-122">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0604c-122">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="0604c-123">URI-parametrar för begäran</span><span class="sxs-lookup"><span data-stu-id="0604c-123">Request URI parameters</span></span>

| <span data-ttu-id="0604c-124">Namn</span><span class="sxs-lookup"><span data-stu-id="0604c-124">Name</span></span>               | <span data-ttu-id="0604c-125">Typ</span><span class="sxs-lookup"><span data-stu-id="0604c-125">Type</span></span> | <span data-ttu-id="0604c-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="0604c-126">Required</span></span> | <span data-ttu-id="0604c-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0604c-127">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="0604c-128">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="0604c-128">customer-tenant-id</span></span> | <span data-ttu-id="0604c-129">GUID</span><span class="sxs-lookup"><span data-stu-id="0604c-129">GUID</span></span> | <span data-ttu-id="0604c-130">Ja</span><span class="sxs-lookup"><span data-stu-id="0604c-130">Yes</span></span> | <span data-ttu-id="0604c-131">Värdet är ett GUID-formaterat **kundklientorganisations-ID,** vilket är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="0604c-131">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="0604c-132">produkt-id</span><span class="sxs-lookup"><span data-stu-id="0604c-132">product-id</span></span> | <span data-ttu-id="0604c-133">sträng</span><span class="sxs-lookup"><span data-stu-id="0604c-133">string</span></span> | <span data-ttu-id="0604c-134">Ja</span><span class="sxs-lookup"><span data-stu-id="0604c-134">Yes</span></span> | <span data-ttu-id="0604c-135">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="0604c-135">A string that identifies the product.</span></span> |
| <span data-ttu-id="0604c-136">sku-id</span><span class="sxs-lookup"><span data-stu-id="0604c-136">sku-id</span></span> | <span data-ttu-id="0604c-137">sträng</span><span class="sxs-lookup"><span data-stu-id="0604c-137">string</span></span> | <span data-ttu-id="0604c-138">Ja</span><span class="sxs-lookup"><span data-stu-id="0604c-138">Yes</span></span> | <span data-ttu-id="0604c-139">En sträng som identifierar SKU:n.</span><span class="sxs-lookup"><span data-stu-id="0604c-139">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="0604c-140">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="0604c-140">Request header</span></span>

<span data-ttu-id="0604c-141">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0604c-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0604c-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="0604c-142">Request body</span></span>

<span data-ttu-id="0604c-143">Inga.</span><span class="sxs-lookup"><span data-stu-id="0604c-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0604c-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="0604c-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="0604c-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="0604c-145">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0604c-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="0604c-146">Response success and error codes</span></span>

<span data-ttu-id="0604c-147">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="0604c-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0604c-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="0604c-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0604c-149">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0604c-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="0604c-150">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="0604c-150">This method returns the following error codes:</span></span>

| <span data-ttu-id="0604c-151">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="0604c-151">HTTP Status Code</span></span> | <span data-ttu-id="0604c-152">Felkod</span><span class="sxs-lookup"><span data-stu-id="0604c-152">Error code</span></span> | <span data-ttu-id="0604c-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0604c-153">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="0604c-154">404</span><span class="sxs-lookup"><span data-stu-id="0604c-154">404</span></span> | <span data-ttu-id="0604c-155">400013</span><span class="sxs-lookup"><span data-stu-id="0604c-155">400013</span></span> | <span data-ttu-id="0604c-156">Den överordnade produkten hittades inte.</span><span class="sxs-lookup"><span data-stu-id="0604c-156">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="0604c-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="0604c-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
