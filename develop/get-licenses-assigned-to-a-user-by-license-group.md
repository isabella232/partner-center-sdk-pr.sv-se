---
title: Hämta licenser tilldelade till en användare efter licensgrupp
description: Hämta en lista över tilldelade licenser för de angivna licens grupperna.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 28c10e3e2acb30e4110213344959a87d4ddfcffb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769669"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="05742-103">Hämta licenser tilldelade till en användare efter licensgrupp</span><span class="sxs-lookup"><span data-stu-id="05742-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="05742-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="05742-104">**Applies To**</span></span>

- <span data-ttu-id="05742-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="05742-105">Partner Center</span></span>

<span data-ttu-id="05742-106">Hämta en lista över tilldelade licenser för de angivna licens grupperna.</span><span class="sxs-lookup"><span data-stu-id="05742-106">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05742-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="05742-107">Prerequisites</span></span>

- <span data-ttu-id="05742-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="05742-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="05742-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="05742-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="05742-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="05742-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="05742-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="05742-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="05742-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="05742-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="05742-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="05742-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="05742-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="05742-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="05742-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="05742-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="05742-116">Ett användar-ID.</span><span class="sxs-lookup"><span data-stu-id="05742-116">A user identifier.</span></span>

- <span data-ttu-id="05742-117">En lista med en eller flera licens grupps identifierare.</span><span class="sxs-lookup"><span data-stu-id="05742-117">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="05742-118">C\#</span><span class="sxs-lookup"><span data-stu-id="05742-118">C\#</span></span>

<span data-ttu-id="05742-119">Om du vill kontrol lera vilka licenser som har tilldelats en användare från angivna licens grupper börjar du genom att instansiera en [List/dotNet/API/system. Collections. Generic. list -1) av typen [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)och lägger sedan till licens grupperna i listan.</span><span class="sxs-lookup"><span data-stu-id="05742-119">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="05742-120">Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="05742-120">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="05742-121">Anropa sedan metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="05742-121">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="05742-122">Hämta sedan ett gränssnitt till kund användar licens åtgärder från egenskapen [**licenser**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) .</span><span class="sxs-lookup"><span data-stu-id="05742-122">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="05742-123">Slutligen skickar du listan över licens grupper till [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) -metoden för att hämta den samling av licenser som tilldelats användaren.</span><span class="sxs-lookup"><span data-stu-id="05742-123">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="05742-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="05742-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="05742-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="05742-125">Request syntax</span></span>

| <span data-ttu-id="05742-126">Metod</span><span class="sxs-lookup"><span data-stu-id="05742-126">Method</span></span>  | <span data-ttu-id="05742-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="05742-127">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="05742-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="05742-128">**GET**</span></span> | <span data-ttu-id="05742-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Grupp1 http/1.1</span><span class="sxs-lookup"><span data-stu-id="05742-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="05742-130">**TA**</span><span class="sxs-lookup"><span data-stu-id="05742-130">**GET**</span></span> | <span data-ttu-id="05742-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = group2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="05742-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="05742-132">**TA**</span><span class="sxs-lookup"><span data-stu-id="05742-132">**GET**</span></span> | <span data-ttu-id="05742-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Grupp1&LicenseGroupIds = group2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="05742-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="05742-134">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="05742-134">URI parameter</span></span>

<span data-ttu-id="05742-135">Använd följande sökväg och frågeparametrar för att identifiera kund-, användar-och licens grupper.</span><span class="sxs-lookup"><span data-stu-id="05742-135">Use the following path and query parameters to identify the customer, user and license groups.</span></span>

| <span data-ttu-id="05742-136">Namn</span><span class="sxs-lookup"><span data-stu-id="05742-136">Name</span></span>            | <span data-ttu-id="05742-137">Typ</span><span class="sxs-lookup"><span data-stu-id="05742-137">Type</span></span>   | <span data-ttu-id="05742-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="05742-138">Required</span></span> | <span data-ttu-id="05742-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="05742-139">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="05742-140">kund-ID</span><span class="sxs-lookup"><span data-stu-id="05742-140">customer-id</span></span>     | <span data-ttu-id="05742-141">sträng</span><span class="sxs-lookup"><span data-stu-id="05742-141">string</span></span> | <span data-ttu-id="05742-142">Yes</span><span class="sxs-lookup"><span data-stu-id="05742-142">Yes</span></span>      | <span data-ttu-id="05742-143">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="05742-143">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="05742-144">användar-id</span><span class="sxs-lookup"><span data-stu-id="05742-144">user-id</span></span>         | <span data-ttu-id="05742-145">sträng</span><span class="sxs-lookup"><span data-stu-id="05742-145">string</span></span> | <span data-ttu-id="05742-146">Yes</span><span class="sxs-lookup"><span data-stu-id="05742-146">Yes</span></span>      | <span data-ttu-id="05742-147">En GUID-formaterad sträng som identifierar användaren.</span><span class="sxs-lookup"><span data-stu-id="05742-147">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="05742-148">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="05742-148">licenseGroupIds</span></span> | <span data-ttu-id="05742-149">sträng</span><span class="sxs-lookup"><span data-stu-id="05742-149">string</span></span> | <span data-ttu-id="05742-150">No</span><span class="sxs-lookup"><span data-stu-id="05742-150">No</span></span>       | <span data-ttu-id="05742-151">Ett Enum-värde som anger licens gruppen för de tilldelade licenserna.</span><span class="sxs-lookup"><span data-stu-id="05742-151">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="05742-152">Giltiga värden: Grupp1, group2 Grupp1 – den här gruppen har alla produkter vars licens kan hanteras i Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="05742-152">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="05742-153">Group2 – den här gruppen har bara Minecraft produkt licenser.</span><span class="sxs-lookup"><span data-stu-id="05742-153">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="05742-154">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="05742-154">Request headers</span></span>

<span data-ttu-id="05742-155">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="05742-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="05742-156">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="05742-156">Request body</span></span>

<span data-ttu-id="05742-157">Inga.</span><span class="sxs-lookup"><span data-stu-id="05742-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="05742-158">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="05742-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="05742-159">REST-svar</span><span class="sxs-lookup"><span data-stu-id="05742-159">REST response</span></span>

<span data-ttu-id="05742-160">Om det lyckas innehåller svars texten samlingen av [licens](license-resources.md#license) resurser.</span><span class="sxs-lookup"><span data-stu-id="05742-160">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="05742-161">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="05742-161">Response success and error codes</span></span>

<span data-ttu-id="05742-162">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="05742-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="05742-163">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="05742-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="05742-164">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="05742-164">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="05742-165">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="05742-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="05742-166">Svars exempel (inga matchande licenser hittades)</span><span class="sxs-lookup"><span data-stu-id="05742-166">Response example (no matching licenses found)</span></span>

<span data-ttu-id="05742-167">Om det inte går att hitta matchande licenser för de angivna licens grupperna innehåller svaret en tom samling med ett totalCount-element vars värde är 0.</span><span class="sxs-lookup"><span data-stu-id="05742-167">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
