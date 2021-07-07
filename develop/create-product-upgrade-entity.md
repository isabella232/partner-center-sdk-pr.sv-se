---
title: Skapa en produktuppgraderingsentitet för en kund
description: Du kan använda resursen ProductUpgradeRequest för att skapa en produktuppgraderingsentitet för att uppgradera en kund till en viss produktfamilj.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4e346b7f5294a8847047c85115d8c80f34eaca84
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973424"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="e481e-103">Skapa en produktuppgraderingsentitet för en kund</span><span class="sxs-lookup"><span data-stu-id="e481e-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="e481e-104">Du kan skapa en produktuppgraderingsentitet för att uppgradera en kund till en viss produktfamilj (till exempel Azure-plan) med hjälp av **resursen ProductUpgradeRequest.**</span><span class="sxs-lookup"><span data-stu-id="e481e-104">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e481e-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e481e-105">Prerequisites</span></span>

- <span data-ttu-id="e481e-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e481e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e481e-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="e481e-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="e481e-108">Följ den [säkra appmodellen när du](enable-secure-app-model.md) använder app-/användarautentisering med Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="e481e-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="e481e-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e481e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e481e-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e481e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e481e-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="e481e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e481e-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="e481e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e481e-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="e481e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e481e-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e481e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e481e-115">Den produktfamilj som du vill uppgradera kunden till.</span><span class="sxs-lookup"><span data-stu-id="e481e-115">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="e481e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e481e-116">C\#</span></span>

<span data-ttu-id="e481e-117">Så här uppgraderar du en kund till en Azure-plan:</span><span class="sxs-lookup"><span data-stu-id="e481e-117">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="e481e-118">Skapa ett **ProductUpgradesRequest-objekt** och ange kundidentifieraren och "Azure" som produktfamilj.</span><span class="sxs-lookup"><span data-stu-id="e481e-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="e481e-119">Använd **samlingen IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="e481e-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="e481e-120">Anropa metoden **Create** och skicka objektet **ProductUpgradesRequest,** som returnerar en platsrubriksträng. </span><span class="sxs-lookup"><span data-stu-id="e481e-120">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="e481e-121">Extrahera **upgrade-id från** platsrubriksträngen som kan användas för att [fråga uppgraderingsstatusen](get-product-upgrade-status.md).</span><span class="sxs-lookup"><span data-stu-id="e481e-121">Extract the **upgrade-id** from the location header string that can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a><span data-ttu-id="e481e-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e481e-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e481e-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="e481e-123">Request syntax</span></span>

| <span data-ttu-id="e481e-124">Metod</span><span class="sxs-lookup"><span data-stu-id="e481e-124">Method</span></span>   | <span data-ttu-id="e481e-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e481e-125">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="e481e-126">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="e481e-126">**POST**</span></span> | <span data-ttu-id="e481e-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e481e-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="e481e-128">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e481e-128">Request headers</span></span>

<span data-ttu-id="e481e-129">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e481e-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="e481e-130">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e481e-130">Request body</span></span>

<span data-ttu-id="e481e-131">Begärandetexten måste innehålla en [ProductUpgradeRequest-resurs.](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="e481e-131">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="e481e-132">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e481e-132">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="e481e-133">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e481e-133">REST response</span></span>

<span data-ttu-id="e481e-134">Om det lyckas innehåller svaret ett **Location-huvud** som har en URI som kan användas för att hämta produktuppgraderingsstatus.</span><span class="sxs-lookup"><span data-stu-id="e481e-134">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="e481e-135">Spara den här URI:en för användning med andra relaterade REST-API:er.</span><span class="sxs-lookup"><span data-stu-id="e481e-135">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e481e-136">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e481e-136">Response success and error codes</span></span>

<span data-ttu-id="e481e-137">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e481e-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e481e-138">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e481e-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e481e-139">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e481e-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e481e-140">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e481e-140">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
