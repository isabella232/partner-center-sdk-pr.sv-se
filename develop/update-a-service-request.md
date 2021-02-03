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
# <a name="update-a-service-request"></a><span data-ttu-id="320b5-103">Uppdatera en tjänstbegäran</span><span class="sxs-lookup"><span data-stu-id="320b5-103">Update a service request</span></span>

<span data-ttu-id="320b5-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="320b5-104">**Applies To**</span></span>

- <span data-ttu-id="320b5-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="320b5-105">Partner Center</span></span>
- <span data-ttu-id="320b5-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="320b5-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="320b5-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="320b5-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="320b5-108">Så här uppdaterar du en befintlig kund service förfrågan som en moln lösnings leverantör har arkiverat med Microsoft på kundens vägnar.</span><span class="sxs-lookup"><span data-stu-id="320b5-108">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="320b5-109">På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="320b5-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="320b5-110">Välj sedan **Service Management** i den vänstra panelen.</span><span class="sxs-lookup"><span data-stu-id="320b5-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="320b5-111">Under rubriken **support begär Anden** väljer du den aktuella tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="320b5-111">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="320b5-112">Slutför genom att utföra önskade ändringar i tjänstbegäran och välj sedan **Skicka.**</span><span class="sxs-lookup"><span data-stu-id="320b5-112">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="320b5-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="320b5-113">Prerequisites</span></span>

- <span data-ttu-id="320b5-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="320b5-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="320b5-115">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="320b5-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="320b5-116">Ett ID för tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="320b5-116">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="320b5-117">C\#</span><span class="sxs-lookup"><span data-stu-id="320b5-117">C\#</span></span>

<span data-ttu-id="320b5-118">Om du vill uppdatera en kunds tjänstbegäran anropar du metoden [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) med service förfrågnings-ID: t för att identifiera och returnera gränssnittet för tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="320b5-118">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request id to identify and return the service request interface.</span></span> <span data-ttu-id="320b5-119">Anropa sedan metoden [**IServiceRequest. patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) eller [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) för att uppdatera tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="320b5-119">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="320b5-120">Om du vill ange de uppdaterade värdena skapar du ett nytt, tomt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) -objekt och anger bara de egenskaps värden som du vill ändra.</span><span class="sxs-lookup"><span data-stu-id="320b5-120">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="320b5-121">Skicka sedan objektet i anropet till patch-eller PatchAsync-metoden.</span><span class="sxs-lookup"><span data-stu-id="320b5-121">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="320b5-122">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="320b5-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="320b5-123">**Projekt**: Partner Center SDK-exempel **klass**: UpdatePartnerServiceRequest.CS</span><span class="sxs-lookup"><span data-stu-id="320b5-123">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="320b5-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="320b5-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="320b5-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="320b5-125">Request syntax</span></span>

| <span data-ttu-id="320b5-126">Metod</span><span class="sxs-lookup"><span data-stu-id="320b5-126">Method</span></span>    | <span data-ttu-id="320b5-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="320b5-127">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="320b5-128">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="320b5-128">**PATCH**</span></span> | <span data-ttu-id="320b5-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="320b5-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="320b5-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="320b5-130">URI parameter</span></span>

<span data-ttu-id="320b5-131">Använd följande URI-parameter för att uppdatera tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="320b5-131">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="320b5-132">Namn</span><span class="sxs-lookup"><span data-stu-id="320b5-132">Name</span></span>                  | <span data-ttu-id="320b5-133">Typ</span><span class="sxs-lookup"><span data-stu-id="320b5-133">Type</span></span>     | <span data-ttu-id="320b5-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="320b5-134">Required</span></span> | <span data-ttu-id="320b5-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="320b5-135">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="320b5-136">**servicerequest-ID**</span><span class="sxs-lookup"><span data-stu-id="320b5-136">**servicerequest-id**</span></span> | <span data-ttu-id="320b5-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="320b5-137">**guid**</span></span> | <span data-ttu-id="320b5-138">Y</span><span class="sxs-lookup"><span data-stu-id="320b5-138">Y</span></span>        | <span data-ttu-id="320b5-139">Ett GUID som identifierar tjänst förfrågan.</span><span class="sxs-lookup"><span data-stu-id="320b5-139">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="320b5-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="320b5-140">Request headers</span></span>

<span data-ttu-id="320b5-141">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="320b5-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="320b5-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="320b5-142">Request body</span></span>

<span data-ttu-id="320b5-143">Begär ande texten bör innehålla en [ServiceRequest](service-request-resources.md) -resurs.</span><span class="sxs-lookup"><span data-stu-id="320b5-143">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="320b5-144">De enda värden som krävs är de som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="320b5-144">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="320b5-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="320b5-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="320b5-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="320b5-146">REST response</span></span>

<span data-ttu-id="320b5-147">Om det lyckas returnerar den här metoden en resurs för **tjänstbegäran** med uppdaterade egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="320b5-147">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="320b5-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="320b5-148">Response success and error codes</span></span>

<span data-ttu-id="320b5-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="320b5-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="320b5-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="320b5-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="320b5-151">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="320b5-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="320b5-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="320b5-152">Response example</span></span>

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
