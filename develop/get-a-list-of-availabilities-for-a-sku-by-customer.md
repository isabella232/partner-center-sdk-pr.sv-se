---
title: Hämta en lista över tillgängliga för en SKU (efter kund)
description: Du kan hämta en samling tillgänglighet för en angiven produkt och SKU genom att använda kund-, produkt-och SKU-identifierare.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 5f4067916fea911963182954eed77f4e230e79d6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769126"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="54347-103">Hämta en lista över tillgängliga för en SKU (efter kund)</span><span class="sxs-lookup"><span data-stu-id="54347-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="54347-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="54347-104">**Applies to:**</span></span>

- <span data-ttu-id="54347-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="54347-105">Partner Center</span></span>
- <span data-ttu-id="54347-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="54347-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="54347-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="54347-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="54347-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="54347-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="54347-109">Du kan använda följande metoder för att hämta en samling tillgänglighet för en angiven produkt och SKU som är tillgänglig för en viss kund.</span><span class="sxs-lookup"><span data-stu-id="54347-109">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54347-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="54347-110">Prerequisites</span></span>

- <span data-ttu-id="54347-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="54347-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="54347-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="54347-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="54347-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54347-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="54347-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="54347-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="54347-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="54347-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="54347-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="54347-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="54347-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="54347-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="54347-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54347-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="54347-119">Ett produkt-**ID (produkt-ID**).</span><span class="sxs-lookup"><span data-stu-id="54347-119">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="54347-120">Ett SKU-ID (**SKU-ID**).</span><span class="sxs-lookup"><span data-stu-id="54347-120">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="54347-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="54347-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="54347-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="54347-122">Request syntax</span></span>

| <span data-ttu-id="54347-123">Metod</span><span class="sxs-lookup"><span data-stu-id="54347-123">Method</span></span> | <span data-ttu-id="54347-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="54347-124">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="54347-125">POST</span><span class="sxs-lookup"><span data-stu-id="54347-125">POST</span></span>   | <span data-ttu-id="54347-126">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products/{Product-ID}/SKUs/{SKU-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="54347-126">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="54347-127">Begär URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="54347-127">Request URI parameters</span></span>

| <span data-ttu-id="54347-128">Namn</span><span class="sxs-lookup"><span data-stu-id="54347-128">Name</span></span>               | <span data-ttu-id="54347-129">Typ</span><span class="sxs-lookup"><span data-stu-id="54347-129">Type</span></span> | <span data-ttu-id="54347-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="54347-130">Required</span></span> | <span data-ttu-id="54347-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="54347-131">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="54347-132">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="54347-132">customer-tenant-id</span></span> | <span data-ttu-id="54347-133">GUID</span><span class="sxs-lookup"><span data-stu-id="54347-133">GUID</span></span> | <span data-ttu-id="54347-134">Yes</span><span class="sxs-lookup"><span data-stu-id="54347-134">Yes</span></span> | <span data-ttu-id="54347-135">Värdet är ett GUID-formaterat **kund-ID**, som är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="54347-135">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="54347-136">produkt-ID</span><span class="sxs-lookup"><span data-stu-id="54347-136">product-id</span></span> | <span data-ttu-id="54347-137">sträng</span><span class="sxs-lookup"><span data-stu-id="54347-137">string</span></span> | <span data-ttu-id="54347-138">Yes</span><span class="sxs-lookup"><span data-stu-id="54347-138">Yes</span></span> | <span data-ttu-id="54347-139">En sträng som identifierar produkten.</span><span class="sxs-lookup"><span data-stu-id="54347-139">A string that identifies the product.</span></span> |
| <span data-ttu-id="54347-140">SKU-ID</span><span class="sxs-lookup"><span data-stu-id="54347-140">sku-id</span></span> | <span data-ttu-id="54347-141">sträng</span><span class="sxs-lookup"><span data-stu-id="54347-141">string</span></span> | <span data-ttu-id="54347-142">Yes</span><span class="sxs-lookup"><span data-stu-id="54347-142">Yes</span></span> | <span data-ttu-id="54347-143">En sträng som identifierar SKU: n.</span><span class="sxs-lookup"><span data-stu-id="54347-143">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="54347-144">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="54347-144">Request header</span></span>

<span data-ttu-id="54347-145">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="54347-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="54347-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="54347-146">Request body</span></span>

<span data-ttu-id="54347-147">Inga.</span><span class="sxs-lookup"><span data-stu-id="54347-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="54347-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="54347-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="54347-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="54347-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="54347-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="54347-150">Response success and error codes</span></span>

<span data-ttu-id="54347-151">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="54347-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="54347-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="54347-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="54347-153">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="54347-153">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="54347-154">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="54347-154">This method returns the following error codes:</span></span>

| <span data-ttu-id="54347-155">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="54347-155">HTTP Status Code</span></span> | <span data-ttu-id="54347-156">Felkod</span><span class="sxs-lookup"><span data-stu-id="54347-156">Error code</span></span> | <span data-ttu-id="54347-157">Description</span><span class="sxs-lookup"><span data-stu-id="54347-157">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="54347-158">404</span><span class="sxs-lookup"><span data-stu-id="54347-158">404</span></span> | <span data-ttu-id="54347-159">400013</span><span class="sxs-lookup"><span data-stu-id="54347-159">400013</span></span> | <span data-ttu-id="54347-160">Det gick inte att hitta den överordnade produkten.</span><span class="sxs-lookup"><span data-stu-id="54347-160">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="54347-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="54347-161">Response example</span></span>

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
