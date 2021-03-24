---
title: Uppdatera en kunds kvalificeringar
description: Uppdaterar en kunds kvalifikationer asynkront, inklusive adressen som är kopplad till profilen.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 7606eeaac4df158ec0fad6ffd4e565bb250f448e
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030614"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="e1a19-103">Uppdatera en kunds kvalifikationer asynkront</span><span class="sxs-lookup"><span data-stu-id="e1a19-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="e1a19-104">Uppdaterar en kunds kvalifikationer asynkront.</span><span class="sxs-lookup"><span data-stu-id="e1a19-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="e1a19-105">En partner kan uppdatera en kunds kvalifikationer asynkront så att de blir "utbildning" eller "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="e1a19-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="e1a19-106">Andra värden, "ingen" och "icke-vinst" kan inte anges.</span><span class="sxs-lookup"><span data-stu-id="e1a19-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1a19-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e1a19-107">Prerequisites</span></span>

- <span data-ttu-id="e1a19-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e1a19-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e1a19-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e1a19-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e1a19-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e1a19-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e1a19-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="e1a19-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e1a19-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="e1a19-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e1a19-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="e1a19-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e1a19-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="e1a19-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e1a19-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e1a19-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e1a19-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e1a19-116">C\#</span></span>

<span data-ttu-id="e1a19-117">Skapa en kunds kvalificering för "utbildning" genom att först skapa ett objekt som representerar kvalificerings typen.</span><span class="sxs-lookup"><span data-stu-id="e1a19-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="e1a19-118">Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID.</span><span class="sxs-lookup"><span data-stu-id="e1a19-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="e1a19-119">Använd sedan egenskapen [**kvalificering**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) för att hämta ett [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) -gränssnitt.</span><span class="sxs-lookup"><span data-stu-id="e1a19-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="e1a19-120">Anropa slutligen `CreateQualifications()` eller `CreateQualificationsAsync()` med kvalificerings typ objektet som en indataparameter.</span><span class="sxs-lookup"><span data-stu-id="e1a19-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationType = { Qualification = "education" };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="e1a19-121">**Exempel**: [app för konsol exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="e1a19-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="e1a19-122">**Projekt**: SdkSamples- **klass**: CreateCustomerQualification. CS</span><span class="sxs-lookup"><span data-stu-id="e1a19-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="e1a19-123">För att kunna uppdatera en kunds kvalificering till **GovernmentCommunityCloud** på en befintlig kund utan kvalificering, måste partnern också inkludera kundens [**ValidationCode**](utility-resources.md#validationcode).</span><span class="sxs-lookup"><span data-stu-id="e1a19-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="e1a19-124">Börja med att skapa ett objekt som representerar kvalificerings typen.</span><span class="sxs-lookup"><span data-stu-id="e1a19-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="e1a19-125">Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID.</span><span class="sxs-lookup"><span data-stu-id="e1a19-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="e1a19-126">Använd sedan egenskapen [**kvalificering**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) för att hämta ett [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) -gränssnitt.</span><span class="sxs-lookup"><span data-stu-id="e1a19-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="e1a19-127">Anropa slutligen `CreateQualifications()` eller `CreateQualificationsAsync()` med kvalificerings typ objekt och validerings koden som indataparametrar.</span><span class="sxs-lookup"><span data-stu-id="e1a19-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="e1a19-128">**Exempel**: [app för konsol exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="e1a19-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="e1a19-129">**Projekt**: SdkSamples- **klass**: CreateCustomerQualificationWithGCC. CS</span><span class="sxs-lookup"><span data-stu-id="e1a19-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e1a19-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e1a19-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e1a19-131">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e1a19-131">Request syntax</span></span>

| <span data-ttu-id="e1a19-132">Metod</span><span class="sxs-lookup"><span data-stu-id="e1a19-132">Method</span></span>  | <span data-ttu-id="e1a19-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e1a19-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e1a19-134">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="e1a19-134">**POST**</span></span> | <span data-ttu-id="e1a19-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? Code = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e1a19-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e1a19-136">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e1a19-136">URI parameter</span></span>

<span data-ttu-id="e1a19-137">Använd följande frågeparameter för att uppdatera kvalificeringen.</span><span class="sxs-lookup"><span data-stu-id="e1a19-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="e1a19-138">Namn</span><span class="sxs-lookup"><span data-stu-id="e1a19-138">Name</span></span>                   | <span data-ttu-id="e1a19-139">Typ</span><span class="sxs-lookup"><span data-stu-id="e1a19-139">Type</span></span> | <span data-ttu-id="e1a19-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e1a19-140">Required</span></span> | <span data-ttu-id="e1a19-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e1a19-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e1a19-142">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="e1a19-142">**customer-tenant-id**</span></span> | <span data-ttu-id="e1a19-143">GUID</span><span class="sxs-lookup"><span data-stu-id="e1a19-143">GUID</span></span> | <span data-ttu-id="e1a19-144">Ja</span><span class="sxs-lookup"><span data-stu-id="e1a19-144">Yes</span></span>      | <span data-ttu-id="e1a19-145">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="e1a19-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="e1a19-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="e1a19-146">**validationCode**</span></span>     | <span data-ttu-id="e1a19-147">int</span><span class="sxs-lookup"><span data-stu-id="e1a19-147">int</span></span>  | <span data-ttu-id="e1a19-148">Inga</span><span class="sxs-lookup"><span data-stu-id="e1a19-148">No</span></span>       | <span data-ttu-id="e1a19-149">Krävs endast för Community-molnet för myndigheter.</span><span class="sxs-lookup"><span data-stu-id="e1a19-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="e1a19-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e1a19-150">Request headers</span></span>

<span data-ttu-id="e1a19-151">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e1a19-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e1a19-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e1a19-152">Request body</span></span>

<span data-ttu-id="e1a19-153">I den här tabellen beskrivs kvalificerings objekt i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="e1a19-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="e1a19-154">Egenskap</span><span class="sxs-lookup"><span data-stu-id="e1a19-154">Property</span></span> | <span data-ttu-id="e1a19-155">Typ</span><span class="sxs-lookup"><span data-stu-id="e1a19-155">Type</span></span> | <span data-ttu-id="e1a19-156">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e1a19-156">Required</span></span> | <span data-ttu-id="e1a19-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e1a19-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="e1a19-158">Kvalificering</span><span class="sxs-lookup"><span data-stu-id="e1a19-158">Qualification</span></span> | <span data-ttu-id="e1a19-159">sträng</span><span class="sxs-lookup"><span data-stu-id="e1a19-159">string</span></span> | <span data-ttu-id="e1a19-160">Ja</span><span class="sxs-lookup"><span data-stu-id="e1a19-160">Yes</span></span> | <span data-ttu-id="e1a19-161">Strängvärdet från [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) -uppräkningen.</span><span class="sxs-lookup"><span data-stu-id="e1a19-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="e1a19-162">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e1a19-162">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e1a19-163">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e1a19-163">REST response</span></span>

<span data-ttu-id="e1a19-164">Om det lyckas returnerar den här metoden ett kvalificerings objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="e1a19-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="e1a19-165">Nedan visas ett exempel på **post** anropet på en kund (med ett tidigare kvalificerings **ingen**) med **utbildnings** kompetensen.</span><span class="sxs-lookup"><span data-stu-id="e1a19-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e1a19-166">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e1a19-166">Response success and error codes</span></span>

<span data-ttu-id="e1a19-167">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e1a19-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e1a19-168">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e1a19-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e1a19-169">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e1a19-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e1a19-170">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e1a19-170">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="e1a19-171">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="e1a19-171">Related articles</span></span>

- [<span data-ttu-id="e1a19-172">Få en kunds kompetens</span><span class="sxs-lookup"><span data-stu-id="e1a19-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="e1a19-173">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="e1a19-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
