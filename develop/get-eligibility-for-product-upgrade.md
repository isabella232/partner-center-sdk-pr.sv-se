---
title: Kontrollera om en kund är berättigad för uppgradering till en Azure-plan
description: Du kan använda resursen ProductUpgradeRequest för att returnera en ProductUpgradesEligibility-resurs för att avgöra om en kund är berättigad att uppgradera från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 34a20611c7d92042b5432c5ffb3ba4702d77e0c2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446266"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="685ea-103">Kontrollera om en kund är berättigad för uppgradering till en Azure-plan</span><span class="sxs-lookup"><span data-stu-id="685ea-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="685ea-104">Du kan använda resursen [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) för att kontrollera om en kund är berättigad att uppgradera till en Azure-plan från en Microsoft Azure-prenumeration (MS-AZR-0145P) Den här metoden returnerar en [**ProductUpgradesEligibility-resurs**](product-upgrade-resources.md#productupgradeseligibility) med kundens berättigande för produktuppgradering.</span><span class="sxs-lookup"><span data-stu-id="685ea-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="685ea-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="685ea-105">Prerequisites</span></span>

- <span data-ttu-id="685ea-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="685ea-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="685ea-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="685ea-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="685ea-108">Följ den [säkra appmodellen när](enable-secure-app-model.md) du använder app-+användarautentisering med Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="685ea-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="685ea-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="685ea-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="685ea-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="685ea-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="685ea-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="685ea-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="685ea-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="685ea-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="685ea-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="685ea-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="685ea-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="685ea-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="685ea-115">Produktfamiljen.</span><span class="sxs-lookup"><span data-stu-id="685ea-115">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="685ea-116">C\#</span><span class="sxs-lookup"><span data-stu-id="685ea-116">C\#</span></span>

<span data-ttu-id="685ea-117">Så här kontrollerar du om en kund är berättigad att uppgradera till En Azure-plan:</span><span class="sxs-lookup"><span data-stu-id="685ea-117">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="685ea-118">Skapa ett **ProductUpgradesRequest-objekt** och ange kundidentifieraren och "Azure" som produktfamilj.</span><span class="sxs-lookup"><span data-stu-id="685ea-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="685ea-119">Använd **samlingen IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="685ea-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="685ea-120">Anropa **metoden CheckEligibility** och skicka objektet **ProductUpgradesRequest,** som returnerar ett **ProductUpgradesEligibility-objekt.**</span><span class="sxs-lookup"><span data-stu-id="685ea-120">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="685ea-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="685ea-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="685ea-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="685ea-122">Request syntax</span></span>

| <span data-ttu-id="685ea-123">Metod</span><span class="sxs-lookup"><span data-stu-id="685ea-123">Method</span></span>   | <span data-ttu-id="685ea-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="685ea-124">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="685ea-125">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="685ea-125">**POST**</span></span> | <span data-ttu-id="685ea-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/berättigande HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="685ea-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="685ea-127">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="685ea-127">Request headers</span></span>

<span data-ttu-id="685ea-128">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="685ea-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="685ea-129">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="685ea-129">Request body</span></span>

<span data-ttu-id="685ea-130">Begärandetexten måste innehålla en [**ProductUpgradeRequest-resurs.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="685ea-130">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="685ea-131">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="685ea-131">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="685ea-132">REST-svar</span><span class="sxs-lookup"><span data-stu-id="685ea-132">REST response</span></span>

<span data-ttu-id="685ea-133">Om det lyckas returnerar den här metoden [**en ProductUpgradesEligibility-resurs**](product-upgrade-resources.md#productupgradeseligibility) i brödtexten.</span><span class="sxs-lookup"><span data-stu-id="685ea-133">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="685ea-134">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="685ea-134">Response success and error codes</span></span>

<span data-ttu-id="685ea-135">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="685ea-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="685ea-136">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="685ea-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="685ea-137">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="685ea-137">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="685ea-138">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="685ea-138">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
