---
title: Hämta licenser tilldelade till en användare efter licensgrupp
description: Så här hämtar du en lista över användar tilldelade licenser för de angivna licensgrupperna.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 54acf6f315e3062d03903a98d0c6c1946065f95e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446011"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="16c61-103">Hämta licenser tilldelade till en användare efter licensgrupp</span><span class="sxs-lookup"><span data-stu-id="16c61-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="16c61-104">Så här hämtar du en lista över användar tilldelade licenser för de angivna licensgrupperna.</span><span class="sxs-lookup"><span data-stu-id="16c61-104">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16c61-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="16c61-105">Prerequisites</span></span>

- <span data-ttu-id="16c61-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="16c61-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="16c61-107">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="16c61-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="16c61-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16c61-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="16c61-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="16c61-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="16c61-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="16c61-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="16c61-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="16c61-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="16c61-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="16c61-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="16c61-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16c61-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="16c61-114">En användaridentifierare.</span><span class="sxs-lookup"><span data-stu-id="16c61-114">A user identifier.</span></span>

- <span data-ttu-id="16c61-115">En lista över en eller flera licensgruppsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="16c61-115">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="16c61-116">C\#</span><span class="sxs-lookup"><span data-stu-id="16c61-116">C\#</span></span>

<span data-ttu-id="16c61-117">Om du vill kontrollera vilka licenser som har tilldelats till en användare från angivna licensgrupper börjar du med att instansiera en [List/dotnet/api/system.collections.generic.list-1) av typen [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)och lägger sedan till licensgrupperna i listan.</span><span class="sxs-lookup"><span data-stu-id="16c61-117">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="16c61-118">Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="16c61-118">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="16c61-119">Anropa sedan metoden [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID:t för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="16c61-119">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="16c61-120">Hämta sedan ett gränssnitt för åtgärder för kundanvändarlicenser [**från**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) egenskapen Licenser.</span><span class="sxs-lookup"><span data-stu-id="16c61-120">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="16c61-121">Slutligen skickar du listan över licensgrupper till metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) för att hämta samlingen med licenser som tilldelats användaren.</span><span class="sxs-lookup"><span data-stu-id="16c61-121">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="16c61-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="16c61-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="16c61-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="16c61-123">Request syntax</span></span>

| <span data-ttu-id="16c61-124">Metod</span><span class="sxs-lookup"><span data-stu-id="16c61-124">Method</span></span>  | <span data-ttu-id="16c61-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="16c61-125">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="16c61-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="16c61-126">**GET**</span></span> | <span data-ttu-id="16c61-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="16c61-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="16c61-128">**Få**</span><span class="sxs-lookup"><span data-stu-id="16c61-128">**GET**</span></span> | <span data-ttu-id="16c61-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="16c61-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="16c61-130">**Få**</span><span class="sxs-lookup"><span data-stu-id="16c61-130">**GET**</span></span> | <span data-ttu-id="16c61-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="16c61-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="16c61-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="16c61-132">URI parameter</span></span>

<span data-ttu-id="16c61-133">Använd följande sökväg och frågeparametrar för att identifiera kund-, användar- och licensgrupper.</span><span class="sxs-lookup"><span data-stu-id="16c61-133">Use the following path and query parameters to identify the customer, user, and license groups.</span></span>

| <span data-ttu-id="16c61-134">Namn</span><span class="sxs-lookup"><span data-stu-id="16c61-134">Name</span></span>            | <span data-ttu-id="16c61-135">Typ</span><span class="sxs-lookup"><span data-stu-id="16c61-135">Type</span></span>   | <span data-ttu-id="16c61-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="16c61-136">Required</span></span> | <span data-ttu-id="16c61-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="16c61-137">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="16c61-138">kund-id</span><span class="sxs-lookup"><span data-stu-id="16c61-138">customer-id</span></span>     | <span data-ttu-id="16c61-139">sträng</span><span class="sxs-lookup"><span data-stu-id="16c61-139">string</span></span> | <span data-ttu-id="16c61-140">Ja</span><span class="sxs-lookup"><span data-stu-id="16c61-140">Yes</span></span>      | <span data-ttu-id="16c61-141">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="16c61-141">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="16c61-142">användar-id</span><span class="sxs-lookup"><span data-stu-id="16c61-142">user-id</span></span>         | <span data-ttu-id="16c61-143">sträng</span><span class="sxs-lookup"><span data-stu-id="16c61-143">string</span></span> | <span data-ttu-id="16c61-144">Ja</span><span class="sxs-lookup"><span data-stu-id="16c61-144">Yes</span></span>      | <span data-ttu-id="16c61-145">En GUID-formaterad sträng som identifierar användaren.</span><span class="sxs-lookup"><span data-stu-id="16c61-145">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="16c61-146">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="16c61-146">licenseGroupIds</span></span> | <span data-ttu-id="16c61-147">sträng</span><span class="sxs-lookup"><span data-stu-id="16c61-147">string</span></span> | <span data-ttu-id="16c61-148">No</span><span class="sxs-lookup"><span data-stu-id="16c61-148">No</span></span>       | <span data-ttu-id="16c61-149">Ett uppräkningsvärde som anger licensgruppen för de tilldelade licenserna.</span><span class="sxs-lookup"><span data-stu-id="16c61-149">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="16c61-150">Giltiga värden: Group1, Group2 Group1 – Den här gruppen har alla produkter vars licens kan hanteras i Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="16c61-150">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="16c61-151">Grupp2 – Den här gruppen har bara Minecraft produktlicenser.</span><span class="sxs-lookup"><span data-stu-id="16c61-151">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="16c61-152">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="16c61-152">Request headers</span></span>

<span data-ttu-id="16c61-153">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="16c61-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="16c61-154">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="16c61-154">Request body</span></span>

<span data-ttu-id="16c61-155">Inga.</span><span class="sxs-lookup"><span data-stu-id="16c61-155">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="16c61-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="16c61-156">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="16c61-157">REST-svar</span><span class="sxs-lookup"><span data-stu-id="16c61-157">REST response</span></span>

<span data-ttu-id="16c61-158">Om det lyckas innehåller svarstexten samlingen [licensresurser.](license-resources.md#license)</span><span class="sxs-lookup"><span data-stu-id="16c61-158">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="16c61-159">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="16c61-159">Response success and error codes</span></span>

<span data-ttu-id="16c61-160">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="16c61-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="16c61-161">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="16c61-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="16c61-162">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="16c61-162">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="16c61-163">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="16c61-163">Response example</span></span>

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

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="16c61-164">Svarsexempel (inga matchande licenser hittades)</span><span class="sxs-lookup"><span data-stu-id="16c61-164">Response example (no matching licenses found)</span></span>

<span data-ttu-id="16c61-165">Om inga matchande licenser hittas för de angivna licensgrupperna innehåller svaret en tom samling med ett totalCount-element vars värde är 0.</span><span class="sxs-lookup"><span data-stu-id="16c61-165">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
