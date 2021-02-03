---
title: Skapa en överföring
description: Så här skapar du en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768829"
---
# <a name="create-a-transfer"></a><span data-ttu-id="992bb-103">Skapa en överföring</span><span class="sxs-lookup"><span data-stu-id="992bb-103">Create a transfer</span></span>

<span data-ttu-id="992bb-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="992bb-104">**Applies to:**</span></span>

- <span data-ttu-id="992bb-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="992bb-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="992bb-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="992bb-106">Prerequisites</span></span>

- <span data-ttu-id="992bb-107">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="992bb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="992bb-108">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="992bb-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="992bb-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="992bb-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="992bb-110">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="992bb-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="992bb-111">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="992bb-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="992bb-112">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="992bb-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="992bb-113">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="992bb-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="992bb-114">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="992bb-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="992bb-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="992bb-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="992bb-116">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="992bb-116">Request syntax</span></span>

| <span data-ttu-id="992bb-117">Metod</span><span class="sxs-lookup"><span data-stu-id="992bb-117">Method</span></span>   | <span data-ttu-id="992bb-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="992bb-118">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="992bb-119">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="992bb-119">**POST**</span></span> | <span data-ttu-id="992bb-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/transfers http/1.1</span><span class="sxs-lookup"><span data-stu-id="992bb-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="992bb-121">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="992bb-121">URI parameter</span></span>

<span data-ttu-id="992bb-122">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="992bb-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="992bb-123">Namn</span><span class="sxs-lookup"><span data-stu-id="992bb-123">Name</span></span>            | <span data-ttu-id="992bb-124">Typ</span><span class="sxs-lookup"><span data-stu-id="992bb-124">Type</span></span>     | <span data-ttu-id="992bb-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="992bb-125">Required</span></span> | <span data-ttu-id="992bb-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="992bb-126">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="992bb-127">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="992bb-127">**customer-id**</span></span> | <span data-ttu-id="992bb-128">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-128">string</span></span>   | <span data-ttu-id="992bb-129">Yes</span><span class="sxs-lookup"><span data-stu-id="992bb-129">Yes</span></span>      | <span data-ttu-id="992bb-130">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="992bb-130">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="992bb-131">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="992bb-131">Request headers</span></span>

<span data-ttu-id="992bb-132">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="992bb-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="992bb-133">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="992bb-133">Request body</span></span>

<span data-ttu-id="992bb-134">I den här tabellen beskrivs egenskaperna för [TransferEntity](transfer-entity-resources.md) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="992bb-134">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="992bb-135">Egenskap</span><span class="sxs-lookup"><span data-stu-id="992bb-135">Property</span></span>              | <span data-ttu-id="992bb-136">Typ</span><span class="sxs-lookup"><span data-stu-id="992bb-136">Type</span></span>          | <span data-ttu-id="992bb-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="992bb-137">Required</span></span>  | <span data-ttu-id="992bb-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="992bb-138">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="992bb-139">id</span><span class="sxs-lookup"><span data-stu-id="992bb-139">id</span></span>                    | <span data-ttu-id="992bb-140">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-140">string</span></span>        | <span data-ttu-id="992bb-141">No</span><span class="sxs-lookup"><span data-stu-id="992bb-141">No</span></span>    | <span data-ttu-id="992bb-142">En transferEntity-identifierare som anges när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-142">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="992bb-143">createdTime</span><span class="sxs-lookup"><span data-stu-id="992bb-143">createdTime</span></span>           | <span data-ttu-id="992bb-144">DateTime</span><span class="sxs-lookup"><span data-stu-id="992bb-144">DateTime</span></span>      | <span data-ttu-id="992bb-145">No</span><span class="sxs-lookup"><span data-stu-id="992bb-145">No</span></span>    | <span data-ttu-id="992bb-146">Datumet då transferEntity skapades, i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="992bb-146">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="992bb-147">Används när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-147">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="992bb-148">lastModifiedTime</span><span class="sxs-lookup"><span data-stu-id="992bb-148">lastModifiedTime</span></span>      | <span data-ttu-id="992bb-149">DateTime</span><span class="sxs-lookup"><span data-stu-id="992bb-149">DateTime</span></span>      | <span data-ttu-id="992bb-150">No</span><span class="sxs-lookup"><span data-stu-id="992bb-150">No</span></span>    | <span data-ttu-id="992bb-151">Datumet då transferEntity senast uppdaterades, i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="992bb-151">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="992bb-152">Används när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-152">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="992bb-153">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="992bb-153">lastModifiedUser</span></span>      | <span data-ttu-id="992bb-154">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-154">string</span></span>        | <span data-ttu-id="992bb-155">No</span><span class="sxs-lookup"><span data-stu-id="992bb-155">No</span></span>    | <span data-ttu-id="992bb-156">Användaren som senast uppdaterade transferEntity.</span><span class="sxs-lookup"><span data-stu-id="992bb-156">The user who last updated the transferEntity.</span></span> <span data-ttu-id="992bb-157">Används när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-157">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="992bb-158">customerName</span><span class="sxs-lookup"><span data-stu-id="992bb-158">customerName</span></span>          | <span data-ttu-id="992bb-159">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-159">string</span></span>        | <span data-ttu-id="992bb-160">No</span><span class="sxs-lookup"><span data-stu-id="992bb-160">No</span></span>    | <span data-ttu-id="992bb-161">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="992bb-161">Optional.</span></span> <span data-ttu-id="992bb-162">Namnet på kunden vars prenumerationer överförs.</span><span class="sxs-lookup"><span data-stu-id="992bb-162">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="992bb-163">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="992bb-163">customerTenantId</span></span>      | <span data-ttu-id="992bb-164">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-164">string</span></span>        | <span data-ttu-id="992bb-165">No</span><span class="sxs-lookup"><span data-stu-id="992bb-165">No</span></span>    | <span data-ttu-id="992bb-166">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="992bb-166">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="992bb-167">Används när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-167">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="992bb-168">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="992bb-168">partnertenantid</span></span>       | <span data-ttu-id="992bb-169">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-169">string</span></span>        | <span data-ttu-id="992bb-170">No</span><span class="sxs-lookup"><span data-stu-id="992bb-170">No</span></span>    | <span data-ttu-id="992bb-171">Ett GUID-formaterat partner-ID som identifierar partnern.</span><span class="sxs-lookup"><span data-stu-id="992bb-171">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="992bb-172">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="992bb-172">sourcePartnerName</span></span>     | <span data-ttu-id="992bb-173">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-173">string</span></span>        | <span data-ttu-id="992bb-174">No</span><span class="sxs-lookup"><span data-stu-id="992bb-174">No</span></span>    | <span data-ttu-id="992bb-175">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="992bb-175">Optional.</span></span> <span data-ttu-id="992bb-176">Namnet på partnerns organisation som initierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="992bb-176">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="992bb-177">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="992bb-177">sourcePartnerTenantId</span></span> | <span data-ttu-id="992bb-178">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-178">string</span></span>        | <span data-ttu-id="992bb-179">Yes</span><span class="sxs-lookup"><span data-stu-id="992bb-179">Yes</span></span>   | <span data-ttu-id="992bb-180">Ett GUID-formaterat partner-ID som identifierar den partner som initierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="992bb-180">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="992bb-181">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="992bb-181">targetPartnerName</span></span>     | <span data-ttu-id="992bb-182">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-182">string</span></span>        | <span data-ttu-id="992bb-183">No</span><span class="sxs-lookup"><span data-stu-id="992bb-183">No</span></span>    | <span data-ttu-id="992bb-184">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="992bb-184">Optional.</span></span> <span data-ttu-id="992bb-185">Namnet på partnerns organisation som överföringen riktas mot.</span><span class="sxs-lookup"><span data-stu-id="992bb-185">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="992bb-186">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="992bb-186">targetPartnerTenantId</span></span> | <span data-ttu-id="992bb-187">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-187">string</span></span>        | <span data-ttu-id="992bb-188">Yes</span><span class="sxs-lookup"><span data-stu-id="992bb-188">Yes</span></span>   | <span data-ttu-id="992bb-189">Ett GUID-formaterat partner-ID som identifierar den partner som överföringen riktas mot.</span><span class="sxs-lookup"><span data-stu-id="992bb-189">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="992bb-190">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="992bb-190">lineItems</span></span>             | <span data-ttu-id="992bb-191">Objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="992bb-191">Array of objects</span></span> | <span data-ttu-id="992bb-192">Yes</span><span class="sxs-lookup"><span data-stu-id="992bb-192">Yes</span></span>| <span data-ttu-id="992bb-193">En matris med [TransferLineItem](transfer-entity-resources.md#transferlineitem) -resurser.</span><span class="sxs-lookup"><span data-stu-id="992bb-193">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="992bb-194">status</span><span class="sxs-lookup"><span data-stu-id="992bb-194">status</span></span>                | <span data-ttu-id="992bb-195">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-195">string</span></span>        | <span data-ttu-id="992bb-196">No</span><span class="sxs-lookup"><span data-stu-id="992bb-196">No</span></span>    | <span data-ttu-id="992bb-197">Status för transferEntity.</span><span class="sxs-lookup"><span data-stu-id="992bb-197">The status of the transferEntity.</span></span> <span data-ttu-id="992bb-198">Möjliga värden är "aktiva" (kan tas bort/skickas) och "slutfört" (har redan slutförts).</span><span class="sxs-lookup"><span data-stu-id="992bb-198">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="992bb-199">Används när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-199">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="992bb-200">I den här tabellen beskrivs egenskaperna för [TransferLineItem](transfer-entity-resources.md#transferlineitem) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="992bb-200">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="992bb-201">Egenskap</span><span class="sxs-lookup"><span data-stu-id="992bb-201">Property</span></span>       |            <span data-ttu-id="992bb-202">Typ</span><span class="sxs-lookup"><span data-stu-id="992bb-202">Type</span></span>             | <span data-ttu-id="992bb-203">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="992bb-203">Required</span></span> | <span data-ttu-id="992bb-204">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="992bb-204">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="992bb-205">id</span><span class="sxs-lookup"><span data-stu-id="992bb-205">id</span></span>                   | <span data-ttu-id="992bb-206">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-206">string</span></span>                     | <span data-ttu-id="992bb-207">No</span><span class="sxs-lookup"><span data-stu-id="992bb-207">No</span></span>       | <span data-ttu-id="992bb-208">En unik identifierare för ett överförings rads objekt.</span><span class="sxs-lookup"><span data-stu-id="992bb-208">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="992bb-209">Används när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-209">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="992bb-210">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="992bb-210">subscriptionId</span></span>       | <span data-ttu-id="992bb-211">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-211">string</span></span>                     | <span data-ttu-id="992bb-212">Yes</span><span class="sxs-lookup"><span data-stu-id="992bb-212">Yes</span></span>      | <span data-ttu-id="992bb-213">Prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="992bb-213">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="992bb-214">quantity</span><span class="sxs-lookup"><span data-stu-id="992bb-214">quantity</span></span>             | <span data-ttu-id="992bb-215">int</span><span class="sxs-lookup"><span data-stu-id="992bb-215">int</span></span>                        | <span data-ttu-id="992bb-216">No</span><span class="sxs-lookup"><span data-stu-id="992bb-216">No</span></span>       | <span data-ttu-id="992bb-217">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="992bb-217">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="992bb-218">billingCycle</span><span class="sxs-lookup"><span data-stu-id="992bb-218">billingCycle</span></span>         | <span data-ttu-id="992bb-219">Objekt</span><span class="sxs-lookup"><span data-stu-id="992bb-219">Object</span></span>                     | <span data-ttu-id="992bb-220">No</span><span class="sxs-lookup"><span data-stu-id="992bb-220">No</span></span>       | <span data-ttu-id="992bb-221">Typ av fakturerings cykel som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="992bb-221">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="992bb-222">friendlyName</span><span class="sxs-lookup"><span data-stu-id="992bb-222">friendlyName</span></span>         | <span data-ttu-id="992bb-223">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-223">string</span></span>                     | <span data-ttu-id="992bb-224">No</span><span class="sxs-lookup"><span data-stu-id="992bb-224">No</span></span>       | <span data-ttu-id="992bb-225">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="992bb-225">Optional.</span></span> <span data-ttu-id="992bb-226">Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.</span><span class="sxs-lookup"><span data-stu-id="992bb-226">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="992bb-227">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="992bb-227">partnerIdOnRecord</span></span>    | <span data-ttu-id="992bb-228">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-228">string</span></span>                     | <span data-ttu-id="992bb-229">No</span><span class="sxs-lookup"><span data-stu-id="992bb-229">No</span></span>       | <span data-ttu-id="992bb-230">Partner on Record (MPNID) på köpet som inträffar när överföringen godkänns.</span><span class="sxs-lookup"><span data-stu-id="992bb-230">PartnerId on Record (MPNID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="992bb-231">offerId</span><span class="sxs-lookup"><span data-stu-id="992bb-231">offerId</span></span>              | <span data-ttu-id="992bb-232">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-232">string</span></span>                     | <span data-ttu-id="992bb-233">No</span><span class="sxs-lookup"><span data-stu-id="992bb-233">No</span></span>       | <span data-ttu-id="992bb-234">Erbjudande-ID.</span><span class="sxs-lookup"><span data-stu-id="992bb-234">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="992bb-235">addonItems</span><span class="sxs-lookup"><span data-stu-id="992bb-235">addonItems</span></span>           | <span data-ttu-id="992bb-236">Lista över **TransferLineItem** -objekt</span><span class="sxs-lookup"><span data-stu-id="992bb-236">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="992bb-237">No</span><span class="sxs-lookup"><span data-stu-id="992bb-237">No</span></span> | <span data-ttu-id="992bb-238">En samling transferEntity rad objekt för tillägg som ska överföras tillsammans med den bas prenumeration som överförs.</span><span class="sxs-lookup"><span data-stu-id="992bb-238">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="992bb-239">Används när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="992bb-239">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="992bb-240">transferError</span><span class="sxs-lookup"><span data-stu-id="992bb-240">transferError</span></span>        | <span data-ttu-id="992bb-241">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-241">string</span></span>                     | <span data-ttu-id="992bb-242">No</span><span class="sxs-lookup"><span data-stu-id="992bb-242">No</span></span>       | <span data-ttu-id="992bb-243">Tillämpas efter att transferEntity accepterats i händelse av ett fel.</span><span class="sxs-lookup"><span data-stu-id="992bb-243">Applied after transferEntity is accepted in case of an error.</span></span>                                        |
| <span data-ttu-id="992bb-244">status</span><span class="sxs-lookup"><span data-stu-id="992bb-244">status</span></span>               | <span data-ttu-id="992bb-245">sträng</span><span class="sxs-lookup"><span data-stu-id="992bb-245">string</span></span>                     | <span data-ttu-id="992bb-246">No</span><span class="sxs-lookup"><span data-stu-id="992bb-246">No</span></span>       | <span data-ttu-id="992bb-247">Status för lineitem i transferEntity.</span><span class="sxs-lookup"><span data-stu-id="992bb-247">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="992bb-248">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="992bb-248">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="992bb-249">REST-svar</span><span class="sxs-lookup"><span data-stu-id="992bb-249">REST response</span></span>

<span data-ttu-id="992bb-250">Om det lyckas returnerar den här metoden den ifyllda [TransferEnity](transfer-entity-resources.md) -resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="992bb-250">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="992bb-251">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="992bb-251">Response success and error codes</span></span>

<span data-ttu-id="992bb-252">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="992bb-252">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="992bb-253">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="992bb-253">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="992bb-254">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="992bb-254">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="992bb-255">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="992bb-255">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
