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
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>Ladda upp en lista över enheter för att skapa en ny batch för den angivna kunden

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland

Ladda upp en lista med information om enheter för att skapa en ny batch för den angivna kunden. Detta skapar en enhets grupp för registrering i Zero Touch-distribution och kopplar enheterna och enhets batchen till den angivna kunden.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter. Följ den [säkra appens modell](enable-secure-app-model.md) när du använder app + User Authentication med API: er för partner Center.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Listan över enhets resurser som innehåller information om de enskilda enheterna.

## <a name="c"></a>C\#

För att ladda upp en lista över enheter för att skapa en ny enhets batch:

1. Instansiera en ny [List/dotNet/API/system. Collections. Generic. list -1) av typen [**enhet**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) och fyll i listan med enheterna. Följande kombinationer av fyllda egenskaper krävs minst för att identifiera varje enhet:

   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - Endast [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .
   - Endast [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .
   - [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

2. Instansiera ett [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) -objekt och ange egenskapen [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) till ett unikt namn som du väljer och egenskapen [**enheter**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) i listan över enheter som ska laddas upp.

3. Bearbeta begäran om att skapa enhets batch genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: n för att hämta ett gränssnitt till åtgärder på den angivna kunden.

4. Anropa metoden [**DeviceBatches. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) med enhets batch-begäran för att skapa batchen.

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: CreateDeviceBatch.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches http/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parametrar när du skapar begäran.

| Namn        | Typ   | Obligatorisk | Beskrivning                                           |
|-------------|--------|----------|-------------------------------------------------------|
| kund-ID | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Begär ande texten måste innehålla en [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) -resurs.

### <a name="request-example"></a>Exempel på begäran

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

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svaret ett **plats** huvud som har en URI som kan användas för att hämta status för enhets uppladdning. Spara denna URI för användning med andra relaterade REST API: er.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

#### <a name="response-example"></a>Exempel på svar

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
