---
title: Uppdatera en kunds kvalificering
description: Lär dig hur du uppdaterar en kunds kvalifikationer via synkron gallring eller först konsumentsajter, inklusive adressen som är kopplad till profilen.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c202d95beab771241a9665243be5f08ab6f82fd5
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711975"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="2761e-103">Uppdatera en kunds kvalificering via synkron verifiering</span><span class="sxs-lookup"><span data-stu-id="2761e-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="2761e-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="2761e-104">**Applies To**</span></span>

- <span data-ttu-id="2761e-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2761e-105">Partner Center</span></span>

<span data-ttu-id="2761e-106">Lär dig hur du uppdaterar en kunds kvalifikationer synkront via API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2761e-106">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="2761e-107">Information om hur du gör detta asynkront finns i [Uppdatera en kunds kvalificering via asynkron verifiering](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="2761e-107">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="2761e-108">En partner kan uppdatera en kunds kvalificering som "utbildning" eller "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="2761e-108">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="2761e-109">Andra värden, "ingen" och "icke-vinst" kan inte anges.</span><span class="sxs-lookup"><span data-stu-id="2761e-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2761e-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2761e-110">Prerequisites</span></span>

- <span data-ttu-id="2761e-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2761e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2761e-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2761e-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2761e-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2761e-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2761e-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2761e-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2761e-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2761e-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2761e-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2761e-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2761e-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2761e-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2761e-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2761e-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2761e-119">C\#</span><span class="sxs-lookup"><span data-stu-id="2761e-119">C\#</span></span>

<span data-ttu-id="2761e-120">Om du vill uppdatera en kunds kvalificering till "utbildning" anropar du **[Update/dotNet/API/Microsoft. Store. Partnercenter. kvalificering. icustomerqualification. Update)** på en befintlig  [**kund**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span><span class="sxs-lookup"><span data-stu-id="2761e-120">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="2761e-121">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2761e-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2761e-122">**Projekt**: PartnerSDK. FeatureSamples- **klass**: CustomerQualificationOperations. CS</span><span class="sxs-lookup"><span data-stu-id="2761e-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="2761e-123">För att uppdatera en kunds kvalificering till **GovernmentCommunityCloud** på en befintlig kund utan kvalificering.</span><span class="sxs-lookup"><span data-stu-id="2761e-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification.</span></span>  <span data-ttu-id="2761e-124">Partnern måste också innehålla kundens [**ValidationCode**](utility-resources.md#validationcode).</span><span class="sxs-lookup"><span data-stu-id="2761e-124">The partner is also are required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="2761e-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2761e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2761e-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2761e-126">Request syntax</span></span>

| <span data-ttu-id="2761e-127">Metod</span><span class="sxs-lookup"><span data-stu-id="2761e-127">Method</span></span>  | <span data-ttu-id="2761e-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2761e-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2761e-129">**PUT**</span><span class="sxs-lookup"><span data-stu-id="2761e-129">**PUT**</span></span> | <span data-ttu-id="2761e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualification? Code = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2761e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2761e-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2761e-131">URI parameter</span></span>

<span data-ttu-id="2761e-132">Använd följande frågeparameter för att uppdatera kvalificeringen.</span><span class="sxs-lookup"><span data-stu-id="2761e-132">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="2761e-133">Namn</span><span class="sxs-lookup"><span data-stu-id="2761e-133">Name</span></span>                   | <span data-ttu-id="2761e-134">Typ</span><span class="sxs-lookup"><span data-stu-id="2761e-134">Type</span></span> | <span data-ttu-id="2761e-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2761e-135">Required</span></span> | <span data-ttu-id="2761e-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2761e-136">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2761e-137">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="2761e-137">**customer-tenant-id**</span></span> | <span data-ttu-id="2761e-138">GUID</span><span class="sxs-lookup"><span data-stu-id="2761e-138">GUID</span></span> | <span data-ttu-id="2761e-139">Ja</span><span class="sxs-lookup"><span data-stu-id="2761e-139">Yes</span></span>      | <span data-ttu-id="2761e-140">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="2761e-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="2761e-141">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="2761e-141">**validationCode**</span></span>     | <span data-ttu-id="2761e-142">int</span><span class="sxs-lookup"><span data-stu-id="2761e-142">int</span></span>  | <span data-ttu-id="2761e-143">Inga</span><span class="sxs-lookup"><span data-stu-id="2761e-143">No</span></span>       | <span data-ttu-id="2761e-144">Krävs endast för Community-molnet för myndigheter.</span><span class="sxs-lookup"><span data-stu-id="2761e-144">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="2761e-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2761e-145">Request headers</span></span>

<span data-ttu-id="2761e-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2761e-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2761e-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2761e-147">Request body</span></span>

<span data-ttu-id="2761e-148">Heltal svärdet från [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) -uppräkningen.</span><span class="sxs-lookup"><span data-stu-id="2761e-148">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="2761e-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2761e-149">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="2761e-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2761e-150">REST response</span></span>

<span data-ttu-id="2761e-151">Om det lyckas returnerar den här metoden en uppdaterad [**kvalificerings**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) egenskap i svars texten.</span><span class="sxs-lookup"><span data-stu-id="2761e-151">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2761e-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2761e-152">Response success and error codes</span></span>

<span data-ttu-id="2761e-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2761e-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2761e-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2761e-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2761e-155">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2761e-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2761e-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2761e-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="2761e-157">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="2761e-157">Related articles</span></span>

- [<span data-ttu-id="2761e-158">Hämta en kunds kvalificering</span><span class="sxs-lookup"><span data-stu-id="2761e-158">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="2761e-159">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="2761e-159">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)