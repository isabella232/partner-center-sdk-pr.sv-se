---
title: Uppdatera en kunds kvalificeringar
description: Uppdaterar en kunds kvalificering asynkront, inklusive adressen som är kopplad till profilen.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572105"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="e9858-103">Uppdatera en kunds kvalificeringar asynkront</span><span class="sxs-lookup"><span data-stu-id="e9858-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="e9858-104">Uppdaterar en kunds kvalificeringar asynkront.</span><span class="sxs-lookup"><span data-stu-id="e9858-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="e9858-105">En partner kan uppdatera en kunds kompetens asynkront till "Utbildning" eller "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="e9858-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="e9858-106">Andra värden, "None" och "Nonprofit", kan inte anges.</span><span class="sxs-lookup"><span data-stu-id="e9858-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9858-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e9858-107">Prerequisites</span></span>

- <span data-ttu-id="e9858-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e9858-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e9858-109">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e9858-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e9858-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9858-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e9858-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e9858-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e9858-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="e9858-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e9858-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="e9858-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e9858-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="e9858-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e9858-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9858-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e9858-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e9858-116">C\#</span></span>

<span data-ttu-id="e9858-117">Om du vill skapa en kunds kvalificering för "Utbildning" skapar du först ett objekt som representerar kvalificeringstypen.</span><span class="sxs-lookup"><span data-stu-id="e9858-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="e9858-118">Anropa sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="e9858-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="e9858-119">Använd sedan egenskapen [**Kvalificering för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) att hämta ett [**ICustomerQualification-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="e9858-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="e9858-120">Anropa eller med `CreateQualifications()` `CreateQualificationsAsync()` objektet för kvalificeringstyp som en indataparameter.</span><span class="sxs-lookup"><span data-stu-id="e9858-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="e9858-121">**Exempel:** [Konsolexempelapp](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="e9858-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="e9858-122">**Project:** SdkSamples-klass: CreateCustomerQualification.cs </span><span class="sxs-lookup"><span data-stu-id="e9858-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="e9858-123">För att uppdatera en kunds kvalificering till **GovernmentCommunityCloud** på en befintlig kund utan kvalificering måste partnern också inkludera kundens [**valideringskod**](utility-resources.md#validationcode).</span><span class="sxs-lookup"><span data-stu-id="e9858-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="e9858-124">Skapa först ett objekt som representerar kvalificeringstypen.</span><span class="sxs-lookup"><span data-stu-id="e9858-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="e9858-125">Anropa sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="e9858-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="e9858-126">Använd sedan egenskapen [**Kvalificering för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) att hämta ett [**ICustomerQualification-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="e9858-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="e9858-127">Anropa eller med `CreateQualifications()` `CreateQualificationsAsync()` kvalificeringstypobjektet och valideringskoden som indataparametrar.</span><span class="sxs-lookup"><span data-stu-id="e9858-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="e9858-128">**Exempel:** [Konsolexempelapp](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="e9858-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="e9858-129">**Project:** SdkSamples-klass: CreateCustomerQualificationWithGCC.cs </span><span class="sxs-lookup"><span data-stu-id="e9858-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e9858-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e9858-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e9858-131">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="e9858-131">Request syntax</span></span>

| <span data-ttu-id="e9858-132">Metod</span><span class="sxs-lookup"><span data-stu-id="e9858-132">Method</span></span>  | <span data-ttu-id="e9858-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e9858-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e9858-134">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="e9858-134">**POST**</span></span> | <span data-ttu-id="e9858-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/kvalificeringar?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e9858-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e9858-136">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e9858-136">URI parameter</span></span>

<span data-ttu-id="e9858-137">Använd följande frågeparameter för att uppdatera kvalificeringen.</span><span class="sxs-lookup"><span data-stu-id="e9858-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="e9858-138">Namn</span><span class="sxs-lookup"><span data-stu-id="e9858-138">Name</span></span>                   | <span data-ttu-id="e9858-139">Typ</span><span class="sxs-lookup"><span data-stu-id="e9858-139">Type</span></span> | <span data-ttu-id="e9858-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e9858-140">Required</span></span> | <span data-ttu-id="e9858-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e9858-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e9858-142">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="e9858-142">**customer-tenant-id**</span></span> | <span data-ttu-id="e9858-143">GUID</span><span class="sxs-lookup"><span data-stu-id="e9858-143">GUID</span></span> | <span data-ttu-id="e9858-144">Yes</span><span class="sxs-lookup"><span data-stu-id="e9858-144">Yes</span></span>      | <span data-ttu-id="e9858-145">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="e9858-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="e9858-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="e9858-146">**validationCode**</span></span>     | <span data-ttu-id="e9858-147">int</span><span class="sxs-lookup"><span data-stu-id="e9858-147">int</span></span>  | <span data-ttu-id="e9858-148">No</span><span class="sxs-lookup"><span data-stu-id="e9858-148">No</span></span>       | <span data-ttu-id="e9858-149">Behövs bara för Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="e9858-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="e9858-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e9858-150">Request headers</span></span>

<span data-ttu-id="e9858-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e9858-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e9858-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e9858-152">Request body</span></span>

<span data-ttu-id="e9858-153">I den här tabellen beskrivs kvalificeringsobjektet i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="e9858-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="e9858-154">Egenskap</span><span class="sxs-lookup"><span data-stu-id="e9858-154">Property</span></span> | <span data-ttu-id="e9858-155">Typ</span><span class="sxs-lookup"><span data-stu-id="e9858-155">Type</span></span> | <span data-ttu-id="e9858-156">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e9858-156">Required</span></span> | <span data-ttu-id="e9858-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e9858-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="e9858-158">Kvalificering</span><span class="sxs-lookup"><span data-stu-id="e9858-158">Qualification</span></span> | <span data-ttu-id="e9858-159">sträng</span><span class="sxs-lookup"><span data-stu-id="e9858-159">string</span></span> | <span data-ttu-id="e9858-160">Yes</span><span class="sxs-lookup"><span data-stu-id="e9858-160">Yes</span></span> | <span data-ttu-id="e9858-161">Strängvärdet från [**uppräkning av CustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)</span><span class="sxs-lookup"><span data-stu-id="e9858-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="e9858-162">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e9858-162">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a><span data-ttu-id="e9858-163">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e9858-163">REST response</span></span>

<span data-ttu-id="e9858-164">Om det lyckas returnerar den här metoden ett kvalificeringsobjekt i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="e9858-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="e9858-165">Nedan visas ett exempel på **POST-anropet** på en kund (med en tidigare kvalificering på **Ingen)** med **utbildningskvalificering.**</span><span class="sxs-lookup"><span data-stu-id="e9858-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e9858-166">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e9858-166">Response success and error codes</span></span>

<span data-ttu-id="e9858-167">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e9858-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e9858-168">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e9858-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e9858-169">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e9858-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e9858-170">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e9858-170">Response example</span></span>

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a><span data-ttu-id="e9858-171">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="e9858-171">Related articles</span></span>

- [<span data-ttu-id="e9858-172">Skaffa en kunds kompetens</span><span class="sxs-lookup"><span data-stu-id="e9858-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="e9858-173">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="e9858-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
