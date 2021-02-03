---
title: Skapa en kundvagn
description: 'Lär dig hur du använder API: er för partner Center för att lägga till en order för en kund i en varukorg. Avsnittet innehåller information om hur du skapar en kundvagn och eventuella krav.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770128"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="00525-104">Skapa en varukorg med en kund order</span><span class="sxs-lookup"><span data-stu-id="00525-104">Create a cart with a customer order</span></span>

<span data-ttu-id="00525-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="00525-105">**Applies to:**</span></span>

- <span data-ttu-id="00525-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="00525-106">Partner Center</span></span>
- <span data-ttu-id="00525-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="00525-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="00525-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="00525-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="00525-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="00525-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="00525-110">Du kan lägga till en order för en kund i en varukorg.</span><span class="sxs-lookup"><span data-stu-id="00525-110">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="00525-111">Mer information om vad som för närvarande är tillgängligt för försäljning finns [i partner erbjudanden i Cloud Solution Provider-programmet](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="00525-111">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00525-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="00525-112">Prerequisites</span></span>

- <span data-ttu-id="00525-113">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="00525-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="00525-114">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="00525-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="00525-115">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="00525-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="00525-116">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="00525-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="00525-117">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="00525-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="00525-118">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="00525-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="00525-119">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="00525-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="00525-120">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="00525-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="00525-121">C\#</span><span class="sxs-lookup"><span data-stu-id="00525-121">C\#</span></span>

<span data-ttu-id="00525-122">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="00525-122">To create an order for a customer:</span></span>

1. <span data-ttu-id="00525-123">Instansiera ett vagn objekt.</span><span class="sxs-lookup"><span data-stu-id="00525-123">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="00525-124">Skapa en lista med **CartLineItem** -objekt och tilldela listan till vagnens rad objekt-egenskap.</span><span class="sxs-lookup"><span data-stu-id="00525-124">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="00525-125">Varje vagn rads objekt innehåller inköps information för en produkt.</span><span class="sxs-lookup"><span data-stu-id="00525-125">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="00525-126">Du måste ha minst ett artikel per vagns rad.</span><span class="sxs-lookup"><span data-stu-id="00525-126">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="00525-127">Hämta ett gränssnitt till shopping-åtgärder genom att anropa metoden **IAggregatePartner. Customers. ById** med kund-ID: t för att identifiera kunden och sedan hämta gränssnittet från egenskapen **kundvagn** .</span><span class="sxs-lookup"><span data-stu-id="00525-127">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="00525-128">Anropa **create** -eller **CreateAsync** -metoden för att skapa vagnen.</span><span class="sxs-lookup"><span data-stu-id="00525-128">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="00525-129">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="00525-129">C\# example</span></span>

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

## <a name="java"></a><span data-ttu-id="00525-130">Java</span><span class="sxs-lookup"><span data-stu-id="00525-130">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="00525-131">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="00525-131">To create an order for a customer:</span></span>

1. <span data-ttu-id="00525-132">Instansiera ett vagn objekt.</span><span class="sxs-lookup"><span data-stu-id="00525-132">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="00525-133">Skapa en lista med **CartLineItem** -objekt och tilldela listan till vagnens rad objekt.</span><span class="sxs-lookup"><span data-stu-id="00525-133">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="00525-134">Varje vagn rads objekt innehåller inköps information för en produkt.</span><span class="sxs-lookup"><span data-stu-id="00525-134">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="00525-135">Du måste ha minst ett artikel per vagns rad.</span><span class="sxs-lookup"><span data-stu-id="00525-135">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="00525-136">Hämta ett gränssnitt till shopping-åtgärder genom att anropa funktionen **IAggregatePartner. getCustomers (). byId** med kund-ID: t för att identifiera kunden och sedan hämta gränssnittet från **getCart** -funktionen.</span><span class="sxs-lookup"><span data-stu-id="00525-136">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="00525-137">Anropa **create** -funktionen för att skapa vagnen.</span><span class="sxs-lookup"><span data-stu-id="00525-137">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="00525-138">Java-exempel</span><span class="sxs-lookup"><span data-stu-id="00525-138">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="00525-139">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00525-139">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="00525-140">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="00525-140">To create an order for a customer:</span></span>

1. <span data-ttu-id="00525-141">Instansiera ett vagn objekt.</span><span class="sxs-lookup"><span data-stu-id="00525-141">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="00525-142">Skapa en lista med **CartLineItem** -objekt och tilldela listan till vagnens rad objekt.</span><span class="sxs-lookup"><span data-stu-id="00525-142">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="00525-143">Varje vagn rads objekt innehåller inköps information för en produkt.</span><span class="sxs-lookup"><span data-stu-id="00525-143">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="00525-144">Du måste ha minst ett artikel per vagns rad.</span><span class="sxs-lookup"><span data-stu-id="00525-144">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="00525-145">Kör kommandot [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) för att skapa vagnen.</span><span class="sxs-lookup"><span data-stu-id="00525-145">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="00525-146">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="00525-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="00525-147">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="00525-147">Request syntax</span></span>

| <span data-ttu-id="00525-148">Metod</span><span class="sxs-lookup"><span data-stu-id="00525-148">Method</span></span>   | <span data-ttu-id="00525-149">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="00525-149">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00525-150">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="00525-150">**POST**</span></span> | <span data-ttu-id="00525-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="00525-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="00525-152">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="00525-152">URI parameter</span></span>

<span data-ttu-id="00525-153">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="00525-153">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="00525-154">Namn</span><span class="sxs-lookup"><span data-stu-id="00525-154">Name</span></span>            | <span data-ttu-id="00525-155">Typ</span><span class="sxs-lookup"><span data-stu-id="00525-155">Type</span></span>     | <span data-ttu-id="00525-156">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="00525-156">Required</span></span> | <span data-ttu-id="00525-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="00525-157">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="00525-158">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="00525-158">**customer-id**</span></span> | <span data-ttu-id="00525-159">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-159">string</span></span>   | <span data-ttu-id="00525-160">Yes</span><span class="sxs-lookup"><span data-stu-id="00525-160">Yes</span></span>      | <span data-ttu-id="00525-161">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="00525-161">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="00525-162">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="00525-162">Request headers</span></span>

<span data-ttu-id="00525-163">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="00525-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="00525-164">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="00525-164">Request body</span></span>

<span data-ttu-id="00525-165">I den här tabellen beskrivs egenskaperna för [kundvagn](cart-resources.md) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="00525-165">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="00525-166">Egenskap</span><span class="sxs-lookup"><span data-stu-id="00525-166">Property</span></span>              | <span data-ttu-id="00525-167">Typ</span><span class="sxs-lookup"><span data-stu-id="00525-167">Type</span></span>             | <span data-ttu-id="00525-168">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="00525-168">Required</span></span>        | <span data-ttu-id="00525-169">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="00525-169">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00525-170">id</span><span class="sxs-lookup"><span data-stu-id="00525-170">id</span></span>                    | <span data-ttu-id="00525-171">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-171">string</span></span>           | <span data-ttu-id="00525-172">No</span><span class="sxs-lookup"><span data-stu-id="00525-172">No</span></span>              | <span data-ttu-id="00525-173">Ett kundvagn-ID som anges när vagnen skapas.</span><span class="sxs-lookup"><span data-stu-id="00525-173">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="00525-174">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="00525-174">creationTimeStamp</span></span>     | <span data-ttu-id="00525-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="00525-175">DateTime</span></span>         | <span data-ttu-id="00525-176">No</span><span class="sxs-lookup"><span data-stu-id="00525-176">No</span></span>              | <span data-ttu-id="00525-177">Datumet då vagnen skapades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="00525-177">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="00525-178">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="00525-178">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="00525-179">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="00525-179">lastModifiedTimeStamp</span></span> | <span data-ttu-id="00525-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="00525-180">DateTime</span></span>         | <span data-ttu-id="00525-181">No</span><span class="sxs-lookup"><span data-stu-id="00525-181">No</span></span>              | <span data-ttu-id="00525-182">Datumet då vagnen senast uppdaterades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="00525-182">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="00525-183">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="00525-183">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="00525-184">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="00525-184">expirationTimeStamp</span></span>   | <span data-ttu-id="00525-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="00525-185">DateTime</span></span>         | <span data-ttu-id="00525-186">No</span><span class="sxs-lookup"><span data-stu-id="00525-186">No</span></span>              | <span data-ttu-id="00525-187">Datumet då vagnen upphör att gälla, i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="00525-187">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="00525-188">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="00525-188">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="00525-189">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="00525-189">lastModifiedUser</span></span>      | <span data-ttu-id="00525-190">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-190">string</span></span>           | <span data-ttu-id="00525-191">No</span><span class="sxs-lookup"><span data-stu-id="00525-191">No</span></span>              | <span data-ttu-id="00525-192">Den användare som senast uppdaterade vagnen.</span><span class="sxs-lookup"><span data-stu-id="00525-192">The user who last updated the cart.</span></span> <span data-ttu-id="00525-193">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="00525-193">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="00525-194">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="00525-194">lineItems</span></span>             | <span data-ttu-id="00525-195">Objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="00525-195">Array of objects</span></span> | <span data-ttu-id="00525-196">Yes</span><span class="sxs-lookup"><span data-stu-id="00525-196">Yes</span></span>             | <span data-ttu-id="00525-197">En matris med [CartLineItem](cart-resources.md#cartlineitem) -resurser.</span><span class="sxs-lookup"><span data-stu-id="00525-197">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="00525-198">I den här tabellen beskrivs egenskaperna för [CartLineItem](cart-resources.md#cartlineitem) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="00525-198">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="00525-199">Egenskap</span><span class="sxs-lookup"><span data-stu-id="00525-199">Property</span></span>       |            <span data-ttu-id="00525-200">Typ</span><span class="sxs-lookup"><span data-stu-id="00525-200">Type</span></span>             | <span data-ttu-id="00525-201">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="00525-201">Required</span></span> |                                                                                         <span data-ttu-id="00525-202">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="00525-202">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="00525-203">id</span><span class="sxs-lookup"><span data-stu-id="00525-203">id</span></span>          |           <span data-ttu-id="00525-204">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-204">string</span></span>            |    <span data-ttu-id="00525-205">No</span><span class="sxs-lookup"><span data-stu-id="00525-205">No</span></span>    |                                                     <span data-ttu-id="00525-206">En unik identifierare för ett vagn rads objekt.</span><span class="sxs-lookup"><span data-stu-id="00525-206">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="00525-207">Används när vagnen har skapats.</span><span class="sxs-lookup"><span data-stu-id="00525-207">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="00525-208">catalogId</span><span class="sxs-lookup"><span data-stu-id="00525-208">catalogId</span></span>      |           <span data-ttu-id="00525-209">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-209">string</span></span>            |   <span data-ttu-id="00525-210">Yes</span><span class="sxs-lookup"><span data-stu-id="00525-210">Yes</span></span>    |                                                                                <span data-ttu-id="00525-211">Katalog objekt identifierare.</span><span class="sxs-lookup"><span data-stu-id="00525-211">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="00525-212">friendlyName</span><span class="sxs-lookup"><span data-stu-id="00525-212">friendlyName</span></span>     |           <span data-ttu-id="00525-213">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-213">string</span></span>            |    <span data-ttu-id="00525-214">No</span><span class="sxs-lookup"><span data-stu-id="00525-214">No</span></span>    |                                                    <span data-ttu-id="00525-215">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="00525-215">Optional.</span></span> <span data-ttu-id="00525-216">Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.</span><span class="sxs-lookup"><span data-stu-id="00525-216">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="00525-217">quantity</span><span class="sxs-lookup"><span data-stu-id="00525-217">quantity</span></span>       |             <span data-ttu-id="00525-218">int</span><span class="sxs-lookup"><span data-stu-id="00525-218">int</span></span>             |   <span data-ttu-id="00525-219">Yes</span><span class="sxs-lookup"><span data-stu-id="00525-219">Yes</span></span>    |                                                                            <span data-ttu-id="00525-220">Antalet licenser eller instanser.</span><span class="sxs-lookup"><span data-stu-id="00525-220">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="00525-221">currencyCode</span><span class="sxs-lookup"><span data-stu-id="00525-221">currencyCode</span></span>     |           <span data-ttu-id="00525-222">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-222">string</span></span>            |    <span data-ttu-id="00525-223">No</span><span class="sxs-lookup"><span data-stu-id="00525-223">No</span></span>    |                                                                                     <span data-ttu-id="00525-224">Valuta koden.</span><span class="sxs-lookup"><span data-stu-id="00525-224">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="00525-225">billingCycle</span><span class="sxs-lookup"><span data-stu-id="00525-225">billingCycle</span></span>     |           <span data-ttu-id="00525-226">Objekt</span><span class="sxs-lookup"><span data-stu-id="00525-226">Object</span></span>            |   <span data-ttu-id="00525-227">Yes</span><span class="sxs-lookup"><span data-stu-id="00525-227">Yes</span></span>    |                                                                    <span data-ttu-id="00525-228">Typ av fakturerings cykel som angetts för den aktuella perioden.</span><span class="sxs-lookup"><span data-stu-id="00525-228">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="00525-229">deltagare</span><span class="sxs-lookup"><span data-stu-id="00525-229">participants</span></span>     | <span data-ttu-id="00525-230">Lista med objekt sträng par</span><span class="sxs-lookup"><span data-stu-id="00525-230">List of Object String pairs</span></span> |    <span data-ttu-id="00525-231">No</span><span class="sxs-lookup"><span data-stu-id="00525-231">No</span></span>    |                                                                <span data-ttu-id="00525-232">En samling partner on Record (MPNID) på köpet.</span><span class="sxs-lookup"><span data-stu-id="00525-232">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="00525-233">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="00525-233">provisioningContext</span></span> | <span data-ttu-id="00525-234">Ord listans<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="00525-234">Dictionary<string, string></span></span>  |    <span data-ttu-id="00525-235">No</span><span class="sxs-lookup"><span data-stu-id="00525-235">No</span></span>    | <span data-ttu-id="00525-236">Information krävs för etablering av vissa objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="00525-236">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="00525-237">Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för vissa objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="00525-237">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="00525-238">orderGroup</span><span class="sxs-lookup"><span data-stu-id="00525-238">orderGroup</span></span>      |           <span data-ttu-id="00525-239">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-239">string</span></span>            |    <span data-ttu-id="00525-240">No</span><span class="sxs-lookup"><span data-stu-id="00525-240">No</span></span>    |                                                                   <span data-ttu-id="00525-241">En grupp som visar vilka objekt som kan placeras tillsammans.</span><span class="sxs-lookup"><span data-stu-id="00525-241">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="00525-242">fel</span><span class="sxs-lookup"><span data-stu-id="00525-242">error</span></span>        |           <span data-ttu-id="00525-243">Objekt</span><span class="sxs-lookup"><span data-stu-id="00525-243">Object</span></span>            |    <span data-ttu-id="00525-244">No</span><span class="sxs-lookup"><span data-stu-id="00525-244">No</span></span>    |                                                                     <span data-ttu-id="00525-245">Tillämpas efter att kundvagn har skapats i händelse av ett fel.</span><span class="sxs-lookup"><span data-stu-id="00525-245">Applied after cart is created in case of an error.</span></span>                                                                      |
|     <span data-ttu-id="00525-246">renewsTo</span><span class="sxs-lookup"><span data-stu-id="00525-246">renewsTo</span></span>        | <span data-ttu-id="00525-247">Objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="00525-247">Array of objects</span></span>            |    <span data-ttu-id="00525-248">No</span><span class="sxs-lookup"><span data-stu-id="00525-248">No</span></span>    |                                                    <span data-ttu-id="00525-249">En matris med [RenewsTo](cart-resources.md#renewsto) -resurser.</span><span class="sxs-lookup"><span data-stu-id="00525-249">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="00525-250">I den här tabellen beskrivs egenskaperna för [RenewsTo](cart-resources.md#renewsto) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="00525-250">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="00525-251">Egenskap</span><span class="sxs-lookup"><span data-stu-id="00525-251">Property</span></span>              | <span data-ttu-id="00525-252">Typ</span><span class="sxs-lookup"><span data-stu-id="00525-252">Type</span></span>             | <span data-ttu-id="00525-253">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="00525-253">Required</span></span>        | <span data-ttu-id="00525-254">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="00525-254">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00525-255">termDuration</span><span class="sxs-lookup"><span data-stu-id="00525-255">termDuration</span></span>          | <span data-ttu-id="00525-256">sträng</span><span class="sxs-lookup"><span data-stu-id="00525-256">string</span></span>           | <span data-ttu-id="00525-257">No</span><span class="sxs-lookup"><span data-stu-id="00525-257">No</span></span>              | <span data-ttu-id="00525-258">En ISO 8601-representation av förnyelse periodens varaktighet.</span><span class="sxs-lookup"><span data-stu-id="00525-258">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="00525-259">De aktuella värdena som stöds är **P1M** (1 månad) och **P1Y** (1 år).</span><span class="sxs-lookup"><span data-stu-id="00525-259">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="00525-260">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="00525-260">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="00525-261">REST-svar</span><span class="sxs-lookup"><span data-stu-id="00525-261">REST response</span></span>

<span data-ttu-id="00525-262">Om det lyckas returnerar den här metoden den fyllda kund [vagns](cart-resources.md) resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="00525-262">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="00525-263">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="00525-263">Response success and error codes</span></span>

<span data-ttu-id="00525-264">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="00525-264">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="00525-265">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="00525-265">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="00525-266">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="00525-266">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="00525-267">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="00525-267">Response example</span></span>

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
