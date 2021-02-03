---
title: Kontrol lera en kunds berättigande för att uppgradera till en Azure-plan
description: Du kan använda ProductUpgradeRequest-resursen för att returnera en ProductUpgradesEligibility-resurs för att avgöra om en kund är berättigad att uppgradera från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768724"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="2324c-103">Kontrol lera en kunds berättigande för att uppgradera till en Azure-plan</span><span class="sxs-lookup"><span data-stu-id="2324c-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="2324c-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="2324c-104">**Applies to:**</span></span>

- <span data-ttu-id="2324c-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2324c-105">Partner Center</span></span>

<span data-ttu-id="2324c-106">Du kan använda [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -resursen för att kontrol lera om en kund är berättigad till att uppgradera till en Azure-plan från en Microsoft Azure (MS-AZR-0145P)-prenumeration den här metoden returnerar en [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -resurs med kundens produkt uppgraderings behörighet.</span><span class="sxs-lookup"><span data-stu-id="2324c-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2324c-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2324c-107">Prerequisites</span></span>

- <span data-ttu-id="2324c-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2324c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2324c-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2324c-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="2324c-110">Följ den [säkra appens modell](enable-secure-app-model.md) när du använder app + User Authentication med API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2324c-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="2324c-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2324c-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2324c-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2324c-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2324c-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2324c-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2324c-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2324c-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2324c-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2324c-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2324c-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2324c-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2324c-117">Produkt serien.</span><span class="sxs-lookup"><span data-stu-id="2324c-117">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="2324c-118">C\#</span><span class="sxs-lookup"><span data-stu-id="2324c-118">C\#</span></span>

<span data-ttu-id="2324c-119">Så här kontrollerar du om en kund är berättigad att uppgradera till Azure-planen:</span><span class="sxs-lookup"><span data-stu-id="2324c-119">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="2324c-120">Skapa ett **ProductUpgradesRequest** -objekt och ange kund-ID och "Azure" som produkt familj.</span><span class="sxs-lookup"><span data-stu-id="2324c-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="2324c-121">Använd samlingen **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="2324c-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="2324c-122">Anropa metoden **CheckEligibility** och skicka in **ProductUpgradesRequest** -objektet, vilket kommer att returnera ett **ProductUpgradesEligibility** -objekt.</span><span class="sxs-lookup"><span data-stu-id="2324c-122">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="2324c-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2324c-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2324c-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2324c-124">Request syntax</span></span>

| <span data-ttu-id="2324c-125">Metod</span><span class="sxs-lookup"><span data-stu-id="2324c-125">Method</span></span>   | <span data-ttu-id="2324c-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2324c-126">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2324c-127">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="2324c-127">**POST**</span></span> | <span data-ttu-id="2324c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/Eligibility http/1.1</span><span class="sxs-lookup"><span data-stu-id="2324c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2324c-129">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2324c-129">Request headers</span></span>

<span data-ttu-id="2324c-130">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2324c-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2324c-131">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2324c-131">Request body</span></span>

<span data-ttu-id="2324c-132">Begär ande texten måste innehålla en [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -resurs.</span><span class="sxs-lookup"><span data-stu-id="2324c-132">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="2324c-133">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2324c-133">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2324c-134">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2324c-134">REST response</span></span>

<span data-ttu-id="2324c-135">Om det lyckas returnerar den här metoden en [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -resurs i bröd texten.</span><span class="sxs-lookup"><span data-stu-id="2324c-135">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2324c-136">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2324c-136">Response success and error codes</span></span>

<span data-ttu-id="2324c-137">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2324c-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2324c-138">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2324c-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2324c-139">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2324c-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2324c-140">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2324c-140">Response example</span></span>

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
