---
title: Uppdatera en kunds kvalificeringar
description: Lär dig hur du uppdaterar en kunds kvalifikationer via asynkron gallring eller först konsumentsajter, inklusive adressen som är kopplad till profilen.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 703585eeaba93b6d7a510a3174a78a28f22e1510
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711941"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="9e376-103">Uppdatera en kunds kvalifikationer asynkront</span><span class="sxs-lookup"><span data-stu-id="9e376-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="9e376-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="9e376-104">**Applies To**</span></span>

- <span data-ttu-id="9e376-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9e376-105">Partner Center</span></span>

<span data-ttu-id="9e376-106">Lär dig hur du uppdaterar en kunds kvalifikationer asynkront via API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="9e376-106">Learn how to update a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="9e376-107">Information om hur du gör detta synkront finns i [Uppdatera en kunds kvalificering via synkron verifiering](update-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="9e376-107">To learn how to do this synchronously, see [Update a customer's qualification via synchronous validation](update-customer-qualification-synchronous.md).</span></span>

<span data-ttu-id="9e376-108">En partner kan uppdatera en kunds kvalifikationer asynkront så att de blir "utbildning" eller "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="9e376-108">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="9e376-109">Andra värden, "ingen" och "icke-vinst" kan inte anges.</span><span class="sxs-lookup"><span data-stu-id="9e376-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e376-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9e376-110">Prerequisites</span></span>

- <span data-ttu-id="9e376-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9e376-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e376-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="9e376-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9e376-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e376-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9e376-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="9e376-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9e376-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="9e376-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9e376-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="9e376-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9e376-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="9e376-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9e376-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e376-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="9e376-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9e376-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e376-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="9e376-120">Request syntax</span></span>

| <span data-ttu-id="9e376-121">Metod</span><span class="sxs-lookup"><span data-stu-id="9e376-121">Method</span></span>  | <span data-ttu-id="9e376-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9e376-122">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e376-123">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="9e376-123">**POST**</span></span> | <span data-ttu-id="9e376-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? Code = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="9e376-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9e376-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="9e376-125">URI parameter</span></span>

<span data-ttu-id="9e376-126">Använd följande frågeparameter för att uppdatera kvalificeringen.</span><span class="sxs-lookup"><span data-stu-id="9e376-126">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="9e376-127">Namn</span><span class="sxs-lookup"><span data-stu-id="9e376-127">Name</span></span>                   | <span data-ttu-id="9e376-128">Typ</span><span class="sxs-lookup"><span data-stu-id="9e376-128">Type</span></span> | <span data-ttu-id="9e376-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="9e376-129">Required</span></span> | <span data-ttu-id="9e376-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="9e376-130">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e376-131">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="9e376-131">**customer-tenant-id**</span></span> | <span data-ttu-id="9e376-132">GUID</span><span class="sxs-lookup"><span data-stu-id="9e376-132">GUID</span></span> | <span data-ttu-id="9e376-133">Ja</span><span class="sxs-lookup"><span data-stu-id="9e376-133">Yes</span></span>      | <span data-ttu-id="9e376-134">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="9e376-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="9e376-135">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="9e376-135">**validationCode**</span></span>     | <span data-ttu-id="9e376-136">int</span><span class="sxs-lookup"><span data-stu-id="9e376-136">int</span></span>  | <span data-ttu-id="9e376-137">Inga</span><span class="sxs-lookup"><span data-stu-id="9e376-137">No</span></span>       | <span data-ttu-id="9e376-138">Krävs endast för Community-molnet för myndigheter.</span><span class="sxs-lookup"><span data-stu-id="9e376-138">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="9e376-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="9e376-139">Request headers</span></span>

<span data-ttu-id="9e376-140">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9e376-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e376-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9e376-141">Request body</span></span>

<span data-ttu-id="9e376-142">Heltal svärdet från [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) -uppräkningen.</span><span class="sxs-lookup"><span data-stu-id="9e376-142">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="9e376-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9e376-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="9e376-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9e376-144">REST response</span></span>

<span data-ttu-id="9e376-145">Om det lyckas returnerar den här metoden ett kvalificerings objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="9e376-145">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="9e376-146">Nedan visas ett exempel på **post** anropet på en kund (med ett tidigare kvalificerings **ingen**) med **utbildnings** kompetensen.</span><span class="sxs-lookup"><span data-stu-id="9e376-146">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e376-147">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9e376-147">Response success and error codes</span></span>

<span data-ttu-id="9e376-148">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="9e376-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e376-149">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9e376-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e376-150">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9e376-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9e376-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9e376-151">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="9e376-152">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="9e376-152">Related articles</span></span>

- [<span data-ttu-id="9e376-153">Få en kunds kompetens</span><span class="sxs-lookup"><span data-stu-id="9e376-153">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="9e376-154">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="9e376-154">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)