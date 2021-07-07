---
title: Kontrollera inventering
description: Lär dig hur du använder Partner Center-API:er för att kontrollera inventeringen för en specifik uppsättning katalogobjekt. Du kan göra detta för att identifiera en kunds produkter eller SKU:er.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b982dbd7e5e10d454ef87a1e750546ea50eb8438
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974088"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="45d90-104">Kontrollera inventeringen av katalogobjekt med partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="45d90-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="45d90-105">Så här kontrollerar du lagret för en specifik uppsättning katalogobjekt.</span><span class="sxs-lookup"><span data-stu-id="45d90-105">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45d90-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="45d90-106">Prerequisites</span></span>

- <span data-ttu-id="45d90-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="45d90-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="45d90-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="45d90-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="45d90-109">Ett eller flera produkt-ID:er.</span><span class="sxs-lookup"><span data-stu-id="45d90-109">One or more product IDs.</span></span> <span data-ttu-id="45d90-110">Du kan också ange SKU-ID:n.</span><span class="sxs-lookup"><span data-stu-id="45d90-110">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="45d90-111">Eventuell ytterligare kontext som behövs för att verifiera inventeringen av de SKU:er som refereras av de tillhandahållna produkt-/SKU-ID:erna.</span><span class="sxs-lookup"><span data-stu-id="45d90-111">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="45d90-112">Dessa krav kan variera beroende på typ av produkt/SKU och kan fastställas från [SKU:ns](product-resources.md#sku) **egenskap InventoryVariables.**</span><span class="sxs-lookup"><span data-stu-id="45d90-112">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="45d90-113">C\#</span><span class="sxs-lookup"><span data-stu-id="45d90-113">C\#</span></span>

<span data-ttu-id="45d90-114">Om du vill kontrollera inventeringen skapar du [ett InventoryCheckRequest-objekt](product-resources.md#inventorycheckrequest) med hjälp av [ett InventoryItem-objekt](product-resources.md#inventoryitem) för varje objekt som ska kontrolleras.</span><span class="sxs-lookup"><span data-stu-id="45d90-114">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="45d90-115">Använd sedan en **åtkomstor för IAggregatePartner.Extensions,** begränsa den till **Produkt** och välj sedan land med hjälp av **metoden ByCountry().**</span><span class="sxs-lookup"><span data-stu-id="45d90-115">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="45d90-116">Anropa slutligen metoden **CheckInventory()** med ditt **InventoryCheckRequest-objekt.**</span><span class="sxs-lookup"><span data-stu-id="45d90-116">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="45d90-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="45d90-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="45d90-118">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="45d90-118">Request syntax</span></span>

| <span data-ttu-id="45d90-119">Metod</span><span class="sxs-lookup"><span data-stu-id="45d90-119">Method</span></span>   | <span data-ttu-id="45d90-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="45d90-120">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="45d90-121">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="45d90-121">**POST**</span></span> | <span data-ttu-id="45d90-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="45d90-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="45d90-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="45d90-123">URI parameter</span></span>

<span data-ttu-id="45d90-124">Använd följande frågeparameter för att kontrollera inventeringen.</span><span class="sxs-lookup"><span data-stu-id="45d90-124">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="45d90-125">Namn</span><span class="sxs-lookup"><span data-stu-id="45d90-125">Name</span></span>                   | <span data-ttu-id="45d90-126">Typ</span><span class="sxs-lookup"><span data-stu-id="45d90-126">Type</span></span>     | <span data-ttu-id="45d90-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="45d90-127">Required</span></span> | <span data-ttu-id="45d90-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="45d90-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="45d90-129">landskod</span><span class="sxs-lookup"><span data-stu-id="45d90-129">country-code</span></span>           | <span data-ttu-id="45d90-130">sträng</span><span class="sxs-lookup"><span data-stu-id="45d90-130">string</span></span>   | <span data-ttu-id="45d90-131">Ja</span><span class="sxs-lookup"><span data-stu-id="45d90-131">Yes</span></span>      | <span data-ttu-id="45d90-132">Ett lands-/regions-ID.</span><span class="sxs-lookup"><span data-stu-id="45d90-132">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="45d90-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="45d90-133">Request headers</span></span>

<span data-ttu-id="45d90-134">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="45d90-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="45d90-135">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="45d90-135">Request body</span></span>

<span data-ttu-id="45d90-136">Information om inventeringsbegäran som består av en [InventoryCheckRequest-resurs](product-resources.md#inventorycheckrequest) som innehåller en eller flera [InventoryItem-resurser.](product-resources.md#inventoryitem)</span><span class="sxs-lookup"><span data-stu-id="45d90-136">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="45d90-137">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="45d90-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="45d90-138">REST-svar</span><span class="sxs-lookup"><span data-stu-id="45d90-138">REST response</span></span>

<span data-ttu-id="45d90-139">Om det lyckas innehåller svarstexten en samling [InventoryItem-objekt](product-resources.md#inventoryitem) ifyllda med begränsningsinformationen, om tillämpligt.</span><span class="sxs-lookup"><span data-stu-id="45d90-139">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="45d90-140">Om indatan InventoryItem representerar ett objekt som inte kunde hittas i katalogen inkluderas det inte i utdatasamlingen.</span><span class="sxs-lookup"><span data-stu-id="45d90-140">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="45d90-141">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="45d90-141">Response success and error codes</span></span>

<span data-ttu-id="45d90-142">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="45d90-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="45d90-143">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="45d90-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="45d90-144">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="45d90-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="45d90-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="45d90-145">Response example</span></span>

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
