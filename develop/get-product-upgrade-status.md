---
title: Hämta produkt uppgraderings status för en kund
description: Du kan använda ProductUpgradeRequest-resursen för att fastställa status för en produkt uppgradering för en kund till en ny produkt familj, till exempel från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1819887d459ec72a48ea2b7a5a4121dc56718313
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769060"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="f2478-103">Hämta produkt uppgraderings status för en kund</span><span class="sxs-lookup"><span data-stu-id="f2478-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="f2478-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="f2478-104">**Applies to:**</span></span>

- <span data-ttu-id="f2478-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="f2478-105">Partner Center</span></span>

<span data-ttu-id="f2478-106">Du kan använda [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -resursen för att hämta status för en uppgradering till en ny produkt familj.</span><span class="sxs-lookup"><span data-stu-id="f2478-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="f2478-107">Den här resursen gäller när du uppgraderar en kund från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="f2478-107">This resource applies when you're upgrading a customer from an Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="f2478-108">En lyckad begäran returnerar [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -resursen.</span><span class="sxs-lookup"><span data-stu-id="f2478-108">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2478-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f2478-109">Prerequisites</span></span>

- <span data-ttu-id="f2478-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f2478-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f2478-111">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f2478-111">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="f2478-112">Följ den [säkra appens modell](enable-secure-app-model.md) när du använder app + User Authentication med API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="f2478-112">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="f2478-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f2478-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f2478-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="f2478-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f2478-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="f2478-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f2478-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="f2478-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f2478-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="f2478-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f2478-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f2478-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f2478-119">Produkt serien.</span><span class="sxs-lookup"><span data-stu-id="f2478-119">The product family.</span></span>

- <span data-ttu-id="f2478-120">Uppgraderings-ID för en uppgraderings förfrågan.</span><span class="sxs-lookup"><span data-stu-id="f2478-120">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="f2478-121">C\#</span><span class="sxs-lookup"><span data-stu-id="f2478-121">C\#</span></span>

<span data-ttu-id="f2478-122">Så här kontrollerar du om en kund är berättigad att uppgradera till Azure-planen:</span><span class="sxs-lookup"><span data-stu-id="f2478-122">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="f2478-123">Skapa ett **ProductUpgradesRequest** -objekt och ange kund-ID och "Azure" som produkt familj.</span><span class="sxs-lookup"><span data-stu-id="f2478-123">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="f2478-124">Använd samlingen **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="f2478-124">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="f2478-125">Anropa metoden **ById** och pass i **Upgrade-ID: t**.</span><span class="sxs-lookup"><span data-stu-id="f2478-125">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="f2478-126">Anropa metoden **CheckStatus** och skicka in **ProductUpgradesRequest** -objektet, vilket kommer att returnera ett **ProductUpgradeStatus** -objekt.</span><span class="sxs-lookup"><span data-stu-id="f2478-126">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="f2478-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f2478-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f2478-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="f2478-128">Request syntax</span></span>

| <span data-ttu-id="f2478-129">Metod</span><span class="sxs-lookup"><span data-stu-id="f2478-129">Method</span></span>   | <span data-ttu-id="f2478-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f2478-130">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f2478-131">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="f2478-131">**POST**</span></span> | <span data-ttu-id="f2478-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{Upgrade-ID}/status http/1.1</span><span class="sxs-lookup"><span data-stu-id="f2478-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f2478-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="f2478-133">URI parameter</span></span>

<span data-ttu-id="f2478-134">Använd följande frågeparameter för att ange vilken kund som du vill få en produkt uppgraderings status för.</span><span class="sxs-lookup"><span data-stu-id="f2478-134">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="f2478-135">Namn</span><span class="sxs-lookup"><span data-stu-id="f2478-135">Name</span></span>               | <span data-ttu-id="f2478-136">Typ</span><span class="sxs-lookup"><span data-stu-id="f2478-136">Type</span></span> | <span data-ttu-id="f2478-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="f2478-137">Required</span></span> | <span data-ttu-id="f2478-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="f2478-138">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="f2478-139">**uppgradera-ID**</span><span class="sxs-lookup"><span data-stu-id="f2478-139">**upgrade-id**</span></span> | <span data-ttu-id="f2478-140">GUID</span><span class="sxs-lookup"><span data-stu-id="f2478-140">GUID</span></span> | <span data-ttu-id="f2478-141">Yes</span><span class="sxs-lookup"><span data-stu-id="f2478-141">Yes</span></span> | <span data-ttu-id="f2478-142">Värdet är ett GUID-formaterat uppgraderings-ID.</span><span class="sxs-lookup"><span data-stu-id="f2478-142">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="f2478-143">Du kan använda den här identifieraren för att ange en uppgradering som ska spåras.</span><span class="sxs-lookup"><span data-stu-id="f2478-143">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f2478-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f2478-144">Request headers</span></span>

<span data-ttu-id="f2478-145">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f2478-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f2478-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f2478-146">Request body</span></span>

<span data-ttu-id="f2478-147">Begär ande texten måste innehålla en [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -resurs.</span><span class="sxs-lookup"><span data-stu-id="f2478-147">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="f2478-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f2478-148">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
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
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a><span data-ttu-id="f2478-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f2478-149">REST response</span></span>

<span data-ttu-id="f2478-150">Om det lyckas returnerar den här metoden en [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -resurs i bröd texten.</span><span class="sxs-lookup"><span data-stu-id="f2478-150">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f2478-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f2478-151">Response success and error codes</span></span>

<span data-ttu-id="f2478-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="f2478-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f2478-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f2478-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f2478-154">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f2478-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f2478-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f2478-155">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
