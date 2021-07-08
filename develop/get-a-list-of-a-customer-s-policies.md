---
title: Hämta en lista över en kunds principer
description: Så här hämtar du en samling av den angivna kundens konfigurationsprinciper.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bf6ace0d2425e28d80c4f2310878c2d2a9e2a876
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874592"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="d308b-103">Hämta en lista över en kunds principer</span><span class="sxs-lookup"><span data-stu-id="d308b-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="d308b-104">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="d308b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="d308b-105">Den här artikeln beskriver hur du hämtar en samling av den angivna kundens konfigurationsprinciper.</span><span class="sxs-lookup"><span data-stu-id="d308b-105">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d308b-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d308b-106">Prerequisites</span></span>

- <span data-ttu-id="d308b-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d308b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d308b-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d308b-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d308b-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d308b-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d308b-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d308b-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d308b-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="d308b-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d308b-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="d308b-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d308b-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="d308b-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d308b-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d308b-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d308b-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d308b-115">C\#</span></span>

<span data-ttu-id="d308b-116">Så här hämtar du en lista över alla en kunds principer:</span><span class="sxs-lookup"><span data-stu-id="d308b-116">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="d308b-117">Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="d308b-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="d308b-118">Hämta egenskapen [**ConfigurationPolicies för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) att hämta ett gränssnitt för konfigurationsprincipinsamlingsåtgärder.</span><span class="sxs-lookup"><span data-stu-id="d308b-118">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="d308b-119">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) för att hämta samlingen med principer.</span><span class="sxs-lookup"><span data-stu-id="d308b-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="d308b-120">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="d308b-120">For an example, see the following:</span></span>

- <span data-ttu-id="d308b-121">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d308b-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d308b-122">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="d308b-122">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="d308b-123">Klass: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="d308b-123">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d308b-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d308b-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d308b-125">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="d308b-125">Request syntax</span></span>

| <span data-ttu-id="d308b-126">Metod</span><span class="sxs-lookup"><span data-stu-id="d308b-126">Method</span></span>  | <span data-ttu-id="d308b-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d308b-127">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="d308b-128">**Få**</span><span class="sxs-lookup"><span data-stu-id="d308b-128">**GET**</span></span> | <span data-ttu-id="d308b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d308b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d308b-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d308b-130">URI parameter</span></span>

<span data-ttu-id="d308b-131">Använd följande sökvägsparameter när du skapar begäran:</span><span class="sxs-lookup"><span data-stu-id="d308b-131">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="d308b-132">Namn</span><span class="sxs-lookup"><span data-stu-id="d308b-132">Name</span></span>        | <span data-ttu-id="d308b-133">Typ</span><span class="sxs-lookup"><span data-stu-id="d308b-133">Type</span></span>   | <span data-ttu-id="d308b-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d308b-134">Required</span></span> | <span data-ttu-id="d308b-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d308b-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="d308b-136">kund-id</span><span class="sxs-lookup"><span data-stu-id="d308b-136">customer-id</span></span> | <span data-ttu-id="d308b-137">sträng</span><span class="sxs-lookup"><span data-stu-id="d308b-137">string</span></span> | <span data-ttu-id="d308b-138">Ja</span><span class="sxs-lookup"><span data-stu-id="d308b-138">Yes</span></span>      | <span data-ttu-id="d308b-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="d308b-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d308b-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d308b-140">Request headers</span></span>

<span data-ttu-id="d308b-141">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d308b-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d308b-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d308b-142">Request body</span></span>

<span data-ttu-id="d308b-143">Ingen</span><span class="sxs-lookup"><span data-stu-id="d308b-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="d308b-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d308b-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
Content-Length:0
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d308b-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d308b-145">REST response</span></span>

<span data-ttu-id="d308b-146">Om det lyckas innehåller svarstexten en samling [ConfigurationPolicy-resurser.](device-deployment-resources.md#configurationpolicy)</span><span class="sxs-lookup"><span data-stu-id="d308b-146">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d308b-147">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d308b-147">Response success and error codes</span></span>

<span data-ttu-id="d308b-148">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="d308b-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d308b-149">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d308b-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d308b-150">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d308b-150">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d308b-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d308b-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1221
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d5ff2573-3ef8-4553-aac4-4b73d97dce1b
MS-RequestId: 6eb7383d-eeb5-44d7-8570-e0ed12c0547a
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:49 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "8c7d25aa-2dbb-409c-a1f0-f55bd9108fa9",
            "name": "Windows 10 Enterprise E3",
            "category": "o_o_b_e",
            "description": "P462017 description",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-04-27T11:30:34.1944704-07:00",
            "lastModifiedDate": "2017-04-27T11:30:34.1944704-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
            "name": "Test policy",
            "category": "o_o_b_e",
            "description": "Test policy creation from API 1",
            "devicesAssigned": 0,
            "policySettings": ["skip_express_settings"],
            "createdDate": "2017-07-25T11:03:03.8457088-07:00",
            "lastModifiedDate": "2017-07-25T11:04:00.8150016-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "a96b5fd9-0f3a-419a-b55c-a8aecd6b1f00",
            "name": "Windows 10 Enterprise E5",
            "category": "o_o_b_e",
            "description": "test policy creation from API",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-07-25T11:07:36.1501184-07:00",
            "lastModifiedDate": "2017-07-25T11:07:36.1501184-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
