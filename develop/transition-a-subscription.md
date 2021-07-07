---
title: Överför en prenumeration
description: Uppgraderar en kunds prenumeration till en angiven målprenumeration.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01455315825cad026830268b6bbd55509e964bb5
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530248"
---
# <a name="transition-a-subscription"></a><span data-ttu-id="52212-103">Överför en prenumeration</span><span class="sxs-lookup"><span data-stu-id="52212-103">Transition a subscription</span></span>

<span data-ttu-id="52212-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="52212-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="52212-105">Uppgraderar en kunds prenumeration till en angiven målprenumeration.</span><span class="sxs-lookup"><span data-stu-id="52212-105">Upgrades a customer's subscription to a specified target subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52212-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="52212-106">Prerequisites</span></span>

- <span data-ttu-id="52212-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="52212-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="52212-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="52212-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="52212-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="52212-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="52212-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="52212-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="52212-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="52212-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="52212-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="52212-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="52212-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="52212-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="52212-114">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="52212-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="52212-115">Två prenumerations-ID:er, ett för den första prenumerationen och ett för målprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="52212-115">Two subscription IDs, one for the initial subscription and one for the target subscription.</span></span>

## <a name="c"></a><span data-ttu-id="52212-116">C\#</span><span class="sxs-lookup"><span data-stu-id="52212-116">C\#</span></span>

<span data-ttu-id="52212-117">Om du vill uppgradera en kunds [prenumeration hämtar du först kundens prenumeration.](get-a-subscription-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="52212-117">To upgrade a customer's subscription, first [get that's customer's subscription](get-a-subscription-by-id.md).</span></span> <span data-ttu-id="52212-118">Hämta sedan en lista över uppgraderingar för prenumerationen genom att anropa **uppgraderingar-egenskapen** följt av **metoderna Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="52212-118">Then, obtain a list of upgrades for that subscription by calling the **Upgrades** property followed by the **Get()** or **GetAsync()** methods.</span></span> <span data-ttu-id="52212-119">Välj en måluppgradering i listan över uppgraderingar och anropa sedan egenskapen **Uppgraderingar** för den första prenumerationen, följt av **metoden Create().**</span><span class="sxs-lookup"><span data-stu-id="52212-119">Choose a target upgrade from that list of upgrades, and then call the **Upgrades** property of the initial subscription, followed by the **Create()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

<span data-ttu-id="52212-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="52212-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="52212-121">**Project:** PartnerSDK.FeatureSamples-klass: UpgradeSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="52212-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpgradeSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="52212-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="52212-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52212-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="52212-123">Request syntax</span></span>

| <span data-ttu-id="52212-124">Metod</span><span class="sxs-lookup"><span data-stu-id="52212-124">Method</span></span>   | <span data-ttu-id="52212-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="52212-125">Request URI</span></span>                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="52212-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="52212-126">**GET**</span></span>  | <span data-ttu-id="52212-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="52212-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span></span> |
| <span data-ttu-id="52212-128">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="52212-128">**POST**</span></span> | <span data-ttu-id="52212-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="52212-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span></span>       |

### <a name="uri-parameter"></a><span data-ttu-id="52212-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="52212-130">URI parameter</span></span>

<span data-ttu-id="52212-131">Använd följande frågeparameter för att övergå till prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="52212-131">Use the following query parameter to transition the subscription.</span></span>

| <span data-ttu-id="52212-132">Namn</span><span class="sxs-lookup"><span data-stu-id="52212-132">Name</span></span>                    | <span data-ttu-id="52212-133">Typ</span><span class="sxs-lookup"><span data-stu-id="52212-133">Type</span></span>     | <span data-ttu-id="52212-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="52212-134">Required</span></span> | <span data-ttu-id="52212-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="52212-135">Description</span></span>                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| <span data-ttu-id="52212-136">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="52212-136">**customer-tenant-id**</span></span>  | <span data-ttu-id="52212-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="52212-137">**guid**</span></span> | <span data-ttu-id="52212-138">Y</span><span class="sxs-lookup"><span data-stu-id="52212-138">Y</span></span>        | <span data-ttu-id="52212-139">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="52212-139">A GUID corresponding to the customer.</span></span>             |
| <span data-ttu-id="52212-140">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="52212-140">**id-for-subscription**</span></span> | <span data-ttu-id="52212-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="52212-141">**guid**</span></span> | <span data-ttu-id="52212-142">Y</span><span class="sxs-lookup"><span data-stu-id="52212-142">Y</span></span>        | <span data-ttu-id="52212-143">Ett GUID som motsvarar den första prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="52212-143">A GUID corresponding to the initial subscription.</span></span> |
| <span data-ttu-id="52212-144">**id-for-target**</span><span class="sxs-lookup"><span data-stu-id="52212-144">**id-for-target**</span></span>       | <span data-ttu-id="52212-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="52212-145">**guid**</span></span> | <span data-ttu-id="52212-146">Y</span><span class="sxs-lookup"><span data-stu-id="52212-146">Y</span></span>        | <span data-ttu-id="52212-147">Ett GUID som motsvarar målprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="52212-147">A GUID corresponding to the target subscription.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="52212-148">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="52212-148">Request headers</span></span>

<span data-ttu-id="52212-149">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="52212-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52212-150">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="52212-150">Request body</span></span>

<span data-ttu-id="52212-151">Ingen</span><span class="sxs-lookup"><span data-stu-id="52212-151">None</span></span>

### <a name="request-example"></a><span data-ttu-id="52212-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="52212-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

POST https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
Content-Type: application/json
Content-Length: 1098
Expect: 100-continue

{
    "TargetOffer":{
        "Id":"796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Name":"Office 365 Enterprise E3",
        "Description":"The best plan for businesses that need full productivity, communication and collaboration tools with the familiar Office suite, including Office Online.",
        "MinimumQuantity":1,
        "MaximumQuantity":10000000,
        "Rank":61,
        "Uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Locale":"en-us",
        "Country":"US",
        "Category":{
            "Id":"Enterprise_Key",
            "Name":"Enterprise",
            "Rank":20,
            "Locale":"en-us",
            "Country":"US",
            "Attributes":{
                "ObjectType":"OfferCategory"
            }
        },
        "PrerequisiteOffers":[],
        "IsAddOn":false,
        "IsAvailableForPurchase":true,
        "Billing":"license",
        "IsAutoRenewable":true,
        "Product":{
            "Id":"6fd2c87f-b296-42f0-b197-1e91e994b900",
            "Name":"Office 365 Enterprise E3",
            "Unit":"Licenses"
        },
        "UnitType":"Licenses",
        "Links":{
            "LearnMore":{
                "Uri":"http://g.microsoftonline.com/0BXPS00en/1015",
                "Method":"GET",
                "Headers":[]
            }
        }
        "Attributes":{
            "ObjectType":"Offer"
        }
    },
    "UpgradeType":1,
    "IsEligible":true,
    "Quantity":1,
    "UpgradeErrors":[],
    "Attributes":{
        "ObjectType":"Upgrade"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="52212-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="52212-153">REST response</span></span>

<span data-ttu-id="52212-154">Om det lyckas returnerar den här metoden **en uppgraderingsresultatresurs** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="52212-154">If successful, this method returns an **Upgrade** result resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52212-155">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="52212-155">Response success and error codes</span></span>

<span data-ttu-id="52212-156">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="52212-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52212-157">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="52212-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52212-158">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="52212-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52212-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="52212-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 29 Jan 2016 20:42:26 GMT

{
    "totalCount": 1,
    "items": [{
        "targetOffer": {
            "id": "91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "name": "Office 365 Enterprise E1",
            "description": "For businesses that need communication and collaboration tools and the ability to read and do lightweight editing of documents with Office Online.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 48,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "locale": "en-us",
            "country": "US",
            "category": {
                "id": "Enterprise_Key",
                "name": "Enterprise",
                "rank": 20,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": [],
            "isAddOn": false,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "isInternal": false,
            "conversionTargetOffers": [],
            "partnerQualifications": ["none"],
            "product": {
                "id": "18181a46-0d4e-45cd-891e-60aabd171b4e",
                "name": "Office 365 Enterprise E1",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "uri": "http://g.microsoftonline.com/0BXPS00en/1013",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/91FD106F-4B2C-4938-95AC-F54F74E9A239?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        },
        "upgradeType": "upgrade_only",
        "isEligible": false,
        "quantity": 1,
        "upgradeErrors": [{
            "code": 2,
            "description": "Subscription cannot be upgraded because the source subscription state is not active.  Additional Details contains the current source subscription state.",
            "attributes": {
                "objectType": "UpgradeError"
            }
        }],
        "attributes": {
            "objectType": "Upgrade"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}

HTTP/1.1 200 OK
Content-Length: 448
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CV: RnK86LBbDkWP/w2R.0
MS-ServerId: 102031201
Date: Fri, 29 Jan 2016 20:44:21 GMT

{
    "sourceSubscriptionId":"896a2862-67e2-4f3d-bb3f-c50c42b5fad8",
    "targetSubscriptionId":"2add8a55-454a-4ae5-a4c9-5107dc6e9768",
    "upgradeType":1,
    "upgradeErrors":[],
    "licenseErrors":[],
    "attributes":{
        "objectType":"UpgradeResult"
    }
}
```
