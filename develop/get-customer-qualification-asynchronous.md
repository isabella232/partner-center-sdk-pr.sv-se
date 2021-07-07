---
title: Skaffa en kunds kompetens
description: Lär dig hur du använder asynkron validering för att få en kunds kvalificering via Partner Center API. Partner kan använda detta för att verifiera Education-kunder.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 4795b6e1ad008f9d854dc7efbee0c2099aefa609
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446317"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="22265-104">Hämta en kunds kvalificering asynkront</span><span class="sxs-lookup"><span data-stu-id="22265-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="22265-105">Hur du får en kunds kompetens asynkront.</span><span class="sxs-lookup"><span data-stu-id="22265-105">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22265-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="22265-106">Prerequisites</span></span>

- <span data-ttu-id="22265-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="22265-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="22265-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="22265-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="22265-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="22265-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="22265-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="22265-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="22265-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="22265-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="22265-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="22265-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="22265-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="22265-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="22265-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="22265-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="22265-115">C\#</span><span class="sxs-lookup"><span data-stu-id="22265-115">C\#</span></span>

<span data-ttu-id="22265-116">För att få en kunds kvalificering anropar du [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="22265-116">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="22265-117">Använd sedan egenskapen [**Kvalificering för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) att hämta ett [**ICustomerQualification-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="22265-117">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="22265-118">Anropa eller `GetQualifications()` för att hämta kundens `GetQualificationsAsync()` kvalificeringar.</span><span class="sxs-lookup"><span data-stu-id="22265-118">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="22265-119">**Exempel:** [Konsolexempelapp](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="22265-119">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="22265-120">**Project:** SdkSamples-klass: GetCustomerQualifications.cs </span><span class="sxs-lookup"><span data-stu-id="22265-120">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="22265-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="22265-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="22265-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="22265-122">Request syntax</span></span>

| <span data-ttu-id="22265-123">Metod</span><span class="sxs-lookup"><span data-stu-id="22265-123">Method</span></span>  | <span data-ttu-id="22265-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="22265-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="22265-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="22265-125">**GET**</span></span> | <span data-ttu-id="22265-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/kvalificering HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="22265-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="22265-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="22265-127">URI parameter</span></span>

<span data-ttu-id="22265-128">Den här tabellen innehåller frågeparametern som krävs för att hämta alla kvalificeringar.</span><span class="sxs-lookup"><span data-stu-id="22265-128">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="22265-129">Namn</span><span class="sxs-lookup"><span data-stu-id="22265-129">Name</span></span>               | <span data-ttu-id="22265-130">Typ</span><span class="sxs-lookup"><span data-stu-id="22265-130">Type</span></span>   | <span data-ttu-id="22265-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="22265-131">Required</span></span> | <span data-ttu-id="22265-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="22265-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="22265-133">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="22265-133">**customer-tenant-id**</span></span> | <span data-ttu-id="22265-134">sträng</span><span class="sxs-lookup"><span data-stu-id="22265-134">string</span></span> | <span data-ttu-id="22265-135">Ja</span><span class="sxs-lookup"><span data-stu-id="22265-135">Yes</span></span>      | <span data-ttu-id="22265-136">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="22265-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="22265-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="22265-137">Request headers</span></span>

<span data-ttu-id="22265-138">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="22265-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="22265-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="22265-139">Request body</span></span>

<span data-ttu-id="22265-140">Inga.</span><span class="sxs-lookup"><span data-stu-id="22265-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="22265-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="22265-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="22265-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="22265-142">REST response</span></span>

<span data-ttu-id="22265-143">Om det lyckas returnerar den här metoden en samling kvalificeringar i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="22265-143">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="22265-144">Nedan visas exempel på **GET-anrop** på en kund med **utbildningskvalificering.**</span><span class="sxs-lookup"><span data-stu-id="22265-144">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="22265-145">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="22265-145">Response success and error codes</span></span>

<span data-ttu-id="22265-146">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="22265-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="22265-147">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="22265-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="22265-148">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="22265-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="22265-149">Svarsexempel</span><span class="sxs-lookup"><span data-stu-id="22265-149">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="22265-150">Godkända</span><span class="sxs-lookup"><span data-stu-id="22265-150">Approved</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Approved",
    }
]

```

#### <a name="in-review"></a><span data-ttu-id="22265-151">Under granskning</span><span class="sxs-lookup"><span data-stu-id="22265-151">In Review</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "InReview",
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

#### <a name="denied"></a><span data-ttu-id="22265-152">Nekad</span><span class="sxs-lookup"><span data-stu-id="22265-152">Denied</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Denied",
        "vettingReason": "Not an Education Customer", // example Vetting Reason
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="22265-153">Exempel på tillståndsägda entiteter</span><span class="sxs-lookup"><span data-stu-id="22265-153">State Owned Entity Samples</span></span>

<span data-ttu-id="22265-154">**Tillståndsägd entitet via POST-exempel**</span><span class="sxs-lookup"><span data-stu-id="22265-154">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="22265-155">**Exempel på tillståndsägd entitet via hämta kvalificering**</span><span class="sxs-lookup"><span data-stu-id="22265-155">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="22265-156">**Tillståndsägd entitet via Hämta utbildningskvalifikationer**</span><span class="sxs-lookup"><span data-stu-id="22265-156">**State Owned Entity via Get Qualifications with Education**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “Education”,
        “vettingStatus”: “Approved”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="22265-157">**Tillståndsägd entitet via Hämta kvalificeringar med GCC**</span><span class="sxs-lookup"><span data-stu-id="22265-157">**State Owned Entity via Get Qualifications with GCC**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “GovernmentCommunityCloud”,
        “vettingStatus”: “Approved”,
        “vettingCreateDate”: “2021-05-06T19:59:56.6832021+00:00”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="22265-158">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="22265-158">Related articles</span></span>

- [<span data-ttu-id="22265-159">Uppdatera en kunds kvalificeringar</span><span class="sxs-lookup"><span data-stu-id="22265-159">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
