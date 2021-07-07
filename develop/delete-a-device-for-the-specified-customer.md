---
title: Ta bort en enhet för den angivna kunden
description: Ta bort en enhet som tillhör en angiven kund.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1e05ceb8615d6f84c1df101c542342f9a6eb04b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973085"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="851a8-103">Ta bort en enhet för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="851a8-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="851a8-104">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="851a8-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="851a8-105">Den här artikeln beskriver hur du tar bort en enhet som tillhör en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="851a8-105">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="851a8-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="851a8-106">Prerequisites</span></span>

- <span data-ttu-id="851a8-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="851a8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="851a8-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="851a8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="851a8-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="851a8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="851a8-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="851a8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="851a8-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="851a8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="851a8-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="851a8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="851a8-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="851a8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="851a8-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="851a8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="851a8-115">Enhetsbatchidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="851a8-115">The device batch identifier.</span></span>

- <span data-ttu-id="851a8-116">Enhetsidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="851a8-116">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="851a8-117">C\#</span><span class="sxs-lookup"><span data-stu-id="851a8-117">C\#</span></span>

<span data-ttu-id="851a8-118">Så här tar du bort en enhet för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="851a8-118">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="851a8-119">Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren för att hämta ett gränssnitt till åtgärder på kunden.</span><span class="sxs-lookup"><span data-stu-id="851a8-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="851a8-120">Anropa metoden [**DeviceBatches.ById med**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) enhetsbatchidentifieraren för att hämta ett gränssnitt till åtgärder för den angivna batchen.</span><span class="sxs-lookup"><span data-stu-id="851a8-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="851a8-121">Anropa metoden [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) för att hämta ett gränssnitt som ska användas på den angivna enheten.</span><span class="sxs-lookup"><span data-stu-id="851a8-121">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="851a8-122">Anropa metoden [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) eller [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) för att ta bort enheten från batchen.</span><span class="sxs-lookup"><span data-stu-id="851a8-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="851a8-123">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="851a8-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="851a8-124">**Project:** Partnercenter-SDK **Exempelklass:** DeleteDevice.cs</span><span class="sxs-lookup"><span data-stu-id="851a8-124">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="851a8-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="851a8-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="851a8-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="851a8-126">Request syntax</span></span>

| <span data-ttu-id="851a8-127">Metod</span><span class="sxs-lookup"><span data-stu-id="851a8-127">Method</span></span>     | <span data-ttu-id="851a8-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="851a8-128">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="851a8-129">DELETE</span><span class="sxs-lookup"><span data-stu-id="851a8-129">DELETE</span></span>     | <span data-ttu-id="851a8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="851a8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="851a8-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="851a8-131">URI parameters</span></span>

<span data-ttu-id="851a8-132">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="851a8-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="851a8-133">Namn</span><span class="sxs-lookup"><span data-stu-id="851a8-133">Name</span></span>           | <span data-ttu-id="851a8-134">Typ</span><span class="sxs-lookup"><span data-stu-id="851a8-134">Type</span></span>   | <span data-ttu-id="851a8-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="851a8-135">Required</span></span> | <span data-ttu-id="851a8-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="851a8-136">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="851a8-137">kund-id</span><span class="sxs-lookup"><span data-stu-id="851a8-137">customer-id</span></span>    | <span data-ttu-id="851a8-138">sträng</span><span class="sxs-lookup"><span data-stu-id="851a8-138">string</span></span> | <span data-ttu-id="851a8-139">Ja</span><span class="sxs-lookup"><span data-stu-id="851a8-139">Yes</span></span>      | <span data-ttu-id="851a8-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="851a8-140">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="851a8-141">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="851a8-141">devicebatch-id</span></span> | <span data-ttu-id="851a8-142">sträng</span><span class="sxs-lookup"><span data-stu-id="851a8-142">string</span></span> | <span data-ttu-id="851a8-143">Ja</span><span class="sxs-lookup"><span data-stu-id="851a8-143">Yes</span></span>      | <span data-ttu-id="851a8-144">Batch-ID för enheten för batchen som innehåller enheten.</span><span class="sxs-lookup"><span data-stu-id="851a8-144">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="851a8-145">device-id</span><span class="sxs-lookup"><span data-stu-id="851a8-145">device-id</span></span>      | <span data-ttu-id="851a8-146">sträng</span><span class="sxs-lookup"><span data-stu-id="851a8-146">string</span></span> | <span data-ttu-id="851a8-147">Ja</span><span class="sxs-lookup"><span data-stu-id="851a8-147">Yes</span></span>      | <span data-ttu-id="851a8-148">Enhetsidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="851a8-148">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="851a8-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="851a8-149">Request headers</span></span>

<span data-ttu-id="851a8-150">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="851a8-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="851a8-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="851a8-151">Request body</span></span>

<span data-ttu-id="851a8-152">Ingen</span><span class="sxs-lookup"><span data-stu-id="851a8-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="851a8-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="851a8-153">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="851a8-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="851a8-154">REST response</span></span>

<span data-ttu-id="851a8-155">Om det lyckas returnerar svaret **statuskoden 204 Inget** innehåll.</span><span class="sxs-lookup"><span data-stu-id="851a8-155">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="851a8-156">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="851a8-156">Response success and error codes</span></span>

<span data-ttu-id="851a8-157">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="851a8-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="851a8-158">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="851a8-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="851a8-159">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="851a8-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="851a8-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="851a8-160">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
