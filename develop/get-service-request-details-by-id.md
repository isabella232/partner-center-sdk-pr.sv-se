---
title: Hämta information om tjänstbegäran efter ID.
description: Så här hämtar du information om en befintlig kundtjänstbegäran efter ID.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66488cf9592d630cb1f0237d379e8df5ead6a3a8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548778"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="2d161-103">Hämta information om tjänstbegäran efter ID</span><span class="sxs-lookup"><span data-stu-id="2d161-103">Get service request details by ID</span></span>

<span data-ttu-id="2d161-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2d161-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2d161-105">Så här hämtar du information om en befintlig kundtjänstbegäran med hjälp av identifieraren för tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="2d161-105">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d161-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2d161-106">Prerequisites</span></span>

- <span data-ttu-id="2d161-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2d161-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2d161-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2d161-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2d161-109">Ett ID för tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="2d161-109">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="2d161-110">C\#</span><span class="sxs-lookup"><span data-stu-id="2d161-110">C\#</span></span>

<span data-ttu-id="2d161-111">Om du vill hämta information om en befintlig kundtjänstbegäran anropar du metoden [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) och skickar en [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) för att identifiera och returnera ett gränssnitt till det specifika [**ServiceRequest-objektet.**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)</span><span class="sxs-lookup"><span data-stu-id="2d161-111">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="2d161-112">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2d161-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2d161-113">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="2d161-113">Request syntax</span></span>

| <span data-ttu-id="2d161-114">Metod</span><span class="sxs-lookup"><span data-stu-id="2d161-114">Method</span></span>    | <span data-ttu-id="2d161-115">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2d161-115">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="2d161-116">**Få**</span><span class="sxs-lookup"><span data-stu-id="2d161-116">**GET**</span></span> | <span data-ttu-id="2d161-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2d161-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="2d161-118">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2d161-118">URI parameter</span></span>

<span data-ttu-id="2d161-119">Använd följande URI-parameter för att hämta den angivna tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="2d161-119">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="2d161-120">Namn</span><span class="sxs-lookup"><span data-stu-id="2d161-120">Name</span></span>                  | <span data-ttu-id="2d161-121">Typ</span><span class="sxs-lookup"><span data-stu-id="2d161-121">Type</span></span>     | <span data-ttu-id="2d161-122">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2d161-122">Required</span></span> | <span data-ttu-id="2d161-123">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2d161-123">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="2d161-124">**servicerequest-id**</span><span class="sxs-lookup"><span data-stu-id="2d161-124">**servicerequest-id**</span></span> | <span data-ttu-id="2d161-125">**guid**</span><span class="sxs-lookup"><span data-stu-id="2d161-125">**guid**</span></span> | <span data-ttu-id="2d161-126">Y</span><span class="sxs-lookup"><span data-stu-id="2d161-126">Y</span></span>        | <span data-ttu-id="2d161-127">Ett GUID som identifierar tjänstbegäran.</span><span class="sxs-lookup"><span data-stu-id="2d161-127">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2d161-128">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2d161-128">Request headers</span></span>

<span data-ttu-id="2d161-129">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2d161-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2d161-130">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2d161-130">Request body</span></span>

<span data-ttu-id="2d161-131">Inga.</span><span class="sxs-lookup"><span data-stu-id="2d161-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2d161-132">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2d161-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2d161-133">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2d161-133">REST response</span></span>

<span data-ttu-id="2d161-134">Om det lyckas returnerar den här metoden en **resurs för** tjänstbegäran i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="2d161-134">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2d161-135">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2d161-135">Response success and error codes</span></span>

<span data-ttu-id="2d161-136">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="2d161-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2d161-137">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2d161-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2d161-138">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2d161-138">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2d161-139">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2d161-139">Response example</span></span>

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
