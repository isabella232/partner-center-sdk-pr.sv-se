---
title: Hämta en lista över tillgängliga licenser
description: Så här hämtar du en lista över licenser som är tillgängliga för användare av den angivna kunden.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f675e5b96b2f2040d662c0dc7f1e06625f267689
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769546"
---
# <a name="get-a-list-of-available-licenses"></a><span data-ttu-id="65616-103">Hämta en lista över tillgängliga licenser</span><span class="sxs-lookup"><span data-stu-id="65616-103">Get a list of available licenses</span></span>

<span data-ttu-id="65616-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="65616-104">**Applies to:**</span></span>

- <span data-ttu-id="65616-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="65616-105">Partner Center</span></span>

<span data-ttu-id="65616-106">Den här artikeln beskriver hur du hämtar en lista över licenser som är tillgängliga för användare av den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="65616-106">This article describes how to get a list of licenses available to users of the specified customer.</span></span>

<span data-ttu-id="65616-107">Följande exempel returnerar licenser som är tillgängliga från **Grupp1**, standard licens gruppen som representerar licenser som hanteras av Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65616-107">The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="65616-108">Information om hur du hämtar tillgängliga licenser för en angiven licens grupp finns i [Hämta en lista över tillgängliga licenser per licens grupp](get-a-list-of-available-licenses-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="65616-108">To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65616-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="65616-109">Prerequisites</span></span>

- <span data-ttu-id="65616-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="65616-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="65616-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="65616-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="65616-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="65616-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="65616-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="65616-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="65616-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="65616-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="65616-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="65616-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="65616-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="65616-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="65616-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="65616-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="65616-118">C\#</span><span class="sxs-lookup"><span data-stu-id="65616-118">C\#</span></span>

<span data-ttu-id="65616-119">Hämta listan över licenser som är tillgängliga från standard licens gruppen till användare av en kund:</span><span class="sxs-lookup"><span data-stu-id="65616-119">To retrieve the list of licenses available from the default license group to users of a customer:</span></span>

1. <span data-ttu-id="65616-120">Använd metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="65616-120">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="65616-121">Hämta värdet för egenskapen [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) för att hämta ett gränssnitt till kunden som prenumererar på SKU-samlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="65616-121">Get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span>

3. <span data-ttu-id="65616-122">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) för att hämta listan över licenser.</span><span class="sxs-lookup"><span data-stu-id="65616-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

<span data-ttu-id="65616-123">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="65616-123">For an example, see the following:</span></span>

- <span data-ttu-id="65616-124">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="65616-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="65616-125">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="65616-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="65616-126">Klass: **GetCustomerSubscribedSkus.cs**</span><span class="sxs-lookup"><span data-stu-id="65616-126">Class: **GetCustomerSubscribedSkus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="65616-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="65616-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="65616-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="65616-128">Request syntax</span></span>

| <span data-ttu-id="65616-129">Metod</span><span class="sxs-lookup"><span data-stu-id="65616-129">Method</span></span>  | <span data-ttu-id="65616-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="65616-130">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="65616-131">**TA**</span><span class="sxs-lookup"><span data-stu-id="65616-131">**GET**</span></span> | <span data-ttu-id="65616-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscribedskus http/1.1</span><span class="sxs-lookup"><span data-stu-id="65616-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="65616-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="65616-133">URI parameter</span></span>

<span data-ttu-id="65616-134">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="65616-134">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="65616-135">Namn</span><span class="sxs-lookup"><span data-stu-id="65616-135">Name</span></span>        | <span data-ttu-id="65616-136">Typ</span><span class="sxs-lookup"><span data-stu-id="65616-136">Type</span></span>   | <span data-ttu-id="65616-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="65616-137">Required</span></span> | <span data-ttu-id="65616-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="65616-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="65616-139">kund-ID</span><span class="sxs-lookup"><span data-stu-id="65616-139">customer-id</span></span> | <span data-ttu-id="65616-140">sträng</span><span class="sxs-lookup"><span data-stu-id="65616-140">string</span></span> | <span data-ttu-id="65616-141">Yes</span><span class="sxs-lookup"><span data-stu-id="65616-141">Yes</span></span>      | <span data-ttu-id="65616-142">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="65616-142">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="65616-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="65616-143">Request headers</span></span>

<span data-ttu-id="65616-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="65616-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="65616-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="65616-145">Request body</span></span>

<span data-ttu-id="65616-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="65616-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="65616-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="65616-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="65616-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="65616-148">REST response</span></span>

<span data-ttu-id="65616-149">Om det lyckas innehåller svars texten en samling [SubscribedSku](license-resources.md#subscribedsku) -resurser.</span><span class="sxs-lookup"><span data-stu-id="65616-149">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="65616-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="65616-150">Response success and error codes</span></span>

<span data-ttu-id="65616-151">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="65616-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="65616-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="65616-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="65616-153">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="65616-153">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="65616-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="65616-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CV: 7BQ0jitzXUCLwRM6.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 17:50:46 GMT

 {
    "totalCount": 2,
    "items": [{
            "availableUnits": 4,
            "activeUnits": 5,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 5,
            "warningUnits": 0,
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
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
        },  {
            "availableUnits": 0,
            "activeUnits": 1,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "f8a1db68-be16-40ed-86d5-cb42ce701560",
                "name": "Power BI Pro",
                "skuPartNumber": "POWER_BI_PRO",
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
                    "displayName": "Power BI Pro",
                    "serviceName": "BI_AZURE_P2",
                    "id": "70d33638-9c74-4d01-bfd3-562de28bd4ba",
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
