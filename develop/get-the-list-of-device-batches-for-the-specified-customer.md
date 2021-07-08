---
title: Hämta en lista över enhetsbatchar för den angivna kunden
description: Så här hämtar du en samling enhetsbatchar för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d020bbfa1faef0be423d2fef2d8982465dfa21f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548432"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="50396-103">Hämta en lista över enhetsbatchar för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="50396-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="50396-104">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="50396-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="50396-105">Så här hämtar du en samling enhetsbatchar för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="50396-105">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="50396-106">Varje enhetsbatch innehåller sammanfattningsstatusinformation om enheter som har registrerats i zero-touch-distribution.</span><span class="sxs-lookup"><span data-stu-id="50396-106">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50396-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="50396-107">Prerequisites</span></span>

- <span data-ttu-id="50396-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="50396-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="50396-109">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="50396-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="50396-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="50396-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="50396-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="50396-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="50396-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="50396-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="50396-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="50396-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="50396-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="50396-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="50396-115">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="50396-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="50396-116">C\#</span><span class="sxs-lookup"><span data-stu-id="50396-116">C\#</span></span>

<span data-ttu-id="50396-117">Om du vill hämta samlingen med enhetsbatchar för den angivna kunden anropar du först [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="50396-117">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="50396-118">Hämta sedan värdet för egenskapen [**DeviceBatches för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) att hämta ett gränssnitt för enhetsbatchinsamlingsåtgärder.</span><span class="sxs-lookup"><span data-stu-id="50396-118">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="50396-119">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="50396-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="50396-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="50396-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="50396-121">**Project:** Partnercenter-SDK **exempelklass:** GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="50396-121">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="50396-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="50396-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="50396-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="50396-123">Request syntax</span></span>

| <span data-ttu-id="50396-124">Metod</span><span class="sxs-lookup"><span data-stu-id="50396-124">Method</span></span>  | <span data-ttu-id="50396-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="50396-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="50396-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="50396-126">**GET**</span></span> | <span data-ttu-id="50396-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="50396-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="50396-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="50396-128">URI parameter</span></span>

<span data-ttu-id="50396-129">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="50396-129">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="50396-130">Namn</span><span class="sxs-lookup"><span data-stu-id="50396-130">Name</span></span>        | <span data-ttu-id="50396-131">Typ</span><span class="sxs-lookup"><span data-stu-id="50396-131">Type</span></span>   | <span data-ttu-id="50396-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="50396-132">Required</span></span> | <span data-ttu-id="50396-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="50396-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="50396-134">kund-id</span><span class="sxs-lookup"><span data-stu-id="50396-134">customer-id</span></span> | <span data-ttu-id="50396-135">sträng</span><span class="sxs-lookup"><span data-stu-id="50396-135">string</span></span> | <span data-ttu-id="50396-136">Ja</span><span class="sxs-lookup"><span data-stu-id="50396-136">Yes</span></span>      | <span data-ttu-id="50396-137">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="50396-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="50396-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="50396-138">Request headers</span></span>

<span data-ttu-id="50396-139">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="50396-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="50396-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="50396-140">Request body</span></span>

<span data-ttu-id="50396-141">Ingen</span><span class="sxs-lookup"><span data-stu-id="50396-141">None</span></span>

### <a name="request-example"></a><span data-ttu-id="50396-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="50396-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="50396-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="50396-143">REST response</span></span>

<span data-ttu-id="50396-144">Om det lyckas innehåller svarstexten samlingen med [DeviceBatch-resurser.](device-deployment-resources.md#devicebatch)</span><span class="sxs-lookup"><span data-stu-id="50396-144">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="50396-145">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="50396-145">Response success and error codes</span></span>

<span data-ttu-id="50396-146">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="50396-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="50396-147">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="50396-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="50396-148">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="50396-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="50396-149">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="50396-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
