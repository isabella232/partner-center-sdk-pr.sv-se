---
title: Ladda upp en lista över enheter till en befintlig batch för den angivna kunden
description: Ladda upp en lista med information om enheter till en befintlig batch för den angivna kunden. Detta associerar enheterna med en enhets grupp som redan har skapats.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d01ac1a42c50416487167070be9d104562300baf
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769744"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="59c1a-104">Ladda upp en lista över enheter till en befintlig batch för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="59c1a-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="59c1a-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="59c1a-105">**Applies To**</span></span>

- <span data-ttu-id="59c1a-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="59c1a-106">Partner Center</span></span>
- <span data-ttu-id="59c1a-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="59c1a-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="59c1a-108">Ladda upp en lista med information om enheter till en befintlig batch för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="59c1a-108">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="59c1a-109">Detta associerar enheterna med en enhets grupp som redan har skapats.</span><span class="sxs-lookup"><span data-stu-id="59c1a-109">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59c1a-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="59c1a-110">Prerequisites</span></span>

- <span data-ttu-id="59c1a-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="59c1a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="59c1a-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="59c1a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="59c1a-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59c1a-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="59c1a-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="59c1a-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="59c1a-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="59c1a-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="59c1a-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="59c1a-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="59c1a-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="59c1a-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="59c1a-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59c1a-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="59c1a-119">Enhetens batch-ID.</span><span class="sxs-lookup"><span data-stu-id="59c1a-119">The device batch identifier.</span></span>

- <span data-ttu-id="59c1a-120">Listan över enhets resurser som innehåller information om de enskilda enheterna.</span><span class="sxs-lookup"><span data-stu-id="59c1a-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="59c1a-121">C\#</span><span class="sxs-lookup"><span data-stu-id="59c1a-121">C\#</span></span>

<span data-ttu-id="59c1a-122">Om du vill ladda upp en lista över enheter till en befintlig enhets grupp måste du först instansiera en ny [List/dotNet/API/system. Collections. Generic. list -1) av typen [**enhet**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) och fylla i listan med enheterna.</span><span class="sxs-lookup"><span data-stu-id="59c1a-122">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="59c1a-123">Följande kombinationer av fyllda egenskaper krävs minst för att identifiera varje enhet:</span><span class="sxs-lookup"><span data-stu-id="59c1a-123">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="59c1a-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="59c1a-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="59c1a-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="59c1a-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="59c1a-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="59c1a-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="59c1a-127">Endast [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="59c1a-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="59c1a-128">Endast [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="59c1a-128">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="59c1a-129">[**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="59c1a-129">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="59c1a-130">Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: n för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="59c1a-130">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="59c1a-131">Anropa sedan metoden [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) med enhetens batch-ID för att hämta ett gränssnitt till åtgärder för den angivna batchen.</span><span class="sxs-lookup"><span data-stu-id="59c1a-131">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="59c1a-132">Slutligen anropar du metoden [**Devices. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) med listan över enheter för att lägga till enheterna i enhets batchen.</span><span class="sxs-lookup"><span data-stu-id="59c1a-132">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

<span data-ttu-id="59c1a-133">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="59c1a-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="59c1a-134">**Projekt**: Partner Center SDK-exempel **klass**: CreateDevices.CS</span><span class="sxs-lookup"><span data-stu-id="59c1a-134">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="59c1a-135">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="59c1a-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="59c1a-136">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="59c1a-136">Request syntax</span></span>

| <span data-ttu-id="59c1a-137">Metod</span><span class="sxs-lookup"><span data-stu-id="59c1a-137">Method</span></span>   | <span data-ttu-id="59c1a-138">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="59c1a-138">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="59c1a-139">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="59c1a-139">**POST**</span></span> | <span data-ttu-id="59c1a-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="59c1a-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="59c1a-141">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="59c1a-141">URI parameter</span></span>

<span data-ttu-id="59c1a-142">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="59c1a-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="59c1a-143">Namn</span><span class="sxs-lookup"><span data-stu-id="59c1a-143">Name</span></span>           | <span data-ttu-id="59c1a-144">Typ</span><span class="sxs-lookup"><span data-stu-id="59c1a-144">Type</span></span>   | <span data-ttu-id="59c1a-145">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="59c1a-145">Required</span></span> | <span data-ttu-id="59c1a-146">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="59c1a-146">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="59c1a-147">kund-ID</span><span class="sxs-lookup"><span data-stu-id="59c1a-147">customer-id</span></span>    | <span data-ttu-id="59c1a-148">sträng</span><span class="sxs-lookup"><span data-stu-id="59c1a-148">string</span></span> | <span data-ttu-id="59c1a-149">Yes</span><span class="sxs-lookup"><span data-stu-id="59c1a-149">Yes</span></span>      | <span data-ttu-id="59c1a-150">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="59c1a-150">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="59c1a-151">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="59c1a-151">devicebatch-id</span></span> | <span data-ttu-id="59c1a-152">sträng</span><span class="sxs-lookup"><span data-stu-id="59c1a-152">string</span></span> | <span data-ttu-id="59c1a-153">Yes</span><span class="sxs-lookup"><span data-stu-id="59c1a-153">Yes</span></span>      | <span data-ttu-id="59c1a-154">En sträng identifierare som identifierar enhets batchen.</span><span class="sxs-lookup"><span data-stu-id="59c1a-154">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="59c1a-155">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="59c1a-155">Request headers</span></span>

<span data-ttu-id="59c1a-156">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="59c1a-156">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="59c1a-157">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="59c1a-157">Request body</span></span>

<span data-ttu-id="59c1a-158">Begär ande texten måste innehålla en matris med [enhets](device-deployment-resources.md#device) objekt.</span><span class="sxs-lookup"><span data-stu-id="59c1a-158">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="59c1a-159">Följande kombinationer av fält för att identifiera en enhet godkänns:</span><span class="sxs-lookup"><span data-stu-id="59c1a-159">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="59c1a-160">hardwareHash + productKey.</span><span class="sxs-lookup"><span data-stu-id="59c1a-160">hardwareHash + productKey.</span></span>
- <span data-ttu-id="59c1a-161">hardwareHash + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="59c1a-161">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="59c1a-162">hardwareHash + productKey + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="59c1a-162">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="59c1a-163">endast hardwareHash.</span><span class="sxs-lookup"><span data-stu-id="59c1a-163">hardwareHash only.</span></span>
- <span data-ttu-id="59c1a-164">endast productKey.</span><span class="sxs-lookup"><span data-stu-id="59c1a-164">productKey only.</span></span>
- <span data-ttu-id="59c1a-165">serialNumber + oemManufacturerName + modelName.</span><span class="sxs-lookup"><span data-stu-id="59c1a-165">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="59c1a-166">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="59c1a-166">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a><span data-ttu-id="59c1a-167">REST-svar</span><span class="sxs-lookup"><span data-stu-id="59c1a-167">REST response</span></span>

<span data-ttu-id="59c1a-168">Om det lyckas innehåller svaret ett **plats** huvud som har en URI som kan användas för att hämta status för enhets uppladdning.</span><span class="sxs-lookup"><span data-stu-id="59c1a-168">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="59c1a-169">Spara denna URI för användning med andra relaterade REST API: er.</span><span class="sxs-lookup"><span data-stu-id="59c1a-169">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="59c1a-170">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="59c1a-170">Response success and error codes</span></span>

<span data-ttu-id="59c1a-171">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="59c1a-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="59c1a-172">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="59c1a-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="59c1a-173">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="59c1a-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="59c1a-174">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="59c1a-174">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
