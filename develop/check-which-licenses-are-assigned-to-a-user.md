---
title: Hämta licenser tilldelade till en användare
description: 'Lär dig hur du använder API: er för partner Center för att hämta en lista över licenser som har tilldelats en användare i ett kund konto.'
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b754ba4ecba7067f78c6868b387bac0190bfd230
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770095"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="6994f-103">Hämta licenser tilldelade till en användare inom ett kund konto</span><span class="sxs-lookup"><span data-stu-id="6994f-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="6994f-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="6994f-104">**Applies to:**</span></span>

- <span data-ttu-id="6994f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="6994f-105">Partner Center</span></span>

<span data-ttu-id="6994f-106">Så här hämtar du en lista över licenser som är tilldelade till en användare inom ett kund konto.</span><span class="sxs-lookup"><span data-stu-id="6994f-106">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="6994f-107">Exemplen som visas här returnerar licenser som tilldelats från Grupp1, standard licens gruppen som representerar licenser som hanteras av Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6994f-107">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="6994f-108">Om du vill hämta licenser som har tilldelats från angivna licens grupper läser du [Hämta licenser tilldelade till en användare efter licens grupp](get-licenses-assigned-to-a-user-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="6994f-108">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6994f-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6994f-109">Prerequisites</span></span>

- <span data-ttu-id="6994f-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6994f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6994f-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6994f-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6994f-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6994f-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6994f-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="6994f-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6994f-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="6994f-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6994f-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="6994f-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6994f-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="6994f-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6994f-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6994f-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6994f-118">Ett användar-ID.</span><span class="sxs-lookup"><span data-stu-id="6994f-118">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="6994f-119">C\#</span><span class="sxs-lookup"><span data-stu-id="6994f-119">C\#</span></span>

<span data-ttu-id="6994f-120">Om du vill kontrol lera vilka licenser som har tilldelats till en användare från standard licens gruppen för Grupp1 använder du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="6994f-120">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="6994f-121">Anropa sedan metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="6994f-121">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="6994f-122">Hämta sedan ett gränssnitt till kund användar licens åtgärder från egenskapen [**licenser**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) .</span><span class="sxs-lookup"><span data-stu-id="6994f-122">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="6994f-123">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) för att hämta samlingen med licenser tilldelade till användaren.</span><span class="sxs-lookup"><span data-stu-id="6994f-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="6994f-124">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6994f-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6994f-125">**Projekt**: Partner Center SDK-exempel **klass**: CustomerUserAssignedLicenses.CS</span><span class="sxs-lookup"><span data-stu-id="6994f-125">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6994f-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6994f-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6994f-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="6994f-127">Request syntax</span></span>

| <span data-ttu-id="6994f-128">Metod</span><span class="sxs-lookup"><span data-stu-id="6994f-128">Method</span></span>  | <span data-ttu-id="6994f-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6994f-129">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6994f-130">**TA**</span><span class="sxs-lookup"><span data-stu-id="6994f-130">**GET**</span></span> | <span data-ttu-id="6994f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses http/1.1</span><span class="sxs-lookup"><span data-stu-id="6994f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6994f-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="6994f-132">URI parameter</span></span>

<span data-ttu-id="6994f-133">Använd följande Sök vägs parametrar för att identifiera kunden och användaren.</span><span class="sxs-lookup"><span data-stu-id="6994f-133">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="6994f-134">Namn</span><span class="sxs-lookup"><span data-stu-id="6994f-134">Name</span></span>        | <span data-ttu-id="6994f-135">Typ</span><span class="sxs-lookup"><span data-stu-id="6994f-135">Type</span></span>   | <span data-ttu-id="6994f-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6994f-136">Required</span></span> | <span data-ttu-id="6994f-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6994f-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="6994f-138">kund-ID</span><span class="sxs-lookup"><span data-stu-id="6994f-138">customer-id</span></span> | <span data-ttu-id="6994f-139">sträng</span><span class="sxs-lookup"><span data-stu-id="6994f-139">string</span></span> | <span data-ttu-id="6994f-140">Yes</span><span class="sxs-lookup"><span data-stu-id="6994f-140">Yes</span></span>      | <span data-ttu-id="6994f-141">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="6994f-141">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="6994f-142">användar-id</span><span class="sxs-lookup"><span data-stu-id="6994f-142">user-id</span></span>     | <span data-ttu-id="6994f-143">sträng</span><span class="sxs-lookup"><span data-stu-id="6994f-143">string</span></span> | <span data-ttu-id="6994f-144">Yes</span><span class="sxs-lookup"><span data-stu-id="6994f-144">Yes</span></span>      | <span data-ttu-id="6994f-145">En GUID-formaterad sträng som identifierar användaren.</span><span class="sxs-lookup"><span data-stu-id="6994f-145">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="6994f-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6994f-146">Request headers</span></span>

<span data-ttu-id="6994f-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6994f-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6994f-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6994f-148">Request body</span></span>

<span data-ttu-id="6994f-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="6994f-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6994f-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6994f-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6994f-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6994f-151">REST response</span></span>

<span data-ttu-id="6994f-152">Om det lyckas innehåller svars texten samlingen av [licens](license-resources.md#license) resurser.</span><span class="sxs-lookup"><span data-stu-id="6994f-152">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6994f-153">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6994f-153">Response success and error codes</span></span>

<span data-ttu-id="6994f-154">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="6994f-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6994f-155">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6994f-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6994f-156">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6994f-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6994f-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6994f-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3883
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CV: WYkHYMfWTUajFosK.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 00:29:24 GMT

{
    "totalCount": 1,
    "items": [{
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
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