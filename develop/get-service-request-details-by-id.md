---
title: Hämta information om tjänstbegäran per ID.
description: Hämta information om en befintlig kund service förfrågan per ID.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c79fd3f5e5609a1893891e9b2a8078f8678497b3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769900"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="8de2f-103">Hämta information om tjänstbegäran efter ID</span><span class="sxs-lookup"><span data-stu-id="8de2f-103">Get service request details by ID</span></span>

<span data-ttu-id="8de2f-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="8de2f-104">**Applies To**</span></span>

- <span data-ttu-id="8de2f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="8de2f-105">Partner Center</span></span>
- <span data-ttu-id="8de2f-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="8de2f-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8de2f-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8de2f-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8de2f-108">Hämta information om en befintlig kund service förfrågan med hjälp av tjänstens förfrågnings-ID.</span><span class="sxs-lookup"><span data-stu-id="8de2f-108">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8de2f-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8de2f-109">Prerequisites</span></span>

- <span data-ttu-id="8de2f-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8de2f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8de2f-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8de2f-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8de2f-112">Ett ID för tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="8de2f-112">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="8de2f-113">C\#</span><span class="sxs-lookup"><span data-stu-id="8de2f-113">C\#</span></span>

<span data-ttu-id="8de2f-114">Hämta information om en befintlig kund service förfrågan genom att anropa metoden [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) och skicka i en [**ServiceRequest.ID**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) för att identifiera och returnera ett gränssnitt till det specifika [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) -objektet.</span><span class="sxs-lookup"><span data-stu-id="8de2f-114">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest as ServiceRequest;

ServiceRequest serviceRequestDetails = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Get();

Console.WriteLine(string.Format("The primary contact for the service request {0} is {1} {2}.",
    serviceRequestDetails.Title,
    serviceRequestDetails.PrimaryContact.FirstName,
    serviceRequestDetails.PrimaryContact.LastName,
));
```

## <a name="rest-request"></a><span data-ttu-id="8de2f-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8de2f-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8de2f-116">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="8de2f-116">Request syntax</span></span>

| <span data-ttu-id="8de2f-117">Metod</span><span class="sxs-lookup"><span data-stu-id="8de2f-117">Method</span></span>    | <span data-ttu-id="8de2f-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8de2f-118">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="8de2f-119">**TA**</span><span class="sxs-lookup"><span data-stu-id="8de2f-119">**GET**</span></span> | <span data-ttu-id="8de2f-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="8de2f-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="8de2f-121">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="8de2f-121">URI parameter</span></span>

<span data-ttu-id="8de2f-122">Använd följande URI-parameter för att hämta den angivna tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="8de2f-122">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="8de2f-123">Namn</span><span class="sxs-lookup"><span data-stu-id="8de2f-123">Name</span></span>                  | <span data-ttu-id="8de2f-124">Typ</span><span class="sxs-lookup"><span data-stu-id="8de2f-124">Type</span></span>     | <span data-ttu-id="8de2f-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8de2f-125">Required</span></span> | <span data-ttu-id="8de2f-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8de2f-126">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="8de2f-127">**servicerequest-ID**</span><span class="sxs-lookup"><span data-stu-id="8de2f-127">**servicerequest-id**</span></span> | <span data-ttu-id="8de2f-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="8de2f-128">**guid**</span></span> | <span data-ttu-id="8de2f-129">Y</span><span class="sxs-lookup"><span data-stu-id="8de2f-129">Y</span></span>        | <span data-ttu-id="8de2f-130">Ett GUID som identifierar tjänst förfrågan.</span><span class="sxs-lookup"><span data-stu-id="8de2f-130">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8de2f-131">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8de2f-131">Request headers</span></span>

<span data-ttu-id="8de2f-132">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8de2f-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8de2f-133">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8de2f-133">Request body</span></span>

<span data-ttu-id="8de2f-134">Inga.</span><span class="sxs-lookup"><span data-stu-id="8de2f-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8de2f-135">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8de2f-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="8de2f-136">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8de2f-136">REST response</span></span>

<span data-ttu-id="8de2f-137">Om det lyckas returnerar den här metoden **en resurs för tjänstbegäran i** svars texten.</span><span class="sxs-lookup"><span data-stu-id="8de2f-137">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8de2f-138">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8de2f-138">Response success and error codes</span></span>

<span data-ttu-id="8de2f-139">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="8de2f-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8de2f-140">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8de2f-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8de2f-141">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8de2f-141">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8de2f-142">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8de2f-142">Response example</span></span>

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
