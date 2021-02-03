---
title: Hämta kundens direkta signerings status för Microsofts kund avtal.
description: Du kan använda DirectSignedCustomerAgreementStatus-resursen för att hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768739"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="51dbd-103">Hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal</span><span class="sxs-lookup"><span data-stu-id="51dbd-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="51dbd-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="51dbd-104">**Applies to:**</span></span>

- <span data-ttu-id="51dbd-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="51dbd-105">Partner Center</span></span>

<span data-ttu-id="51dbd-106">**DirectSignedCustomerAgreementStatus** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="51dbd-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="51dbd-107">Den här resursen är *inte tillämplig* för:</span><span class="sxs-lookup"><span data-stu-id="51dbd-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="51dbd-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="51dbd-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="51dbd-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="51dbd-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="51dbd-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="51dbd-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="51dbd-111">Den här artikeln förklarar hur du kan hämta statusen för en kunds direkta godkännande av Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="51dbd-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="rest-request"></a><span data-ttu-id="51dbd-112">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="51dbd-112">REST request</span></span>

<span data-ttu-id="51dbd-113">Om du vill hämta statusen för en kunds direkta godkännande av Microsofts kund avtal, skapar du en REST-begäran för att hämta [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) för kunden.</span><span class="sxs-lookup"><span data-stu-id="51dbd-113">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="51dbd-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="51dbd-114">Request syntax</span></span>

<span data-ttu-id="51dbd-115">Använd följande syntax för begäran:</span><span class="sxs-lookup"><span data-stu-id="51dbd-115">Use the following request syntax:</span></span>

| <span data-ttu-id="51dbd-116">Metod</span><span class="sxs-lookup"><span data-stu-id="51dbd-116">Method</span></span> | <span data-ttu-id="51dbd-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="51dbd-117">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="51dbd-118">GET</span><span class="sxs-lookup"><span data-stu-id="51dbd-118">GET</span></span>    | <span data-ttu-id="51dbd-119">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="51dbd-119">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="51dbd-120">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="51dbd-120">URI parameters</span></span>

<span data-ttu-id="51dbd-121">Du kan använda följande URI-parametrar med din begäran:</span><span class="sxs-lookup"><span data-stu-id="51dbd-121">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="51dbd-122">Namn</span><span class="sxs-lookup"><span data-stu-id="51dbd-122">Name</span></span>             | <span data-ttu-id="51dbd-123">Typ</span><span class="sxs-lookup"><span data-stu-id="51dbd-123">Type</span></span> | <span data-ttu-id="51dbd-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="51dbd-124">Required</span></span> | <span data-ttu-id="51dbd-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="51dbd-125">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="51dbd-126">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="51dbd-126">customer-tenant-id</span></span> | <span data-ttu-id="51dbd-127">GUID</span><span class="sxs-lookup"><span data-stu-id="51dbd-127">GUID</span></span> | <span data-ttu-id="51dbd-128">Yes</span><span class="sxs-lookup"><span data-stu-id="51dbd-128">Yes</span></span> | <span data-ttu-id="51dbd-129">Värdet är en GUID-formaterad **CustomerTenantId** som gör att du kan ange klient-ID för en kund.</span><span class="sxs-lookup"><span data-stu-id="51dbd-129">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="51dbd-130">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="51dbd-130">Request headers</span></span>

<span data-ttu-id="51dbd-131">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="51dbd-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="51dbd-132">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="51dbd-132">Request body</span></span>

<span data-ttu-id="51dbd-133">Inga.</span><span class="sxs-lookup"><span data-stu-id="51dbd-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="51dbd-134">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="51dbd-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="51dbd-135">REST-svar</span><span class="sxs-lookup"><span data-stu-id="51dbd-135">REST response</span></span>

<span data-ttu-id="51dbd-136">Om det lyckas returnerar den här metoden en [ **DirectSignedCustomerAgreementStatus** -resurs](./customer-agreement-direct-sign-status-resource.md) i svars texten.</span><span class="sxs-lookup"><span data-stu-id="51dbd-136">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="51dbd-137">Resursen har en **isSigned** -egenskap som anger kundens direkta signerings status (direkt godkännande).</span><span class="sxs-lookup"><span data-stu-id="51dbd-137">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="51dbd-138">Värdet **True** anger att avtalet har signerats (accepterats) direkt av kunden.</span><span class="sxs-lookup"><span data-stu-id="51dbd-138">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="51dbd-139">Värdet **false** anger att avtalet *inte* har signerats (accepterats) direkt av kunden.</span><span class="sxs-lookup"><span data-stu-id="51dbd-139">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="51dbd-140">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="51dbd-140">Response success and error codes</span></span>

<span data-ttu-id="51dbd-141">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="51dbd-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="51dbd-142">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="51dbd-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="51dbd-143">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="51dbd-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="51dbd-144">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="51dbd-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
