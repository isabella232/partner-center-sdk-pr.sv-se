---
title: Skapa en kundvagn med tillägg
description: 'Lär dig hur du använder API: er för partner Center för att lägga till en kund order med tillägg via en kundvagn. Artikeln delar krav och steg för att skapa en kundvagn med tilläggsprogram.'
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770131"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="b548f-104">Skapa en kundvagn med tillägg till en kund order</span><span class="sxs-lookup"><span data-stu-id="b548f-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="b548f-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="b548f-105">**Applies to:**</span></span>

- <span data-ttu-id="b548f-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b548f-106">Partner Center</span></span>

<span data-ttu-id="b548f-107">Du kan köpa tillägg via en kundvagn.</span><span class="sxs-lookup"><span data-stu-id="b548f-107">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="b548f-108">Mer information om vad som för närvarande är tillgängligt för försäljning finns [i partner erbjudanden i Cloud Solution Provider-programmet](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="b548f-108">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b548f-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b548f-109">Prerequisites</span></span>

- <span data-ttu-id="b548f-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b548f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b548f-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b548f-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b548f-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b548f-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b548f-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="b548f-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b548f-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="b548f-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b548f-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="b548f-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b548f-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="b548f-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b548f-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b548f-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b548f-118">C\#</span><span class="sxs-lookup"><span data-stu-id="b548f-118">C\#</span></span>

<span data-ttu-id="b548f-119">En varukorg gör det möjligt att köpa ett bas erbjudande och dess motsvarande tillägg.</span><span class="sxs-lookup"><span data-stu-id="b548f-119">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="b548f-120">Följ de här stegen för att skapa en kundvagn:</span><span class="sxs-lookup"><span data-stu-id="b548f-120">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="b548f-121">Instansiera ett [**vagn**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) objekt.</span><span class="sxs-lookup"><span data-stu-id="b548f-121">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="b548f-122">Skapa en lista med [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) -objekt som representerar bas erbjudandet och tilldela listan till vagnens [**rad objekt**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) -egenskap.</span><span class="sxs-lookup"><span data-stu-id="b548f-122">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects which represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="b548f-123">Under varje bas erbjudandes rad artikel fyller du i listan över **AddOnItems** med andra **CartLineItem** -objekt som var och en representerar ett tillägg som ska köpas mot bas erbjudandet.</span><span class="sxs-lookup"><span data-stu-id="b548f-123">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="b548f-124">Få ett gränssnitt till shopping operationer genom att använda [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) för att anropa metoden [**ICustomerCollection. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och sedan hämta gränssnittet från egenskapen **kundvagn** .</span><span class="sxs-lookup"><span data-stu-id="b548f-124">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="b548f-125">Anropa slutligen metoden [**create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) för att skapa vagnen.</span><span class="sxs-lookup"><span data-stu-id="b548f-125">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="b548f-126">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="b548f-126">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

<span data-ttu-id="b548f-127">Följ de här stegen för att skapa en varukorg som gör det möjligt att köpa tillägg mot befintliga bas prenumerationer:</span><span class="sxs-lookup"><span data-stu-id="b548f-127">Follow these steps to create a cart which will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="b548f-128">Skapa en **varukorg** med en ny **CartLineItem** som innehåller prenumerations-ID: t i egenskapen **ProvisioningContext** med nyckeln "ParentSubscriptionId".</span><span class="sxs-lookup"><span data-stu-id="b548f-128">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="b548f-129">Anropa metoden **create** eller **CreateAsync** .</span><span class="sxs-lookup"><span data-stu-id="b548f-129">Call the **Create** or **CreateAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a><span data-ttu-id="b548f-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b548f-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b548f-131">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b548f-131">Request syntax</span></span>

| <span data-ttu-id="b548f-132">Metod</span><span class="sxs-lookup"><span data-stu-id="b548f-132">Method</span></span>   | <span data-ttu-id="b548f-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b548f-133">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b548f-134">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="b548f-134">**POST**</span></span> | <span data-ttu-id="b548f-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="b548f-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="b548f-136">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="b548f-136">URI parameter</span></span>

<span data-ttu-id="b548f-137">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="b548f-137">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="b548f-138">Namn</span><span class="sxs-lookup"><span data-stu-id="b548f-138">Name</span></span>            | <span data-ttu-id="b548f-139">Typ</span><span class="sxs-lookup"><span data-stu-id="b548f-139">Type</span></span>     | <span data-ttu-id="b548f-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b548f-140">Required</span></span> | <span data-ttu-id="b548f-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b548f-141">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="b548f-142">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="b548f-142">**customer-id**</span></span> | <span data-ttu-id="b548f-143">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-143">string</span></span>   | <span data-ttu-id="b548f-144">Yes</span><span class="sxs-lookup"><span data-stu-id="b548f-144">Yes</span></span>      | <span data-ttu-id="b548f-145">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="b548f-145">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="b548f-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b548f-146">Request headers</span></span>

<span data-ttu-id="b548f-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b548f-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b548f-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b548f-148">Request body</span></span>

<span data-ttu-id="b548f-149">I den här tabellen beskrivs egenskaperna för [kundvagn](cart-resources.md) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="b548f-149">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="b548f-150">Egenskap</span><span class="sxs-lookup"><span data-stu-id="b548f-150">Property</span></span>              | <span data-ttu-id="b548f-151">Typ</span><span class="sxs-lookup"><span data-stu-id="b548f-151">Type</span></span>             | <span data-ttu-id="b548f-152">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b548f-152">Required</span></span>        | <span data-ttu-id="b548f-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b548f-153">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b548f-154">id</span><span class="sxs-lookup"><span data-stu-id="b548f-154">id</span></span>                    | <span data-ttu-id="b548f-155">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-155">string</span></span>           | <span data-ttu-id="b548f-156">No</span><span class="sxs-lookup"><span data-stu-id="b548f-156">No</span></span>              | <span data-ttu-id="b548f-157">Ett kundvagn-ID som anges när vagnen skapas.</span><span class="sxs-lookup"><span data-stu-id="b548f-157">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="b548f-158">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="b548f-158">creationTimeStamp</span></span>     | <span data-ttu-id="b548f-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="b548f-159">DateTime</span></span>         | <span data-ttu-id="b548f-160">No</span><span class="sxs-lookup"><span data-stu-id="b548f-160">No</span></span>              | <span data-ttu-id="b548f-161">Datumet då vagnen skapades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="b548f-161">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="b548f-162">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="b548f-162">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="b548f-163">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="b548f-163">lastModifiedTimeStamp</span></span> | <span data-ttu-id="b548f-164">DateTime</span><span class="sxs-lookup"><span data-stu-id="b548f-164">DateTime</span></span>         | <span data-ttu-id="b548f-165">No</span><span class="sxs-lookup"><span data-stu-id="b548f-165">No</span></span>              | <span data-ttu-id="b548f-166">Datumet då vagnen senast uppdaterades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="b548f-166">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="b548f-167">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="b548f-167">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="b548f-168">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="b548f-168">expirationTimeStamp</span></span>   | <span data-ttu-id="b548f-169">DateTime</span><span class="sxs-lookup"><span data-stu-id="b548f-169">DateTime</span></span>         | <span data-ttu-id="b548f-170">No</span><span class="sxs-lookup"><span data-stu-id="b548f-170">No</span></span>              | <span data-ttu-id="b548f-171">Datumet då vagnen upphör att gälla, i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="b548f-171">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="b548f-172">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="b548f-172">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="b548f-173">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="b548f-173">lastModifiedUser</span></span>      | <span data-ttu-id="b548f-174">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-174">string</span></span>           | <span data-ttu-id="b548f-175">No</span><span class="sxs-lookup"><span data-stu-id="b548f-175">No</span></span>              | <span data-ttu-id="b548f-176">Den användare som senast uppdaterade vagnen.</span><span class="sxs-lookup"><span data-stu-id="b548f-176">The user who last updated the cart.</span></span> <span data-ttu-id="b548f-177">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="b548f-177">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="b548f-178">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="b548f-178">lineItems</span></span>             | <span data-ttu-id="b548f-179">Objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="b548f-179">Array of objects</span></span> | <span data-ttu-id="b548f-180">Yes</span><span class="sxs-lookup"><span data-stu-id="b548f-180">Yes</span></span>             | <span data-ttu-id="b548f-181">En matris med [CartLineItem](cart-resources.md#cartlineitem) -resurser.</span><span class="sxs-lookup"><span data-stu-id="b548f-181">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="b548f-182">I den här tabellen beskrivs egenskaperna för [CartLineItem](cart-resources.md#cartlineitem) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="b548f-182">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="b548f-183">Egenskap</span><span class="sxs-lookup"><span data-stu-id="b548f-183">Property</span></span>             | <span data-ttu-id="b548f-184">Typ</span><span class="sxs-lookup"><span data-stu-id="b548f-184">Type</span></span>                             | <span data-ttu-id="b548f-185">Description</span><span class="sxs-lookup"><span data-stu-id="b548f-185">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b548f-186">id</span><span class="sxs-lookup"><span data-stu-id="b548f-186">id</span></span>                   | <span data-ttu-id="b548f-187">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-187">string</span></span>                           | <span data-ttu-id="b548f-188">En unik identifierare för ett vagn rads objekt.</span><span class="sxs-lookup"><span data-stu-id="b548f-188">A unique identifier for a cart line item.</span></span> <span data-ttu-id="b548f-189">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="b548f-189">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="b548f-190">catalogId</span><span class="sxs-lookup"><span data-stu-id="b548f-190">catalogId</span></span>            | <span data-ttu-id="b548f-191">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-191">string</span></span>                           | <span data-ttu-id="b548f-192">Katalog objekt identifierare.</span><span class="sxs-lookup"><span data-stu-id="b548f-192">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="b548f-193">friendlyName</span><span class="sxs-lookup"><span data-stu-id="b548f-193">friendlyName</span></span>         | <span data-ttu-id="b548f-194">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-194">string</span></span>                           | <span data-ttu-id="b548f-195">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="b548f-195">Optional.</span></span> <span data-ttu-id="b548f-196">Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.</span><span class="sxs-lookup"><span data-stu-id="b548f-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="b548f-197">quantity</span><span class="sxs-lookup"><span data-stu-id="b548f-197">quantity</span></span>             | <span data-ttu-id="b548f-198">int</span><span class="sxs-lookup"><span data-stu-id="b548f-198">int</span></span>                              | <span data-ttu-id="b548f-199">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="b548f-199">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="b548f-200">currencyCode</span><span class="sxs-lookup"><span data-stu-id="b548f-200">currencyCode</span></span>         | <span data-ttu-id="b548f-201">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-201">string</span></span>                           | <span data-ttu-id="b548f-202">Valuta koden.</span><span class="sxs-lookup"><span data-stu-id="b548f-202">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="b548f-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="b548f-203">billingCycle</span></span>         | <span data-ttu-id="b548f-204">Objekt</span><span class="sxs-lookup"><span data-stu-id="b548f-204">Object</span></span>                           | <span data-ttu-id="b548f-205">Typ av fakturerings cykel som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="b548f-205">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="b548f-206">deltagare</span><span class="sxs-lookup"><span data-stu-id="b548f-206">participants</span></span>         | <span data-ttu-id="b548f-207">Lista med objekt sträng par</span><span class="sxs-lookup"><span data-stu-id="b548f-207">List of Object String pairs</span></span>      | <span data-ttu-id="b548f-208">En samling partner on Record (MPNID) på köpet.</span><span class="sxs-lookup"><span data-stu-id="b548f-208">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="b548f-209">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="b548f-209">provisioningContext</span></span>  | <span data-ttu-id="b548f-210">Ord listans<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="b548f-210">Dictionary<string, string></span></span>       | <span data-ttu-id="b548f-211">En kontext som används för etablering av erbjudande.</span><span class="sxs-lookup"><span data-stu-id="b548f-211">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="b548f-212">orderGroup</span><span class="sxs-lookup"><span data-stu-id="b548f-212">orderGroup</span></span>           | <span data-ttu-id="b548f-213">sträng</span><span class="sxs-lookup"><span data-stu-id="b548f-213">string</span></span>                           | <span data-ttu-id="b548f-214">En grupp som visar vilka objekt som kan placeras tillsammans.</span><span class="sxs-lookup"><span data-stu-id="b548f-214">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="b548f-215">addonItems</span><span class="sxs-lookup"><span data-stu-id="b548f-215">addonItems</span></span>           | <span data-ttu-id="b548f-216">Lista över **CartLineItem** -objekt</span><span class="sxs-lookup"><span data-stu-id="b548f-216">List of **CartLineItem** objects</span></span> | <span data-ttu-id="b548f-217">En samling av vagn rads objekt för tillägg som kommer att köpas mot bas prenumerationen som är resultatet av den överordnade vagnens rad objekts inköp.</span><span class="sxs-lookup"><span data-stu-id="b548f-217">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="b548f-218">fel</span><span class="sxs-lookup"><span data-stu-id="b548f-218">error</span></span>                | <span data-ttu-id="b548f-219">Objekt</span><span class="sxs-lookup"><span data-stu-id="b548f-219">Object</span></span>                           | <span data-ttu-id="b548f-220">Tillämpas efter att kundvagn har skapats i händelse av ett fel.</span><span class="sxs-lookup"><span data-stu-id="b548f-220">Applied after cart is created in case of an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="b548f-221">Exempel på begäran (ny bas prenumeration)</span><span class="sxs-lookup"><span data-stu-id="b548f-221">Request example (new base subscription)</span></span>

<span data-ttu-id="b548f-222">I följande REST-exempel visas hur du skapar en kundvagn med tilläggs objekt för en ny bas prenumeration.</span><span class="sxs-lookup"><span data-stu-id="b548f-222">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="b548f-223">Exempel på begäran (befintlig bas prenumeration)</span><span class="sxs-lookup"><span data-stu-id="b548f-223">Request example (existing base subscription)</span></span>

<span data-ttu-id="b548f-224">I följande REST-exempel visas hur du lägger till tillägg i en befintlig bas prenumeration.</span><span class="sxs-lookup"><span data-stu-id="b548f-224">The following REST example show how to append add-ons to an existing base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="b548f-225">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b548f-225">REST response</span></span>

<span data-ttu-id="b548f-226">Om det lyckas returnerar den här metoden den fyllda kund [vagns](cart-resources.md) resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="b548f-226">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="b548f-227">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b548f-227">Response success and error codes</span></span>

<span data-ttu-id="b548f-228">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b548f-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b548f-229">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b548f-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b548f-230">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b548f-230">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="b548f-231">Svars exempel (ny bas prenumeration)</span><span class="sxs-lookup"><span data-stu-id="b548f-231">Response example (new base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="b548f-232">Svars exempel (befintlig bas prenumeration)</span><span class="sxs-lookup"><span data-stu-id="b548f-232">Response example (existing base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
