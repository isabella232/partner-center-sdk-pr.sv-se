---
title: Hämta kundens direktsigneringsstatus för Microsoft-kundavtal.
description: Du kan använda resursen DirectSignedCustomerAgreementStatus för att hämta status för en kunds direktsignering (direkt godkännande) av Microsoft-kundavtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a17775614b4eb328514b2b32b4cac1e513019cff
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549186"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="c6ecf-103">Hämta status för en kunds direktsignering (direkt godkännande) av Microsoft-kundavtal</span><span class="sxs-lookup"><span data-stu-id="c6ecf-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="c6ecf-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="c6ecf-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="c6ecf-105">**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c6ecf-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c6ecf-106">Resursen **DirectSignedCustomerAgreementStatus** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="c6ecf-107">Den här artikeln förklarar hur du kan hämta status för en kunds direkta godkännande av Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-107">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6ecf-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c6ecf-108">Prerequisites</span></span>

- <span data-ttu-id="c6ecf-109">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c6ecf-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c6ecf-110">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c6ecf-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c6ecf-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c6ecf-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="c6ecf-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c6ecf-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c6ecf-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c6ecf-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c6ecf-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c6ecf-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c6ecf-117">C\#</span><span class="sxs-lookup"><span data-stu-id="c6ecf-117">C\#</span></span>

<span data-ttu-id="c6ecf-118">Om du vill hämta status för en kunds direkta godkännande av Microsoft-kundavtal anropar du [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-118">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="c6ecf-119">Använd sedan egenskapen [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) för att hämta ett [**ICustomerAgreementCollection-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection)</span><span class="sxs-lookup"><span data-stu-id="c6ecf-119">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="c6ecf-120">Anropa eller `GetDirectSignedCustomerAgreementStatus()` för att hämta `GetDirectSignedCustomerAgreementStatusAsync()` statusen.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-120">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="c6ecf-121">**Exempel:** [Konsolexempelapp](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="c6ecf-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="c6ecf-122">**Project:** SdkSamples-klass: GetDirectSignedCustomerAgreementStatus.cs </span><span class="sxs-lookup"><span data-stu-id="c6ecf-122">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c6ecf-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c6ecf-123">REST request</span></span>

<span data-ttu-id="c6ecf-124">Om du vill hämta status för en kunds direkta godkännande av Microsoft-kundavtal skapar du en REST-begäran för att hämta [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) för kunden.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-124">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c6ecf-125">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="c6ecf-125">Request syntax</span></span>

<span data-ttu-id="c6ecf-126">Använd följande syntax för begäran:</span><span class="sxs-lookup"><span data-stu-id="c6ecf-126">Use the following request syntax:</span></span>

| <span data-ttu-id="c6ecf-127">Metod</span><span class="sxs-lookup"><span data-stu-id="c6ecf-127">Method</span></span> | <span data-ttu-id="c6ecf-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c6ecf-128">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c6ecf-129">GET</span><span class="sxs-lookup"><span data-stu-id="c6ecf-129">GET</span></span>    | <span data-ttu-id="c6ecf-130">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c6ecf-130">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="c6ecf-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="c6ecf-131">URI parameters</span></span>

<span data-ttu-id="c6ecf-132">Du kan använda följande URI-parametrar med din begäran:</span><span class="sxs-lookup"><span data-stu-id="c6ecf-132">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="c6ecf-133">Namn</span><span class="sxs-lookup"><span data-stu-id="c6ecf-133">Name</span></span>             | <span data-ttu-id="c6ecf-134">Typ</span><span class="sxs-lookup"><span data-stu-id="c6ecf-134">Type</span></span> | <span data-ttu-id="c6ecf-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c6ecf-135">Required</span></span> | <span data-ttu-id="c6ecf-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c6ecf-136">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="c6ecf-137">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="c6ecf-137">customer-tenant-id</span></span> | <span data-ttu-id="c6ecf-138">GUID</span><span class="sxs-lookup"><span data-stu-id="c6ecf-138">GUID</span></span> | <span data-ttu-id="c6ecf-139">Ja</span><span class="sxs-lookup"><span data-stu-id="c6ecf-139">Yes</span></span> | <span data-ttu-id="c6ecf-140">Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange klient-ID för en kund.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-140">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c6ecf-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c6ecf-141">Request headers</span></span>

<span data-ttu-id="c6ecf-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c6ecf-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c6ecf-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="c6ecf-143">Request body</span></span>

<span data-ttu-id="c6ecf-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c6ecf-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="c6ecf-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="c6ecf-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c6ecf-146">REST response</span></span>

<span data-ttu-id="c6ecf-147">Om det lyckas returnerar den här metoden en [ **DirectSignedCustomerAgreementStatus-resurs**](./customer-agreement-direct-sign-status-resource.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-147">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="c6ecf-148">Resursen har en **isSigned-egenskap** som anger kundens status för direktsignering (direktgodkännande).</span><span class="sxs-lookup"><span data-stu-id="c6ecf-148">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="c6ecf-149">Värdet true **anger** att avtalet har signerats (godkänts) direkt av kunden.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-149">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="c6ecf-150">Värdet false **anger** att avtalet inte har *signerats* (godkänts) direkt av kunden.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-150">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c6ecf-151">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c6ecf-151">Response success and error codes</span></span>

<span data-ttu-id="c6ecf-152">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="c6ecf-153">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c6ecf-154">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c6ecf-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c6ecf-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="c6ecf-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
