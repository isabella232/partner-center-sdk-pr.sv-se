---
title: Ladda upp en lista över enheter för att skapa en ny batch för den angivna kunden
description: Ladda upp en lista med information om enheter för att skapa en ny batch för den angivna kunden. Detta skapar en enhets grupp för registrering i Zero Touch-distribution och kopplar enheterna och enhets batchen till den angivna kunden.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b48971b862418136c42e78ae973a5aea27404a1
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769738"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="7a093-104">Ladda upp en lista över enheter för att skapa en ny batch för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="7a093-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="7a093-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="7a093-105">**Applies to:**</span></span>

- <span data-ttu-id="7a093-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7a093-106">Partner Center</span></span>
- <span data-ttu-id="7a093-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="7a093-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7a093-108">Ladda upp en lista med information om enheter för att skapa en ny batch för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="7a093-108">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="7a093-109">Detta skapar en enhets grupp för registrering i Zero Touch-distribution och kopplar enheterna och enhets batchen till den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="7a093-109">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a093-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7a093-110">Prerequisites</span></span>

- <span data-ttu-id="7a093-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7a093-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7a093-112">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7a093-112">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="7a093-113">Följ den [säkra appens modell](enable-secure-app-model.md) när du använder app + User Authentication med API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="7a093-113">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="7a093-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7a093-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7a093-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="7a093-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7a093-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="7a093-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7a093-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="7a093-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7a093-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="7a093-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7a093-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7a093-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7a093-120">Listan över enhets resurser som innehåller information om de enskilda enheterna.</span><span class="sxs-lookup"><span data-stu-id="7a093-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="7a093-121">C\#</span><span class="sxs-lookup"><span data-stu-id="7a093-121">C\#</span></span>

<span data-ttu-id="7a093-122">För att ladda upp en lista över enheter för att skapa en ny enhets batch:</span><span class="sxs-lookup"><span data-stu-id="7a093-122">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="7a093-123">Instansiera en ny [List/dotNet/API/system. Collections. Generic. list -1) av typen [**enhet**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) och fyll i listan med enheterna.</span><span class="sxs-lookup"><span data-stu-id="7a093-123">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="7a093-124">Följande kombinationer av fyllda egenskaper krävs minst för att identifiera varje enhet:</span><span class="sxs-lookup"><span data-stu-id="7a093-124">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="7a093-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="7a093-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="7a093-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="7a093-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="7a093-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="7a093-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="7a093-128">Endast [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="7a093-128">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="7a093-129">Endast [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="7a093-129">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="7a093-130">[**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="7a093-130">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="7a093-131">Instansiera ett [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) -objekt och ange egenskapen [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) till ett unikt namn som du väljer och egenskapen [**enheter**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) i listan över enheter som ska laddas upp.</span><span class="sxs-lookup"><span data-stu-id="7a093-131">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="7a093-132">Bearbeta begäran om att skapa enhets batch genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: n för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="7a093-132">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="7a093-133">Anropa metoden [**DeviceBatches. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) med enhets batch-begäran för att skapa batchen.</span><span class="sxs-lookup"><span data-stu-id="7a093-133">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

<span data-ttu-id="7a093-134">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7a093-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7a093-135">**Projekt**: Partner Center SDK-exempel **klass**: CreateDeviceBatch.CS</span><span class="sxs-lookup"><span data-stu-id="7a093-135">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7a093-136">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7a093-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7a093-137">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="7a093-137">Request syntax</span></span>

| <span data-ttu-id="7a093-138">Metod</span><span class="sxs-lookup"><span data-stu-id="7a093-138">Method</span></span>   | <span data-ttu-id="7a093-139">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7a093-139">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="7a093-140">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="7a093-140">**POST**</span></span> | <span data-ttu-id="7a093-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches http/1.1</span><span class="sxs-lookup"><span data-stu-id="7a093-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="7a093-142">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="7a093-142">URI parameter</span></span>

<span data-ttu-id="7a093-143">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="7a093-143">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="7a093-144">Namn</span><span class="sxs-lookup"><span data-stu-id="7a093-144">Name</span></span>        | <span data-ttu-id="7a093-145">Typ</span><span class="sxs-lookup"><span data-stu-id="7a093-145">Type</span></span>   | <span data-ttu-id="7a093-146">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7a093-146">Required</span></span> | <span data-ttu-id="7a093-147">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7a093-147">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7a093-148">kund-ID</span><span class="sxs-lookup"><span data-stu-id="7a093-148">customer-id</span></span> | <span data-ttu-id="7a093-149">sträng</span><span class="sxs-lookup"><span data-stu-id="7a093-149">string</span></span> | <span data-ttu-id="7a093-150">Yes</span><span class="sxs-lookup"><span data-stu-id="7a093-150">Yes</span></span>      | <span data-ttu-id="7a093-151">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="7a093-151">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7a093-152">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7a093-152">Request headers</span></span>

<span data-ttu-id="7a093-153">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7a093-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7a093-154">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7a093-154">Request body</span></span>

<span data-ttu-id="7a093-155">Begär ande texten måste innehålla en [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) -resurs.</span><span class="sxs-lookup"><span data-stu-id="7a093-155">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="7a093-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7a093-156">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="7a093-157">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7a093-157">REST response</span></span>

<span data-ttu-id="7a093-158">Om det lyckas innehåller svaret ett **plats** huvud som har en URI som kan användas för att hämta status för enhets uppladdning.</span><span class="sxs-lookup"><span data-stu-id="7a093-158">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="7a093-159">Spara denna URI för användning med andra relaterade REST API: er.</span><span class="sxs-lookup"><span data-stu-id="7a093-159">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7a093-160">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7a093-160">Response success and error codes</span></span>

<span data-ttu-id="7a093-161">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="7a093-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7a093-162">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7a093-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7a093-163">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7a093-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="7a093-164">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7a093-164">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
