---
title: Uppdatera en tjänstbegäran
description: Så här uppdaterar du en befintlig kund service förfrågan som en moln lösnings leverantör har arkiverat med Microsoft på kundens vägnar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769741"
---
# <a name="update-a-service-request"></a>Uppdatera en tjänstbegäran

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här uppdaterar du en befintlig kund service förfrågan som en moln lösnings leverantör har arkiverat med Microsoft på kundens vägnar.

På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md). Välj sedan **Service Management** i den vänstra panelen. Under rubriken **support begär Anden** väljer du den aktuella tjänstbegäran. Slutför genom att utföra önskade ändringar i tjänstbegäran och välj sedan **Skicka.**

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett ID för tjänstbegäran.

## <a name="c"></a>C\#

Om du vill uppdatera en kunds tjänstbegäran anropar du metoden [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) med service förfrågnings-ID: t för att identifiera och returnera gränssnittet för tjänstbegäran. Anropa sedan metoden [**IServiceRequest. patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) eller [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) för att uppdatera tjänstbegäran. Om du vill ange de uppdaterade värdena skapar du ett nytt, tomt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) -objekt och anger bara de egenskaps värden som du vill ändra. Skicka sedan objektet i anropet till patch-eller PatchAsync-metoden.

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: UpdatePartnerServiceRequest.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **9.0a** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande URI-parameter för att uppdatera tjänstbegäran.

| Namn                  | Typ     | Obligatorisk | Beskrivning                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **servicerequest-ID** | **guid** | Y        | Ett GUID som identifierar tjänst förfrågan. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Begär ande texten bör innehålla en [ServiceRequest](service-request-resources.md) -resurs. De enda värden som krävs är de som ska uppdateras.

### <a name="request-example"></a>Exempel på begäran

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en resurs för **tjänstbegäran** med uppdaterade egenskaper i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
