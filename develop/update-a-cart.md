---
title: Uppdatera en kundvagn
description: Så här uppdaterar du en order för en kund i en kundvagn.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446691"
---
# <a name="update-a-cart"></a><span data-ttu-id="8f316-103">Uppdatera en kundvagn</span><span class="sxs-lookup"><span data-stu-id="8f316-103">Update a cart</span></span>

<span data-ttu-id="8f316-104">Så här uppdaterar du en order för en kund i en kundvagn.</span><span class="sxs-lookup"><span data-stu-id="8f316-104">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f316-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8f316-105">Prerequisites</span></span>

- <span data-ttu-id="8f316-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8f316-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f316-107">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8f316-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8f316-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f316-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8f316-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8f316-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8f316-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="8f316-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8f316-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="8f316-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8f316-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="8f316-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8f316-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f316-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8f316-114">Ett kundvagns-ID för en befintlig kundvagn.</span><span class="sxs-lookup"><span data-stu-id="8f316-114">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="8f316-115">C\#</span><span class="sxs-lookup"><span data-stu-id="8f316-115">C\#</span></span>

<span data-ttu-id="8f316-116">Om du vill uppdatera en order för en kund hämtar du kundvagnen med hjälp av metoden **Get()** genom att skicka kund- och kundvagns-ID:n med hjälp av **funktionen ById().**</span><span class="sxs-lookup"><span data-stu-id="8f316-116">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart IDs using the **ById()** function.</span></span> <span data-ttu-id="8f316-117">Gör nödvändiga ändringar i kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="8f316-117">Make the necessary changes to the cart.</span></span> <span data-ttu-id="8f316-118">Anropa nu metoden **Put** med hjälp av kund- och kundvagns-ID:n med hjälp av **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="8f316-118">Now call the **Put** method by using customer and cart IDs using the **ById()** method.</span></span>

<span data-ttu-id="8f316-119">Anropa slutligen metoden **Put()** eller **PutAsync()** för att skapa ordern.</span><span class="sxs-lookup"><span data-stu-id="8f316-119">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="8f316-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8f316-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f316-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="8f316-121">Request syntax</span></span>

| <span data-ttu-id="8f316-122">Metod</span><span class="sxs-lookup"><span data-stu-id="8f316-122">Method</span></span>  | <span data-ttu-id="8f316-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8f316-123">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f316-124">**PUT**</span><span class="sxs-lookup"><span data-stu-id="8f316-124">**PUT**</span></span> | <span data-ttu-id="8f316-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8f316-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="8f316-126">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="8f316-126">URI parameters</span></span>

<span data-ttu-id="8f316-127">Använd följande sökvägsparametrar för att identifiera kunden och ange vilken kundvagn som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="8f316-127">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="8f316-128">Namn</span><span class="sxs-lookup"><span data-stu-id="8f316-128">Name</span></span>            | <span data-ttu-id="8f316-129">Typ</span><span class="sxs-lookup"><span data-stu-id="8f316-129">Type</span></span>     | <span data-ttu-id="8f316-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8f316-130">Required</span></span> | <span data-ttu-id="8f316-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8f316-131">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="8f316-132">**kund-id**</span><span class="sxs-lookup"><span data-stu-id="8f316-132">**customer-id**</span></span> | <span data-ttu-id="8f316-133">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-133">string</span></span>   | <span data-ttu-id="8f316-134">Ja</span><span class="sxs-lookup"><span data-stu-id="8f316-134">Yes</span></span>      | <span data-ttu-id="8f316-135">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="8f316-135">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="8f316-136">**cart-id**</span><span class="sxs-lookup"><span data-stu-id="8f316-136">**cart-id**</span></span>     | <span data-ttu-id="8f316-137">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-137">string</span></span>   | <span data-ttu-id="8f316-138">Ja</span><span class="sxs-lookup"><span data-stu-id="8f316-138">Yes</span></span>      | <span data-ttu-id="8f316-139">Ett GUID-formaterat kundvagns-ID som identifierar kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="8f316-139">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="8f316-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8f316-140">Request headers</span></span>

<span data-ttu-id="8f316-141">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8f316-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8f316-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8f316-142">Request body</span></span>

<span data-ttu-id="8f316-143">I den här tabellen beskrivs [egenskaperna för](cart-resources.md) Kundvagn i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="8f316-143">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="8f316-144">Egenskap</span><span class="sxs-lookup"><span data-stu-id="8f316-144">Property</span></span>              | <span data-ttu-id="8f316-145">Typ</span><span class="sxs-lookup"><span data-stu-id="8f316-145">Type</span></span>             | <span data-ttu-id="8f316-146">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8f316-146">Required</span></span>        | <span data-ttu-id="8f316-147">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8f316-147">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f316-148">id</span><span class="sxs-lookup"><span data-stu-id="8f316-148">id</span></span>                    | <span data-ttu-id="8f316-149">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-149">string</span></span>           | <span data-ttu-id="8f316-150">No</span><span class="sxs-lookup"><span data-stu-id="8f316-150">No</span></span>              | <span data-ttu-id="8f316-151">En kundvagnsidentifierare som anges när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="8f316-151">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="8f316-152">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="8f316-152">creationTimeStamp</span></span>     | <span data-ttu-id="8f316-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="8f316-153">DateTime</span></span>         | <span data-ttu-id="8f316-154">Inga</span><span class="sxs-lookup"><span data-stu-id="8f316-154">No</span></span>              | <span data-ttu-id="8f316-155">Datumet då kundvagnen skapades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="8f316-155">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="8f316-156">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="8f316-156">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="8f316-157">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="8f316-157">lastModifiedTimeStamp</span></span> | <span data-ttu-id="8f316-158">DateTime</span><span class="sxs-lookup"><span data-stu-id="8f316-158">DateTime</span></span>         | <span data-ttu-id="8f316-159">Inga</span><span class="sxs-lookup"><span data-stu-id="8f316-159">No</span></span>              | <span data-ttu-id="8f316-160">Datum då kundvagnen senast uppdaterades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="8f316-160">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="8f316-161">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="8f316-161">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="8f316-162">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="8f316-162">expirationTimeStamp</span></span>   | <span data-ttu-id="8f316-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="8f316-163">DateTime</span></span>         | <span data-ttu-id="8f316-164">Inga</span><span class="sxs-lookup"><span data-stu-id="8f316-164">No</span></span>              | <span data-ttu-id="8f316-165">Datumet då kundvagnen upphör att gälla i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="8f316-165">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="8f316-166">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="8f316-166">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="8f316-167">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="8f316-167">lastModifiedUser</span></span>      | <span data-ttu-id="8f316-168">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-168">string</span></span>           | <span data-ttu-id="8f316-169">No</span><span class="sxs-lookup"><span data-stu-id="8f316-169">No</span></span>              | <span data-ttu-id="8f316-170">Den användare som senast uppdaterade kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="8f316-170">The user who last updated the cart.</span></span> <span data-ttu-id="8f316-171">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="8f316-171">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="8f316-172">lineItems</span><span class="sxs-lookup"><span data-stu-id="8f316-172">lineItems</span></span>             | <span data-ttu-id="8f316-173">Matris med objekt</span><span class="sxs-lookup"><span data-stu-id="8f316-173">Array of objects</span></span> | <span data-ttu-id="8f316-174">Ja</span><span class="sxs-lookup"><span data-stu-id="8f316-174">Yes</span></span>             | <span data-ttu-id="8f316-175">En matris med [CartLineItem-resurser.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="8f316-175">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="8f316-176">I den här tabellen beskrivs [egenskaperna för CartLineItem](cart-resources.md#cartlineitem) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="8f316-176">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="8f316-177">Egenskap</span><span class="sxs-lookup"><span data-stu-id="8f316-177">Property</span></span>             | <span data-ttu-id="8f316-178">Typ</span><span class="sxs-lookup"><span data-stu-id="8f316-178">Type</span></span>                        | <span data-ttu-id="8f316-179">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8f316-179">Required</span></span>     | <span data-ttu-id="8f316-180">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8f316-180">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f316-181">id</span><span class="sxs-lookup"><span data-stu-id="8f316-181">id</span></span>                   | <span data-ttu-id="8f316-182">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-182">string</span></span>                      | <span data-ttu-id="8f316-183">No</span><span class="sxs-lookup"><span data-stu-id="8f316-183">No</span></span>           | <span data-ttu-id="8f316-184">En unik identifierare för ett kundvagnsradsobjekt.</span><span class="sxs-lookup"><span data-stu-id="8f316-184">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="8f316-185">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="8f316-185">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="8f316-186">catalogId</span><span class="sxs-lookup"><span data-stu-id="8f316-186">catalogId</span></span>            | <span data-ttu-id="8f316-187">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-187">string</span></span>                      | <span data-ttu-id="8f316-188">Ja</span><span class="sxs-lookup"><span data-stu-id="8f316-188">Yes</span></span>          | <span data-ttu-id="8f316-189">Katalogobjektets identifierare.</span><span class="sxs-lookup"><span data-stu-id="8f316-189">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="8f316-190">friendlyName</span><span class="sxs-lookup"><span data-stu-id="8f316-190">friendlyName</span></span>         | <span data-ttu-id="8f316-191">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-191">string</span></span>                      | <span data-ttu-id="8f316-192">No</span><span class="sxs-lookup"><span data-stu-id="8f316-192">No</span></span>           | <span data-ttu-id="8f316-193">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="8f316-193">Optional.</span></span> <span data-ttu-id="8f316-194">Det egna namnet för det objekt som definierats av partnern för att undvika tvetydighet.</span><span class="sxs-lookup"><span data-stu-id="8f316-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="8f316-195">quantity</span><span class="sxs-lookup"><span data-stu-id="8f316-195">quantity</span></span>             | <span data-ttu-id="8f316-196">int</span><span class="sxs-lookup"><span data-stu-id="8f316-196">int</span></span>                         | <span data-ttu-id="8f316-197">Ja</span><span class="sxs-lookup"><span data-stu-id="8f316-197">Yes</span></span>          | <span data-ttu-id="8f316-198">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="8f316-198">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="8f316-199">currencyCode</span><span class="sxs-lookup"><span data-stu-id="8f316-199">currencyCode</span></span>         | <span data-ttu-id="8f316-200">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-200">string</span></span>                      | <span data-ttu-id="8f316-201">No</span><span class="sxs-lookup"><span data-stu-id="8f316-201">No</span></span>           | <span data-ttu-id="8f316-202">Valutakoden.</span><span class="sxs-lookup"><span data-stu-id="8f316-202">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="8f316-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="8f316-203">billingCycle</span></span>         | <span data-ttu-id="8f316-204">Objekt</span><span class="sxs-lookup"><span data-stu-id="8f316-204">Object</span></span>                      | <span data-ttu-id="8f316-205">Ja</span><span class="sxs-lookup"><span data-stu-id="8f316-205">Yes</span></span>          | <span data-ttu-id="8f316-206">Den typ av faktureringsperiod som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="8f316-206">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="8f316-207">deltagare</span><span class="sxs-lookup"><span data-stu-id="8f316-207">participants</span></span>         | <span data-ttu-id="8f316-208">Lista över objektsträngpar</span><span class="sxs-lookup"><span data-stu-id="8f316-208">List of Object String pairs</span></span> | <span data-ttu-id="8f316-209">Inga</span><span class="sxs-lookup"><span data-stu-id="8f316-209">No</span></span>           | <span data-ttu-id="8f316-210">En samling deltagare i köpet.</span><span class="sxs-lookup"><span data-stu-id="8f316-210">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="8f316-211">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="8f316-211">provisioningContext</span></span>  | <span data-ttu-id="8f316-212">Ordlista<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="8f316-212">Dictionary<string, string></span></span>  | <span data-ttu-id="8f316-213">Inga</span><span class="sxs-lookup"><span data-stu-id="8f316-213">No</span></span>           | <span data-ttu-id="8f316-214">En kontext som används för etablering av erbjudande.</span><span class="sxs-lookup"><span data-stu-id="8f316-214">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="8f316-215">orderGroup</span><span class="sxs-lookup"><span data-stu-id="8f316-215">orderGroup</span></span>           | <span data-ttu-id="8f316-216">sträng</span><span class="sxs-lookup"><span data-stu-id="8f316-216">string</span></span>                      | <span data-ttu-id="8f316-217">No</span><span class="sxs-lookup"><span data-stu-id="8f316-217">No</span></span>           | <span data-ttu-id="8f316-218">En grupp som anger vilka objekt som kan placeras tillsammans.</span><span class="sxs-lookup"><span data-stu-id="8f316-218">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="8f316-219">fel</span><span class="sxs-lookup"><span data-stu-id="8f316-219">error</span></span>                | <span data-ttu-id="8f316-220">Objekt</span><span class="sxs-lookup"><span data-stu-id="8f316-220">Object</span></span>                      | <span data-ttu-id="8f316-221">Inga</span><span class="sxs-lookup"><span data-stu-id="8f316-221">No</span></span>           | <span data-ttu-id="8f316-222">Tillämpas när kundvagnen har skapats i händelse av ett fel.</span><span class="sxs-lookup"><span data-stu-id="8f316-222">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="8f316-223">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8f316-223">Request example</span></span>

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="8f316-224">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8f316-224">REST response</span></span>

<span data-ttu-id="8f316-225">Om det lyckas returnerar den här metoden den ifyllda [kundvagnsresursen](cart-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="8f316-225">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f316-226">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8f316-226">Response success and error codes</span></span>

<span data-ttu-id="8f316-227">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="8f316-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f316-228">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8f316-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8f316-229">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8f316-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8f316-230">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8f316-230">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
