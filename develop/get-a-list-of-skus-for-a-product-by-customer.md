---
title: Hämta en lista över SKU:er för en produkt (efter kund)
description: Hämtar en samling SKU:er för den angivna produkten per kund.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b76526d97ba9027897fc88954ba45186d58aefb8
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874167"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="640ba-103">Hämta en lista över SKU:er för en produkt (efter kund)</span><span class="sxs-lookup"><span data-stu-id="640ba-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="640ba-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="640ba-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="640ba-105">Hämtar en samling SKU:er för en viss produkt som är tillgänglig för en befintlig kund.</span><span class="sxs-lookup"><span data-stu-id="640ba-105">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="640ba-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="640ba-106">Prerequisites</span></span>

- <span data-ttu-id="640ba-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="640ba-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="640ba-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="640ba-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="640ba-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="640ba-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="640ba-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="640ba-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="640ba-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="640ba-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="640ba-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="640ba-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="640ba-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="640ba-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="640ba-114">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="640ba-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="640ba-115">Ett produkt-ID (**product-id**).</span><span class="sxs-lookup"><span data-stu-id="640ba-115">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="640ba-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="640ba-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="640ba-117">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="640ba-117">Request syntax</span></span>

| <span data-ttu-id="640ba-118">Metod</span><span class="sxs-lookup"><span data-stu-id="640ba-118">Method</span></span> | <span data-ttu-id="640ba-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="640ba-119">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="640ba-120">POST</span><span class="sxs-lookup"><span data-stu-id="640ba-120">POST</span></span>   | <span data-ttu-id="640ba-121">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="640ba-121">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="640ba-122">URI-parameter för begäran</span><span class="sxs-lookup"><span data-stu-id="640ba-122">Request URI parameter</span></span>

| <span data-ttu-id="640ba-123">Namn</span><span class="sxs-lookup"><span data-stu-id="640ba-123">Name</span></span>               | <span data-ttu-id="640ba-124">Typ</span><span class="sxs-lookup"><span data-stu-id="640ba-124">Type</span></span> | <span data-ttu-id="640ba-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="640ba-125">Required</span></span> | <span data-ttu-id="640ba-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="640ba-126">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="640ba-127">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="640ba-127">customer-tenant-id</span></span> | <span data-ttu-id="640ba-128">GUID</span><span class="sxs-lookup"><span data-stu-id="640ba-128">GUID</span></span> | <span data-ttu-id="640ba-129">Ja</span><span class="sxs-lookup"><span data-stu-id="640ba-129">Yes</span></span> | <span data-ttu-id="640ba-130">Värdet är ett GUID-formaterat **kundklientorganisations-ID,** vilket är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="640ba-130">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="640ba-131">produkt-id</span><span class="sxs-lookup"><span data-stu-id="640ba-131">product-id</span></span> | <span data-ttu-id="640ba-132">sträng</span><span class="sxs-lookup"><span data-stu-id="640ba-132">string</span></span> | <span data-ttu-id="640ba-133">Ja</span><span class="sxs-lookup"><span data-stu-id="640ba-133">Yes</span></span> | <span data-ttu-id="640ba-134">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="640ba-134">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="640ba-135">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="640ba-135">Request header</span></span>

<span data-ttu-id="640ba-136">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="640ba-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="640ba-137">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="640ba-137">Request body</span></span>

<span data-ttu-id="640ba-138">Inga.</span><span class="sxs-lookup"><span data-stu-id="640ba-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="640ba-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="640ba-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="640ba-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="640ba-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="640ba-141">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="640ba-141">Response success and error codes</span></span>

<span data-ttu-id="640ba-142">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="640ba-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="640ba-143">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="640ba-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="640ba-144">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="640ba-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="640ba-145">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="640ba-145">This method returns the following error codes:</span></span>

| <span data-ttu-id="640ba-146">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="640ba-146">HTTP Status Code</span></span> | <span data-ttu-id="640ba-147">Felkod</span><span class="sxs-lookup"><span data-stu-id="640ba-147">Error code</span></span> | <span data-ttu-id="640ba-148">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="640ba-148">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="640ba-149">404</span><span class="sxs-lookup"><span data-stu-id="640ba-149">404</span></span> | <span data-ttu-id="640ba-150">400013</span><span class="sxs-lookup"><span data-stu-id="640ba-150">400013</span></span> | <span data-ttu-id="640ba-151">Den överordnade produkten hittades inte.</span><span class="sxs-lookup"><span data-stu-id="640ba-151">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="640ba-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="640ba-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```
