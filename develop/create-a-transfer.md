---
title: Skapa en överföring
description: Så här skapar du en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d459a0a96912ab27f312bc73af16af2d4fdb518c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973714"
---
# <a name="create-a-transfer"></a><span data-ttu-id="14888-103">Skapa en överföring</span><span class="sxs-lookup"><span data-stu-id="14888-103">Create a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14888-104">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="14888-104">Prerequisites</span></span>

- <span data-ttu-id="14888-105">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="14888-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="14888-106">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="14888-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="14888-107">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14888-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="14888-108">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="14888-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="14888-109">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="14888-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="14888-110">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="14888-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="14888-111">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="14888-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="14888-112">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14888-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="14888-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="14888-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="14888-114">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="14888-114">Request syntax</span></span>

| <span data-ttu-id="14888-115">Metod</span><span class="sxs-lookup"><span data-stu-id="14888-115">Method</span></span>   | <span data-ttu-id="14888-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="14888-116">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14888-117">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="14888-117">**POST**</span></span> | <span data-ttu-id="14888-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="14888-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="14888-119">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="14888-119">URI parameter</span></span>

<span data-ttu-id="14888-120">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="14888-120">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="14888-121">Namn</span><span class="sxs-lookup"><span data-stu-id="14888-121">Name</span></span>            | <span data-ttu-id="14888-122">Typ</span><span class="sxs-lookup"><span data-stu-id="14888-122">Type</span></span>     | <span data-ttu-id="14888-123">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="14888-123">Required</span></span> | <span data-ttu-id="14888-124">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="14888-124">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="14888-125">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="14888-125">**customer-id**</span></span> | <span data-ttu-id="14888-126">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-126">string</span></span>   | <span data-ttu-id="14888-127">Ja</span><span class="sxs-lookup"><span data-stu-id="14888-127">Yes</span></span>      | <span data-ttu-id="14888-128">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="14888-128">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="14888-129">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="14888-129">Request headers</span></span>

<span data-ttu-id="14888-130">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="14888-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="14888-131">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="14888-131">Request body</span></span>

<span data-ttu-id="14888-132">I den här tabellen beskrivs [transferEntity-egenskaperna](transfer-entity-resources.md) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="14888-132">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="14888-133">Egenskap</span><span class="sxs-lookup"><span data-stu-id="14888-133">Property</span></span>              | <span data-ttu-id="14888-134">Typ</span><span class="sxs-lookup"><span data-stu-id="14888-134">Type</span></span>          | <span data-ttu-id="14888-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="14888-135">Required</span></span>  | <span data-ttu-id="14888-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="14888-136">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="14888-137">id</span><span class="sxs-lookup"><span data-stu-id="14888-137">id</span></span>                    | <span data-ttu-id="14888-138">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-138">string</span></span>        | <span data-ttu-id="14888-139">No</span><span class="sxs-lookup"><span data-stu-id="14888-139">No</span></span>    | <span data-ttu-id="14888-140">En transferEntity-identifierare som anges när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-140">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="14888-141">createdTime</span><span class="sxs-lookup"><span data-stu-id="14888-141">createdTime</span></span>           | <span data-ttu-id="14888-142">DateTime</span><span class="sxs-lookup"><span data-stu-id="14888-142">DateTime</span></span>      | <span data-ttu-id="14888-143">Inga</span><span class="sxs-lookup"><span data-stu-id="14888-143">No</span></span>    | <span data-ttu-id="14888-144">Det datum då transferEntity skapades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="14888-144">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="14888-145">Tillämpas när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-145">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="14888-146">lastModifiedTime</span><span class="sxs-lookup"><span data-stu-id="14888-146">lastModifiedTime</span></span>      | <span data-ttu-id="14888-147">DateTime</span><span class="sxs-lookup"><span data-stu-id="14888-147">DateTime</span></span>      | <span data-ttu-id="14888-148">Inga</span><span class="sxs-lookup"><span data-stu-id="14888-148">No</span></span>    | <span data-ttu-id="14888-149">Det datum då transferEntity senast uppdaterades, i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="14888-149">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="14888-150">Tillämpas när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-150">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="14888-151">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="14888-151">lastModifiedUser</span></span>      | <span data-ttu-id="14888-152">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-152">string</span></span>        | <span data-ttu-id="14888-153">No</span><span class="sxs-lookup"><span data-stu-id="14888-153">No</span></span>    | <span data-ttu-id="14888-154">Den användare som senast uppdaterade transferEntity.</span><span class="sxs-lookup"><span data-stu-id="14888-154">The user who last updated the transferEntity.</span></span> <span data-ttu-id="14888-155">Tillämpas när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-155">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="14888-156">customerName</span><span class="sxs-lookup"><span data-stu-id="14888-156">customerName</span></span>          | <span data-ttu-id="14888-157">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-157">string</span></span>        | <span data-ttu-id="14888-158">No</span><span class="sxs-lookup"><span data-stu-id="14888-158">No</span></span>    | <span data-ttu-id="14888-159">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="14888-159">Optional.</span></span> <span data-ttu-id="14888-160">Namnet på den kund vars prenumerationer överförs.</span><span class="sxs-lookup"><span data-stu-id="14888-160">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="14888-161">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="14888-161">customerTenantId</span></span>      | <span data-ttu-id="14888-162">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-162">string</span></span>        | <span data-ttu-id="14888-163">No</span><span class="sxs-lookup"><span data-stu-id="14888-163">No</span></span>    | <span data-ttu-id="14888-164">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="14888-164">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="14888-165">Tillämpas när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-165">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="14888-166">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="14888-166">partnertenantid</span></span>       | <span data-ttu-id="14888-167">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-167">string</span></span>        | <span data-ttu-id="14888-168">No</span><span class="sxs-lookup"><span data-stu-id="14888-168">No</span></span>    | <span data-ttu-id="14888-169">Ett GUID-formaterat partner-ID som identifierar partnern.</span><span class="sxs-lookup"><span data-stu-id="14888-169">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="14888-170">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="14888-170">sourcePartnerName</span></span>     | <span data-ttu-id="14888-171">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-171">string</span></span>        | <span data-ttu-id="14888-172">No</span><span class="sxs-lookup"><span data-stu-id="14888-172">No</span></span>    | <span data-ttu-id="14888-173">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="14888-173">Optional.</span></span> <span data-ttu-id="14888-174">Namnet på den partnerorganisation som initierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="14888-174">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="14888-175">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="14888-175">sourcePartnerTenantId</span></span> | <span data-ttu-id="14888-176">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-176">string</span></span>        | <span data-ttu-id="14888-177">Ja</span><span class="sxs-lookup"><span data-stu-id="14888-177">Yes</span></span>   | <span data-ttu-id="14888-178">Ett GUID-formaterat partner-ID som identifierar den partner som initierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="14888-178">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="14888-179">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="14888-179">targetPartnerName</span></span>     | <span data-ttu-id="14888-180">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-180">string</span></span>        | <span data-ttu-id="14888-181">No</span><span class="sxs-lookup"><span data-stu-id="14888-181">No</span></span>    | <span data-ttu-id="14888-182">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="14888-182">Optional.</span></span> <span data-ttu-id="14888-183">Namnet på den partnerorganisation som överföringen är riktad mot.</span><span class="sxs-lookup"><span data-stu-id="14888-183">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="14888-184">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="14888-184">targetPartnerTenantId</span></span> | <span data-ttu-id="14888-185">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-185">string</span></span>        | <span data-ttu-id="14888-186">Ja</span><span class="sxs-lookup"><span data-stu-id="14888-186">Yes</span></span>   | <span data-ttu-id="14888-187">Ett GUID-formaterat partner-ID som identifierar den partner som överföringen är riktad mot.</span><span class="sxs-lookup"><span data-stu-id="14888-187">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="14888-188">lineItems</span><span class="sxs-lookup"><span data-stu-id="14888-188">lineItems</span></span>             | <span data-ttu-id="14888-189">Matris med objekt</span><span class="sxs-lookup"><span data-stu-id="14888-189">Array of objects</span></span> | <span data-ttu-id="14888-190">Ja</span><span class="sxs-lookup"><span data-stu-id="14888-190">Yes</span></span>| <span data-ttu-id="14888-191">En matris med [TransferLineItem-resurser.](transfer-entity-resources.md#transferlineitem)</span><span class="sxs-lookup"><span data-stu-id="14888-191">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="14888-192">status</span><span class="sxs-lookup"><span data-stu-id="14888-192">status</span></span>                | <span data-ttu-id="14888-193">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-193">string</span></span>        | <span data-ttu-id="14888-194">No</span><span class="sxs-lookup"><span data-stu-id="14888-194">No</span></span>    | <span data-ttu-id="14888-195">Status för transferEntity.</span><span class="sxs-lookup"><span data-stu-id="14888-195">The status of the transferEntity.</span></span> <span data-ttu-id="14888-196">Möjliga värden är "Aktiv" (kan tas bort/skickas) och "Slutförd" (har redan slutförts).</span><span class="sxs-lookup"><span data-stu-id="14888-196">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="14888-197">Tillämpas när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-197">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="14888-198">I den här tabellen beskrivs [transferLineItem-egenskaperna](transfer-entity-resources.md#transferlineitem) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="14888-198">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="14888-199">Egenskap</span><span class="sxs-lookup"><span data-stu-id="14888-199">Property</span></span>       |            <span data-ttu-id="14888-200">Typ</span><span class="sxs-lookup"><span data-stu-id="14888-200">Type</span></span>             | <span data-ttu-id="14888-201">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="14888-201">Required</span></span> | <span data-ttu-id="14888-202">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="14888-202">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14888-203">id</span><span class="sxs-lookup"><span data-stu-id="14888-203">id</span></span>                   | <span data-ttu-id="14888-204">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-204">string</span></span>                     | <span data-ttu-id="14888-205">No</span><span class="sxs-lookup"><span data-stu-id="14888-205">No</span></span>       | <span data-ttu-id="14888-206">En unik identifierare för ett överföringsradsobjekt.</span><span class="sxs-lookup"><span data-stu-id="14888-206">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="14888-207">Tillämpas när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-207">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="14888-208">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="14888-208">subscriptionId</span></span>       | <span data-ttu-id="14888-209">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-209">string</span></span>                     | <span data-ttu-id="14888-210">Ja</span><span class="sxs-lookup"><span data-stu-id="14888-210">Yes</span></span>      | <span data-ttu-id="14888-211">Prenumerationsidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="14888-211">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="14888-212">quantity</span><span class="sxs-lookup"><span data-stu-id="14888-212">quantity</span></span>             | <span data-ttu-id="14888-213">int</span><span class="sxs-lookup"><span data-stu-id="14888-213">int</span></span>                        | <span data-ttu-id="14888-214">Inga</span><span class="sxs-lookup"><span data-stu-id="14888-214">No</span></span>       | <span data-ttu-id="14888-215">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="14888-215">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="14888-216">billingCycle</span><span class="sxs-lookup"><span data-stu-id="14888-216">billingCycle</span></span>         | <span data-ttu-id="14888-217">Objekt</span><span class="sxs-lookup"><span data-stu-id="14888-217">Object</span></span>                     | <span data-ttu-id="14888-218">Inga</span><span class="sxs-lookup"><span data-stu-id="14888-218">No</span></span>       | <span data-ttu-id="14888-219">Den typ av faktureringsperiod som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="14888-219">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="14888-220">friendlyName</span><span class="sxs-lookup"><span data-stu-id="14888-220">friendlyName</span></span>         | <span data-ttu-id="14888-221">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-221">string</span></span>                     | <span data-ttu-id="14888-222">No</span><span class="sxs-lookup"><span data-stu-id="14888-222">No</span></span>       | <span data-ttu-id="14888-223">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="14888-223">Optional.</span></span> <span data-ttu-id="14888-224">Det egna namnet för det objekt som definierats av partnern för att undvika tvetydighet.</span><span class="sxs-lookup"><span data-stu-id="14888-224">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="14888-225">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="14888-225">partnerIdOnRecord</span></span>    | <span data-ttu-id="14888-226">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-226">string</span></span>                     | <span data-ttu-id="14888-227">No</span><span class="sxs-lookup"><span data-stu-id="14888-227">No</span></span>       | <span data-ttu-id="14888-228">PartnerId på post (MPN-ID) för köpet som inträffar när överföringen godkänns.</span><span class="sxs-lookup"><span data-stu-id="14888-228">PartnerId on Record (MPN ID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="14888-229">offerId</span><span class="sxs-lookup"><span data-stu-id="14888-229">offerId</span></span>              | <span data-ttu-id="14888-230">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-230">string</span></span>                     | <span data-ttu-id="14888-231">No</span><span class="sxs-lookup"><span data-stu-id="14888-231">No</span></span>       | <span data-ttu-id="14888-232">Erbjudandeidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="14888-232">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="14888-233">addonItems</span><span class="sxs-lookup"><span data-stu-id="14888-233">addonItems</span></span>           | <span data-ttu-id="14888-234">Lista över **TransferLineItem-objekt**</span><span class="sxs-lookup"><span data-stu-id="14888-234">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="14888-235">Inga</span><span class="sxs-lookup"><span data-stu-id="14888-235">No</span></span> | <span data-ttu-id="14888-236">En samling transferEntity-radobjekt för addons som ska överföras tillsammans med basprenumerationen som överförs.</span><span class="sxs-lookup"><span data-stu-id="14888-236">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="14888-237">Tillämpas när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="14888-237">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="14888-238">transferError</span><span class="sxs-lookup"><span data-stu-id="14888-238">transferError</span></span>        | <span data-ttu-id="14888-239">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-239">string</span></span>                     | <span data-ttu-id="14888-240">No</span><span class="sxs-lookup"><span data-stu-id="14888-240">No</span></span>       | <span data-ttu-id="14888-241">Tillämpas efter överföringEntity godkänns om det finns ett fel.</span><span class="sxs-lookup"><span data-stu-id="14888-241">Applied after transferEntity is accepted if there is an error.</span></span>                                        |
| <span data-ttu-id="14888-242">status</span><span class="sxs-lookup"><span data-stu-id="14888-242">status</span></span>               | <span data-ttu-id="14888-243">sträng</span><span class="sxs-lookup"><span data-stu-id="14888-243">string</span></span>                     | <span data-ttu-id="14888-244">No</span><span class="sxs-lookup"><span data-stu-id="14888-244">No</span></span>       | <span data-ttu-id="14888-245">Status för lineitem i transferEntity.</span><span class="sxs-lookup"><span data-stu-id="14888-245">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="14888-246">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="14888-246">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="14888-247">REST-svar</span><span class="sxs-lookup"><span data-stu-id="14888-247">REST response</span></span>

<span data-ttu-id="14888-248">Om det lyckas returnerar den här metoden den [ifyllda TransferEnity-resursen](transfer-entity-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="14888-248">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="14888-249">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="14888-249">Response success and error codes</span></span>

<span data-ttu-id="14888-250">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="14888-250">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="14888-251">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="14888-251">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="14888-252">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="14888-252">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="14888-253">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="14888-253">Response example</span></span>

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
