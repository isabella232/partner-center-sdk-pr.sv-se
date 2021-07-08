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
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>Hämta en lista över enheter för den angivna batchen och kunden

**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Tyskland

Den här artikeln beskriver hur du hämtar en samling enheter i en angiven enhetsbatch för en angiven kund. Varje enhetsresurs innehåller information om enheten.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- En enhets batchidentifierare.

## <a name="c"></a>C\#

Så här hämtar du en samling enheter i en angiven enhetsbatch för den angivna kunden:

1. Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt för åtgärder på den angivna kunden.

2. Anropa metoden [**DeviceBatches.ById för**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) att hämta ett gränssnitt till enhetsbatchinsamlingsåtgärder för den angivna batchen.

3. Hämta egenskapen [**Enheter**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) för att hämta ett gränssnitt för enhetssamlingsåtgärder för batchen.

4. Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) för att hämta samlingen med enheter.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Ett exempel finns i följande:

- Exempel: [Konsoltestapp](console-test-app.md)
- Project: **Partnercenter-SDK exempel**
- Klass: **GetDevices.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökvägsparametrar när du skapar begäran.

| Namn           | Typ   | Obligatorisk | Beskrivning                                           |
|----------------|--------|----------|-------------------------------------------------------|
| kund-ID    | sträng | Ja      | En GUID-formaterad sträng som identifierar kunden. |
| devicebatch-id | sträng | Ja      | En strängidentifierare som identifierar enhetsbatchen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten [](device-deployment-resources.md#device) en sidad samling enhetsresurser. Samlingen innehåller 100 enheter på en sida. För att hämta nästa sida med 100 enheter måste continuationToken i svarstexten inkluderas i efterföljande begäran som ett MS-ContinuationToken huvud.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

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
