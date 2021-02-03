---
title: Hämta en lista över produkter (efter kund)
description: Du kan använda ett kund-ID för att få en samling produkter per kund.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 98a099c458535123f675c6452db950b087b9f387
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769450"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="0cb59-103">Hämta en lista över produkter (efter kund)</span><span class="sxs-lookup"><span data-stu-id="0cb59-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="0cb59-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="0cb59-104">**Applies to:**</span></span>

- <span data-ttu-id="0cb59-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="0cb59-105">Partner Center</span></span>
- <span data-ttu-id="0cb59-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0cb59-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0cb59-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="0cb59-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0cb59-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0cb59-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0cb59-109">Du kan använda följande metoder för att hämta en samling produkter för en befintlig kund.</span><span class="sxs-lookup"><span data-stu-id="0cb59-109">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cb59-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="0cb59-110">Prerequisites</span></span>

- <span data-ttu-id="0cb59-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0cb59-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0cb59-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="0cb59-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0cb59-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0cb59-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0cb59-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="0cb59-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0cb59-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="0cb59-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0cb59-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="0cb59-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0cb59-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="0cb59-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0cb59-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0cb59-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="0cb59-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="0cb59-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0cb59-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="0cb59-120">Request syntax</span></span>

| <span data-ttu-id="0cb59-121">Metod</span><span class="sxs-lookup"><span data-stu-id="0cb59-121">Method</span></span> | <span data-ttu-id="0cb59-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="0cb59-122">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0cb59-123">POST</span><span class="sxs-lookup"><span data-stu-id="0cb59-123">POST</span></span>   | <span data-ttu-id="0cb59-124">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products? targetView = {targetView} http/1.1</span><span class="sxs-lookup"><span data-stu-id="0cb59-124">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="0cb59-125">Begär URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="0cb59-125">Request URI parameters</span></span>

| <span data-ttu-id="0cb59-126">Namn</span><span class="sxs-lookup"><span data-stu-id="0cb59-126">Name</span></span>               | <span data-ttu-id="0cb59-127">Typ</span><span class="sxs-lookup"><span data-stu-id="0cb59-127">Type</span></span> | <span data-ttu-id="0cb59-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="0cb59-128">Required</span></span> | <span data-ttu-id="0cb59-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0cb59-129">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="0cb59-130">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="0cb59-130">**customer-tenant-id**</span></span> | <span data-ttu-id="0cb59-131">GUID</span><span class="sxs-lookup"><span data-stu-id="0cb59-131">GUID</span></span> | <span data-ttu-id="0cb59-132">Yes</span><span class="sxs-lookup"><span data-stu-id="0cb59-132">Yes</span></span> | <span data-ttu-id="0cb59-133">Värdet är ett GUID-formaterat **kund-ID**, som är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="0cb59-133">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="0cb59-134">**targetView**</span><span class="sxs-lookup"><span data-stu-id="0cb59-134">**targetView**</span></span> | <span data-ttu-id="0cb59-135">sträng</span><span class="sxs-lookup"><span data-stu-id="0cb59-135">string</span></span> | <span data-ttu-id="0cb59-136">Yes</span><span class="sxs-lookup"><span data-stu-id="0cb59-136">Yes</span></span> | <span data-ttu-id="0cb59-137">Identifierar katalogens mållista.</span><span class="sxs-lookup"><span data-stu-id="0cb59-137">Identifies the target view of the catalog.</span></span> <span data-ttu-id="0cb59-138">De värden som stöds är:</span><span class="sxs-lookup"><span data-stu-id="0cb59-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="0cb59-139">**Azure**, som innehåller alla Azure-objekt</span><span class="sxs-lookup"><span data-stu-id="0cb59-139">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="0cb59-140">**AzureReservations**, som innehåller alla Azure reservation-objekt</span><span class="sxs-lookup"><span data-stu-id="0cb59-140">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="0cb59-141">**AzureReservationsVM**, som innehåller alla reservations objekt för virtuella datorer (VM)</span><span class="sxs-lookup"><span data-stu-id="0cb59-141">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="0cb59-142">**AzureReservationsSQL**, som innehåller alla SQL reservation-objekt</span><span class="sxs-lookup"><span data-stu-id="0cb59-142">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="0cb59-143">**AzureReservationsCosmosDb**, som innehåller alla Cosmos-databas reservations objekt</span><span class="sxs-lookup"><span data-stu-id="0cb59-143">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="0cb59-144">**MicrosoftAzure**, som innehåller objekt för Microsoft Azure prenumerationer (**MS-AZR-0145P**) och Azure-planer</span><span class="sxs-lookup"><span data-stu-id="0cb59-144">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="0cb59-145">**OnlineServices**, som omfattar alla online tjänst objekt, inklusive kommersiella Marketplace-produkter</span><span class="sxs-lookup"><span data-stu-id="0cb59-145">**OnlineServices**, which  includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="0cb59-146">**Program vara**, som innehåller alla program varu objekt</span><span class="sxs-lookup"><span data-stu-id="0cb59-146">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="0cb59-147">**SoftwareSUSELinux**, som innehåller alla program vara SUSE Linux-objekt</span><span class="sxs-lookup"><span data-stu-id="0cb59-147">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="0cb59-148">**SoftwarePerpetual**, som innehåller alla objekt med beständig program vara</span><span class="sxs-lookup"><span data-stu-id="0cb59-148">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="0cb59-149">**SoftwareSubscriptions**, som innehåller alla program prenumerations objekt</span><span class="sxs-lookup"><span data-stu-id="0cb59-149">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="0cb59-150">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="0cb59-150">Request header</span></span>

<span data-ttu-id="0cb59-151">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0cb59-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0cb59-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="0cb59-152">Request body</span></span>

<span data-ttu-id="0cb59-153">Inga.</span><span class="sxs-lookup"><span data-stu-id="0cb59-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0cb59-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="0cb59-154">Request example</span></span>

<span data-ttu-id="0cb59-155">Begär en lista över Azure Usage-baserade produkter som är tillgängliga för en bestämd kund.</span><span class="sxs-lookup"><span data-stu-id="0cb59-155">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="0cb59-156">Produkter för både Microsoft Azure (MS-AZR-0145P) och Azure-planer kommer att returneras för kunder i det offentliga molnet:</span><span class="sxs-lookup"><span data-stu-id="0cb59-156">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="0cb59-157">Rest-svar</span><span class="sxs-lookup"><span data-stu-id="0cb59-157">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0cb59-158">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="0cb59-158">Response success and error codes</span></span>

<span data-ttu-id="0cb59-159">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="0cb59-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0cb59-160">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="0cb59-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0cb59-161">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0cb59-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="0cb59-162">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="0cb59-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="0cb59-163">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="0cb59-163">HTTP Status Code</span></span> | <span data-ttu-id="0cb59-164">Felkod</span><span class="sxs-lookup"><span data-stu-id="0cb59-164">Error code</span></span>   | <span data-ttu-id="0cb59-165">Description</span><span class="sxs-lookup"><span data-stu-id="0cb59-165">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="0cb59-166">403</span><span class="sxs-lookup"><span data-stu-id="0cb59-166">403</span></span> | <span data-ttu-id="0cb59-167">400036</span><span class="sxs-lookup"><span data-stu-id="0cb59-167">400036</span></span> | <span data-ttu-id="0cb59-168">Åtkomst till den begärda targetView är inte tillåten.</span><span class="sxs-lookup"><span data-stu-id="0cb59-168">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="0cb59-169">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="0cb59-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
