---
title: Ladda upp en lista över enheter för att skapa en ny batch för den angivna kunden
description: Så här laddar du upp en lista med information om enheter för att skapa en ny batch för den angivna kunden. Detta skapar en enhetsbatch för registrering i zero-touch-distribution och associerar enheterna och enhetsbatchen med den angivna kunden.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 285af12034562262c99b2aa3b139e948b0fdd462
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529740"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="8c5ef-104">Ladda upp en lista över enheter för att skapa en ny batch för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="8c5ef-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="8c5ef-105">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="8c5ef-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8c5ef-106">Så här laddar du upp en lista med information om enheter för att skapa en ny batch för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-106">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="8c5ef-107">Detta skapar en enhetsbatch för registrering i zero-touch-distribution och associerar enheterna och enhetsbatchen med den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-107">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c5ef-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8c5ef-108">Prerequisites</span></span>

- <span data-ttu-id="8c5ef-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8c5ef-110">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-110">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="8c5ef-111">Följ den [säkra appmodellen när du](enable-secure-app-model.md) använder app-/användarautentisering med Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-111">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="8c5ef-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8c5ef-113">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8c5ef-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8c5ef-114">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8c5ef-115">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="8c5ef-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8c5ef-116">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="8c5ef-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8c5ef-117">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8c5ef-118">Listan över enhetsresurser som innehåller information om de enskilda enheterna.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="8c5ef-119">C\#</span><span class="sxs-lookup"><span data-stu-id="8c5ef-119">C\#</span></span>

<span data-ttu-id="8c5ef-120">Så här laddar du upp en lista över enheter för att skapa en ny enhetsbatch:</span><span class="sxs-lookup"><span data-stu-id="8c5ef-120">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="8c5ef-121">Skapa en instans av en ny [List/dotnet/api/system.collections.generic.list-1) av typen [**Enhet**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) och fyll i listan med enheterna.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-121">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="8c5ef-122">Följande kombinationer av ifyllda egenskaper krävs minst för att identifiera varje enhet:</span><span class="sxs-lookup"><span data-stu-id="8c5ef-122">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="8c5ef-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="8c5ef-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="8c5ef-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="8c5ef-126">[**Endast HardwareHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)</span><span class="sxs-lookup"><span data-stu-id="8c5ef-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="8c5ef-127">[**Endast ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="8c5ef-127">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="8c5ef-128">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-128">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="8c5ef-129">Instansiera [**ett DeviceBatchCreationRequest-objekt**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) och ange egenskapen [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) till ett unikt namn som du väljer och egenskapen [**Enheter**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) till listan över enheter som ska laddas upp.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-129">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="8c5ef-130">Bearbeta begäran om att skapa enhetsbatch genom att anropa [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren för att hämta ett gränssnitt för åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-130">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="8c5ef-131">Anropa metoden [**DeviceBatches.Create eller**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) med begäran om att skapa batchen för enheten.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-131">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

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

<span data-ttu-id="8c5ef-132">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8c5ef-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8c5ef-133">**Project:** Partnercenter-SDK **Exempelklass:** CreateDeviceBatch.cs</span><span class="sxs-lookup"><span data-stu-id="8c5ef-133">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8c5ef-134">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8c5ef-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8c5ef-135">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="8c5ef-135">Request syntax</span></span>

| <span data-ttu-id="8c5ef-136">Metod</span><span class="sxs-lookup"><span data-stu-id="8c5ef-136">Method</span></span>   | <span data-ttu-id="8c5ef-137">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8c5ef-137">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="8c5ef-138">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="8c5ef-138">**POST**</span></span> | <span data-ttu-id="8c5ef-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8c5ef-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="8c5ef-140">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="8c5ef-140">URI parameter</span></span>

<span data-ttu-id="8c5ef-141">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-141">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="8c5ef-142">Namn</span><span class="sxs-lookup"><span data-stu-id="8c5ef-142">Name</span></span>        | <span data-ttu-id="8c5ef-143">Typ</span><span class="sxs-lookup"><span data-stu-id="8c5ef-143">Type</span></span>   | <span data-ttu-id="8c5ef-144">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8c5ef-144">Required</span></span> | <span data-ttu-id="8c5ef-145">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8c5ef-145">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8c5ef-146">kund-id</span><span class="sxs-lookup"><span data-stu-id="8c5ef-146">customer-id</span></span> | <span data-ttu-id="8c5ef-147">sträng</span><span class="sxs-lookup"><span data-stu-id="8c5ef-147">string</span></span> | <span data-ttu-id="8c5ef-148">Ja</span><span class="sxs-lookup"><span data-stu-id="8c5ef-148">Yes</span></span>      | <span data-ttu-id="8c5ef-149">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-149">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8c5ef-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8c5ef-150">Request headers</span></span>

<span data-ttu-id="8c5ef-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8c5ef-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8c5ef-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8c5ef-152">Request body</span></span>

<span data-ttu-id="8c5ef-153">Begärandetexten måste innehålla en [DeviceBatchCreationRequest-resurs.](device-deployment-resources.md#devicebatchcreationrequest)</span><span class="sxs-lookup"><span data-stu-id="8c5ef-153">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="8c5ef-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8c5ef-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8c5ef-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8c5ef-155">REST response</span></span>

<span data-ttu-id="8c5ef-156">Om det lyckas innehåller svaret ett **Platshuvud** som har en URI som kan användas för att hämta enhetens uppladdningsstatus.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-156">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="8c5ef-157">Spara den här URI:en för användning med andra relaterade REST-API:er.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-157">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8c5ef-158">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8c5ef-158">Response success and error codes</span></span>

<span data-ttu-id="8c5ef-159">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8c5ef-160">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8c5ef-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8c5ef-161">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8c5ef-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="8c5ef-162">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8c5ef-162">Response example</span></span>

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
