---
title: Hämta en kunds kvalificering
description: Lär dig hur du använder synkron verifiering för att få en kund kvalificering via API för partner Center. Partner kan använda detta för att validera utbildnings kunder.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e39ace3b598736abed6ab22021a8b93d473486a3
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711905"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="e9af5-104">Få en kund kvalificering via synkron verifiering</span><span class="sxs-lookup"><span data-stu-id="e9af5-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="e9af5-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="e9af5-105">**Applies To**</span></span>

- <span data-ttu-id="e9af5-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e9af5-106">Partner Center</span></span>

<span data-ttu-id="e9af5-107">Lär dig hur du får en kund kvalificering synkront via API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="e9af5-107">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="e9af5-108">Information om hur du gör detta asynkront finns i [Hämta en kunds kvalificering via asynkron verifiering](get-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="e9af5-108">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9af5-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e9af5-109">Prerequisites</span></span>

- <span data-ttu-id="e9af5-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e9af5-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e9af5-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e9af5-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e9af5-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9af5-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e9af5-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="e9af5-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e9af5-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="e9af5-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e9af5-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="e9af5-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e9af5-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="e9af5-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e9af5-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9af5-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e9af5-118">C\#</span><span class="sxs-lookup"><span data-stu-id="e9af5-118">C\#</span></span>

<span data-ttu-id="e9af5-119">För att få en kund kvalificering kan du anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID.</span><span class="sxs-lookup"><span data-stu-id="e9af5-119">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="e9af5-120">Använd sedan egenskapen [**kvalificering**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) för att hämta ett [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) -gränssnitt.</span><span class="sxs-lookup"><span data-stu-id="e9af5-120">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="e9af5-121">Anropa slutligen [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta kundens kvalificering.</span><span class="sxs-lookup"><span data-stu-id="e9af5-121">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="e9af5-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e9af5-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e9af5-123">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e9af5-123">Request syntax</span></span>

| <span data-ttu-id="e9af5-124">Metod</span><span class="sxs-lookup"><span data-stu-id="e9af5-124">Method</span></span>  | <span data-ttu-id="e9af5-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e9af5-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e9af5-126">**TA**</span><span class="sxs-lookup"><span data-stu-id="e9af5-126">**GET**</span></span> | <span data-ttu-id="e9af5-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualification http/1.1</span><span class="sxs-lookup"><span data-stu-id="e9af5-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e9af5-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e9af5-128">URI parameter</span></span>

<span data-ttu-id="e9af5-129">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta all kvalificering.</span><span class="sxs-lookup"><span data-stu-id="e9af5-129">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="e9af5-130">Namn</span><span class="sxs-lookup"><span data-stu-id="e9af5-130">Name</span></span>               | <span data-ttu-id="e9af5-131">Typ</span><span class="sxs-lookup"><span data-stu-id="e9af5-131">Type</span></span>   | <span data-ttu-id="e9af5-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e9af5-132">Required</span></span> | <span data-ttu-id="e9af5-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e9af5-133">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e9af5-134">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="e9af5-134">**customer-tenant-id**</span></span> | <span data-ttu-id="e9af5-135">sträng</span><span class="sxs-lookup"><span data-stu-id="e9af5-135">string</span></span> | <span data-ttu-id="e9af5-136">Ja</span><span class="sxs-lookup"><span data-stu-id="e9af5-136">Yes</span></span>      | <span data-ttu-id="e9af5-137">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="e9af5-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e9af5-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e9af5-138">Request headers</span></span>

<span data-ttu-id="e9af5-139">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e9af5-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e9af5-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e9af5-140">Request body</span></span>

<span data-ttu-id="e9af5-141">Inga.</span><span class="sxs-lookup"><span data-stu-id="e9af5-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e9af5-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e9af5-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="e9af5-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e9af5-143">REST response</span></span>

<span data-ttu-id="e9af5-144">Om det lyckas returnerar den här metoden ett kvalificerings värde i svars texten.</span><span class="sxs-lookup"><span data-stu-id="e9af5-144">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="e9af5-145">Nedan visas ett exempel på **Get** -anropet på en kund med **utbildnings** kompetensen.</span><span class="sxs-lookup"><span data-stu-id="e9af5-145">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e9af5-146">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e9af5-146">Response success and error codes</span></span>

<span data-ttu-id="e9af5-147">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e9af5-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e9af5-148">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e9af5-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e9af5-149">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e9af5-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e9af5-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e9af5-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="e9af5-151">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="e9af5-151">Related articles</span></span>

- [<span data-ttu-id="e9af5-152">Uppdatera en kunds kvalificering</span><span class="sxs-lookup"><span data-stu-id="e9af5-152">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)