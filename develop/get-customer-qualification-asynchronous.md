---
title: Få en kunds kompetens
description: Lär dig hur du använder asynkron verifiering för att få en kund kvalificering via API för partner Center. Partner kan använda detta för att validera utbildnings kunder.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 09801792c059873b9f6b842e99286eda09d38b1a
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030579"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="8e852-104">Få en kund kvalificering asynkront</span><span class="sxs-lookup"><span data-stu-id="8e852-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="8e852-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="8e852-105">**Applies To**</span></span>

- <span data-ttu-id="8e852-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="8e852-106">Partner Center</span></span>

<span data-ttu-id="8e852-107">Så här får du en kunds kvalifikationer asynkront.</span><span class="sxs-lookup"><span data-stu-id="8e852-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e852-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8e852-108">Prerequisites</span></span>

- <span data-ttu-id="8e852-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8e852-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8e852-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8e852-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8e852-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8e852-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8e852-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="8e852-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8e852-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="8e852-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8e852-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="8e852-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8e852-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="8e852-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8e852-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8e852-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="8e852-117">C\#</span><span class="sxs-lookup"><span data-stu-id="8e852-117">C\#</span></span>

<span data-ttu-id="8e852-118">För att få en kunds kvalifikationer, anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID.</span><span class="sxs-lookup"><span data-stu-id="8e852-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="8e852-119">Använd sedan egenskapen [**kvalificering**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) för att hämta ett [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) -gränssnitt.</span><span class="sxs-lookup"><span data-stu-id="8e852-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="8e852-120">Till sist kan du ringa `GetQualifications()` eller `GetQualificationsAsync()` Hämta kundens kvalifikationer.</span><span class="sxs-lookup"><span data-stu-id="8e852-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="8e852-121">**Exempel**: [app för konsol exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="8e852-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="8e852-122">**Projekt**: SdkSamples- **klass**: GetCustomerQualifications. CS</span><span class="sxs-lookup"><span data-stu-id="8e852-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8e852-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8e852-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8e852-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="8e852-124">Request syntax</span></span>

| <span data-ttu-id="8e852-125">Metod</span><span class="sxs-lookup"><span data-stu-id="8e852-125">Method</span></span>  | <span data-ttu-id="8e852-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8e852-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8e852-127">**TA**</span><span class="sxs-lookup"><span data-stu-id="8e852-127">**GET**</span></span> | <span data-ttu-id="8e852-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="8e852-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8e852-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="8e852-129">URI parameter</span></span>

<span data-ttu-id="8e852-130">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta all kvalificering.</span><span class="sxs-lookup"><span data-stu-id="8e852-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="8e852-131">Namn</span><span class="sxs-lookup"><span data-stu-id="8e852-131">Name</span></span>               | <span data-ttu-id="8e852-132">Typ</span><span class="sxs-lookup"><span data-stu-id="8e852-132">Type</span></span>   | <span data-ttu-id="8e852-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8e852-133">Required</span></span> | <span data-ttu-id="8e852-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8e852-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8e852-135">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="8e852-135">**customer-tenant-id**</span></span> | <span data-ttu-id="8e852-136">sträng</span><span class="sxs-lookup"><span data-stu-id="8e852-136">string</span></span> | <span data-ttu-id="8e852-137">Ja</span><span class="sxs-lookup"><span data-stu-id="8e852-137">Yes</span></span>      | <span data-ttu-id="8e852-138">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="8e852-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8e852-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8e852-139">Request headers</span></span>

<span data-ttu-id="8e852-140">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8e852-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8e852-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8e852-141">Request body</span></span>

<span data-ttu-id="8e852-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="8e852-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8e852-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8e852-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="8e852-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8e852-144">REST response</span></span>

<span data-ttu-id="8e852-145">Om det lyckas returnerar den här metoden en samling kvalifikationer i svars texten.</span><span class="sxs-lookup"><span data-stu-id="8e852-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="8e852-146">Nedan visas exempel på **Get** -anrop på en kund med **utbildnings** kompetensen.</span><span class="sxs-lookup"><span data-stu-id="8e852-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8e852-147">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8e852-147">Response success and error codes</span></span>

<span data-ttu-id="8e852-148">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="8e852-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8e852-149">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8e852-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8e852-150">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8e852-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="8e852-151">Svars exempel</span><span class="sxs-lookup"><span data-stu-id="8e852-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="8e852-152">Godkända</span><span class="sxs-lookup"><span data-stu-id="8e852-152">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="8e852-153">Under granskning</span><span class="sxs-lookup"><span data-stu-id="8e852-153">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="8e852-154">Nekad</span><span class="sxs-lookup"><span data-stu-id="8e852-154">Denied</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="8e852-155">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="8e852-155">Related articles</span></span>

- [<span data-ttu-id="8e852-156">Uppdatera en kunds kvalificeringar</span><span class="sxs-lookup"><span data-stu-id="8e852-156">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
