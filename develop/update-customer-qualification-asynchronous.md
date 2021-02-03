---
title: Uppdatera en kunds kompetens
description: Lär dig hur du uppdaterar en kunds kvalifikationer via asynkron gallring eller först konsumentsajter, inklusive adressen som är kopplad till profilen.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: e0390e8a9c2a277dcb9e18b026f12625400ae176
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770201"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="01386-103">Uppdatera en kunds kvalifikationer asynkront</span><span class="sxs-lookup"><span data-stu-id="01386-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="01386-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="01386-104">**Applies To**</span></span>

- <span data-ttu-id="01386-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="01386-105">Partner Center</span></span>

<span data-ttu-id="01386-106">Lär dig hur du uppdaterar en kunds kvalifikationer asynkront via API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="01386-106">Learn how to update a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="01386-107">Information om hur du gör detta synkront finns i [Uppdatera en kunds kvalificering via synkron verifiering](update-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="01386-107">To learn how to do this synchronously, see [Update a customer's qualification via synchronous validation](update-customer-qualification-synchronous.md).</span></span>

<span data-ttu-id="01386-108">En partner kan uppdatera en kunds kvalifikationer asynkront så att de blir "utbildning" eller "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="01386-108">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="01386-109">Andra värden, "ingen" och "icke-vinst" kan inte anges.</span><span class="sxs-lookup"><span data-stu-id="01386-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01386-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="01386-110">Prerequisites</span></span>

- <span data-ttu-id="01386-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="01386-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="01386-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="01386-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="01386-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="01386-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="01386-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="01386-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="01386-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="01386-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="01386-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="01386-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="01386-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="01386-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="01386-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="01386-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="01386-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="01386-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="01386-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="01386-120">Request syntax</span></span>

| <span data-ttu-id="01386-121">Metod</span><span class="sxs-lookup"><span data-stu-id="01386-121">Method</span></span>  | <span data-ttu-id="01386-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="01386-122">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="01386-123">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="01386-123">**POST**</span></span> | <span data-ttu-id="01386-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? Code = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="01386-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="01386-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="01386-125">URI parameter</span></span>

<span data-ttu-id="01386-126">Använd följande frågeparameter för att uppdatera kvalificeringen.</span><span class="sxs-lookup"><span data-stu-id="01386-126">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="01386-127">Namn</span><span class="sxs-lookup"><span data-stu-id="01386-127">Name</span></span>                   | <span data-ttu-id="01386-128">Typ</span><span class="sxs-lookup"><span data-stu-id="01386-128">Type</span></span> | <span data-ttu-id="01386-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="01386-129">Required</span></span> | <span data-ttu-id="01386-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="01386-130">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="01386-131">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="01386-131">**customer-tenant-id**</span></span> | <span data-ttu-id="01386-132">GUID</span><span class="sxs-lookup"><span data-stu-id="01386-132">GUID</span></span> | <span data-ttu-id="01386-133">Yes</span><span class="sxs-lookup"><span data-stu-id="01386-133">Yes</span></span>      | <span data-ttu-id="01386-134">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="01386-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="01386-135">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="01386-135">**validationCode**</span></span>     | <span data-ttu-id="01386-136">int</span><span class="sxs-lookup"><span data-stu-id="01386-136">int</span></span>  | <span data-ttu-id="01386-137">No</span><span class="sxs-lookup"><span data-stu-id="01386-137">No</span></span>       | <span data-ttu-id="01386-138">Krävs endast för Community-molnet för myndigheter.</span><span class="sxs-lookup"><span data-stu-id="01386-138">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="01386-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="01386-139">Request headers</span></span>

<span data-ttu-id="01386-140">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="01386-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="01386-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="01386-141">Request body</span></span>

<span data-ttu-id="01386-142">Heltal svärdet från [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) -uppräkningen.</span><span class="sxs-lookup"><span data-stu-id="01386-142">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="01386-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="01386-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="01386-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="01386-144">REST response</span></span>

<span data-ttu-id="01386-145">Om det lyckas returnerar den här metoden ett kvalificerings objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="01386-145">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="01386-146">Nedan visas ett exempel på **post** anropet på en kund (med ett tidigare kvalificerings **ingen**) med **utbildnings** kompetensen.</span><span class="sxs-lookup"><span data-stu-id="01386-146">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="01386-147">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="01386-147">Response success and error codes</span></span>

<span data-ttu-id="01386-148">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="01386-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="01386-149">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="01386-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="01386-150">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="01386-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="01386-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="01386-151">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="01386-152">Relaterade artiklar</span><span class="sxs-lookup"><span data-stu-id="01386-152">Related articles</span></span>

- [<span data-ttu-id="01386-153">Få en kunds kompetens</span><span class="sxs-lookup"><span data-stu-id="01386-153">Get a customer's qualifications</span></span>](get-a-customer-s-qualifications.md)
- [<span data-ttu-id="01386-154">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="01386-154">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)