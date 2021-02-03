---
title: Hämta en URL för relationsbegäran
description: Hämta en URL för Relations förfrågan att skicka till en kund.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5f899734b774ff460e005e20df8658275b2ce9d5
ms.sourcegitcommit: d4e652e3b73c6137704d43d4a472cc5aa5549f11
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/09/2020
ms.locfileid: "97770273"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="35448-103">Hämta en URL för relationsbegäran</span><span class="sxs-lookup"><span data-stu-id="35448-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="35448-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="35448-104">**Applies To**</span></span>

- <span data-ttu-id="35448-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="35448-105">Partner Center</span></span>
- <span data-ttu-id="35448-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="35448-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="35448-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="35448-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="35448-108">Hämta en URL för Relations förfrågan att skicka till en kund.</span><span class="sxs-lookup"><span data-stu-id="35448-108">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35448-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="35448-109">Prerequisites</span></span>

- <span data-ttu-id="35448-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="35448-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="35448-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="35448-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="35448-112">C\#</span><span class="sxs-lookup"><span data-stu-id="35448-112">C\#</span></span>

<span data-ttu-id="35448-113">Om du vill hämta en URL för en Relations förfrågan använder du först [**IAggregatePartner. kunder**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att få ett gränssnitt till partnerns kund åtgärder.</span><span class="sxs-lookup"><span data-stu-id="35448-113">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="35448-114">Använd sedan egenskapen [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) för att hämta ett gränssnitt till begär ande åtgärder för kund relation.</span><span class="sxs-lookup"><span data-stu-id="35448-114">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="35448-115">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) för att hämta URL: en.</span><span class="sxs-lookup"><span data-stu-id="35448-115">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="35448-116">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="35448-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="35448-117">**Projekt**: Partner Center SDK-exempel **klass**: GetCustomerRelationshipRequest.CS</span><span class="sxs-lookup"><span data-stu-id="35448-117">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="35448-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="35448-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="35448-119">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="35448-119">Request syntax</span></span>

| <span data-ttu-id="35448-120">Metod</span><span class="sxs-lookup"><span data-stu-id="35448-120">Method</span></span>  | <span data-ttu-id="35448-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="35448-121">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="35448-122">**TA**</span><span class="sxs-lookup"><span data-stu-id="35448-122">**GET**</span></span> | <span data-ttu-id="35448-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/relationshiprequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="35448-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="35448-124">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="35448-124">Request headers</span></span>

<span data-ttu-id="35448-125">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="35448-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="35448-126">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="35448-126">Request body</span></span>

<span data-ttu-id="35448-127">Inget</span><span class="sxs-lookup"><span data-stu-id="35448-127">None</span></span>

### <a name="request-example"></a><span data-ttu-id="35448-128">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="35448-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="35448-129">REST-svar</span><span class="sxs-lookup"><span data-stu-id="35448-129">REST response</span></span>

<span data-ttu-id="35448-130">Om det lyckas innehåller svaret [RelationshipRequest](relationships-resources.md#relationshiprequest) -objektet.</span><span class="sxs-lookup"><span data-stu-id="35448-130">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="35448-131">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="35448-131">Response success and error codes</span></span>

<span data-ttu-id="35448-132">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="35448-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="35448-133">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="35448-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="35448-134">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="35448-134">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="35448-135">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="35448-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
