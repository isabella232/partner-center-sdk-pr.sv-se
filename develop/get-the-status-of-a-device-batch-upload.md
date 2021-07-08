---
title: Hämta status för en uppladdning av enhetsbatch
description: Så här hämtar du status för en enhets batchuppladdning för en angiven kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd8726af41fe4399797f39a0790cf962fde64acc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548489"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="73e35-103">Hämta status för en uppladdning av enhetsbatch</span><span class="sxs-lookup"><span data-stu-id="73e35-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="73e35-104">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="73e35-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="73e35-105">Så här hämtar du status för en enhets batchuppladdning för en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="73e35-105">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73e35-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="73e35-106">Prerequisites</span></span>

- <span data-ttu-id="73e35-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="73e35-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="73e35-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="73e35-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="73e35-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73e35-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="73e35-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="73e35-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="73e35-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="73e35-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="73e35-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="73e35-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="73e35-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="73e35-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="73e35-114">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73e35-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="73e35-115">Batchspårningsidentifieraren som returnerades i platsrubriken när enhetsbatchen skickades.</span><span class="sxs-lookup"><span data-stu-id="73e35-115">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="73e35-116">Mer information finns i [Upload en lista över enheter för den angivna kunden](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="73e35-116">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="73e35-117">C\#</span><span class="sxs-lookup"><span data-stu-id="73e35-117">C\#</span></span>

<span data-ttu-id="73e35-118">Om du vill hämta statusen för en enhets batchuppladdning anropar du först metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="73e35-118">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="73e35-119">Anropa sedan metoden [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) med batchspårnings-ID:t för att hämta ett gränssnitt för batchuppladdningsstatusåtgärder.</span><span class="sxs-lookup"><span data-stu-id="73e35-119">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="73e35-120">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) för att hämta statusen.</span><span class="sxs-lookup"><span data-stu-id="73e35-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="73e35-121">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="73e35-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="73e35-122">**Project:** Partnercenter-SDK **Exempelklass:** GetBatchUploadStatus.cs</span><span class="sxs-lookup"><span data-stu-id="73e35-122">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="73e35-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="73e35-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="73e35-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="73e35-124">Request syntax</span></span>

| <span data-ttu-id="73e35-125">Metod</span><span class="sxs-lookup"><span data-stu-id="73e35-125">Method</span></span>  | <span data-ttu-id="73e35-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="73e35-126">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="73e35-127">**Få**</span><span class="sxs-lookup"><span data-stu-id="73e35-127">**GET**</span></span> | <span data-ttu-id="73e35-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="73e35-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="73e35-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="73e35-129">URI parameter</span></span>

<span data-ttu-id="73e35-130">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="73e35-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="73e35-131">Namn</span><span class="sxs-lookup"><span data-stu-id="73e35-131">Name</span></span>             | <span data-ttu-id="73e35-132">Typ</span><span class="sxs-lookup"><span data-stu-id="73e35-132">Type</span></span>   | <span data-ttu-id="73e35-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="73e35-133">Required</span></span> | <span data-ttu-id="73e35-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="73e35-134">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="73e35-135">kund-id</span><span class="sxs-lookup"><span data-stu-id="73e35-135">customer-id</span></span>      | <span data-ttu-id="73e35-136">sträng</span><span class="sxs-lookup"><span data-stu-id="73e35-136">string</span></span> | <span data-ttu-id="73e35-137">Ja</span><span class="sxs-lookup"><span data-stu-id="73e35-137">Yes</span></span>      | <span data-ttu-id="73e35-138">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="73e35-138">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="73e35-139">batchtracking-id</span><span class="sxs-lookup"><span data-stu-id="73e35-139">batchtracking-id</span></span> | <span data-ttu-id="73e35-140">sträng</span><span class="sxs-lookup"><span data-stu-id="73e35-140">string</span></span> | <span data-ttu-id="73e35-141">Ja</span><span class="sxs-lookup"><span data-stu-id="73e35-141">Yes</span></span>      | <span data-ttu-id="73e35-142">En GUID-formaterad identifierare som används för att hämta en enhets batchuppladdningsstatus.</span><span class="sxs-lookup"><span data-stu-id="73e35-142">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="73e35-143">Det här ID:t returneras i platshuvudet när enhetsbatchen har skickats.</span><span class="sxs-lookup"><span data-stu-id="73e35-143">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="73e35-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="73e35-144">Request headers</span></span>

<span data-ttu-id="73e35-145">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="73e35-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="73e35-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="73e35-146">Request body</span></span>

<span data-ttu-id="73e35-147">Ingen</span><span class="sxs-lookup"><span data-stu-id="73e35-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="73e35-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="73e35-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="73e35-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="73e35-149">REST response</span></span>

<span data-ttu-id="73e35-150">Om det lyckas innehåller svaret en [BatchUploadDetails-resurs.](device-deployment-resources.md#batchuploaddetails)</span><span class="sxs-lookup"><span data-stu-id="73e35-150">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="73e35-151">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="73e35-151">Response success and error codes</span></span>

<span data-ttu-id="73e35-152">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="73e35-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="73e35-153">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="73e35-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="73e35-154">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="73e35-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="73e35-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="73e35-155">Response example</span></span>

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
