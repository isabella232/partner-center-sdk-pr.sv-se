---
title: Kontrol lera inventering
description: 'Lär dig hur du använder API: er för partner Center för att kontrol lera inventeringen för en bestämd uppsättning katalog objekt. Du kan göra detta för att identifiera en kunds produkter eller SKU: er.'
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6921760abc0b95aff820467e84b3e8e9435731cd
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770086"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="fee13-104">Kontrol lera förteckningen över katalog objekt med API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="fee13-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="fee13-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="fee13-105">**Applies to:**</span></span>

- <span data-ttu-id="fee13-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="fee13-106">Partner Center</span></span>

<span data-ttu-id="fee13-107">Så här kontrollerar du inventeringen för en bestämd uppsättning katalog objekt.</span><span class="sxs-lookup"><span data-stu-id="fee13-107">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fee13-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="fee13-108">Prerequisites</span></span>

- <span data-ttu-id="fee13-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fee13-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fee13-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="fee13-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fee13-111">Ett eller flera produkt-ID: n.</span><span class="sxs-lookup"><span data-stu-id="fee13-111">One or more product IDs.</span></span> <span data-ttu-id="fee13-112">Du kan också ange SKU-ID: n.</span><span class="sxs-lookup"><span data-stu-id="fee13-112">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="fee13-113">Eventuell ytterligare kontext som krävs för att verifiera inventeringen av de SKU: er som refereras av de tillhandahållna produkt-eller SKU-ID: n.</span><span class="sxs-lookup"><span data-stu-id="fee13-113">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="fee13-114">Dessa krav kan variera beroende på typ av produkt/SKU och kan fastställas från [SKU: s](product-resources.md#sku) **InventoryVariables** -egenskap.</span><span class="sxs-lookup"><span data-stu-id="fee13-114">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="fee13-115">C\#</span><span class="sxs-lookup"><span data-stu-id="fee13-115">C\#</span></span>

<span data-ttu-id="fee13-116">Om du vill kontrol lera inventeringen skapar du ett [InventoryCheckRequest](product-resources.md#inventorycheckrequest) -objekt med ett [InventoryItem](product-resources.md#inventoryitem) -objekt för varje objekt som ska kontrol leras.</span><span class="sxs-lookup"><span data-stu-id="fee13-116">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="fee13-117">Använd sedan en **IAggregatePartner. Extensions** -accessor, omfånget till **produkten** och välj sedan landet med **ByCountry ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="fee13-117">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="fee13-118">Anropa slutligen metoden **CheckInventory ()** med **InventoryCheckRequest** -objektet.</span><span class="sxs-lookup"><span data-stu-id="fee13-118">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a><span data-ttu-id="fee13-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="fee13-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fee13-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="fee13-120">Request syntax</span></span>

| <span data-ttu-id="fee13-121">Metod</span><span class="sxs-lookup"><span data-stu-id="fee13-121">Method</span></span>   | <span data-ttu-id="fee13-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="fee13-122">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fee13-123">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="fee13-123">**POST**</span></span> | <span data-ttu-id="fee13-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? land = {Country-Code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fee13-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="fee13-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="fee13-125">URI parameter</span></span>

<span data-ttu-id="fee13-126">Använd följande frågeparameter för att kontrol lera inventeringen.</span><span class="sxs-lookup"><span data-stu-id="fee13-126">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="fee13-127">Namn</span><span class="sxs-lookup"><span data-stu-id="fee13-127">Name</span></span>                   | <span data-ttu-id="fee13-128">Typ</span><span class="sxs-lookup"><span data-stu-id="fee13-128">Type</span></span>     | <span data-ttu-id="fee13-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="fee13-129">Required</span></span> | <span data-ttu-id="fee13-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="fee13-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="fee13-131">landskod</span><span class="sxs-lookup"><span data-stu-id="fee13-131">country-code</span></span>           | <span data-ttu-id="fee13-132">sträng</span><span class="sxs-lookup"><span data-stu-id="fee13-132">string</span></span>   | <span data-ttu-id="fee13-133">Yes</span><span class="sxs-lookup"><span data-stu-id="fee13-133">Yes</span></span>      | <span data-ttu-id="fee13-134">Ett land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="fee13-134">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="fee13-135">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="fee13-135">Request headers</span></span>

<span data-ttu-id="fee13-136">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fee13-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fee13-137">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="fee13-137">Request body</span></span>

<span data-ttu-id="fee13-138">Information om inventerings begär Anden som består av en [InventoryCheckRequest](product-resources.md#inventorycheckrequest) -resurs som innehåller en eller flera [InventoryItem](product-resources.md#inventoryitem) -resurser.</span><span class="sxs-lookup"><span data-stu-id="fee13-138">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="fee13-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="fee13-139">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a><span data-ttu-id="fee13-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="fee13-140">REST response</span></span>

<span data-ttu-id="fee13-141">Om det lyckas innehåller svars texten en samling [InventoryItem](product-resources.md#inventoryitem) -objekt som är ifyllda med begränsnings informationen, om tillämpligt.</span><span class="sxs-lookup"><span data-stu-id="fee13-141">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="fee13-142">Om en InventoryItem för indata representerar ett objekt som inte kunde hittas i katalogen, kommer det inte att tas med i insamlingen av utdata.</span><span class="sxs-lookup"><span data-stu-id="fee13-142">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fee13-143">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="fee13-143">Response success and error codes</span></span>

<span data-ttu-id="fee13-144">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="fee13-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fee13-145">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="fee13-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fee13-146">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fee13-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fee13-147">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="fee13-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
