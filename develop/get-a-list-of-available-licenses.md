---
title: Hämta en lista över tillgängliga licenser
description: Så här hämtar du en lista över licenser som är tillgängliga för användare av den angivna kunden.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 02a6fccc2cf7f3f4dc929b96ec0f17e0f4a31b06
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874507"
---
# <a name="get-a-list-of-available-licenses"></a><span data-ttu-id="6bcef-103">Hämta en lista över tillgängliga licenser</span><span class="sxs-lookup"><span data-stu-id="6bcef-103">Get a list of available licenses</span></span>

<span data-ttu-id="6bcef-104">Den här artikeln beskriver hur du hämtar en lista över licenser som är tillgängliga för användare av den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="6bcef-104">This article describes how to get a list of licenses available to users of the specified customer.</span></span>

<span data-ttu-id="6bcef-105">I följande exempel returneras licenser som är **tillgängliga från group1**, standardlicensgruppen som representerar licenser som hanteras av Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6bcef-105">The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6bcef-106">Information om hur du hämtar tillgängliga licenser för en angiven [licensgrupp finns i Hämta en lista över tillgängliga licenser efter licensgrupp.](get-a-list-of-available-licenses-by-license-group.md)</span><span class="sxs-lookup"><span data-stu-id="6bcef-106">To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bcef-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6bcef-107">Prerequisites</span></span>

- <span data-ttu-id="6bcef-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6bcef-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6bcef-109">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6bcef-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6bcef-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6bcef-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6bcef-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6bcef-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6bcef-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="6bcef-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6bcef-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="6bcef-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6bcef-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="6bcef-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6bcef-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6bcef-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6bcef-116">C\#</span><span class="sxs-lookup"><span data-stu-id="6bcef-116">C\#</span></span>

<span data-ttu-id="6bcef-117">Så här hämtar du listan över licenser som är tillgängliga från standardlicensgruppen för användare av en kund:</span><span class="sxs-lookup"><span data-stu-id="6bcef-117">To retrieve the list of licenses available from the default license group to users of a customer:</span></span>

1. <span data-ttu-id="6bcef-118">Använd metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="6bcef-118">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="6bcef-119">Hämta värdet för egenskapen [**SubscribedSkus för att**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) hämta ett gränssnitt till SKU-insamlingsåtgärder som kunden prenumererar på.</span><span class="sxs-lookup"><span data-stu-id="6bcef-119">Get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span>

3. <span data-ttu-id="6bcef-120">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) för att hämta listan över licenser.</span><span class="sxs-lookup"><span data-stu-id="6bcef-120">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

<span data-ttu-id="6bcef-121">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="6bcef-121">For an example, see the following:</span></span>

- <span data-ttu-id="6bcef-122">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6bcef-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6bcef-123">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="6bcef-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="6bcef-124">Klass: **GetCustomerSubscribedSkus.cs**</span><span class="sxs-lookup"><span data-stu-id="6bcef-124">Class: **GetCustomerSubscribedSkus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6bcef-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6bcef-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6bcef-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="6bcef-126">Request syntax</span></span>

| <span data-ttu-id="6bcef-127">Metod</span><span class="sxs-lookup"><span data-stu-id="6bcef-127">Method</span></span>  | <span data-ttu-id="6bcef-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6bcef-128">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6bcef-129">**Få**</span><span class="sxs-lookup"><span data-stu-id="6bcef-129">**GET**</span></span> | <span data-ttu-id="6bcef-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6bcef-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="6bcef-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="6bcef-131">URI parameter</span></span>

<span data-ttu-id="6bcef-132">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="6bcef-132">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="6bcef-133">Namn</span><span class="sxs-lookup"><span data-stu-id="6bcef-133">Name</span></span>        | <span data-ttu-id="6bcef-134">Typ</span><span class="sxs-lookup"><span data-stu-id="6bcef-134">Type</span></span>   | <span data-ttu-id="6bcef-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6bcef-135">Required</span></span> | <span data-ttu-id="6bcef-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6bcef-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="6bcef-137">kund-ID</span><span class="sxs-lookup"><span data-stu-id="6bcef-137">customer-id</span></span> | <span data-ttu-id="6bcef-138">sträng</span><span class="sxs-lookup"><span data-stu-id="6bcef-138">string</span></span> | <span data-ttu-id="6bcef-139">Ja</span><span class="sxs-lookup"><span data-stu-id="6bcef-139">Yes</span></span>      | <span data-ttu-id="6bcef-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="6bcef-140">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6bcef-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6bcef-141">Request headers</span></span>

<span data-ttu-id="6bcef-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6bcef-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6bcef-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6bcef-143">Request body</span></span>

<span data-ttu-id="6bcef-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="6bcef-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6bcef-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6bcef-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6bcef-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6bcef-146">REST response</span></span>

<span data-ttu-id="6bcef-147">Om det lyckas innehåller svarstexten en samling [SubscribedSku-resurser.](license-resources.md#subscribedsku)</span><span class="sxs-lookup"><span data-stu-id="6bcef-147">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6bcef-148">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6bcef-148">Response success and error codes</span></span>

<span data-ttu-id="6bcef-149">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="6bcef-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6bcef-150">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6bcef-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6bcef-151">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6bcef-151">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6bcef-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6bcef-152">Response example</span></span>

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
