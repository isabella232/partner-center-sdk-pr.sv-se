---
title: Hämta en URL för relationsbegäran
description: Så här hämtar du en URL för relationsbegäran som ska skickas till en kund.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07804b36dfe0892cf8b531e0731188260c014f49
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547466"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="364ef-103">Hämta en URL för relationsbegäran</span><span class="sxs-lookup"><span data-stu-id="364ef-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="364ef-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="364ef-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="364ef-105">Så här hämtar du en URL för relationsbegäran som ska skickas till en kund.</span><span class="sxs-lookup"><span data-stu-id="364ef-105">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="364ef-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="364ef-106">Prerequisites</span></span>

- <span data-ttu-id="364ef-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="364ef-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="364ef-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="364ef-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="364ef-109">C\#</span><span class="sxs-lookup"><span data-stu-id="364ef-109">C\#</span></span>

<span data-ttu-id="364ef-110">Om du vill hämta en URL för relationsbegäran [**använder du först IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att hämta ett gränssnitt till partnerns kundåtgärder.</span><span class="sxs-lookup"><span data-stu-id="364ef-110">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="364ef-111">Använd sedan egenskapen [**RelationshipRequest för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) att hämta ett gränssnitt till åtgärder för kundrelationsbegäran.</span><span class="sxs-lookup"><span data-stu-id="364ef-111">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="364ef-112">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) för att hämta URL:en.</span><span class="sxs-lookup"><span data-stu-id="364ef-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="364ef-113">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="364ef-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="364ef-114">**Project:** Partnercenter-SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span><span class="sxs-lookup"><span data-stu-id="364ef-114">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="364ef-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="364ef-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="364ef-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="364ef-116">Request syntax</span></span>

| <span data-ttu-id="364ef-117">Metod</span><span class="sxs-lookup"><span data-stu-id="364ef-117">Method</span></span>  | <span data-ttu-id="364ef-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="364ef-118">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="364ef-119">**Få**</span><span class="sxs-lookup"><span data-stu-id="364ef-119">**GET**</span></span> | <span data-ttu-id="364ef-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="364ef-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="364ef-121">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="364ef-121">Request headers</span></span>

<span data-ttu-id="364ef-122">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="364ef-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="364ef-123">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="364ef-123">Request body</span></span>

<span data-ttu-id="364ef-124">Ingen</span><span class="sxs-lookup"><span data-stu-id="364ef-124">None</span></span>

### <a name="request-example"></a><span data-ttu-id="364ef-125">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="364ef-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="364ef-126">REST-svar</span><span class="sxs-lookup"><span data-stu-id="364ef-126">REST response</span></span>

<span data-ttu-id="364ef-127">Om det lyckas innehåller svaret [Objektet RelationshipRequest.](relationships-resources.md#relationshiprequest)</span><span class="sxs-lookup"><span data-stu-id="364ef-127">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="364ef-128">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="364ef-128">Response success and error codes</span></span>

<span data-ttu-id="364ef-129">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="364ef-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="364ef-130">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="364ef-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="364ef-131">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="364ef-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="364ef-132">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="364ef-132">Response example</span></span>

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
