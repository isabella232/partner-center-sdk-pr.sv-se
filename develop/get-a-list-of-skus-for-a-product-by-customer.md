---
title: 'Hämta en lista över SKU: er för en produkt (per kund)'
description: 'Hämtar en samling SKU: er för den angivna produkten per kund.'
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6b9c9bcd52798006d7f686405f059192a722c7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769096"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="657bc-103">Hämta en lista över SKU: er för en produkt (per kund)</span><span class="sxs-lookup"><span data-stu-id="657bc-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="657bc-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="657bc-104">**Applies To**</span></span>

- <span data-ttu-id="657bc-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="657bc-105">Partner Center</span></span>
- <span data-ttu-id="657bc-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="657bc-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="657bc-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="657bc-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="657bc-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="657bc-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="657bc-109">Hämtar en samling SKU: er för en viss produkt som är tillgänglig för en befintlig kund.</span><span class="sxs-lookup"><span data-stu-id="657bc-109">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="657bc-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="657bc-110">Prerequisites</span></span>

- <span data-ttu-id="657bc-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="657bc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="657bc-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="657bc-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="657bc-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="657bc-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="657bc-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="657bc-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="657bc-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="657bc-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="657bc-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="657bc-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="657bc-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="657bc-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="657bc-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="657bc-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="657bc-119">Ett produkt-ID (**produkt-ID**).</span><span class="sxs-lookup"><span data-stu-id="657bc-119">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="657bc-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="657bc-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="657bc-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="657bc-121">Request syntax</span></span>

| <span data-ttu-id="657bc-122">Metod</span><span class="sxs-lookup"><span data-stu-id="657bc-122">Method</span></span> | <span data-ttu-id="657bc-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="657bc-123">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="657bc-124">POST</span><span class="sxs-lookup"><span data-stu-id="657bc-124">POST</span></span>   | <span data-ttu-id="657bc-125">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products/{Product-ID}/SKUs http/1.1</span><span class="sxs-lookup"><span data-stu-id="657bc-125">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="657bc-126">URI-parameter för begäran</span><span class="sxs-lookup"><span data-stu-id="657bc-126">Request URI parameter</span></span>

| <span data-ttu-id="657bc-127">Namn</span><span class="sxs-lookup"><span data-stu-id="657bc-127">Name</span></span>               | <span data-ttu-id="657bc-128">Typ</span><span class="sxs-lookup"><span data-stu-id="657bc-128">Type</span></span> | <span data-ttu-id="657bc-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="657bc-129">Required</span></span> | <span data-ttu-id="657bc-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="657bc-130">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="657bc-131">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="657bc-131">customer-tenant-id</span></span> | <span data-ttu-id="657bc-132">GUID</span><span class="sxs-lookup"><span data-stu-id="657bc-132">GUID</span></span> | <span data-ttu-id="657bc-133">Yes</span><span class="sxs-lookup"><span data-stu-id="657bc-133">Yes</span></span> | <span data-ttu-id="657bc-134">Värdet är ett GUID-formaterat **kund-ID**, som är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="657bc-134">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="657bc-135">produkt-ID</span><span class="sxs-lookup"><span data-stu-id="657bc-135">product-id</span></span> | <span data-ttu-id="657bc-136">sträng</span><span class="sxs-lookup"><span data-stu-id="657bc-136">string</span></span> | <span data-ttu-id="657bc-137">Yes</span><span class="sxs-lookup"><span data-stu-id="657bc-137">Yes</span></span> | <span data-ttu-id="657bc-138">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="657bc-138">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="657bc-139">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="657bc-139">Request header</span></span>

<span data-ttu-id="657bc-140">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="657bc-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="657bc-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="657bc-141">Request body</span></span>

<span data-ttu-id="657bc-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="657bc-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="657bc-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="657bc-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="657bc-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="657bc-144">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="657bc-145">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="657bc-145">Response success and error codes</span></span>

<span data-ttu-id="657bc-146">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="657bc-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="657bc-147">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="657bc-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="657bc-148">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="657bc-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="657bc-149">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="657bc-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="657bc-150">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="657bc-150">HTTP Status Code</span></span> | <span data-ttu-id="657bc-151">Felkod</span><span class="sxs-lookup"><span data-stu-id="657bc-151">Error code</span></span> | <span data-ttu-id="657bc-152">Description</span><span class="sxs-lookup"><span data-stu-id="657bc-152">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="657bc-153">404</span><span class="sxs-lookup"><span data-stu-id="657bc-153">404</span></span> | <span data-ttu-id="657bc-154">400013</span><span class="sxs-lookup"><span data-stu-id="657bc-154">400013</span></span> | <span data-ttu-id="657bc-155">Det gick inte att hitta den överordnade produkten.</span><span class="sxs-lookup"><span data-stu-id="657bc-155">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="657bc-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="657bc-156">Response example</span></span>

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
