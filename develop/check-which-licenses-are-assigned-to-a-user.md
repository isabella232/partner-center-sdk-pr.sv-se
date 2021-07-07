---
title: Hämta licenser tilldelade till en användare
description: Lär dig hur du använder Partner Center-API:er för att hämta en lista över licenser som tilldelats till en användare i ett kundkonto.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a51fc4493e2476107206b03be66004d030e2aa47
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974071"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="c36e1-103">Hämta licenser som tilldelats en användare inom ett kundkonto</span><span class="sxs-lookup"><span data-stu-id="c36e1-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="c36e1-104">Så här hämtar du en lista över licenser som tilldelats en användare i ett kundkonto.</span><span class="sxs-lookup"><span data-stu-id="c36e1-104">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="c36e1-105">Exemplen som visas här returnerar licenser som tilldelats från group1, standardlicensgruppen som representerar licenser som hanteras av Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c36e1-105">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="c36e1-106">Information om hur du hämtar licenser som tilldelats från angivna licensgrupper finns i [Hämta licenser som tilldelats till en användare efter licensgrupp.](get-licenses-assigned-to-a-user-by-license-group.md)</span><span class="sxs-lookup"><span data-stu-id="c36e1-106">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c36e1-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c36e1-107">Prerequisites</span></span>

- <span data-ttu-id="c36e1-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c36e1-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c36e1-109">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="c36e1-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c36e1-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c36e1-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c36e1-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="c36e1-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c36e1-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="c36e1-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c36e1-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="c36e1-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c36e1-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="c36e1-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c36e1-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c36e1-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c36e1-116">En användaridentifierare.</span><span class="sxs-lookup"><span data-stu-id="c36e1-116">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="c36e1-117">C\#</span><span class="sxs-lookup"><span data-stu-id="c36e1-117">C\#</span></span>

<span data-ttu-id="c36e1-118">Om du vill kontrollera vilka licenser som har tilldelats till en användare från standardlicensgruppen group1 använder du först [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="c36e1-118">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="c36e1-119">Anropa sedan metoden [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID:t för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="c36e1-119">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="c36e1-120">Hämta sedan ett gränssnitt för åtgärder för kundanvändarlicenser från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) Licenser.</span><span class="sxs-lookup"><span data-stu-id="c36e1-120">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="c36e1-121">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) eller [**GetAsync för**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) att hämta samlingen med licenser som tilldelats användaren.</span><span class="sxs-lookup"><span data-stu-id="c36e1-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="c36e1-122">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c36e1-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c36e1-123">**Project:** Partnercenter-SDK **Exempelklass:** CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="c36e1-123">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c36e1-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c36e1-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c36e1-125">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="c36e1-125">Request syntax</span></span>

| <span data-ttu-id="c36e1-126">Metod</span><span class="sxs-lookup"><span data-stu-id="c36e1-126">Method</span></span>  | <span data-ttu-id="c36e1-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c36e1-127">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c36e1-128">**Få**</span><span class="sxs-lookup"><span data-stu-id="c36e1-128">**GET**</span></span> | <span data-ttu-id="c36e1-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c36e1-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c36e1-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="c36e1-130">URI parameter</span></span>

<span data-ttu-id="c36e1-131">Använd följande sökvägsparametrar för att identifiera kunden och användaren.</span><span class="sxs-lookup"><span data-stu-id="c36e1-131">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="c36e1-132">Namn</span><span class="sxs-lookup"><span data-stu-id="c36e1-132">Name</span></span>        | <span data-ttu-id="c36e1-133">Typ</span><span class="sxs-lookup"><span data-stu-id="c36e1-133">Type</span></span>   | <span data-ttu-id="c36e1-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c36e1-134">Required</span></span> | <span data-ttu-id="c36e1-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c36e1-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="c36e1-136">kund-id</span><span class="sxs-lookup"><span data-stu-id="c36e1-136">customer-id</span></span> | <span data-ttu-id="c36e1-137">sträng</span><span class="sxs-lookup"><span data-stu-id="c36e1-137">string</span></span> | <span data-ttu-id="c36e1-138">Ja</span><span class="sxs-lookup"><span data-stu-id="c36e1-138">Yes</span></span>      | <span data-ttu-id="c36e1-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="c36e1-139">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="c36e1-140">användar-id</span><span class="sxs-lookup"><span data-stu-id="c36e1-140">user-id</span></span>     | <span data-ttu-id="c36e1-141">sträng</span><span class="sxs-lookup"><span data-stu-id="c36e1-141">string</span></span> | <span data-ttu-id="c36e1-142">Ja</span><span class="sxs-lookup"><span data-stu-id="c36e1-142">Yes</span></span>      | <span data-ttu-id="c36e1-143">En GUID-formaterad sträng som identifierar användaren.</span><span class="sxs-lookup"><span data-stu-id="c36e1-143">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="c36e1-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c36e1-144">Request headers</span></span>

<span data-ttu-id="c36e1-145">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c36e1-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c36e1-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="c36e1-146">Request body</span></span>

<span data-ttu-id="c36e1-147">Inga.</span><span class="sxs-lookup"><span data-stu-id="c36e1-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c36e1-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="c36e1-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="c36e1-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c36e1-149">REST response</span></span>

<span data-ttu-id="c36e1-150">Om det lyckas innehåller svarstexten samlingen [licensresurser.](license-resources.md#license)</span><span class="sxs-lookup"><span data-stu-id="c36e1-150">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c36e1-151">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c36e1-151">Response success and error codes</span></span>

<span data-ttu-id="c36e1-152">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="c36e1-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c36e1-153">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c36e1-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c36e1-154">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c36e1-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c36e1-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="c36e1-155">Response example</span></span>

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