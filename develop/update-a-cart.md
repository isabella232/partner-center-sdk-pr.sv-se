---
title: Uppdatera en kundvagn
description: Så här uppdaterar du en order för en kund i en varukorg.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768940"
---
# <a name="update-a-cart"></a><span data-ttu-id="6c2c0-103">Uppdatera en kundvagn</span><span class="sxs-lookup"><span data-stu-id="6c2c0-103">Update a cart</span></span>

<span data-ttu-id="6c2c0-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="6c2c0-104">**Applies To**</span></span>

- <span data-ttu-id="6c2c0-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="6c2c0-105">Partner Center</span></span>

<span data-ttu-id="6c2c0-106">Så här uppdaterar du en order för en kund i en varukorg.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-106">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c2c0-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6c2c0-107">Prerequisites</span></span>

- <span data-ttu-id="6c2c0-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6c2c0-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6c2c0-109">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6c2c0-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c2c0-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6c2c0-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6c2c0-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6c2c0-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6c2c0-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="6c2c0-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6c2c0-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c2c0-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6c2c0-116">Ett kundvagn-ID för en befintlig varukorg.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-116">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="6c2c0-117">C\#</span><span class="sxs-lookup"><span data-stu-id="6c2c0-117">C\#</span></span>

<span data-ttu-id="6c2c0-118">Om du vill uppdatera en order för en kund hämtar du vagnen med hjälp av metoden **Get ()** genom att skicka kund-och kundvagn-ID: t med funktionen **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="6c2c0-118">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart ID's using the **ById()** function.</span></span> <span data-ttu-id="6c2c0-119">Gör nödvändiga ändringar i vagnen.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-119">Make the necessary changes to the cart.</span></span> <span data-ttu-id="6c2c0-120">Anropa nu metoden för att **Skicka** med hjälp av kund-och shopping-ID: t med hjälp av metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="6c2c0-120">Now call the **Put** method by using customer and cart ID's using the **ById()** method.</span></span>

<span data-ttu-id="6c2c0-121">Anropa slutligen metoden PutAsync ( **)** eller metoden **()** för att skapa ordern.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-121">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="6c2c0-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6c2c0-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6c2c0-123">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="6c2c0-123">Request syntax</span></span>

| <span data-ttu-id="6c2c0-124">Metod</span><span class="sxs-lookup"><span data-stu-id="6c2c0-124">Method</span></span>  | <span data-ttu-id="6c2c0-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6c2c0-125">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c2c0-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="6c2c0-126">**PUT**</span></span> | <span data-ttu-id="6c2c0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6c2c0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="6c2c0-128">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="6c2c0-128">URI parameters</span></span>

<span data-ttu-id="6c2c0-129">Använd följande Sök vägs parametrar för att identifiera kunden och ange den varukorg som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-129">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="6c2c0-130">Namn</span><span class="sxs-lookup"><span data-stu-id="6c2c0-130">Name</span></span>            | <span data-ttu-id="6c2c0-131">Typ</span><span class="sxs-lookup"><span data-stu-id="6c2c0-131">Type</span></span>     | <span data-ttu-id="6c2c0-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6c2c0-132">Required</span></span> | <span data-ttu-id="6c2c0-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6c2c0-133">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="6c2c0-134">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="6c2c0-134">**customer-id**</span></span> | <span data-ttu-id="6c2c0-135">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-135">string</span></span>   | <span data-ttu-id="6c2c0-136">Yes</span><span class="sxs-lookup"><span data-stu-id="6c2c0-136">Yes</span></span>      | <span data-ttu-id="6c2c0-137">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-137">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="6c2c0-138">**kundvagn-ID**</span><span class="sxs-lookup"><span data-stu-id="6c2c0-138">**cart-id**</span></span>     | <span data-ttu-id="6c2c0-139">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-139">string</span></span>   | <span data-ttu-id="6c2c0-140">Yes</span><span class="sxs-lookup"><span data-stu-id="6c2c0-140">Yes</span></span>      | <span data-ttu-id="6c2c0-141">Ett GUID-formaterat vagn-ID som identifierar vagnen.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-141">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="6c2c0-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6c2c0-142">Request headers</span></span>

<span data-ttu-id="6c2c0-143">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6c2c0-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6c2c0-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6c2c0-144">Request body</span></span>

<span data-ttu-id="6c2c0-145">I den här tabellen beskrivs egenskaperna för [kundvagn](cart-resources.md) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-145">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="6c2c0-146">Egenskap</span><span class="sxs-lookup"><span data-stu-id="6c2c0-146">Property</span></span>              | <span data-ttu-id="6c2c0-147">Typ</span><span class="sxs-lookup"><span data-stu-id="6c2c0-147">Type</span></span>             | <span data-ttu-id="6c2c0-148">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6c2c0-148">Required</span></span>        | <span data-ttu-id="6c2c0-149">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6c2c0-149">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c2c0-150">id</span><span class="sxs-lookup"><span data-stu-id="6c2c0-150">id</span></span>                    | <span data-ttu-id="6c2c0-151">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-151">string</span></span>           | <span data-ttu-id="6c2c0-152">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-152">No</span></span>              | <span data-ttu-id="6c2c0-153">Ett kundvagn-ID som anges när vagnen skapas.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-153">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="6c2c0-154">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="6c2c0-154">creationTimeStamp</span></span>     | <span data-ttu-id="6c2c0-155">DateTime</span><span class="sxs-lookup"><span data-stu-id="6c2c0-155">DateTime</span></span>         | <span data-ttu-id="6c2c0-156">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-156">No</span></span>              | <span data-ttu-id="6c2c0-157">Datumet då vagnen skapades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-157">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="6c2c0-158">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-158">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="6c2c0-159">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="6c2c0-159">lastModifiedTimeStamp</span></span> | <span data-ttu-id="6c2c0-160">DateTime</span><span class="sxs-lookup"><span data-stu-id="6c2c0-160">DateTime</span></span>         | <span data-ttu-id="6c2c0-161">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-161">No</span></span>              | <span data-ttu-id="6c2c0-162">Datumet då vagnen senast uppdaterades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-162">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="6c2c0-163">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-163">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="6c2c0-164">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="6c2c0-164">expirationTimeStamp</span></span>   | <span data-ttu-id="6c2c0-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="6c2c0-165">DateTime</span></span>         | <span data-ttu-id="6c2c0-166">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-166">No</span></span>              | <span data-ttu-id="6c2c0-167">Datumet då vagnen upphör att gälla, i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-167">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="6c2c0-168">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-168">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="6c2c0-169">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="6c2c0-169">lastModifiedUser</span></span>      | <span data-ttu-id="6c2c0-170">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-170">string</span></span>           | <span data-ttu-id="6c2c0-171">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-171">No</span></span>              | <span data-ttu-id="6c2c0-172">Den användare som senast uppdaterade vagnen.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-172">The user who last updated the cart.</span></span> <span data-ttu-id="6c2c0-173">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-173">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="6c2c0-174">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="6c2c0-174">lineItems</span></span>             | <span data-ttu-id="6c2c0-175">Objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="6c2c0-175">Array of objects</span></span> | <span data-ttu-id="6c2c0-176">Yes</span><span class="sxs-lookup"><span data-stu-id="6c2c0-176">Yes</span></span>             | <span data-ttu-id="6c2c0-177">En matris med [CartLineItem](cart-resources.md#cartlineitem) -resurser.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-177">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="6c2c0-178">I den här tabellen beskrivs egenskaperna för [CartLineItem](cart-resources.md#cartlineitem) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-178">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="6c2c0-179">Egenskap</span><span class="sxs-lookup"><span data-stu-id="6c2c0-179">Property</span></span>             | <span data-ttu-id="6c2c0-180">Typ</span><span class="sxs-lookup"><span data-stu-id="6c2c0-180">Type</span></span>                        | <span data-ttu-id="6c2c0-181">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6c2c0-181">Required</span></span>     | <span data-ttu-id="6c2c0-182">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6c2c0-182">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c2c0-183">id</span><span class="sxs-lookup"><span data-stu-id="6c2c0-183">id</span></span>                   | <span data-ttu-id="6c2c0-184">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-184">string</span></span>                      | <span data-ttu-id="6c2c0-185">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-185">No</span></span>           | <span data-ttu-id="6c2c0-186">En unik identifierare för ett vagn rads objekt.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-186">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="6c2c0-187">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-187">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="6c2c0-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="6c2c0-188">catalogId</span></span>            | <span data-ttu-id="6c2c0-189">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-189">string</span></span>                      | <span data-ttu-id="6c2c0-190">Yes</span><span class="sxs-lookup"><span data-stu-id="6c2c0-190">Yes</span></span>          | <span data-ttu-id="6c2c0-191">Katalog objekt identifierare.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-191">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="6c2c0-192">friendlyName</span><span class="sxs-lookup"><span data-stu-id="6c2c0-192">friendlyName</span></span>         | <span data-ttu-id="6c2c0-193">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-193">string</span></span>                      | <span data-ttu-id="6c2c0-194">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-194">No</span></span>           | <span data-ttu-id="6c2c0-195">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-195">Optional.</span></span> <span data-ttu-id="6c2c0-196">Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="6c2c0-197">quantity</span><span class="sxs-lookup"><span data-stu-id="6c2c0-197">quantity</span></span>             | <span data-ttu-id="6c2c0-198">int</span><span class="sxs-lookup"><span data-stu-id="6c2c0-198">int</span></span>                         | <span data-ttu-id="6c2c0-199">Yes</span><span class="sxs-lookup"><span data-stu-id="6c2c0-199">Yes</span></span>          | <span data-ttu-id="6c2c0-200">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-200">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="6c2c0-201">currencyCode</span><span class="sxs-lookup"><span data-stu-id="6c2c0-201">currencyCode</span></span>         | <span data-ttu-id="6c2c0-202">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-202">string</span></span>                      | <span data-ttu-id="6c2c0-203">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-203">No</span></span>           | <span data-ttu-id="6c2c0-204">Valuta koden.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-204">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="6c2c0-205">billingCycle</span><span class="sxs-lookup"><span data-stu-id="6c2c0-205">billingCycle</span></span>         | <span data-ttu-id="6c2c0-206">Objekt</span><span class="sxs-lookup"><span data-stu-id="6c2c0-206">Object</span></span>                      | <span data-ttu-id="6c2c0-207">Yes</span><span class="sxs-lookup"><span data-stu-id="6c2c0-207">Yes</span></span>          | <span data-ttu-id="6c2c0-208">Typ av fakturerings cykel som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-208">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="6c2c0-209">deltagare</span><span class="sxs-lookup"><span data-stu-id="6c2c0-209">participants</span></span>         | <span data-ttu-id="6c2c0-210">Lista med objekt sträng par</span><span class="sxs-lookup"><span data-stu-id="6c2c0-210">List of Object String pairs</span></span> | <span data-ttu-id="6c2c0-211">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-211">No</span></span>           | <span data-ttu-id="6c2c0-212">En samling deltagare på köpet.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-212">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="6c2c0-213">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="6c2c0-213">provisioningContext</span></span>  | <span data-ttu-id="6c2c0-214">Ord listans<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="6c2c0-214">Dictionary<string, string></span></span>  | <span data-ttu-id="6c2c0-215">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-215">No</span></span>           | <span data-ttu-id="6c2c0-216">En kontext som används för etablering av erbjudande.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-216">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="6c2c0-217">orderGroup</span><span class="sxs-lookup"><span data-stu-id="6c2c0-217">orderGroup</span></span>           | <span data-ttu-id="6c2c0-218">sträng</span><span class="sxs-lookup"><span data-stu-id="6c2c0-218">string</span></span>                      | <span data-ttu-id="6c2c0-219">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-219">No</span></span>           | <span data-ttu-id="6c2c0-220">En grupp som visar vilka objekt som kan placeras tillsammans.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-220">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="6c2c0-221">fel</span><span class="sxs-lookup"><span data-stu-id="6c2c0-221">error</span></span>                | <span data-ttu-id="6c2c0-222">Objekt</span><span class="sxs-lookup"><span data-stu-id="6c2c0-222">Object</span></span>                      | <span data-ttu-id="6c2c0-223">No</span><span class="sxs-lookup"><span data-stu-id="6c2c0-223">No</span></span>           | <span data-ttu-id="6c2c0-224">Tillämpas efter att kundvagn har skapats i händelse av ett fel.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-224">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="6c2c0-225">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6c2c0-225">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6c2c0-226">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6c2c0-226">REST response</span></span>

<span data-ttu-id="6c2c0-227">Om det lyckas returnerar den här metoden den fyllda kund [vagns](cart-resources.md) resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-227">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6c2c0-228">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6c2c0-228">Response success and error codes</span></span>

<span data-ttu-id="6c2c0-229">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6c2c0-230">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6c2c0-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6c2c0-231">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6c2c0-231">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6c2c0-232">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6c2c0-232">Response example</span></span>

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
