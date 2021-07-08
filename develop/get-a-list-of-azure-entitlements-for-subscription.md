---
title: Hämta en lista över Azure-berättigande för en prenumeration
description: Du kan använda azureEntitlement-resursen för att hämta en samling Azure-berättiganderesurser som tillhör en prenumeration.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 280da155122ed9efd99838d7819fb34f8f7ec52c
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874371"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="5a2d5-103">Hämta en lista över Azure-berättigande för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="5a2d5-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="5a2d5-104">Du kan använda [Azure-rättighetsresursen](subscription-resources.md#azureentitlement) **(AzureEntitlement)** för att hämta en samling resurser som tillhör en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-104">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a2d5-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="5a2d5-105">Prerequisites</span></span>

- <span data-ttu-id="5a2d5-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5a2d5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5a2d5-107">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5a2d5-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5a2d5-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5a2d5-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5a2d5-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5a2d5-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5a2d5-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="5a2d5-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5a2d5-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="5a2d5-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5a2d5-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5a2d5-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5a2d5-114">En prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-114">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5a2d5-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="5a2d5-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5a2d5-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="5a2d5-116">Request syntax</span></span>

| <span data-ttu-id="5a2d5-117">Metod</span><span class="sxs-lookup"><span data-stu-id="5a2d5-117">Method</span></span>  | <span data-ttu-id="5a2d5-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="5a2d5-118">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="5a2d5-119">**Få**</span><span class="sxs-lookup"><span data-stu-id="5a2d5-119">**GET**</span></span> | <span data-ttu-id="5a2d5-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5a2d5-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="5a2d5-121">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="5a2d5-121">URI parameters</span></span>

<span data-ttu-id="5a2d5-122">I följande tabell visas de frågeparametrar som krävs för att hämta alla Azure-rättigheter för en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-122">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="5a2d5-123">Namn</span><span class="sxs-lookup"><span data-stu-id="5a2d5-123">Name</span></span>                   | <span data-ttu-id="5a2d5-124">Typ</span><span class="sxs-lookup"><span data-stu-id="5a2d5-124">Type</span></span>     | <span data-ttu-id="5a2d5-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="5a2d5-125">Required</span></span> | <span data-ttu-id="5a2d5-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5a2d5-126">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="5a2d5-127">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="5a2d5-127">**customer-tenant-id**</span></span> | <span data-ttu-id="5a2d5-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="5a2d5-128">**guid**</span></span> | <span data-ttu-id="5a2d5-129">Y</span><span class="sxs-lookup"><span data-stu-id="5a2d5-129">Y</span></span>        | <span data-ttu-id="5a2d5-130">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-130">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="5a2d5-131">**prenumerations-id**</span><span class="sxs-lookup"><span data-stu-id="5a2d5-131">**subscription-id**</span></span>       | <span data-ttu-id="5a2d5-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="5a2d5-132">**guid**</span></span> | <span data-ttu-id="5a2d5-133">Y</span><span class="sxs-lookup"><span data-stu-id="5a2d5-133">Y</span></span>        | <span data-ttu-id="5a2d5-134">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-134">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="5a2d5-135">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="5a2d5-135">Request headers</span></span>

<span data-ttu-id="5a2d5-136">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5a2d5-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5a2d5-137">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="5a2d5-137">Request body</span></span>

<span data-ttu-id="5a2d5-138">Inga.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5a2d5-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="5a2d5-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="5a2d5-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="5a2d5-140">REST response</span></span>

<span data-ttu-id="5a2d5-141">Om det lyckas returnerar den här metoden en [**samling AzureEntitlement-resurser**](subscription-resources.md#azureentitlement) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-141">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5a2d5-142">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="5a2d5-142">Response success and error codes</span></span>

<span data-ttu-id="5a2d5-143">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5a2d5-144">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="5a2d5-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5a2d5-145">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5a2d5-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5a2d5-146">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="5a2d5-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
```
