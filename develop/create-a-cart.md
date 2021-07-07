---
title: Skapa en kundvagn
description: Lär dig hur du använder Partner Center-API:er för att lägga till en order för en kund i en kundvagn. Ämnet innehåller information om hur du skapar en kundvagn och eventuella krav.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: dba54d4f6b97f3d0a51e2f87b32edca686466b89
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973782"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="1f909-104">Skapa en kundvagn med en kundorder</span><span class="sxs-lookup"><span data-stu-id="1f909-104">Create a cart with a customer order</span></span>

<span data-ttu-id="1f909-105">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1f909-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1f909-106">Du kan lägga till en order för en kund i en kundvagn.</span><span class="sxs-lookup"><span data-stu-id="1f909-106">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="1f909-107">Mer information om vad som för närvarande är tillgängligt för försäljning finns [i Partnererbjudanden i Molnlösningsleverantör program](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="1f909-107">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f909-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1f909-108">Prerequisites</span></span>

- <span data-ttu-id="1f909-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1f909-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1f909-110">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1f909-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1f909-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1f909-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1f909-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1f909-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1f909-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="1f909-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1f909-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="1f909-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1f909-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="1f909-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1f909-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1f909-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1f909-117">C\#</span><span class="sxs-lookup"><span data-stu-id="1f909-117">C\#</span></span>

<span data-ttu-id="1f909-118">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="1f909-118">To create an order for a customer:</span></span>

1. <span data-ttu-id="1f909-119">Skapa en instans av ett kundvagnsobjekt.</span><span class="sxs-lookup"><span data-stu-id="1f909-119">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="1f909-120">Skapa en lista över **CartLineItem-objekt** och tilldela listan till kundvagnens LineItems-egenskap.</span><span class="sxs-lookup"><span data-stu-id="1f909-120">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="1f909-121">Varje kundvagnsrad innehåller inköpsinformationen för en produkt.</span><span class="sxs-lookup"><span data-stu-id="1f909-121">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="1f909-122">Du måste ha minst en kundvagnsrad.</span><span class="sxs-lookup"><span data-stu-id="1f909-122">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="1f909-123">Hämta ett gränssnitt för kundvagnsåtgärder genom att anropa metoden **IAggregatePartner.Customers.ById** med kund-ID:t för att identifiera kunden och sedan hämta gränssnittet från **egenskapen Cart.**</span><span class="sxs-lookup"><span data-stu-id="1f909-123">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="1f909-124">Anropa metoden **Create** eller **CreateAsync** för att skapa kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="1f909-124">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="1f909-125">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="1f909-125">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a><span data-ttu-id="1f909-126">Java</span><span class="sxs-lookup"><span data-stu-id="1f909-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="1f909-127">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="1f909-127">To create an order for a customer:</span></span>

1. <span data-ttu-id="1f909-128">Skapa en instans av ett kundvagnsobjekt.</span><span class="sxs-lookup"><span data-stu-id="1f909-128">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="1f909-129">Skapa en lista över **CartLineItem-objekt** och tilldela listan till kundvagnens radobjekt.</span><span class="sxs-lookup"><span data-stu-id="1f909-129">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="1f909-130">Varje kundvagnsrad innehåller inköpsinformationen för en produkt.</span><span class="sxs-lookup"><span data-stu-id="1f909-130">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="1f909-131">Du måste ha minst en kundvagnsrad.</span><span class="sxs-lookup"><span data-stu-id="1f909-131">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="1f909-132">Hämta ett gränssnitt för kundvagnsåtgärder genom att anropa funktionen **IAggregatePartner.getCustomers().byId** med kund-ID:t för att identifiera kunden och sedan hämta gränssnittet från **funktionen getCart.**</span><span class="sxs-lookup"><span data-stu-id="1f909-132">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="1f909-133">Anropa **create-funktionen** för att skapa kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="1f909-133">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="1f909-134">Java-exempel</span><span class="sxs-lookup"><span data-stu-id="1f909-134">Java example</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a><span data-ttu-id="1f909-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f909-135">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="1f909-136">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="1f909-136">To create an order for a customer:</span></span>

1. <span data-ttu-id="1f909-137">Skapa en instans av ett kundvagnsobjekt.</span><span class="sxs-lookup"><span data-stu-id="1f909-137">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="1f909-138">Skapa en lista över **CartLineItem-objekt** och tilldela listan till kundvagnens radobjekt.</span><span class="sxs-lookup"><span data-stu-id="1f909-138">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="1f909-139">Varje kundvagnsrad innehåller inköpsinformationen för en produkt.</span><span class="sxs-lookup"><span data-stu-id="1f909-139">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="1f909-140">Du måste ha minst en kundvagnsrad.</span><span class="sxs-lookup"><span data-stu-id="1f909-140">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="1f909-141">Kör kommandot [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) för att skapa kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="1f909-141">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a><span data-ttu-id="1f909-142">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1f909-142">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1f909-143">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="1f909-143">Request syntax</span></span>

| <span data-ttu-id="1f909-144">Metod</span><span class="sxs-lookup"><span data-stu-id="1f909-144">Method</span></span>   | <span data-ttu-id="1f909-145">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1f909-145">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1f909-146">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="1f909-146">**POST**</span></span> | <span data-ttu-id="1f909-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1f909-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="1f909-148">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="1f909-148">URI parameter</span></span>

<span data-ttu-id="1f909-149">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="1f909-149">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="1f909-150">Namn</span><span class="sxs-lookup"><span data-stu-id="1f909-150">Name</span></span>            | <span data-ttu-id="1f909-151">Typ</span><span class="sxs-lookup"><span data-stu-id="1f909-151">Type</span></span>     | <span data-ttu-id="1f909-152">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1f909-152">Required</span></span> | <span data-ttu-id="1f909-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1f909-153">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="1f909-154">**kund-id**</span><span class="sxs-lookup"><span data-stu-id="1f909-154">**customer-id**</span></span> | <span data-ttu-id="1f909-155">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-155">string</span></span>   | <span data-ttu-id="1f909-156">Ja</span><span class="sxs-lookup"><span data-stu-id="1f909-156">Yes</span></span>      | <span data-ttu-id="1f909-157">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="1f909-157">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="1f909-158">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1f909-158">Request headers</span></span>

<span data-ttu-id="1f909-159">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1f909-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1f909-160">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1f909-160">Request body</span></span>

<span data-ttu-id="1f909-161">I den här tabellen beskrivs [egenskaperna för](cart-resources.md) Kundvagn i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="1f909-161">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="1f909-162">Egenskap</span><span class="sxs-lookup"><span data-stu-id="1f909-162">Property</span></span>              | <span data-ttu-id="1f909-163">Typ</span><span class="sxs-lookup"><span data-stu-id="1f909-163">Type</span></span>             | <span data-ttu-id="1f909-164">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1f909-164">Required</span></span>        | <span data-ttu-id="1f909-165">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1f909-165">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1f909-166">id</span><span class="sxs-lookup"><span data-stu-id="1f909-166">id</span></span>                    | <span data-ttu-id="1f909-167">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-167">string</span></span>           | <span data-ttu-id="1f909-168">No</span><span class="sxs-lookup"><span data-stu-id="1f909-168">No</span></span>              | <span data-ttu-id="1f909-169">En kundvagnsidentifierare som anges när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1f909-169">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="1f909-170">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="1f909-170">creationTimeStamp</span></span>     | <span data-ttu-id="1f909-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="1f909-171">DateTime</span></span>         | <span data-ttu-id="1f909-172">Inga</span><span class="sxs-lookup"><span data-stu-id="1f909-172">No</span></span>              | <span data-ttu-id="1f909-173">Datumet då kundvagnen skapades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="1f909-173">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="1f909-174">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1f909-174">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="1f909-175">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="1f909-175">lastModifiedTimeStamp</span></span> | <span data-ttu-id="1f909-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="1f909-176">DateTime</span></span>         | <span data-ttu-id="1f909-177">Inga</span><span class="sxs-lookup"><span data-stu-id="1f909-177">No</span></span>              | <span data-ttu-id="1f909-178">Datum då kundvagnen senast uppdaterades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="1f909-178">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="1f909-179">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1f909-179">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="1f909-180">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="1f909-180">expirationTimeStamp</span></span>   | <span data-ttu-id="1f909-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="1f909-181">DateTime</span></span>         | <span data-ttu-id="1f909-182">Inga</span><span class="sxs-lookup"><span data-stu-id="1f909-182">No</span></span>              | <span data-ttu-id="1f909-183">Datumet då kundvagnen upphör att gälla i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="1f909-183">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="1f909-184">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1f909-184">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="1f909-185">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="1f909-185">lastModifiedUser</span></span>      | <span data-ttu-id="1f909-186">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-186">string</span></span>           | <span data-ttu-id="1f909-187">No</span><span class="sxs-lookup"><span data-stu-id="1f909-187">No</span></span>              | <span data-ttu-id="1f909-188">Den användare som senast uppdaterade kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="1f909-188">The user who last updated the cart.</span></span> <span data-ttu-id="1f909-189">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1f909-189">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="1f909-190">lineItems</span><span class="sxs-lookup"><span data-stu-id="1f909-190">lineItems</span></span>             | <span data-ttu-id="1f909-191">Matris med objekt</span><span class="sxs-lookup"><span data-stu-id="1f909-191">Array of objects</span></span> | <span data-ttu-id="1f909-192">Ja</span><span class="sxs-lookup"><span data-stu-id="1f909-192">Yes</span></span>             | <span data-ttu-id="1f909-193">En matris med [CartLineItem-resurser.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="1f909-193">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="1f909-194">I den här tabellen beskrivs [egenskaperna för CartLineItem](cart-resources.md#cartlineitem) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="1f909-194">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="1f909-195">Egenskap</span><span class="sxs-lookup"><span data-stu-id="1f909-195">Property</span></span>       |            <span data-ttu-id="1f909-196">Typ</span><span class="sxs-lookup"><span data-stu-id="1f909-196">Type</span></span>             | <span data-ttu-id="1f909-197">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1f909-197">Required</span></span> |                                                                                         <span data-ttu-id="1f909-198">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1f909-198">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="1f909-199">id</span><span class="sxs-lookup"><span data-stu-id="1f909-199">id</span></span>          |           <span data-ttu-id="1f909-200">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-200">string</span></span>            |    <span data-ttu-id="1f909-201">No</span><span class="sxs-lookup"><span data-stu-id="1f909-201">No</span></span>    |                                                     <span data-ttu-id="1f909-202">En unik identifierare för ett kundvagnsradsobjekt.</span><span class="sxs-lookup"><span data-stu-id="1f909-202">A unique identifier for a cart line item.</span></span> <span data-ttu-id="1f909-203">Tillämpas när kundvagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1f909-203">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="1f909-204">catalogId</span><span class="sxs-lookup"><span data-stu-id="1f909-204">catalogId</span></span>      |           <span data-ttu-id="1f909-205">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-205">string</span></span>            |   <span data-ttu-id="1f909-206">Ja</span><span class="sxs-lookup"><span data-stu-id="1f909-206">Yes</span></span>    |                                                                                <span data-ttu-id="1f909-207">Katalogobjektets identifierare.</span><span class="sxs-lookup"><span data-stu-id="1f909-207">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="1f909-208">friendlyName</span><span class="sxs-lookup"><span data-stu-id="1f909-208">friendlyName</span></span>     |           <span data-ttu-id="1f909-209">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-209">string</span></span>            |    <span data-ttu-id="1f909-210">No</span><span class="sxs-lookup"><span data-stu-id="1f909-210">No</span></span>    |                                                    <span data-ttu-id="1f909-211">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="1f909-211">Optional.</span></span> <span data-ttu-id="1f909-212">Det egna namnet för objektet som definierats av partnern för att undvika tvetydighet.</span><span class="sxs-lookup"><span data-stu-id="1f909-212">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="1f909-213">quantity</span><span class="sxs-lookup"><span data-stu-id="1f909-213">quantity</span></span>       |             <span data-ttu-id="1f909-214">int</span><span class="sxs-lookup"><span data-stu-id="1f909-214">int</span></span>             |   <span data-ttu-id="1f909-215">Ja</span><span class="sxs-lookup"><span data-stu-id="1f909-215">Yes</span></span>    |                                                                            <span data-ttu-id="1f909-216">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="1f909-216">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="1f909-217">currencyCode</span><span class="sxs-lookup"><span data-stu-id="1f909-217">currencyCode</span></span>     |           <span data-ttu-id="1f909-218">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-218">string</span></span>            |    <span data-ttu-id="1f909-219">No</span><span class="sxs-lookup"><span data-stu-id="1f909-219">No</span></span>    |                                                                                     <span data-ttu-id="1f909-220">Valutakoden.</span><span class="sxs-lookup"><span data-stu-id="1f909-220">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="1f909-221">billingCycle</span><span class="sxs-lookup"><span data-stu-id="1f909-221">billingCycle</span></span>     |           <span data-ttu-id="1f909-222">Objekt</span><span class="sxs-lookup"><span data-stu-id="1f909-222">Object</span></span>            |   <span data-ttu-id="1f909-223">Ja</span><span class="sxs-lookup"><span data-stu-id="1f909-223">Yes</span></span>    |                                                                    <span data-ttu-id="1f909-224">Den typ av faktureringsperiod som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="1f909-224">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="1f909-225">deltagare</span><span class="sxs-lookup"><span data-stu-id="1f909-225">participants</span></span>     | <span data-ttu-id="1f909-226">Lista över objektsträngpar</span><span class="sxs-lookup"><span data-stu-id="1f909-226">List of Object String pairs</span></span> |    <span data-ttu-id="1f909-227">Inga</span><span class="sxs-lookup"><span data-stu-id="1f909-227">No</span></span>    |                                                                <span data-ttu-id="1f909-228">En samling PartnerId on Record (MPNID) för köpet.</span><span class="sxs-lookup"><span data-stu-id="1f909-228">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="1f909-229">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="1f909-229">provisioningContext</span></span> | <span data-ttu-id="1f909-230">Ordlista<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="1f909-230">Dictionary<string, string></span></span>  |    <span data-ttu-id="1f909-231">Inga</span><span class="sxs-lookup"><span data-stu-id="1f909-231">No</span></span>    | <span data-ttu-id="1f909-232">Information som krävs för etablering för vissa objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="1f909-232">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="1f909-233">Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för specifika objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="1f909-233">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="1f909-234">orderGroup</span><span class="sxs-lookup"><span data-stu-id="1f909-234">orderGroup</span></span>      |           <span data-ttu-id="1f909-235">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-235">string</span></span>            |    <span data-ttu-id="1f909-236">No</span><span class="sxs-lookup"><span data-stu-id="1f909-236">No</span></span>    |                                                                   <span data-ttu-id="1f909-237">En grupp som anger vilka objekt som kan placeras tillsammans.</span><span class="sxs-lookup"><span data-stu-id="1f909-237">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="1f909-238">fel</span><span class="sxs-lookup"><span data-stu-id="1f909-238">error</span></span>        |           <span data-ttu-id="1f909-239">Objekt</span><span class="sxs-lookup"><span data-stu-id="1f909-239">Object</span></span>            |    <span data-ttu-id="1f909-240">Inga</span><span class="sxs-lookup"><span data-stu-id="1f909-240">No</span></span>    |                                                                     <span data-ttu-id="1f909-241">Tillämpas efter att kundvagnen har skapats om det finns ett fel.</span><span class="sxs-lookup"><span data-stu-id="1f909-241">Applied after cart is created if there is an error.</span></span>                                                                      |
|     <span data-ttu-id="1f909-242">renewsTo</span><span class="sxs-lookup"><span data-stu-id="1f909-242">renewsTo</span></span>        | <span data-ttu-id="1f909-243">Matris med objekt</span><span class="sxs-lookup"><span data-stu-id="1f909-243">Array of objects</span></span>            |    <span data-ttu-id="1f909-244">Inga</span><span class="sxs-lookup"><span data-stu-id="1f909-244">No</span></span>    |                                                    <span data-ttu-id="1f909-245">En matris med [RenewsTo-resurser.](cart-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="1f909-245">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="1f909-246">I den här tabellen beskrivs [egenskaperna RenewsTo](cart-resources.md#renewsto) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="1f909-246">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="1f909-247">Egenskap</span><span class="sxs-lookup"><span data-stu-id="1f909-247">Property</span></span>              | <span data-ttu-id="1f909-248">Typ</span><span class="sxs-lookup"><span data-stu-id="1f909-248">Type</span></span>             | <span data-ttu-id="1f909-249">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1f909-249">Required</span></span>        | <span data-ttu-id="1f909-250">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1f909-250">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1f909-251">termDuration</span><span class="sxs-lookup"><span data-stu-id="1f909-251">termDuration</span></span>          | <span data-ttu-id="1f909-252">sträng</span><span class="sxs-lookup"><span data-stu-id="1f909-252">string</span></span>           | <span data-ttu-id="1f909-253">No</span><span class="sxs-lookup"><span data-stu-id="1f909-253">No</span></span>              | <span data-ttu-id="1f909-254">En ISO 8601-representation av förnyelseperiodens varaktighet.</span><span class="sxs-lookup"><span data-stu-id="1f909-254">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="1f909-255">De aktuella värdena som stöds **är P1M** (1 månad) och **P1Y** (1 år).</span><span class="sxs-lookup"><span data-stu-id="1f909-255">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="1f909-256">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1f909-256">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
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
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="1f909-257">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1f909-257">REST response</span></span>

<span data-ttu-id="1f909-258">Om det lyckas returnerar den här metoden den [ifyllda kundvagnsresursen](cart-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="1f909-258">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1f909-259">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1f909-259">Response success and error codes</span></span>

<span data-ttu-id="1f909-260">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="1f909-260">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1f909-261">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1f909-261">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1f909-262">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1f909-262">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1f909-263">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1f909-263">Response example</span></span>

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
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
