---
title: Hämta kundens direkta signerings status för Microsofts kund avtal.
description: Du kan använda DirectSignedCustomerAgreementStatus-resursen för att hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030578"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="cb07d-103">Hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal</span><span class="sxs-lookup"><span data-stu-id="cb07d-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="cb07d-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="cb07d-104">**Applies to:**</span></span>

- <span data-ttu-id="cb07d-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="cb07d-105">Partner Center</span></span>

<span data-ttu-id="cb07d-106">**DirectSignedCustomerAgreementStatus** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="cb07d-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="cb07d-107">Den här resursen är *inte tillämplig* för:</span><span class="sxs-lookup"><span data-stu-id="cb07d-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="cb07d-108">Partnercenter drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cb07d-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cb07d-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="cb07d-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cb07d-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cb07d-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cb07d-111">Den här artikeln förklarar hur du kan hämta statusen för en kunds direkta godkännande av Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="cb07d-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb07d-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cb07d-112">Prerequisites</span></span>

- <span data-ttu-id="cb07d-113">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cb07d-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cb07d-114">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cb07d-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cb07d-115">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb07d-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cb07d-116">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="cb07d-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cb07d-117">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="cb07d-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cb07d-118">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="cb07d-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cb07d-119">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="cb07d-119">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cb07d-120">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb07d-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="cb07d-121">C\#</span><span class="sxs-lookup"><span data-stu-id="cb07d-121">C\#</span></span>

<span data-ttu-id="cb07d-122">För att hämta statusen för en kunds direkta godkännande av Microsofts kund avtal, anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID.</span><span class="sxs-lookup"><span data-stu-id="cb07d-122">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="cb07d-123">Använd sedan egenskapen [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) för att hämta ett [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) -gränssnitt.</span><span class="sxs-lookup"><span data-stu-id="cb07d-123">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="cb07d-124">Till sist anropa `GetDirectSignedCustomerAgreementStatus()` eller `GetDirectSignedCustomerAgreementStatusAsync()` för att hämta statusen.</span><span class="sxs-lookup"><span data-stu-id="cb07d-124">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="cb07d-125">**Exempel**: [app för konsol exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="cb07d-125">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="cb07d-126">**Projekt**: SdkSamples- **klass**: GetDirectSignedCustomerAgreementStatus. CS</span><span class="sxs-lookup"><span data-stu-id="cb07d-126">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cb07d-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cb07d-127">REST request</span></span>

<span data-ttu-id="cb07d-128">Om du vill hämta statusen för en kunds direkta godkännande av Microsofts kund avtal, skapar du en REST-begäran för att hämta [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) för kunden.</span><span class="sxs-lookup"><span data-stu-id="cb07d-128">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cb07d-129">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="cb07d-129">Request syntax</span></span>

<span data-ttu-id="cb07d-130">Använd följande syntax för begäran:</span><span class="sxs-lookup"><span data-stu-id="cb07d-130">Use the following request syntax:</span></span>

| <span data-ttu-id="cb07d-131">Metod</span><span class="sxs-lookup"><span data-stu-id="cb07d-131">Method</span></span> | <span data-ttu-id="cb07d-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cb07d-132">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb07d-133">GET</span><span class="sxs-lookup"><span data-stu-id="cb07d-133">GET</span></span>    | <span data-ttu-id="cb07d-134">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="cb07d-134">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="cb07d-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="cb07d-135">URI parameters</span></span>

<span data-ttu-id="cb07d-136">Du kan använda följande URI-parametrar med din begäran:</span><span class="sxs-lookup"><span data-stu-id="cb07d-136">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="cb07d-137">Namn</span><span class="sxs-lookup"><span data-stu-id="cb07d-137">Name</span></span>             | <span data-ttu-id="cb07d-138">Typ</span><span class="sxs-lookup"><span data-stu-id="cb07d-138">Type</span></span> | <span data-ttu-id="cb07d-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cb07d-139">Required</span></span> | <span data-ttu-id="cb07d-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cb07d-140">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb07d-141">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="cb07d-141">customer-tenant-id</span></span> | <span data-ttu-id="cb07d-142">GUID</span><span class="sxs-lookup"><span data-stu-id="cb07d-142">GUID</span></span> | <span data-ttu-id="cb07d-143">Ja</span><span class="sxs-lookup"><span data-stu-id="cb07d-143">Yes</span></span> | <span data-ttu-id="cb07d-144">Värdet är en GUID-formaterad **CustomerTenantId** som gör att du kan ange klient-ID för en kund.</span><span class="sxs-lookup"><span data-stu-id="cb07d-144">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cb07d-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cb07d-145">Request headers</span></span>

<span data-ttu-id="cb07d-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cb07d-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cb07d-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cb07d-147">Request body</span></span>

<span data-ttu-id="cb07d-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="cb07d-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cb07d-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cb07d-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="cb07d-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cb07d-150">REST response</span></span>

<span data-ttu-id="cb07d-151">Om det lyckas returnerar den här metoden en [ **DirectSignedCustomerAgreementStatus** -resurs](./customer-agreement-direct-sign-status-resource.md) i svars texten.</span><span class="sxs-lookup"><span data-stu-id="cb07d-151">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="cb07d-152">Resursen har en **isSigned** -egenskap som anger kundens direkta signerings status (direkt godkännande).</span><span class="sxs-lookup"><span data-stu-id="cb07d-152">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="cb07d-153">Värdet **True** anger att avtalet har signerats (accepterats) direkt av kunden.</span><span class="sxs-lookup"><span data-stu-id="cb07d-153">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="cb07d-154">Värdet **false** anger att avtalet *inte* har signerats (accepterats) direkt av kunden.</span><span class="sxs-lookup"><span data-stu-id="cb07d-154">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cb07d-155">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cb07d-155">Response success and error codes</span></span>

<span data-ttu-id="cb07d-156">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="cb07d-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="cb07d-157">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cb07d-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cb07d-158">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cb07d-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cb07d-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cb07d-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
