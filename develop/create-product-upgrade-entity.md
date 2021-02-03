---
title: Skapa en produkt uppgraderings enhet för en kund
description: Du kan använda ProductUpgradeRequest-resursen för att skapa en enhet för produkt uppgradering för att uppgradera en kund till en specifik produkt familj.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768814"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="f921c-103">Skapa en produkt uppgraderings enhet för en kund</span><span class="sxs-lookup"><span data-stu-id="f921c-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="f921c-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="f921c-104">**Applies to:**</span></span>

- <span data-ttu-id="f921c-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="f921c-105">Partner Center</span></span>

<span data-ttu-id="f921c-106">Du kan skapa en produkt uppgraderings enhet för att uppgradera en kund till en specifik produkt serie (till exempel Azure-plan) med hjälp av **ProductUpgradeRequest** -resursen.</span><span class="sxs-lookup"><span data-stu-id="f921c-106">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f921c-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f921c-107">Prerequisites</span></span>

- <span data-ttu-id="f921c-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f921c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f921c-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f921c-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="f921c-110">Följ den [säkra appens modell](enable-secure-app-model.md) när du använder app + User Authentication med API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="f921c-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="f921c-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f921c-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f921c-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="f921c-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f921c-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="f921c-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f921c-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="f921c-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f921c-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="f921c-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f921c-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f921c-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f921c-117">Produkt familjen som du vill uppgradera kunden till.</span><span class="sxs-lookup"><span data-stu-id="f921c-117">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="f921c-118">C\#</span><span class="sxs-lookup"><span data-stu-id="f921c-118">C\#</span></span>

<span data-ttu-id="f921c-119">Uppgradera en kund till Azure-plan:</span><span class="sxs-lookup"><span data-stu-id="f921c-119">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="f921c-120">Skapa ett **ProductUpgradesRequest** -objekt och ange kund-ID och "Azure" som produkt familj.</span><span class="sxs-lookup"><span data-stu-id="f921c-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="f921c-121">Använd samlingen **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="f921c-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="f921c-122">Anropa metoden **create** och skicka i **ProductUpgradesRequest** -objektet, vilket kommer att returnera en **plats rubrik** sträng.</span><span class="sxs-lookup"><span data-stu-id="f921c-122">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="f921c-123">Extrahera **uppgraderings-ID: t** från plats huvud strängen som kan användas för att [fråga uppgraderings statusen](get-product-upgrade-status.md).</span><span class="sxs-lookup"><span data-stu-id="f921c-123">Extract the **upgrade-id** from the location header string which can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="f921c-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f921c-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f921c-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="f921c-125">Request syntax</span></span>

| <span data-ttu-id="f921c-126">Metod</span><span class="sxs-lookup"><span data-stu-id="f921c-126">Method</span></span>   | <span data-ttu-id="f921c-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f921c-127">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f921c-128">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="f921c-128">**POST**</span></span> | <span data-ttu-id="f921c-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades http/1.1</span><span class="sxs-lookup"><span data-stu-id="f921c-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="f921c-130">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f921c-130">Request headers</span></span>

<span data-ttu-id="f921c-131">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f921c-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="f921c-132">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f921c-132">Request body</span></span>

<span data-ttu-id="f921c-133">Begär ande texten måste innehålla en [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) -resurs.</span><span class="sxs-lookup"><span data-stu-id="f921c-133">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="f921c-134">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f921c-134">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f921c-135">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f921c-135">REST response</span></span>

<span data-ttu-id="f921c-136">Om det lyckas innehåller svaret ett **plats** huvud som har en URI som kan användas för att hämta produkt uppgraderings status.</span><span class="sxs-lookup"><span data-stu-id="f921c-136">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="f921c-137">Spara denna URI för användning med andra relaterade REST API: er.</span><span class="sxs-lookup"><span data-stu-id="f921c-137">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f921c-138">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f921c-138">Response success and error codes</span></span>

<span data-ttu-id="f921c-139">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="f921c-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f921c-140">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f921c-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f921c-141">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f921c-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f921c-142">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f921c-142">Response example</span></span>

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
