---
title: Hämta en lista över Azure-berättigande för en prenumeration
description: Du kan använda AzureEntitlement-resursen för att hämta en samling av Azures rättighets resurser som tillhör en prenumeration.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: d7d0a10c571dc073bd49e82084f3b7ece7234daf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769117"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="144f9-103">Hämta en lista över Azure-berättigande för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="144f9-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="144f9-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="144f9-104">**Applies to:**</span></span>

- <span data-ttu-id="144f9-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="144f9-105">Partner Center</span></span>

<span data-ttu-id="144f9-106">Du kan använda [Azure](subscription-resources.md#azureentitlement) -**AzureEntitlement** för att få en samling resurser som tillhör en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="144f9-106">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="144f9-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="144f9-107">Prerequisites</span></span>

- <span data-ttu-id="144f9-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="144f9-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="144f9-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="144f9-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="144f9-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="144f9-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="144f9-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="144f9-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="144f9-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="144f9-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="144f9-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="144f9-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="144f9-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="144f9-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="144f9-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="144f9-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="144f9-116">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="144f9-116">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="144f9-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="144f9-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="144f9-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="144f9-118">Request syntax</span></span>

| <span data-ttu-id="144f9-119">Metod</span><span class="sxs-lookup"><span data-stu-id="144f9-119">Method</span></span>  | <span data-ttu-id="144f9-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="144f9-120">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="144f9-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="144f9-121">**GET**</span></span> | <span data-ttu-id="144f9-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/azureentitlements http/1.1</span><span class="sxs-lookup"><span data-stu-id="144f9-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="144f9-123">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="144f9-123">URI parameters</span></span>

<span data-ttu-id="144f9-124">I följande tabell visas de parametrar som krävs för att hämta alla Azure-rättigheter för en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="144f9-124">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="144f9-125">Namn</span><span class="sxs-lookup"><span data-stu-id="144f9-125">Name</span></span>                   | <span data-ttu-id="144f9-126">Typ</span><span class="sxs-lookup"><span data-stu-id="144f9-126">Type</span></span>     | <span data-ttu-id="144f9-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="144f9-127">Required</span></span> | <span data-ttu-id="144f9-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="144f9-128">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="144f9-129">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="144f9-129">**customer-tenant-id**</span></span> | <span data-ttu-id="144f9-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="144f9-130">**guid**</span></span> | <span data-ttu-id="144f9-131">Y</span><span class="sxs-lookup"><span data-stu-id="144f9-131">Y</span></span>        | <span data-ttu-id="144f9-132">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="144f9-132">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="144f9-133">**prenumerations-ID**</span><span class="sxs-lookup"><span data-stu-id="144f9-133">**subscription-id**</span></span>       | <span data-ttu-id="144f9-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="144f9-134">**guid**</span></span> | <span data-ttu-id="144f9-135">Y</span><span class="sxs-lookup"><span data-stu-id="144f9-135">Y</span></span>        | <span data-ttu-id="144f9-136">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="144f9-136">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="144f9-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="144f9-137">Request headers</span></span>

<span data-ttu-id="144f9-138">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="144f9-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="144f9-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="144f9-139">Request body</span></span>

<span data-ttu-id="144f9-140">Inga.</span><span class="sxs-lookup"><span data-stu-id="144f9-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="144f9-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="144f9-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="144f9-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="144f9-142">REST response</span></span>

<span data-ttu-id="144f9-143">Om det lyckas returnerar den här metoden en samling [**AzureEntitlement**](subscription-resources.md#azureentitlement) -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="144f9-143">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="144f9-144">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="144f9-144">Response success and error codes</span></span>

<span data-ttu-id="144f9-145">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="144f9-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="144f9-146">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="144f9-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="144f9-147">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="144f9-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="144f9-148">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="144f9-148">Response example</span></span>

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
