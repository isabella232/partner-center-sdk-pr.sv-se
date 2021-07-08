---
title: Hämta en lista över produkter (efter kund)
description: Du kan använda en kundidentifierare för att hämta en samling produkter per kund.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: a7cb2430aa93beb89e4d1f9b8c89a016d66624ca
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874201"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="70008-103">Hämta en lista över produkter (efter kund)</span><span class="sxs-lookup"><span data-stu-id="70008-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="70008-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="70008-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="70008-105">Du kan använda följande metoder för att hämta en samling produkter för en befintlig kund.</span><span class="sxs-lookup"><span data-stu-id="70008-105">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70008-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="70008-106">Prerequisites</span></span>

- <span data-ttu-id="70008-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="70008-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="70008-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="70008-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="70008-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="70008-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="70008-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="70008-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="70008-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="70008-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="70008-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="70008-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="70008-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="70008-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="70008-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="70008-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="70008-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="70008-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="70008-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="70008-116">Request syntax</span></span>

| <span data-ttu-id="70008-117">Metod</span><span class="sxs-lookup"><span data-stu-id="70008-117">Method</span></span> | <span data-ttu-id="70008-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="70008-118">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="70008-119">POST</span><span class="sxs-lookup"><span data-stu-id="70008-119">POST</span></span>   | <span data-ttu-id="70008-120">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="70008-120">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="70008-121">URI-parametrar för begäran</span><span class="sxs-lookup"><span data-stu-id="70008-121">Request URI parameters</span></span>

| <span data-ttu-id="70008-122">Namn</span><span class="sxs-lookup"><span data-stu-id="70008-122">Name</span></span>               | <span data-ttu-id="70008-123">Typ</span><span class="sxs-lookup"><span data-stu-id="70008-123">Type</span></span> | <span data-ttu-id="70008-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="70008-124">Required</span></span> | <span data-ttu-id="70008-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="70008-125">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="70008-126">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="70008-126">**customer-tenant-id**</span></span> | <span data-ttu-id="70008-127">GUID</span><span class="sxs-lookup"><span data-stu-id="70008-127">GUID</span></span> | <span data-ttu-id="70008-128">Ja</span><span class="sxs-lookup"><span data-stu-id="70008-128">Yes</span></span> | <span data-ttu-id="70008-129">Värdet är ett GUID-formaterat **kundklient-id,** vilket är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="70008-129">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="70008-130">**targetView**</span><span class="sxs-lookup"><span data-stu-id="70008-130">**targetView**</span></span> | <span data-ttu-id="70008-131">sträng</span><span class="sxs-lookup"><span data-stu-id="70008-131">string</span></span> | <span data-ttu-id="70008-132">Ja</span><span class="sxs-lookup"><span data-stu-id="70008-132">Yes</span></span> | <span data-ttu-id="70008-133">Identifierar målvyn för katalogen.</span><span class="sxs-lookup"><span data-stu-id="70008-133">Identifies the target view of the catalog.</span></span> <span data-ttu-id="70008-134">Värdena som stöds är:</span><span class="sxs-lookup"><span data-stu-id="70008-134">The supported values are:</span></span> <br/><br/><span data-ttu-id="70008-135">**Azure**, som innehåller alla Azure-objekt</span><span class="sxs-lookup"><span data-stu-id="70008-135">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="70008-136">**AzureReservations**, som innehåller alla Reservationsobjekt i Azure</span><span class="sxs-lookup"><span data-stu-id="70008-136">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="70008-137">**AzureReservationsVM**, som innehåller alla reservationsobjekt för virtuella datorer (VM)</span><span class="sxs-lookup"><span data-stu-id="70008-137">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="70008-138">**AzureReservationsSQL**, som innehåller alla SQL reservationsobjekt</span><span class="sxs-lookup"><span data-stu-id="70008-138">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="70008-139">**AzureReservationsCosmosDb**, som innehåller alla reservationsobjekt för Cosmos-databasen</span><span class="sxs-lookup"><span data-stu-id="70008-139">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="70008-140">**MicrosoftAzure**, som innehåller objekt för Microsoft Azure-prenumerationer **(MS-AZR-0145P)** och Azure-planer</span><span class="sxs-lookup"><span data-stu-id="70008-140">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="70008-141">**OnlineServices**, som innehåller alla onlinetjänstobjekt, inklusive produkter på den kommersiella marknadsplatsen</span><span class="sxs-lookup"><span data-stu-id="70008-141">**OnlineServices**, which includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="70008-142">**Programvara**, som innehåller alla programvaruobjekt</span><span class="sxs-lookup"><span data-stu-id="70008-142">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="70008-143">**SoftwareSUSELinux**, som innehåller alla SUSE Linux-programobjekt</span><span class="sxs-lookup"><span data-stu-id="70008-143">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="70008-144">**SoftwarePerpetual**, som innehåller alla permanenta programvaruobjekt</span><span class="sxs-lookup"><span data-stu-id="70008-144">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="70008-145">**SoftwareSubscriptions**, som innehåller alla programprenumerationsobjekt</span><span class="sxs-lookup"><span data-stu-id="70008-145">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="70008-146">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="70008-146">Request header</span></span>

<span data-ttu-id="70008-147">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="70008-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="70008-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="70008-148">Request body</span></span>

<span data-ttu-id="70008-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="70008-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="70008-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="70008-150">Request example</span></span>

<span data-ttu-id="70008-151">Begäran om en lista över Användningsbaserade Azure-produkter som är tillgängliga för en viss kund.</span><span class="sxs-lookup"><span data-stu-id="70008-151">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="70008-152">Produkter för både Microsoft Azure (MS-AZR-0145P) och Azure-planer returneras för kunder i det offentliga molnet:</span><span class="sxs-lookup"><span data-stu-id="70008-152">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="70008-153">Rest-svar</span><span class="sxs-lookup"><span data-stu-id="70008-153">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="70008-154">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="70008-154">Response success and error codes</span></span>

<span data-ttu-id="70008-155">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="70008-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="70008-156">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="70008-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="70008-157">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="70008-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="70008-158">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="70008-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="70008-159">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="70008-159">HTTP Status Code</span></span> | <span data-ttu-id="70008-160">Felkod</span><span class="sxs-lookup"><span data-stu-id="70008-160">Error code</span></span>   | <span data-ttu-id="70008-161">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="70008-161">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="70008-162">403</span><span class="sxs-lookup"><span data-stu-id="70008-162">403</span></span> | <span data-ttu-id="70008-163">400036</span><span class="sxs-lookup"><span data-stu-id="70008-163">400036</span></span> | <span data-ttu-id="70008-164">Åtkomst till begärd targetView tillåts inte.</span><span class="sxs-lookup"><span data-stu-id="70008-164">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="70008-165">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="70008-165">Response example</span></span>

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
