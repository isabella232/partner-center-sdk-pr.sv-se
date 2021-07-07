---
title: Ladda upp en lista över enheter till en befintlig batch för den angivna kunden
description: Så här laddar du upp en lista med information om enheter till en befintlig batch för den angivna kunden. Detta associerar enheterna med en enhetsbatch som redan har skapats.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3fa9cff39113130c54cecfaef1f8ca28e0ac5adf
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530318"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="5776f-104">Ladda upp en lista över enheter till en befintlig batch för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="5776f-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="5776f-105">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="5776f-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5776f-106">Så här laddar du upp en lista med information om enheter till en befintlig batch för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="5776f-106">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="5776f-107">Detta associerar enheterna med en enhetsbatch som redan har skapats.</span><span class="sxs-lookup"><span data-stu-id="5776f-107">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5776f-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="5776f-108">Prerequisites</span></span>

- <span data-ttu-id="5776f-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5776f-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5776f-110">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="5776f-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5776f-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5776f-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5776f-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5776f-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5776f-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="5776f-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5776f-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="5776f-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5776f-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="5776f-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5776f-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5776f-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5776f-117">Enhetsbatchidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="5776f-117">The device batch identifier.</span></span>

- <span data-ttu-id="5776f-118">Listan över enhetsresurser som innehåller information om de enskilda enheterna.</span><span class="sxs-lookup"><span data-stu-id="5776f-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="5776f-119">C\#</span><span class="sxs-lookup"><span data-stu-id="5776f-119">C\#</span></span>

<span data-ttu-id="5776f-120">Om du vill ladda upp en lista över enheter till en befintlig enhetsbatch ska du först instansiera en ny [List/dotnet/api/system.collections.generic.list-1) av typen [**Enhet**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) och fylla i listan med enheterna.</span><span class="sxs-lookup"><span data-stu-id="5776f-120">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="5776f-121">Följande kombinationer av ifyllda egenskaper krävs minst för att identifiera varje enhet:</span><span class="sxs-lookup"><span data-stu-id="5776f-121">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="5776f-122">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="5776f-122">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="5776f-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="5776f-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="5776f-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="5776f-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="5776f-125">[**Endast HardwareHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)</span><span class="sxs-lookup"><span data-stu-id="5776f-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="5776f-126">[**Endast ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="5776f-126">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="5776f-127">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="5776f-127">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="5776f-128">Anropa sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="5776f-128">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="5776f-129">Anropa sedan metoden [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) med enhetsbatchidentifieraren för att hämta ett gränssnitt för åtgärder för den angivna batchen.</span><span class="sxs-lookup"><span data-stu-id="5776f-129">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="5776f-130">Anropa slutligen metoden [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) med listan över enheter för att lägga till enheterna i enhetsbatchen.</span><span class="sxs-lookup"><span data-stu-id="5776f-130">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

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

<span data-ttu-id="5776f-131">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5776f-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5776f-132">**Project:** Partnercenter-SDK **Exempelklass:** CreateDevices.cs</span><span class="sxs-lookup"><span data-stu-id="5776f-132">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5776f-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="5776f-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5776f-134">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="5776f-134">Request syntax</span></span>

| <span data-ttu-id="5776f-135">Metod</span><span class="sxs-lookup"><span data-stu-id="5776f-135">Method</span></span>   | <span data-ttu-id="5776f-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="5776f-136">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5776f-137">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="5776f-137">**POST**</span></span> | <span data-ttu-id="5776f-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5776f-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5776f-139">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="5776f-139">URI parameter</span></span>

<span data-ttu-id="5776f-140">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="5776f-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="5776f-141">Namn</span><span class="sxs-lookup"><span data-stu-id="5776f-141">Name</span></span>           | <span data-ttu-id="5776f-142">Typ</span><span class="sxs-lookup"><span data-stu-id="5776f-142">Type</span></span>   | <span data-ttu-id="5776f-143">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="5776f-143">Required</span></span> | <span data-ttu-id="5776f-144">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5776f-144">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="5776f-145">kund-id</span><span class="sxs-lookup"><span data-stu-id="5776f-145">customer-id</span></span>    | <span data-ttu-id="5776f-146">sträng</span><span class="sxs-lookup"><span data-stu-id="5776f-146">string</span></span> | <span data-ttu-id="5776f-147">Ja</span><span class="sxs-lookup"><span data-stu-id="5776f-147">Yes</span></span>      | <span data-ttu-id="5776f-148">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="5776f-148">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="5776f-149">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="5776f-149">devicebatch-id</span></span> | <span data-ttu-id="5776f-150">sträng</span><span class="sxs-lookup"><span data-stu-id="5776f-150">string</span></span> | <span data-ttu-id="5776f-151">Ja</span><span class="sxs-lookup"><span data-stu-id="5776f-151">Yes</span></span>      | <span data-ttu-id="5776f-152">En strängidentifierare som identifierar enhetsbatchen.</span><span class="sxs-lookup"><span data-stu-id="5776f-152">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5776f-153">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="5776f-153">Request headers</span></span>

<span data-ttu-id="5776f-154">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5776f-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5776f-155">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="5776f-155">Request body</span></span>

<span data-ttu-id="5776f-156">Begärandetexten måste innehålla en matris med [enhetsobjekt.](device-deployment-resources.md#device)</span><span class="sxs-lookup"><span data-stu-id="5776f-156">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="5776f-157">Följande kombinationer av fält för att identifiera en enhet accepteras:</span><span class="sxs-lookup"><span data-stu-id="5776f-157">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="5776f-158">hardwareHash + productKey.</span><span class="sxs-lookup"><span data-stu-id="5776f-158">hardwareHash + productKey.</span></span>
- <span data-ttu-id="5776f-159">hardwareHash + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="5776f-159">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="5776f-160">hardwareHash + productKey + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="5776f-160">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="5776f-161">hardwareHash endast.</span><span class="sxs-lookup"><span data-stu-id="5776f-161">hardwareHash only.</span></span>
- <span data-ttu-id="5776f-162">productKey endast.</span><span class="sxs-lookup"><span data-stu-id="5776f-162">productKey only.</span></span>
- <span data-ttu-id="5776f-163">serialNumber + oemManufacturerName + modelName.</span><span class="sxs-lookup"><span data-stu-id="5776f-163">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="5776f-164">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="5776f-164">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5776f-165">REST-svar</span><span class="sxs-lookup"><span data-stu-id="5776f-165">REST response</span></span>

<span data-ttu-id="5776f-166">Om det lyckas innehåller svaret ett **Platshuvud** som har en URI som kan användas för att hämta enhetens uppladdningsstatus.</span><span class="sxs-lookup"><span data-stu-id="5776f-166">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="5776f-167">Spara den här URI:en för användning med andra relaterade REST-API:er.</span><span class="sxs-lookup"><span data-stu-id="5776f-167">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5776f-168">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="5776f-168">Response success and error codes</span></span>

<span data-ttu-id="5776f-169">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="5776f-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5776f-170">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="5776f-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5776f-171">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5776f-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5776f-172">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="5776f-172">Response example</span></span>

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
