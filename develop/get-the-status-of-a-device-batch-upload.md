---
title: Hämta status för en uppladdning av enhetsbatch
description: Så här hämtar du statusen för en enhets batch-överföring för en angiven kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fb887ba257d6fbe68f95ae4b59d701ac4c934860
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769795"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="45829-103">Hämta status för en uppladdning av enhetsbatch</span><span class="sxs-lookup"><span data-stu-id="45829-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="45829-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="45829-104">**Applies To**</span></span>

- <span data-ttu-id="45829-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="45829-105">Partner Center</span></span>
- <span data-ttu-id="45829-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="45829-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="45829-107">Så här hämtar du statusen för en enhets batch-överföring för en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="45829-107">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45829-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="45829-108">Prerequisites</span></span>

- <span data-ttu-id="45829-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="45829-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="45829-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="45829-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="45829-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="45829-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="45829-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="45829-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="45829-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="45829-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="45829-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="45829-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="45829-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="45829-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="45829-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="45829-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="45829-117">Den batch spårnings identifierare som returnerades i plats rubriken när enhets gruppen skickades.</span><span class="sxs-lookup"><span data-stu-id="45829-117">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="45829-118">Mer information finns i [Ladda upp en lista över enheter för den angivna kunden](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="45829-118">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="45829-119">C\#</span><span class="sxs-lookup"><span data-stu-id="45829-119">C\#</span></span>

<span data-ttu-id="45829-120">Om du vill hämta statusen för en enhets batch-överföring anropar du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="45829-120">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="45829-121">Anropa sedan metoden [**BatchUploadStatus. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) med batch-spårnings-ID: t för att hämta ett gränssnitt till status åtgärder för batch-överföring.</span><span class="sxs-lookup"><span data-stu-id="45829-121">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="45829-122">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) för att hämta statusen.</span><span class="sxs-lookup"><span data-stu-id="45829-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="45829-123">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="45829-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="45829-124">**Projekt**: Partner Center SDK-exempel **klass**: GetBatchUploadStatus.CS</span><span class="sxs-lookup"><span data-stu-id="45829-124">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="45829-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="45829-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="45829-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="45829-126">Request syntax</span></span>

| <span data-ttu-id="45829-127">Metod</span><span class="sxs-lookup"><span data-stu-id="45829-127">Method</span></span>  | <span data-ttu-id="45829-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="45829-128">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="45829-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="45829-129">**GET**</span></span> | <span data-ttu-id="45829-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="45829-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="45829-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="45829-131">URI parameter</span></span>

<span data-ttu-id="45829-132">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="45829-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="45829-133">Namn</span><span class="sxs-lookup"><span data-stu-id="45829-133">Name</span></span>             | <span data-ttu-id="45829-134">Typ</span><span class="sxs-lookup"><span data-stu-id="45829-134">Type</span></span>   | <span data-ttu-id="45829-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="45829-135">Required</span></span> | <span data-ttu-id="45829-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="45829-136">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="45829-137">kund-ID</span><span class="sxs-lookup"><span data-stu-id="45829-137">customer-id</span></span>      | <span data-ttu-id="45829-138">sträng</span><span class="sxs-lookup"><span data-stu-id="45829-138">string</span></span> | <span data-ttu-id="45829-139">Yes</span><span class="sxs-lookup"><span data-stu-id="45829-139">Yes</span></span>      | <span data-ttu-id="45829-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="45829-140">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="45829-141">batchtracking-ID</span><span class="sxs-lookup"><span data-stu-id="45829-141">batchtracking-id</span></span> | <span data-ttu-id="45829-142">sträng</span><span class="sxs-lookup"><span data-stu-id="45829-142">string</span></span> | <span data-ttu-id="45829-143">Yes</span><span class="sxs-lookup"><span data-stu-id="45829-143">Yes</span></span>      | <span data-ttu-id="45829-144">En GUID-formaterad identifierare som används för att hämta en enhets grupp överförings status.</span><span class="sxs-lookup"><span data-stu-id="45829-144">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="45829-145">Detta ID returneras i plats rubriken när enhets gruppen har skickats.</span><span class="sxs-lookup"><span data-stu-id="45829-145">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="45829-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="45829-146">Request headers</span></span>

<span data-ttu-id="45829-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="45829-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="45829-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="45829-148">Request body</span></span>

<span data-ttu-id="45829-149">Inget</span><span class="sxs-lookup"><span data-stu-id="45829-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="45829-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="45829-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="45829-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="45829-151">REST response</span></span>

<span data-ttu-id="45829-152">Om det lyckas innehåller svaret en [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) -resurs.</span><span class="sxs-lookup"><span data-stu-id="45829-152">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="45829-153">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="45829-153">Response success and error codes</span></span>

<span data-ttu-id="45829-154">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="45829-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="45829-155">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="45829-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="45829-156">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="45829-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="45829-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="45829-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```
