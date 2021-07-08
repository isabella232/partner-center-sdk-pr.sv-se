---
title: Hämta en lista över tillgängliga licenser efter licensgrupp
description: Så här hämtar du en lista över licenser för de angivna licensgrupperna som är tillgängliga för användare av den angivna kunden.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: de59dfccf723c8f2411d9dadc51beb88688d5b02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874524"
---
# <a name="get-a-list-of-available-licenses-by-license-group"></a><span data-ttu-id="54a13-103">Hämta en lista över tillgängliga licenser efter licensgrupp</span><span class="sxs-lookup"><span data-stu-id="54a13-103">Get a list of available licenses by license group</span></span>

<span data-ttu-id="54a13-104">Så här hämtar du en lista över licenser för de angivna licensgrupperna som är tillgängliga för användare av den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="54a13-104">How to get a list of licenses for the specified license groups available to users of the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54a13-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="54a13-105">Prerequisites</span></span>

- <span data-ttu-id="54a13-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="54a13-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="54a13-107">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="54a13-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="54a13-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54a13-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="54a13-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="54a13-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="54a13-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="54a13-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="54a13-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="54a13-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="54a13-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="54a13-112">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="54a13-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54a13-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="54a13-114">En lista över en eller flera licensgruppsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="54a13-114">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="54a13-115">C\#</span><span class="sxs-lookup"><span data-stu-id="54a13-115">C\#</span></span>

<span data-ttu-id="54a13-116">Om du vill hämta en lista över tillgängliga licenser för [](/dotnet/api/system.collections.generic.list-1) de angivna licensgrupperna börjar du med att skapa en instans av en lista av typen [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)och lägger sedan till licensgrupperna i listan.</span><span class="sxs-lookup"><span data-stu-id="54a13-116">To get a list of available licenses for the specified license groups, start by instantiating a [List](/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="54a13-117">Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="54a13-117">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="54a13-118">Hämta sedan värdet för egenskapen [**SubscribedSkus för att hämta**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) ett gränssnitt för SKU-samlingsåtgärder som kunden prenumererar på.</span><span class="sxs-lookup"><span data-stu-id="54a13-118">Then, get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span> <span data-ttu-id="54a13-119">Slutligen skickar du listan över licensgrupper till metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) för att hämta listan över prenumererade SKU:er med information om tillgängliga licensenheter.</span><span class="sxs-lookup"><span data-stu-id="54a13-119">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of subscribed SKUs with details on available license units.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get subscribed SKUs available for group1, the license group for Azure Active Directory (AAD).
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1};
var customerUserAadSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get subscribed SKUs available for group2, the license group for Minecraft product licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group2};
var customerUserSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get both AAD and Minecraft subscribed SKUs.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1, LicenseGroupId.Group2};
var customerUserBothAadAndSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="54a13-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="54a13-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="54a13-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="54a13-121">Request syntax</span></span>

| <span data-ttu-id="54a13-122">Metod</span><span class="sxs-lookup"><span data-stu-id="54a13-122">Method</span></span>  | <span data-ttu-id="54a13-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="54a13-123">Request URI</span></span>                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="54a13-124">**Få**</span><span class="sxs-lookup"><span data-stu-id="54a13-124">**GET**</span></span> | <span data-ttu-id="54a13-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="54a13-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="54a13-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="54a13-126">**GET**</span></span> | <span data-ttu-id="54a13-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="54a13-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="54a13-128">**Få**</span><span class="sxs-lookup"><span data-stu-id="54a13-128">**GET**</span></span> | <span data-ttu-id="54a13-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="54a13-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="54a13-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="54a13-130">URI parameter</span></span>

<span data-ttu-id="54a13-131">Använd följande sökväg och frågeparametrar för att identifiera kunden och licensgrupperna.</span><span class="sxs-lookup"><span data-stu-id="54a13-131">Use the following path and query parameters to identify the customer and the license groups.</span></span>

| <span data-ttu-id="54a13-132">Namn</span><span class="sxs-lookup"><span data-stu-id="54a13-132">Name</span></span>            | <span data-ttu-id="54a13-133">Typ</span><span class="sxs-lookup"><span data-stu-id="54a13-133">Type</span></span>   | <span data-ttu-id="54a13-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="54a13-134">Required</span></span> | <span data-ttu-id="54a13-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="54a13-135">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="54a13-136">kund-id</span><span class="sxs-lookup"><span data-stu-id="54a13-136">customer-id</span></span>     | <span data-ttu-id="54a13-137">sträng</span><span class="sxs-lookup"><span data-stu-id="54a13-137">string</span></span> | <span data-ttu-id="54a13-138">Ja</span><span class="sxs-lookup"><span data-stu-id="54a13-138">Yes</span></span>      | <span data-ttu-id="54a13-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="54a13-139">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="54a13-140">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="54a13-140">licenseGroupIds</span></span> | <span data-ttu-id="54a13-141">sträng</span><span class="sxs-lookup"><span data-stu-id="54a13-141">string</span></span> | <span data-ttu-id="54a13-142">No</span><span class="sxs-lookup"><span data-stu-id="54a13-142">No</span></span>       | <span data-ttu-id="54a13-143">Ett uppräkningsvärde som anger licensgruppen för de tilldelade licenserna.</span><span class="sxs-lookup"><span data-stu-id="54a13-143">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="54a13-144">Giltiga värden: Group1, Group2 Group1 – Den här gruppen har alla produkter vars licens kan hanteras i Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="54a13-144">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="54a13-145">Grupp2 – Den här gruppen har bara Minecraft produktlicenser.</span><span class="sxs-lookup"><span data-stu-id="54a13-145">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="54a13-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="54a13-146">Request headers</span></span>

<span data-ttu-id="54a13-147">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="54a13-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="54a13-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="54a13-148">Request body</span></span>

<span data-ttu-id="54a13-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="54a13-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="54a13-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="54a13-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="54a13-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="54a13-151">REST response</span></span>

<span data-ttu-id="54a13-152">Om det lyckas innehåller svarstexten en samling [SubscribedSku-resurser.](license-resources.md#subscribedsku)</span><span class="sxs-lookup"><span data-stu-id="54a13-152">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="54a13-153">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="54a13-153">Response success and error codes</span></span>

<span data-ttu-id="54a13-154">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="54a13-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="54a13-155">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="54a13-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="54a13-156">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="54a13-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="54a13-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="54a13-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: S6Pd5XQAx0Ss/zQi.0
MS-ServerId: 030011719
Date: Sat, 10 Jun 2017 00:19:44 GMT

{
    "totalCount": 04,
    "items": [{
            "availableUnits": 15,
            "activeUnits": 15,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 15,
            "warningUnits": 0,
            "productSku": {
                "id": "078d2b04-f1bd-4111-bbd4-b4b1b354cef4",
                "name": "Azure Active Directory Premium P1",
                "skuPartNumber": "AAD_PREMIUM",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 1,
            "activeUnits": 1,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "54b84594-9c77-4499-8d65-5e0d5f410e78",
                "name": "Dynamics AX Task",
                "skuPartNumber": "AX_TASK_USER",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 23,
            "activeUnits": 72,
            "consumedUnits": 49,
            "suspendedUnits": 0,
            "totalUnits": 72,
            "warningUnits": 0,
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "targetType": "User",
                "licenseGroupId": "group2"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 71,
            "activeUnits": 112,
            "consumedUnits": 41,
            "suspendedUnits": 0,
            "totalUnits": 112,
            "warningUnits": 0,
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-skus-found"></a><span data-ttu-id="54a13-158">Svarsexempel (inga matchande SKU:er hittades)</span><span class="sxs-lookup"><span data-stu-id="54a13-158">Response example (no matching SKUs found)</span></span>

<span data-ttu-id="54a13-159">Om det inte går att hitta några matchande prenumerations-SKU:er för de angivna licensgrupperna innehåller svaret en tom samling med ett totalCount-element vars värde är 0.</span><span class="sxs-lookup"><span data-stu-id="54a13-159">If no matching subscribed SKUs can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
