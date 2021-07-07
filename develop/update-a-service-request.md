---
title: Uppdatera en tjänstbegäran
description: Så här uppdaterar du en befintlig kundtjänstbegäran som en Molnlösningsleverantör har arkiverat hos Microsoft för kundens räkning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: efa7b2a98b6f95a763ca6e3811c43cc655c18e2b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530097"
---
# <a name="update-a-service-request"></a><span data-ttu-id="446f8-103">Uppdatera en tjänstbegäran</span><span class="sxs-lookup"><span data-stu-id="446f8-103">Update a service request</span></span>

<span data-ttu-id="446f8-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="446f8-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="446f8-105">Så här uppdaterar du en befintlig kundtjänstbegäran som en Molnlösningsleverantör har arkiverat hos Microsoft för kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="446f8-105">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="446f8-106">På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först [välja en kund.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="446f8-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="446f8-107">Välj sedan **Tjänsthantering** i det vänstra sidofältet.</span><span class="sxs-lookup"><span data-stu-id="446f8-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="446f8-108">Under rubriken **Supportbegäranden** väljer du den tjänstbegäran som är i fråga.</span><span class="sxs-lookup"><span data-stu-id="446f8-108">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="446f8-109">Slutför genom att göra önskade ändringar i tjänstbegäran och sedan välja **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="446f8-109">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="446f8-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="446f8-110">Prerequisites</span></span>

- <span data-ttu-id="446f8-111">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="446f8-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="446f8-112">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="446f8-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="446f8-113">Ett ID för tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="446f8-113">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="446f8-114">C\#</span><span class="sxs-lookup"><span data-stu-id="446f8-114">C\#</span></span>

<span data-ttu-id="446f8-115">Om du vill uppdatera en kunds tjänstbegäran anropar du [**metoden IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) med id:t för tjänstbegäran för att identifiera och returnera gränssnittet för tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="446f8-115">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request ID to identify and return the service request interface.</span></span> <span data-ttu-id="446f8-116">Anropa sedan metoden [**IServiceRequest.Patch eller**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) för att uppdatera tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="446f8-116">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="446f8-117">Om du vill ange de uppdaterade värdena skapar du ett nytt, tomt [**ServiceRequest-objekt**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) och anger endast de egenskapsvärden som du vill ändra.</span><span class="sxs-lookup"><span data-stu-id="446f8-117">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="446f8-118">Skicka sedan objektet i anropet till metoden Patch eller PatchAsync.</span><span class="sxs-lookup"><span data-stu-id="446f8-118">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="446f8-119">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="446f8-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="446f8-120">**Project:** Partnercenter-SDK **exempelklass:** UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="446f8-120">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="446f8-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="446f8-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="446f8-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="446f8-122">Request syntax</span></span>

| <span data-ttu-id="446f8-123">Metod</span><span class="sxs-lookup"><span data-stu-id="446f8-123">Method</span></span>    | <span data-ttu-id="446f8-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="446f8-124">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="446f8-125">**Patch**</span><span class="sxs-lookup"><span data-stu-id="446f8-125">**PATCH**</span></span> | <span data-ttu-id="446f8-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="446f8-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="446f8-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="446f8-127">URI parameter</span></span>

<span data-ttu-id="446f8-128">Använd följande URI-parameter för att uppdatera tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="446f8-128">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="446f8-129">Namn</span><span class="sxs-lookup"><span data-stu-id="446f8-129">Name</span></span>                  | <span data-ttu-id="446f8-130">Typ</span><span class="sxs-lookup"><span data-stu-id="446f8-130">Type</span></span>     | <span data-ttu-id="446f8-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="446f8-131">Required</span></span> | <span data-ttu-id="446f8-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="446f8-132">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="446f8-133">**servicerequest-id**</span><span class="sxs-lookup"><span data-stu-id="446f8-133">**servicerequest-id**</span></span> | <span data-ttu-id="446f8-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="446f8-134">**guid**</span></span> | <span data-ttu-id="446f8-135">Y</span><span class="sxs-lookup"><span data-stu-id="446f8-135">Y</span></span>        | <span data-ttu-id="446f8-136">Ett GUID som identifierar tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="446f8-136">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="446f8-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="446f8-137">Request headers</span></span>

<span data-ttu-id="446f8-138">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="446f8-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="446f8-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="446f8-139">Request body</span></span>

<span data-ttu-id="446f8-140">Begärandetexten ska innehålla en [ServiceRequest-resurs.](service-request-resources.md)</span><span class="sxs-lookup"><span data-stu-id="446f8-140">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="446f8-141">De enda obligatoriska värdena är de som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="446f8-141">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="446f8-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="446f8-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="446f8-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="446f8-143">REST response</span></span>

<span data-ttu-id="446f8-144">Om det lyckas returnerar den här metoden **en resurs för tjänstbegäran** med uppdaterade egenskaper i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="446f8-144">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="446f8-145">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="446f8-145">Response success and error codes</span></span>

<span data-ttu-id="446f8-146">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="446f8-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="446f8-147">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="446f8-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="446f8-148">En fullständig lista finns i [Felkoder för Partner Center REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="446f8-148">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="446f8-149">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="446f8-149">Response example</span></span>

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
