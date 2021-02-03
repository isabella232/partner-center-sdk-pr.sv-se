---
title: Hämta en lista över en kunds principer
description: Hämta en samling av den angivna kundens konfigurations principer.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 16886b1adca393ed2967f2a4fe74a379bef1c1c7
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769339"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="e8511-103">Hämta en lista över en kunds principer</span><span class="sxs-lookup"><span data-stu-id="e8511-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="e8511-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="e8511-104">**Applies to:**</span></span>

- <span data-ttu-id="e8511-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e8511-105">Partner Center</span></span>
- <span data-ttu-id="e8511-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="e8511-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e8511-107">Den här artikeln beskriver hur du hämtar en samling av den angivna kundens konfigurations principer.</span><span class="sxs-lookup"><span data-stu-id="e8511-107">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8511-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e8511-108">Prerequisites</span></span>

- <span data-ttu-id="e8511-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e8511-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e8511-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e8511-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e8511-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e8511-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e8511-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="e8511-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e8511-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="e8511-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e8511-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="e8511-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e8511-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="e8511-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e8511-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e8511-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e8511-117">C\#</span><span class="sxs-lookup"><span data-stu-id="e8511-117">C\#</span></span>

<span data-ttu-id="e8511-118">Så här hämtar du en lista över alla kund principer:</span><span class="sxs-lookup"><span data-stu-id="e8511-118">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="e8511-119">Anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="e8511-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="e8511-120">Hämta egenskapen [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) för att hämta ett gränssnitt för konfiguration av princip insamlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="e8511-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="e8511-121">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) för att hämta princip samlingen.</span><span class="sxs-lookup"><span data-stu-id="e8511-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="e8511-122">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="e8511-122">For an example, see the following:</span></span>

- <span data-ttu-id="e8511-123">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e8511-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e8511-124">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="e8511-124">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="e8511-125">Klass: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="e8511-125">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e8511-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e8511-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e8511-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e8511-127">Request syntax</span></span>

| <span data-ttu-id="e8511-128">Metod</span><span class="sxs-lookup"><span data-stu-id="e8511-128">Method</span></span>  | <span data-ttu-id="e8511-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e8511-129">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="e8511-130">**TA**</span><span class="sxs-lookup"><span data-stu-id="e8511-130">**GET**</span></span> | <span data-ttu-id="e8511-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="e8511-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e8511-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e8511-132">URI parameter</span></span>

<span data-ttu-id="e8511-133">Använd följande Sök vägs parameter när du skapar begäran:</span><span class="sxs-lookup"><span data-stu-id="e8511-133">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="e8511-134">Namn</span><span class="sxs-lookup"><span data-stu-id="e8511-134">Name</span></span>        | <span data-ttu-id="e8511-135">Typ</span><span class="sxs-lookup"><span data-stu-id="e8511-135">Type</span></span>   | <span data-ttu-id="e8511-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e8511-136">Required</span></span> | <span data-ttu-id="e8511-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e8511-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e8511-138">kund-ID</span><span class="sxs-lookup"><span data-stu-id="e8511-138">customer-id</span></span> | <span data-ttu-id="e8511-139">sträng</span><span class="sxs-lookup"><span data-stu-id="e8511-139">string</span></span> | <span data-ttu-id="e8511-140">Yes</span><span class="sxs-lookup"><span data-stu-id="e8511-140">Yes</span></span>      | <span data-ttu-id="e8511-141">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="e8511-141">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e8511-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e8511-142">Request headers</span></span>

<span data-ttu-id="e8511-143">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e8511-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e8511-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e8511-144">Request body</span></span>

<span data-ttu-id="e8511-145">Inget</span><span class="sxs-lookup"><span data-stu-id="e8511-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e8511-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e8511-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e8511-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e8511-147">REST response</span></span>

<span data-ttu-id="e8511-148">Om det lyckas innehåller svars texten samlingen av [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -resurser.</span><span class="sxs-lookup"><span data-stu-id="e8511-148">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e8511-149">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e8511-149">Response success and error codes</span></span>

<span data-ttu-id="e8511-150">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e8511-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e8511-151">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e8511-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e8511-152">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e8511-152">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e8511-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e8511-153">Response example</span></span>

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
