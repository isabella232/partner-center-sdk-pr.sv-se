---
title: Hämta produktuppgraderingsstatus för en kund
description: Du kan använda resursen ProductUpgradeRequest för att fastställa status för en produktuppgradering för en kund till en ny produktfamilj, till exempel från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d925dd0fae987226ad1f8e71fad380ba144b83
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445569"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="77960-103">Hämta produktuppgraderingsstatus för en kund</span><span class="sxs-lookup"><span data-stu-id="77960-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="77960-104">Du kan använda [**resursen ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) för att hämta statusen för en uppgradering till en ny produktfamilj.</span><span class="sxs-lookup"><span data-stu-id="77960-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="77960-105">Den här resursen gäller när du uppgraderar en kund från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="77960-105">This resource applies when you're upgrading a customer from a Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="77960-106">En lyckad begäran returnerar [**resursen ProductUpgradesEligibility.**](product-upgrade-resources.md#productupgradeseligibility)</span><span class="sxs-lookup"><span data-stu-id="77960-106">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77960-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="77960-107">Prerequisites</span></span>

- <span data-ttu-id="77960-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="77960-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="77960-109">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="77960-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="77960-110">Följ den [säkra appmodellen när du](enable-secure-app-model.md) använder app-/användarautentisering med Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="77960-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="77960-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="77960-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="77960-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="77960-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="77960-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="77960-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="77960-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="77960-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="77960-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="77960-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="77960-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="77960-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="77960-117">Produktfamiljen.</span><span class="sxs-lookup"><span data-stu-id="77960-117">The product family.</span></span>

- <span data-ttu-id="77960-118">Uppgraderings-ID för en uppgraderingsbegäran.</span><span class="sxs-lookup"><span data-stu-id="77960-118">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="77960-119">C\#</span><span class="sxs-lookup"><span data-stu-id="77960-119">C\#</span></span>

<span data-ttu-id="77960-120">Så här kontrollerar du om en kund är berättigad att uppgradera till En Azure-plan:</span><span class="sxs-lookup"><span data-stu-id="77960-120">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="77960-121">Skapa ett **ProductUpgradesRequest-objekt** och ange kundidentifieraren och "Azure" som produktfamilj.</span><span class="sxs-lookup"><span data-stu-id="77960-121">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="77960-122">Använd **samlingen IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="77960-122">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="77960-123">Anropa **ById-metoden** och skicka **upgrade-id.**</span><span class="sxs-lookup"><span data-stu-id="77960-123">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="77960-124">Anropa **checkStatus-metoden** och skicka objektet **ProductUpgradesRequest,** som returnerar ett **ProductUpgradeStatus-objekt.**</span><span class="sxs-lookup"><span data-stu-id="77960-124">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="77960-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="77960-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="77960-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="77960-126">Request syntax</span></span>

| <span data-ttu-id="77960-127">Metod</span><span class="sxs-lookup"><span data-stu-id="77960-127">Method</span></span>   | <span data-ttu-id="77960-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="77960-128">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="77960-129">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="77960-129">**POST**</span></span> | <span data-ttu-id="77960-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="77960-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="77960-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="77960-131">URI parameter</span></span>

<span data-ttu-id="77960-132">Använd följande frågeparameter för att ange den kund som du får en produktuppgraderingsstatus för.</span><span class="sxs-lookup"><span data-stu-id="77960-132">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="77960-133">Namn</span><span class="sxs-lookup"><span data-stu-id="77960-133">Name</span></span>               | <span data-ttu-id="77960-134">Typ</span><span class="sxs-lookup"><span data-stu-id="77960-134">Type</span></span> | <span data-ttu-id="77960-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="77960-135">Required</span></span> | <span data-ttu-id="77960-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="77960-136">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="77960-137">**upgrade-id**</span><span class="sxs-lookup"><span data-stu-id="77960-137">**upgrade-id**</span></span> | <span data-ttu-id="77960-138">GUID</span><span class="sxs-lookup"><span data-stu-id="77960-138">GUID</span></span> | <span data-ttu-id="77960-139">Ja</span><span class="sxs-lookup"><span data-stu-id="77960-139">Yes</span></span> | <span data-ttu-id="77960-140">Värdet är en GUID-formaterad uppgraderingsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="77960-140">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="77960-141">Du kan använda den här identifieraren för att ange en uppgradering som ska spåras.</span><span class="sxs-lookup"><span data-stu-id="77960-141">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="77960-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="77960-142">Request headers</span></span>

<span data-ttu-id="77960-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="77960-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="77960-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="77960-144">Request body</span></span>

<span data-ttu-id="77960-145">Begärandetexten måste innehålla en [**ProductUpgradeRequest-resurs.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="77960-145">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="77960-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="77960-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="77960-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="77960-147">REST response</span></span>

<span data-ttu-id="77960-148">Om det lyckas returnerar den här metoden [**en ProductUpgradesEligibility-resurs**](product-upgrade-resources.md#productupgradeseligibility) i brödtexten.</span><span class="sxs-lookup"><span data-stu-id="77960-148">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="77960-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="77960-149">Response success and error codes</span></span>

<span data-ttu-id="77960-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="77960-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="77960-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="77960-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="77960-152">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="77960-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="77960-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="77960-153">Response example</span></span>

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
