---
title: Skapa en kundvagn med tillägg
description: Lär dig hur du använder Partner Center-API:er för att lägga till en kundorder med tillägg via en kundvagn. Artikeln delar krav och steg för att skapa en kundvagn med tillägg.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 513a9607b9194c36253630c91de9622325317c3a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973765"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="ad6ab-104">Skapa en kundvagn med tillägg till en kundbeställning</span><span class="sxs-lookup"><span data-stu-id="ad6ab-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="ad6ab-105">Du kan köpa tillägg via en kundvagn.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-105">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="ad6ab-106">Mer information om vad som för närvarande är tillgängligt för försäljning finns [i Partnererbjudanden i Molnlösningsleverantör program](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="ad6ab-106">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad6ab-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ad6ab-107">Prerequisites</span></span>

- <span data-ttu-id="ad6ab-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ad6ab-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ad6ab-109">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ad6ab-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ad6ab-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ad6ab-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ad6ab-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ad6ab-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="ad6ab-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ad6ab-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="ad6ab-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ad6ab-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ad6ab-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ad6ab-116">C\#</span><span class="sxs-lookup"><span data-stu-id="ad6ab-116">C\#</span></span>

<span data-ttu-id="ad6ab-117">Med en kundvagn kan du köpa ett baserbjudande och motsvarande tillägg.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-117">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="ad6ab-118">Följ dessa steg för att skapa en kundvagn:</span><span class="sxs-lookup"><span data-stu-id="ad6ab-118">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="ad6ab-119">Skapa en instans av [**ett kundvagnsobjekt.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-119">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="ad6ab-120">Skapa en lista över [**CartLineItem-objekt**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) som representerar baserbjudandet och tilldela listan till kundvagnens [**lineItems-egenskap.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-120">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects that represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="ad6ab-121">Under varje baserbjudandes kundvagnsradsobjekt fyller du i listan **med AddOnItems** med andra **CartLineItem-objekt** som var och en representerar ett tillägg som ska köpas mot baserbjudandet.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-121">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="ad6ab-122">Hämta ett gränssnitt för kundvagnsåtgärder med [**hjälp av IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) för att anropa [**metoden ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och hämta sedan gränssnittet från **egenskapen Cart.**</span><span class="sxs-lookup"><span data-stu-id="ad6ab-122">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="ad6ab-123">Anropa slutligen metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) för att skapa kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-123">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="ad6ab-124">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="ad6ab-124">C\# example</span></span>

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

<span data-ttu-id="ad6ab-125">Följ de här stegen för att skapa en kundvagn som aktiverar köp av tillägg mot befintliga basprenumerationerna:</span><span class="sxs-lookup"><span data-stu-id="ad6ab-125">Follow these steps to create a cart that will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="ad6ab-126">Skapa en **kundvagn** med en ny **CartLineItem** som innehåller prenumerations-ID:t i **egenskapen ProvisioningContext** med nyckeln "ParentSubscriptionId".</span><span class="sxs-lookup"><span data-stu-id="ad6ab-126">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="ad6ab-127">Anropa metoden **Create** eller **CreateAsync.**</span><span class="sxs-lookup"><span data-stu-id="ad6ab-127">Call the **Create** or **CreateAsync** method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="ad6ab-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ad6ab-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ad6ab-129">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ad6ab-129">Request syntax</span></span>

| <span data-ttu-id="ad6ab-130">Metod</span><span class="sxs-lookup"><span data-stu-id="ad6ab-130">Method</span></span>   | <span data-ttu-id="ad6ab-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ad6ab-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad6ab-132">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="ad6ab-132">**POST**</span></span> | <span data-ttu-id="ad6ab-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ad6ab-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="ad6ab-134">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ad6ab-134">URI parameter</span></span>

<span data-ttu-id="ad6ab-135">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-135">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="ad6ab-136">Namn</span><span class="sxs-lookup"><span data-stu-id="ad6ab-136">Name</span></span>            | <span data-ttu-id="ad6ab-137">Typ</span><span class="sxs-lookup"><span data-stu-id="ad6ab-137">Type</span></span>     | <span data-ttu-id="ad6ab-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ad6ab-138">Required</span></span> | <span data-ttu-id="ad6ab-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ad6ab-139">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="ad6ab-140">**kund-id**</span><span class="sxs-lookup"><span data-stu-id="ad6ab-140">**customer-id**</span></span> | <span data-ttu-id="ad6ab-141">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-141">string</span></span>   | <span data-ttu-id="ad6ab-142">Ja</span><span class="sxs-lookup"><span data-stu-id="ad6ab-142">Yes</span></span>      | <span data-ttu-id="ad6ab-143">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-143">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="ad6ab-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ad6ab-144">Request headers</span></span>

<span data-ttu-id="ad6ab-145">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ad6ab-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ad6ab-146">Request body</span></span>

<span data-ttu-id="ad6ab-147">I den här tabellen beskrivs [egenskaperna för](cart-resources.md) Kundvagn i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-147">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="ad6ab-148">Egenskap</span><span class="sxs-lookup"><span data-stu-id="ad6ab-148">Property</span></span>              | <span data-ttu-id="ad6ab-149">Typ</span><span class="sxs-lookup"><span data-stu-id="ad6ab-149">Type</span></span>             | <span data-ttu-id="ad6ab-150">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ad6ab-150">Required</span></span>        | <span data-ttu-id="ad6ab-151">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ad6ab-151">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad6ab-152">id</span><span class="sxs-lookup"><span data-stu-id="ad6ab-152">id</span></span>                    | <span data-ttu-id="ad6ab-153">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-153">string</span></span>           | <span data-ttu-id="ad6ab-154">No</span><span class="sxs-lookup"><span data-stu-id="ad6ab-154">No</span></span>              | <span data-ttu-id="ad6ab-155">En kundvagnsidentifierare som anges när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-155">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="ad6ab-156">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ad6ab-156">creationTimeStamp</span></span>     | <span data-ttu-id="ad6ab-157">DateTime</span><span class="sxs-lookup"><span data-stu-id="ad6ab-157">DateTime</span></span>         | <span data-ttu-id="ad6ab-158">Inga</span><span class="sxs-lookup"><span data-stu-id="ad6ab-158">No</span></span>              | <span data-ttu-id="ad6ab-159">Datumet då kundvagnen skapades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-159">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="ad6ab-160">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-160">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="ad6ab-161">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ad6ab-161">lastModifiedTimeStamp</span></span> | <span data-ttu-id="ad6ab-162">DateTime</span><span class="sxs-lookup"><span data-stu-id="ad6ab-162">DateTime</span></span>         | <span data-ttu-id="ad6ab-163">Inga</span><span class="sxs-lookup"><span data-stu-id="ad6ab-163">No</span></span>              | <span data-ttu-id="ad6ab-164">Datum då kundvagnen senast uppdaterades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-164">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="ad6ab-165">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-165">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="ad6ab-166">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ad6ab-166">expirationTimeStamp</span></span>   | <span data-ttu-id="ad6ab-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="ad6ab-167">DateTime</span></span>         | <span data-ttu-id="ad6ab-168">Inga</span><span class="sxs-lookup"><span data-stu-id="ad6ab-168">No</span></span>              | <span data-ttu-id="ad6ab-169">Datumet då kundvagnen upphör att gälla i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-169">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="ad6ab-170">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-170">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="ad6ab-171">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="ad6ab-171">lastModifiedUser</span></span>      | <span data-ttu-id="ad6ab-172">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-172">string</span></span>           | <span data-ttu-id="ad6ab-173">No</span><span class="sxs-lookup"><span data-stu-id="ad6ab-173">No</span></span>              | <span data-ttu-id="ad6ab-174">Den användare som senast uppdaterade kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-174">The user who last updated the cart.</span></span> <span data-ttu-id="ad6ab-175">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-175">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="ad6ab-176">lineItems</span><span class="sxs-lookup"><span data-stu-id="ad6ab-176">lineItems</span></span>             | <span data-ttu-id="ad6ab-177">Matris med objekt</span><span class="sxs-lookup"><span data-stu-id="ad6ab-177">Array of objects</span></span> | <span data-ttu-id="ad6ab-178">Ja</span><span class="sxs-lookup"><span data-stu-id="ad6ab-178">Yes</span></span>             | <span data-ttu-id="ad6ab-179">En matris med [CartLineItem-resurser.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-179">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="ad6ab-180">I den här tabellen beskrivs [egenskaperna för CartLineItem](cart-resources.md#cartlineitem) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-180">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="ad6ab-181">Egenskap</span><span class="sxs-lookup"><span data-stu-id="ad6ab-181">Property</span></span>             | <span data-ttu-id="ad6ab-182">Typ</span><span class="sxs-lookup"><span data-stu-id="ad6ab-182">Type</span></span>                             | <span data-ttu-id="ad6ab-183">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ad6ab-183">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad6ab-184">id</span><span class="sxs-lookup"><span data-stu-id="ad6ab-184">id</span></span>                   | <span data-ttu-id="ad6ab-185">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-185">string</span></span>                           | <span data-ttu-id="ad6ab-186">En unik identifierare för ett kundvagnsradsobjekt.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-186">A unique identifier for a cart line item.</span></span> <span data-ttu-id="ad6ab-187">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-187">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="ad6ab-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="ad6ab-188">catalogId</span></span>            | <span data-ttu-id="ad6ab-189">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-189">string</span></span>                           | <span data-ttu-id="ad6ab-190">Katalogobjektets identifierare.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-190">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="ad6ab-191">friendlyName</span><span class="sxs-lookup"><span data-stu-id="ad6ab-191">friendlyName</span></span>         | <span data-ttu-id="ad6ab-192">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-192">string</span></span>                           | <span data-ttu-id="ad6ab-193">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-193">Optional.</span></span> <span data-ttu-id="ad6ab-194">Det egna namnet för det objekt som definierats av partnern för att undvika tvetydighet.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="ad6ab-195">quantity</span><span class="sxs-lookup"><span data-stu-id="ad6ab-195">quantity</span></span>             | <span data-ttu-id="ad6ab-196">int</span><span class="sxs-lookup"><span data-stu-id="ad6ab-196">int</span></span>                              | <span data-ttu-id="ad6ab-197">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-197">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="ad6ab-198">currencyCode</span><span class="sxs-lookup"><span data-stu-id="ad6ab-198">currencyCode</span></span>         | <span data-ttu-id="ad6ab-199">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-199">string</span></span>                           | <span data-ttu-id="ad6ab-200">Valutakoden.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-200">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="ad6ab-201">billingCycle</span><span class="sxs-lookup"><span data-stu-id="ad6ab-201">billingCycle</span></span>         | <span data-ttu-id="ad6ab-202">Objekt</span><span class="sxs-lookup"><span data-stu-id="ad6ab-202">Object</span></span>                           | <span data-ttu-id="ad6ab-203">Den typ av faktureringsperiod som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-203">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="ad6ab-204">deltagare</span><span class="sxs-lookup"><span data-stu-id="ad6ab-204">participants</span></span>         | <span data-ttu-id="ad6ab-205">Lista över objektsträngpar</span><span class="sxs-lookup"><span data-stu-id="ad6ab-205">List of Object String pairs</span></span>      | <span data-ttu-id="ad6ab-206">En samling PartnerId on Record (MPN ID) för köpet.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-206">A collection of PartnerId on Record (MPN ID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="ad6ab-207">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="ad6ab-207">provisioningContext</span></span>  | <span data-ttu-id="ad6ab-208">Ordlista<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="ad6ab-208">Dictionary<string, string></span></span>       | <span data-ttu-id="ad6ab-209">En kontext som används för etablering av erbjudande.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-209">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="ad6ab-210">orderGroup</span><span class="sxs-lookup"><span data-stu-id="ad6ab-210">orderGroup</span></span>           | <span data-ttu-id="ad6ab-211">sträng</span><span class="sxs-lookup"><span data-stu-id="ad6ab-211">string</span></span>                           | <span data-ttu-id="ad6ab-212">En grupp som anger vilka objekt som kan placeras tillsammans.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-212">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="ad6ab-213">addonItems</span><span class="sxs-lookup"><span data-stu-id="ad6ab-213">addonItems</span></span>           | <span data-ttu-id="ad6ab-214">Lista över **CartLineItem-objekt**</span><span class="sxs-lookup"><span data-stu-id="ad6ab-214">List of **CartLineItem** objects</span></span> | <span data-ttu-id="ad6ab-215">En samling kundvagnsradsobjekt för tillägg som ska köpas mot basprenumerationen som är resultatet av den överordnade kundvagnsradens köp.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-215">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="ad6ab-216">fel</span><span class="sxs-lookup"><span data-stu-id="ad6ab-216">error</span></span>                | <span data-ttu-id="ad6ab-217">Objekt</span><span class="sxs-lookup"><span data-stu-id="ad6ab-217">Object</span></span>                           | <span data-ttu-id="ad6ab-218">Tillämpas efter att kundvagnen har skapats om det finns ett fel.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-218">Applied after cart is created if there is an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="ad6ab-219">Exempel på begäran (ny basprenumeration)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-219">Request example (new base subscription)</span></span>

<span data-ttu-id="ad6ab-220">I följande REST-exempel visas hur du skapar en kundvagn med tillägg för en ny basprenumeration.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-220">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

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

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="ad6ab-221">Exempel på begäran (befintlig basprenumeration)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-221">Request example (existing base subscription)</span></span>

<span data-ttu-id="ad6ab-222">I följande REST-exempel visas hur du lägger till tillägg till en befintlig basprenumeration.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-222">The following REST example shows how to append add-ons to an existing base subscription.</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ad6ab-223">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ad6ab-223">REST response</span></span>

<span data-ttu-id="ad6ab-224">Om det lyckas returnerar den här metoden den [ifyllda kundvagnsresursen](cart-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-224">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="ad6ab-225">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ad6ab-225">Response success and error codes</span></span>

<span data-ttu-id="ad6ab-226">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-226">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ad6ab-227">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ad6ab-227">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ad6ab-228">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-228">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="ad6ab-229">Svarsexempel (ny basprenumeration)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-229">Response example (new base subscription)</span></span>

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

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="ad6ab-230">Svarsexempel (befintlig basprenumeration)</span><span class="sxs-lookup"><span data-stu-id="ad6ab-230">Response example (existing base subscription)</span></span>

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
