---
title: Hämta en lista över enhetsbatchar för den angivna kunden
description: Hämta en samling av enhets batchar för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea5797bbaff4d4eafd1e63428556ab784bcb0ee2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769810"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="7f655-103">Hämta en lista över enhetsbatchar för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="7f655-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="7f655-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="7f655-104">**Applies To**</span></span>

- <span data-ttu-id="7f655-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7f655-105">Partner Center</span></span>
- <span data-ttu-id="7f655-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="7f655-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7f655-107">Hämta en samling av enhets batchar för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="7f655-107">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="7f655-108">Varje enhets grupp innehåller information om sammanfattnings status om enheter som har registrerats i Zero Touch-distribution.</span><span class="sxs-lookup"><span data-stu-id="7f655-108">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f655-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7f655-109">Prerequisites</span></span>

- <span data-ttu-id="7f655-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7f655-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7f655-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7f655-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7f655-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7f655-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7f655-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="7f655-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7f655-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="7f655-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7f655-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="7f655-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7f655-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="7f655-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7f655-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7f655-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7f655-118">C\#</span><span class="sxs-lookup"><span data-stu-id="7f655-118">C\#</span></span>

<span data-ttu-id="7f655-119">Om du vill hämta en samling av enhets batchar för den angivna kunden anropar du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="7f655-119">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="7f655-120">Hämta sedan värdet för egenskapen [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) för att hämta ett gränssnitt till enhetens batch-insamlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="7f655-120">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="7f655-121">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="7f655-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="7f655-122">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7f655-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7f655-123">**Projekt**: Partner Center SDK-exempel **klass**: GetDevicesBatches.CS</span><span class="sxs-lookup"><span data-stu-id="7f655-123">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7f655-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7f655-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7f655-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="7f655-125">Request syntax</span></span>

| <span data-ttu-id="7f655-126">Metod</span><span class="sxs-lookup"><span data-stu-id="7f655-126">Method</span></span>  | <span data-ttu-id="7f655-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7f655-127">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="7f655-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="7f655-128">**GET**</span></span> | <span data-ttu-id="7f655-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches http/1.1</span><span class="sxs-lookup"><span data-stu-id="7f655-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7f655-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="7f655-130">URI parameter</span></span>

<span data-ttu-id="7f655-131">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="7f655-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="7f655-132">Namn</span><span class="sxs-lookup"><span data-stu-id="7f655-132">Name</span></span>        | <span data-ttu-id="7f655-133">Typ</span><span class="sxs-lookup"><span data-stu-id="7f655-133">Type</span></span>   | <span data-ttu-id="7f655-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7f655-134">Required</span></span> | <span data-ttu-id="7f655-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7f655-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7f655-136">kund-ID</span><span class="sxs-lookup"><span data-stu-id="7f655-136">customer-id</span></span> | <span data-ttu-id="7f655-137">sträng</span><span class="sxs-lookup"><span data-stu-id="7f655-137">string</span></span> | <span data-ttu-id="7f655-138">Yes</span><span class="sxs-lookup"><span data-stu-id="7f655-138">Yes</span></span>      | <span data-ttu-id="7f655-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="7f655-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7f655-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7f655-140">Request headers</span></span>

<span data-ttu-id="7f655-141">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7f655-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7f655-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7f655-142">Request body</span></span>

<span data-ttu-id="7f655-143">Inget</span><span class="sxs-lookup"><span data-stu-id="7f655-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7f655-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7f655-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7f655-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7f655-145">REST response</span></span>

<span data-ttu-id="7f655-146">Om det lyckas innehåller svars texten samlingen av [DeviceBatch](device-deployment-resources.md#devicebatch) -resurser.</span><span class="sxs-lookup"><span data-stu-id="7f655-146">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7f655-147">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7f655-147">Response success and error codes</span></span>

<span data-ttu-id="7f655-148">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="7f655-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7f655-149">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7f655-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7f655-150">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7f655-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7f655-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7f655-151">Response example</span></span>

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
