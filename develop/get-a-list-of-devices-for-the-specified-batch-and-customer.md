---
title: Hämta en lista över enheter för den angivna batchen och kunden
description: Hämta en samling enheter och enhets information i den angivna enhets batchen för en kund.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 36fe3b97612adfd26c1b498f31b90f743bf774cb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769549"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="81f7c-103">Hämta en lista över enheter för den angivna batchen och kunden</span><span class="sxs-lookup"><span data-stu-id="81f7c-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="81f7c-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="81f7c-104">**Applies to:**</span></span>

- <span data-ttu-id="81f7c-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="81f7c-105">Partner Center</span></span>
- <span data-ttu-id="81f7c-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="81f7c-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="81f7c-107">Den här artikeln beskriver hur du hämtar en samling enheter i en angiven enhets batch för en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="81f7c-107">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="81f7c-108">Varje enhets resurs innehåller information om enheten.</span><span class="sxs-lookup"><span data-stu-id="81f7c-108">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81f7c-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="81f7c-109">Prerequisites</span></span>

- <span data-ttu-id="81f7c-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="81f7c-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="81f7c-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="81f7c-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="81f7c-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="81f7c-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="81f7c-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="81f7c-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="81f7c-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="81f7c-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="81f7c-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="81f7c-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="81f7c-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="81f7c-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="81f7c-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="81f7c-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="81f7c-118">Ett batch-ID för enheten.</span><span class="sxs-lookup"><span data-stu-id="81f7c-118">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="81f7c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="81f7c-119">C\#</span></span>

<span data-ttu-id="81f7c-120">Hämta en samling enheter i en angiven enhets grupp för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="81f7c-120">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="81f7c-121">Anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="81f7c-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="81f7c-122">Anropa metoden [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) för att hämta ett gränssnitt till enhetens batch Collection-åtgärder för den angivna batchen.</span><span class="sxs-lookup"><span data-stu-id="81f7c-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="81f7c-123">Hämta egenskapen [**enheter**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) för att hämta ett gränssnitt till enhets samlings åtgärder för batchen.</span><span class="sxs-lookup"><span data-stu-id="81f7c-123">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="81f7c-124">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) -metoden för att hämta samlingen med enheter.</span><span class="sxs-lookup"><span data-stu-id="81f7c-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="81f7c-125">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="81f7c-125">For an example, see the following:</span></span>

- <span data-ttu-id="81f7c-126">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="81f7c-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="81f7c-127">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="81f7c-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="81f7c-128">Klass: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="81f7c-128">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="81f7c-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="81f7c-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="81f7c-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="81f7c-130">Request syntax</span></span>

| <span data-ttu-id="81f7c-131">Metod</span><span class="sxs-lookup"><span data-stu-id="81f7c-131">Method</span></span>  | <span data-ttu-id="81f7c-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="81f7c-132">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="81f7c-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="81f7c-133">**GET**</span></span> | <span data-ttu-id="81f7c-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="81f7c-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="81f7c-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="81f7c-135">URI parameters</span></span>

<span data-ttu-id="81f7c-136">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="81f7c-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="81f7c-137">Namn</span><span class="sxs-lookup"><span data-stu-id="81f7c-137">Name</span></span>           | <span data-ttu-id="81f7c-138">Typ</span><span class="sxs-lookup"><span data-stu-id="81f7c-138">Type</span></span>   | <span data-ttu-id="81f7c-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="81f7c-139">Required</span></span> | <span data-ttu-id="81f7c-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="81f7c-140">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="81f7c-141">kund-ID</span><span class="sxs-lookup"><span data-stu-id="81f7c-141">customer-id</span></span>    | <span data-ttu-id="81f7c-142">sträng</span><span class="sxs-lookup"><span data-stu-id="81f7c-142">string</span></span> | <span data-ttu-id="81f7c-143">Yes</span><span class="sxs-lookup"><span data-stu-id="81f7c-143">Yes</span></span>      | <span data-ttu-id="81f7c-144">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="81f7c-144">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="81f7c-145">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="81f7c-145">devicebatch-id</span></span> | <span data-ttu-id="81f7c-146">sträng</span><span class="sxs-lookup"><span data-stu-id="81f7c-146">string</span></span> | <span data-ttu-id="81f7c-147">Yes</span><span class="sxs-lookup"><span data-stu-id="81f7c-147">Yes</span></span>      | <span data-ttu-id="81f7c-148">En sträng identifierare som identifierar enhets batchen.</span><span class="sxs-lookup"><span data-stu-id="81f7c-148">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="81f7c-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="81f7c-149">Request headers</span></span>

<span data-ttu-id="81f7c-150">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="81f7c-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="81f7c-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="81f7c-151">Request body</span></span>

<span data-ttu-id="81f7c-152">Inget</span><span class="sxs-lookup"><span data-stu-id="81f7c-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="81f7c-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="81f7c-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="81f7c-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="81f7c-154">REST response</span></span>

<span data-ttu-id="81f7c-155">Om det lyckas innehåller svars texten en växlings Bart samling av [enhets](device-deployment-resources.md#device) resurser.</span><span class="sxs-lookup"><span data-stu-id="81f7c-155">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="81f7c-156">Samlingen innehåller 100 enheter på en sida.</span><span class="sxs-lookup"><span data-stu-id="81f7c-156">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="81f7c-157">Om du vill hämta nästa sida med 100 enheter måste continuationToken i svars texten inkluderas i efterföljande begäran som MS-ContinuationToken rubrik.</span><span class="sxs-lookup"><span data-stu-id="81f7c-157">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="81f7c-158">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="81f7c-158">Response success and error codes</span></span>

<span data-ttu-id="81f7c-159">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="81f7c-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="81f7c-160">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="81f7c-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="81f7c-161">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="81f7c-161">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="81f7c-162">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="81f7c-162">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
