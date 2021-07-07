---
title: Uppdatera en kunds kvalificering
description: Lär dig hur du uppdaterar en kunds kompetens via synkron kontroll eller kontroll, inklusive adressen som är associerad med profilen.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446657"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="64244-103">Uppdatera en kunds kvalificering via synkron validering</span><span class="sxs-lookup"><span data-stu-id="64244-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="64244-104">Lär dig hur du uppdaterar en kunds kvalificeringar synkront via Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="64244-104">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="64244-105">Information om hur du gör detta asynkront finns i [Uppdatera en kunds kvalificering via asynkron validering](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="64244-105">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="64244-106">En partner kan uppdatera en kunds kvalificering till "Education" eller "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="64244-106">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="64244-107">Andra värden, "None" och "Nonprofit", kan inte anges.</span><span class="sxs-lookup"><span data-stu-id="64244-107">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64244-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="64244-108">Prerequisites</span></span>

- <span data-ttu-id="64244-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="64244-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="64244-110">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="64244-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="64244-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="64244-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="64244-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="64244-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="64244-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="64244-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="64244-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="64244-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="64244-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="64244-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="64244-116">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="64244-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="64244-117">C\#</span><span class="sxs-lookup"><span data-stu-id="64244-117">C\#</span></span>

<span data-ttu-id="64244-118">Om du vill uppdatera en kunds kvalificering till "Education" anropar du **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** på en  [**befintlig kund**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span><span class="sxs-lookup"><span data-stu-id="64244-118">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="64244-119">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="64244-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="64244-120">**Project:** PartnerSDK.FeatureSamples-klass: CustomerQualificationOperations.cs </span><span class="sxs-lookup"><span data-stu-id="64244-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="64244-121">För att uppdatera en kunds kvalificering **till GovernmentCommunityCloud** på en befintlig kund utan kvalificering måste partnern inkludera kundens [**valideringskod.**](utility-resources.md#validationcode)</span><span class="sxs-lookup"><span data-stu-id="64244-121">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="64244-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="64244-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="64244-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="64244-123">Request syntax</span></span>

| <span data-ttu-id="64244-124">Metod</span><span class="sxs-lookup"><span data-stu-id="64244-124">Method</span></span>  | <span data-ttu-id="64244-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="64244-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="64244-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="64244-126">**PUT**</span></span> | <span data-ttu-id="64244-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="64244-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="64244-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="64244-128">URI parameter</span></span>

<span data-ttu-id="64244-129">Använd följande frågeparameter för att uppdatera kvalificeringen.</span><span class="sxs-lookup"><span data-stu-id="64244-129">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="64244-130">Namn</span><span class="sxs-lookup"><span data-stu-id="64244-130">Name</span></span>                   | <span data-ttu-id="64244-131">Typ</span><span class="sxs-lookup"><span data-stu-id="64244-131">Type</span></span> | <span data-ttu-id="64244-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="64244-132">Required</span></span> | <span data-ttu-id="64244-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="64244-133">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="64244-134">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="64244-134">**customer-tenant-id**</span></span> | <span data-ttu-id="64244-135">GUID</span><span class="sxs-lookup"><span data-stu-id="64244-135">GUID</span></span> | <span data-ttu-id="64244-136">Ja</span><span class="sxs-lookup"><span data-stu-id="64244-136">Yes</span></span>      | <span data-ttu-id="64244-137">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="64244-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="64244-138">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="64244-138">**validationCode**</span></span>     | <span data-ttu-id="64244-139">int</span><span class="sxs-lookup"><span data-stu-id="64244-139">int</span></span>  | <span data-ttu-id="64244-140">Inga</span><span class="sxs-lookup"><span data-stu-id="64244-140">No</span></span>       | <span data-ttu-id="64244-141">Behövs bara för Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="64244-141">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="64244-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="64244-142">Request headers</span></span>

<span data-ttu-id="64244-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="64244-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="64244-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="64244-144">Request body</span></span>

<span data-ttu-id="64244-145">Heltalsvärdet från [**CustomerQualification-uppräkning.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)</span><span class="sxs-lookup"><span data-stu-id="64244-145">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="64244-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="64244-146">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="64244-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="64244-147">REST response</span></span>

<span data-ttu-id="64244-148">Om det lyckas returnerar den här metoden den uppdaterade kvalificeringsegenskapen i svarstexten. [](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification)</span><span class="sxs-lookup"><span data-stu-id="64244-148">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="64244-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="64244-149">Response success and error codes</span></span>

<span data-ttu-id="64244-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="64244-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="64244-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="64244-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="64244-152">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="64244-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="64244-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="64244-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="64244-154">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="64244-154">Related articles</span></span>

- [<span data-ttu-id="64244-155">Hämta en kunds kvalificering</span><span class="sxs-lookup"><span data-stu-id="64244-155">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="64244-156">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="64244-156">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
