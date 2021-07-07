---
title: Hämta en kunds kvalificering
description: Lär dig hur du använder synkron validering för att få en kunds kvalificering via Partner Center API. Partner kan använda detta för att verifiera Education-kunder.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d215ddb105efe3acd1182c4ff4bb25b045b121f0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446351"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="a509b-104">Hämta en kunds kvalificering via synkron validering</span><span class="sxs-lookup"><span data-stu-id="a509b-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="a509b-105">Lär dig hur du hämtar en kunds kvalificering synkront via Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="a509b-105">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="a509b-106">Information om hur du gör detta asynkront finns i [Hämta en kunds kvalificering via asynkron validering.](get-customer-qualification-asynchronous.md)</span><span class="sxs-lookup"><span data-stu-id="a509b-106">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a509b-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a509b-107">Prerequisites</span></span>

- <span data-ttu-id="a509b-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a509b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a509b-109">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a509b-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a509b-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a509b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a509b-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a509b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a509b-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="a509b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a509b-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="a509b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a509b-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="a509b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a509b-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a509b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="a509b-116">C\#</span><span class="sxs-lookup"><span data-stu-id="a509b-116">C\#</span></span>

<span data-ttu-id="a509b-117">För att få en kunds kvalificering anropar du [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="a509b-117">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="a509b-118">Använd sedan egenskapen [**Kvalificering för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) att hämta ett [**ICustomerQualification-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="a509b-118">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="a509b-119">Anropa slutligen [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync för**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) att hämta kundens kvalificering.</span><span class="sxs-lookup"><span data-stu-id="a509b-119">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="a509b-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a509b-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a509b-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="a509b-121">Request syntax</span></span>

| <span data-ttu-id="a509b-122">Metod</span><span class="sxs-lookup"><span data-stu-id="a509b-122">Method</span></span>  | <span data-ttu-id="a509b-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a509b-123">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a509b-124">**Få**</span><span class="sxs-lookup"><span data-stu-id="a509b-124">**GET**</span></span> | <span data-ttu-id="a509b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/kvalificering HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a509b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a509b-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="a509b-126">URI parameter</span></span>

<span data-ttu-id="a509b-127">I den här tabellen visas den frågeparameter som krävs för att hämta alla kvalificeringar.</span><span class="sxs-lookup"><span data-stu-id="a509b-127">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="a509b-128">Namn</span><span class="sxs-lookup"><span data-stu-id="a509b-128">Name</span></span>               | <span data-ttu-id="a509b-129">Typ</span><span class="sxs-lookup"><span data-stu-id="a509b-129">Type</span></span>   | <span data-ttu-id="a509b-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a509b-130">Required</span></span> | <span data-ttu-id="a509b-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a509b-131">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="a509b-132">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="a509b-132">**customer-tenant-id**</span></span> | <span data-ttu-id="a509b-133">sträng</span><span class="sxs-lookup"><span data-stu-id="a509b-133">string</span></span> | <span data-ttu-id="a509b-134">Ja</span><span class="sxs-lookup"><span data-stu-id="a509b-134">Yes</span></span>      | <span data-ttu-id="a509b-135">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="a509b-135">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a509b-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a509b-136">Request headers</span></span>

<span data-ttu-id="a509b-137">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a509b-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a509b-138">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a509b-138">Request body</span></span>

<span data-ttu-id="a509b-139">Inga.</span><span class="sxs-lookup"><span data-stu-id="a509b-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a509b-140">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a509b-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="a509b-141">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a509b-141">REST response</span></span>

<span data-ttu-id="a509b-142">Om det lyckas returnerar den här metoden ett kvalificeringsvärde i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="a509b-142">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="a509b-143">Nedan visas ett exempel på **GET-anropet** för en kund med **utbildningskvalifikationen.**</span><span class="sxs-lookup"><span data-stu-id="a509b-143">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a509b-144">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a509b-144">Response success and error codes</span></span>

<span data-ttu-id="a509b-145">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="a509b-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a509b-146">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a509b-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a509b-147">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a509b-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a509b-148">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a509b-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="a509b-149">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="a509b-149">Related articles</span></span>

- [<span data-ttu-id="a509b-150">Uppdatera en kunds kvalificering</span><span class="sxs-lookup"><span data-stu-id="a509b-150">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)