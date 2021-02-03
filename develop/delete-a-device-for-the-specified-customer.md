---
title: Ta bort en enhet för den angivna kunden
description: Så här tar du bort en enhet som tillhör en angiven kund.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69b5440f2cf07d3cb4ecd5addf429acd64530257
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769387"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="b64b5-103">Ta bort en enhet för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="b64b5-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="b64b5-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="b64b5-104">**Applies to:**</span></span>

- <span data-ttu-id="b64b5-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b64b5-105">Partner Center</span></span>
- <span data-ttu-id="b64b5-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="b64b5-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="b64b5-107">Den här artikeln förklarar hur du tar bort en enhet som tillhör en viss kund.</span><span class="sxs-lookup"><span data-stu-id="b64b5-107">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b64b5-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b64b5-108">Prerequisites</span></span>

- <span data-ttu-id="b64b5-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b64b5-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b64b5-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b64b5-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b64b5-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b64b5-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b64b5-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="b64b5-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b64b5-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="b64b5-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b64b5-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="b64b5-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b64b5-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="b64b5-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b64b5-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b64b5-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b64b5-117">Enhetens batch-ID.</span><span class="sxs-lookup"><span data-stu-id="b64b5-117">The device batch identifier.</span></span>

- <span data-ttu-id="b64b5-118">Enhets-ID.</span><span class="sxs-lookup"><span data-stu-id="b64b5-118">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="b64b5-119">C\#</span><span class="sxs-lookup"><span data-stu-id="b64b5-119">C\#</span></span>

<span data-ttu-id="b64b5-120">Så här tar du bort en enhet för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="b64b5-120">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="b64b5-121">Anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: n för att hämta ett gränssnitt till åtgärder på kunden.</span><span class="sxs-lookup"><span data-stu-id="b64b5-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="b64b5-122">Anropa metoden [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) med enhetens batch-ID för att hämta ett gränssnitt till åtgärder för den angivna batchen.</span><span class="sxs-lookup"><span data-stu-id="b64b5-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="b64b5-123">Anropa metoden [**Devices. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) för att hämta ett gränssnitt för åtgärden på den angivna enheten.</span><span class="sxs-lookup"><span data-stu-id="b64b5-123">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="b64b5-124">Anropa [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) -eller [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) -metoden för att ta bort enheten från batchen.</span><span class="sxs-lookup"><span data-stu-id="b64b5-124">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="b64b5-125">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b64b5-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b64b5-126">**Projekt**: Partner Center SDK-exempel **klass**: DeleteDevice.CS</span><span class="sxs-lookup"><span data-stu-id="b64b5-126">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b64b5-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b64b5-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b64b5-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b64b5-128">Request syntax</span></span>

| <span data-ttu-id="b64b5-129">Metod</span><span class="sxs-lookup"><span data-stu-id="b64b5-129">Method</span></span>     | <span data-ttu-id="b64b5-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b64b5-130">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b64b5-131">DELETE</span><span class="sxs-lookup"><span data-stu-id="b64b5-131">DELETE</span></span>     | <span data-ttu-id="b64b5-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices/{Device-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b64b5-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="b64b5-133">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b64b5-133">URI parameters</span></span>

<span data-ttu-id="b64b5-134">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="b64b5-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="b64b5-135">Namn</span><span class="sxs-lookup"><span data-stu-id="b64b5-135">Name</span></span>           | <span data-ttu-id="b64b5-136">Typ</span><span class="sxs-lookup"><span data-stu-id="b64b5-136">Type</span></span>   | <span data-ttu-id="b64b5-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b64b5-137">Required</span></span> | <span data-ttu-id="b64b5-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b64b5-138">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="b64b5-139">kund-ID</span><span class="sxs-lookup"><span data-stu-id="b64b5-139">customer-id</span></span>    | <span data-ttu-id="b64b5-140">sträng</span><span class="sxs-lookup"><span data-stu-id="b64b5-140">string</span></span> | <span data-ttu-id="b64b5-141">Yes</span><span class="sxs-lookup"><span data-stu-id="b64b5-141">Yes</span></span>      | <span data-ttu-id="b64b5-142">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="b64b5-142">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="b64b5-143">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="b64b5-143">devicebatch-id</span></span> | <span data-ttu-id="b64b5-144">sträng</span><span class="sxs-lookup"><span data-stu-id="b64b5-144">string</span></span> | <span data-ttu-id="b64b5-145">Yes</span><span class="sxs-lookup"><span data-stu-id="b64b5-145">Yes</span></span>      | <span data-ttu-id="b64b5-146">Enhetens batch-identifierare för den batch som innehåller enheten.</span><span class="sxs-lookup"><span data-stu-id="b64b5-146">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="b64b5-147">enhets-ID</span><span class="sxs-lookup"><span data-stu-id="b64b5-147">device-id</span></span>      | <span data-ttu-id="b64b5-148">sträng</span><span class="sxs-lookup"><span data-stu-id="b64b5-148">string</span></span> | <span data-ttu-id="b64b5-149">Yes</span><span class="sxs-lookup"><span data-stu-id="b64b5-149">Yes</span></span>      | <span data-ttu-id="b64b5-150">Enhets-ID.</span><span class="sxs-lookup"><span data-stu-id="b64b5-150">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="b64b5-151">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b64b5-151">Request headers</span></span>

<span data-ttu-id="b64b5-152">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b64b5-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b64b5-153">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b64b5-153">Request body</span></span>

<span data-ttu-id="b64b5-154">Inget</span><span class="sxs-lookup"><span data-stu-id="b64b5-154">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b64b5-155">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b64b5-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b64b5-156">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b64b5-156">REST response</span></span>

<span data-ttu-id="b64b5-157">Om det lyckas returnerar svaret en **204-innehålls** status kod.</span><span class="sxs-lookup"><span data-stu-id="b64b5-157">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b64b5-158">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b64b5-158">Response success and error codes</span></span>

<span data-ttu-id="b64b5-159">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b64b5-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b64b5-160">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b64b5-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b64b5-161">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b64b5-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b64b5-162">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b64b5-162">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
