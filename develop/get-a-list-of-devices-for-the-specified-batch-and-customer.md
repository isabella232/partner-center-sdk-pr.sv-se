---
title: Hämta en lista över enheter för den angivna batchen och kunden
description: Så här hämtar du en samling enheter och enhetsinformation i den angivna enhetsbatchen för en kund.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 28af1f568f755ba4c50cfac21529d6c677656c8e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874269"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="33854-103">Hämta en lista över enheter för den angivna batchen och kunden</span><span class="sxs-lookup"><span data-stu-id="33854-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="33854-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="33854-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="33854-105">Den här artikeln beskriver hur du hämtar en samling enheter i en angiven enhetsbatch för en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="33854-105">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="33854-106">Varje enhetsresurs innehåller information om enheten.</span><span class="sxs-lookup"><span data-stu-id="33854-106">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33854-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="33854-107">Prerequisites</span></span>

- <span data-ttu-id="33854-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="33854-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="33854-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="33854-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="33854-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="33854-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="33854-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="33854-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="33854-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="33854-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="33854-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="33854-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="33854-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="33854-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="33854-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="33854-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="33854-116">En enhets batchidentifierare.</span><span class="sxs-lookup"><span data-stu-id="33854-116">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="33854-117">C\#</span><span class="sxs-lookup"><span data-stu-id="33854-117">C\#</span></span>

<span data-ttu-id="33854-118">Så här hämtar du en samling enheter i en angiven enhetsbatch för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="33854-118">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="33854-119">Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt för åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="33854-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="33854-120">Anropa metoden [**DeviceBatches.ById för**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) att hämta ett gränssnitt till enhetsbatchinsamlingsåtgärder för den angivna batchen.</span><span class="sxs-lookup"><span data-stu-id="33854-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="33854-121">Hämta egenskapen [**Enheter**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) för att hämta ett gränssnitt för enhetssamlingsåtgärder för batchen.</span><span class="sxs-lookup"><span data-stu-id="33854-121">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="33854-122">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) för att hämta samlingen med enheter.</span><span class="sxs-lookup"><span data-stu-id="33854-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="33854-123">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="33854-123">For an example, see the following:</span></span>

- <span data-ttu-id="33854-124">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="33854-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="33854-125">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="33854-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="33854-126">Klass: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="33854-126">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="33854-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="33854-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="33854-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="33854-128">Request syntax</span></span>

| <span data-ttu-id="33854-129">Metod</span><span class="sxs-lookup"><span data-stu-id="33854-129">Method</span></span>  | <span data-ttu-id="33854-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="33854-130">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="33854-131">**Få**</span><span class="sxs-lookup"><span data-stu-id="33854-131">**GET**</span></span> | <span data-ttu-id="33854-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="33854-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="33854-133">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="33854-133">URI parameters</span></span>

<span data-ttu-id="33854-134">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="33854-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="33854-135">Namn</span><span class="sxs-lookup"><span data-stu-id="33854-135">Name</span></span>           | <span data-ttu-id="33854-136">Typ</span><span class="sxs-lookup"><span data-stu-id="33854-136">Type</span></span>   | <span data-ttu-id="33854-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="33854-137">Required</span></span> | <span data-ttu-id="33854-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="33854-138">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="33854-139">kund-ID</span><span class="sxs-lookup"><span data-stu-id="33854-139">customer-id</span></span>    | <span data-ttu-id="33854-140">sträng</span><span class="sxs-lookup"><span data-stu-id="33854-140">string</span></span> | <span data-ttu-id="33854-141">Ja</span><span class="sxs-lookup"><span data-stu-id="33854-141">Yes</span></span>      | <span data-ttu-id="33854-142">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="33854-142">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="33854-143">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="33854-143">devicebatch-id</span></span> | <span data-ttu-id="33854-144">sträng</span><span class="sxs-lookup"><span data-stu-id="33854-144">string</span></span> | <span data-ttu-id="33854-145">Ja</span><span class="sxs-lookup"><span data-stu-id="33854-145">Yes</span></span>      | <span data-ttu-id="33854-146">En strängidentifierare som identifierar enhetsbatchen.</span><span class="sxs-lookup"><span data-stu-id="33854-146">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="33854-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="33854-147">Request headers</span></span>

<span data-ttu-id="33854-148">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="33854-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="33854-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="33854-149">Request body</span></span>

<span data-ttu-id="33854-150">Ingen</span><span class="sxs-lookup"><span data-stu-id="33854-150">None</span></span>

### <a name="request-example"></a><span data-ttu-id="33854-151">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="33854-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="33854-152">REST-svar</span><span class="sxs-lookup"><span data-stu-id="33854-152">REST response</span></span>

<span data-ttu-id="33854-153">Om det lyckas innehåller svarstexten [](device-deployment-resources.md#device) en sidad samling enhetsresurser.</span><span class="sxs-lookup"><span data-stu-id="33854-153">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="33854-154">Samlingen innehåller 100 enheter på en sida.</span><span class="sxs-lookup"><span data-stu-id="33854-154">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="33854-155">För att hämta nästa sida med 100 enheter måste continuationToken i svarstexten inkluderas i efterföljande begäran som ett MS-ContinuationToken huvud.</span><span class="sxs-lookup"><span data-stu-id="33854-155">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="33854-156">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="33854-156">Response success and error codes</span></span>

<span data-ttu-id="33854-157">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="33854-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="33854-158">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="33854-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="33854-159">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="33854-159">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="33854-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="33854-160">Response example</span></span>

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
