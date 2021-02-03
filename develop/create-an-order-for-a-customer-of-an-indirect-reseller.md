---
title: Skapa kund ordning för indirekt åter försäljare
description: 'Lär dig hur du använder API: er för partner Center för att skapa en order för en indirekt åter försäljares kund. Artikeln innehåller krav, steg och exmaples.'
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770153"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="1a1c3-104">Skapa en beställning för en kund till en indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="1a1c3-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="1a1c3-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="1a1c3-105">**Applies to:**</span></span>

- <span data-ttu-id="1a1c3-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="1a1c3-106">Partner Center</span></span>

<span data-ttu-id="1a1c3-107">Så här skapar du en order för en indirekt åter försäljares kund.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-107">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a1c3-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1a1c3-108">Prerequisites</span></span>

- <span data-ttu-id="1a1c3-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1a1c3-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1a1c3-110">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1a1c3-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a1c3-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1a1c3-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1a1c3-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1a1c3-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1a1c3-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="1a1c3-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1a1c3-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a1c3-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1a1c3-117">Erbjudande identifieraren för det objekt som ska köpas.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-117">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="1a1c3-118">Klient-ID för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-118">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="1a1c3-119">C\#</span><span class="sxs-lookup"><span data-stu-id="1a1c3-119">C\#</span></span>

<span data-ttu-id="1a1c3-120">Så här skapar du en order för en indirekt åter försäljares kund:</span><span class="sxs-lookup"><span data-stu-id="1a1c3-120">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="1a1c3-121">Hämta en samling av de indirekta åter försäljare som har en relation med den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-121">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="1a1c3-122">Hämta en lokal variabel till objektet i samlingen som matchar det indirekta åter försäljarens ID.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-122">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="1a1c3-123">Det här steget hjälper dig att komma åt åter försäljarens [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) -egenskap när du skapar ordern.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-123">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="1a1c3-124">Instansiera ett [**order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) -objekt och ange [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) -egenskapen till kund-ID för att kunna registrera kunden.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-124">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="1a1c3-125">Skapa en lista med [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -objekt och tilldela listan till orderns [**rad objekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) -egenskap.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-125">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="1a1c3-126">Varje order rads objekt innehåller inköps information för ett erbjudande.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="1a1c3-127">Var noga med att fylla i egenskapen [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) i varje rad objekt med MPN-ID: t för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-127">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="1a1c3-128">Du måste ha minst ett order rads objekt.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-128">You must have at least one order line item.</span></span>

5. <span data-ttu-id="1a1c3-129">Hämta ett gränssnitt för att beställa åtgärder genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och hämta sedan gränssnittet från egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .</span><span class="sxs-lookup"><span data-stu-id="1a1c3-129">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="1a1c3-130">Anropa [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) -eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) -metoden för att skapa ordern.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-130">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="1a1c3-131">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="1a1c3-131">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="1a1c3-132">**Exempel**: [konsol test app](console-test-app.md)-**projekt**: Partner Center SDK-exempel **klass**: PlaceOrderForCustomer.CS</span><span class="sxs-lookup"><span data-stu-id="1a1c3-132">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1a1c3-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1a1c3-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1a1c3-134">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="1a1c3-134">Request syntax</span></span>

| <span data-ttu-id="1a1c3-135">Metod</span><span class="sxs-lookup"><span data-stu-id="1a1c3-135">Method</span></span>   | <span data-ttu-id="1a1c3-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1a1c3-136">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="1a1c3-137">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="1a1c3-137">**POST**</span></span> | <span data-ttu-id="1a1c3-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="1a1c3-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1a1c3-139">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="1a1c3-139">URI parameters</span></span>

<span data-ttu-id="1a1c3-140">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-140">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="1a1c3-141">Namn</span><span class="sxs-lookup"><span data-stu-id="1a1c3-141">Name</span></span>        | <span data-ttu-id="1a1c3-142">Typ</span><span class="sxs-lookup"><span data-stu-id="1a1c3-142">Type</span></span>   | <span data-ttu-id="1a1c3-143">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1a1c3-143">Required</span></span> | <span data-ttu-id="1a1c3-144">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1a1c3-144">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1a1c3-145">kund-ID</span><span class="sxs-lookup"><span data-stu-id="1a1c3-145">customer-id</span></span> | <span data-ttu-id="1a1c3-146">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-146">string</span></span> | <span data-ttu-id="1a1c3-147">Yes</span><span class="sxs-lookup"><span data-stu-id="1a1c3-147">Yes</span></span>      | <span data-ttu-id="1a1c3-148">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-148">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1a1c3-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1a1c3-149">Request headers</span></span>

<span data-ttu-id="1a1c3-150">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1a1c3-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1a1c3-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1a1c3-151">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="1a1c3-152">Beställning</span><span class="sxs-lookup"><span data-stu-id="1a1c3-152">Order</span></span>

<span data-ttu-id="1a1c3-153">I den här tabellen beskrivs **beställnings** egenskaperna i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-153">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="1a1c3-154">Namn</span><span class="sxs-lookup"><span data-stu-id="1a1c3-154">Name</span></span> | <span data-ttu-id="1a1c3-155">Typ</span><span class="sxs-lookup"><span data-stu-id="1a1c3-155">Type</span></span> | <span data-ttu-id="1a1c3-156">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1a1c3-156">Required</span></span> | <span data-ttu-id="1a1c3-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1a1c3-157">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="1a1c3-158">id</span><span class="sxs-lookup"><span data-stu-id="1a1c3-158">id</span></span> | <span data-ttu-id="1a1c3-159">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-159">string</span></span> | <span data-ttu-id="1a1c3-160">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-160">No</span></span> | <span data-ttu-id="1a1c3-161">En beställnings identifierare som anges när beställningen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-161">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="1a1c3-162">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="1a1c3-162">referenceCustomerId</span></span> | <span data-ttu-id="1a1c3-163">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-163">string</span></span> | <span data-ttu-id="1a1c3-164">Yes</span><span class="sxs-lookup"><span data-stu-id="1a1c3-164">Yes</span></span> | <span data-ttu-id="1a1c3-165">Kund-ID.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-165">The customer identifier.</span></span> |
| <span data-ttu-id="1a1c3-166">billingCycle</span><span class="sxs-lookup"><span data-stu-id="1a1c3-166">billingCycle</span></span> | <span data-ttu-id="1a1c3-167">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-167">string</span></span> | <span data-ttu-id="1a1c3-168">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-168">No</span></span> | <span data-ttu-id="1a1c3-169">Den frekvens med vilken partnern debiteras för den här ordern.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-169">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="1a1c3-170">Standardvärdet är &quot; månatlig &quot; och används när beställningen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-170">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="1a1c3-171">De värden som stöds är medlems namnen som finns i [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="1a1c3-171">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="1a1c3-172">OBS! den årliga fakturerings funktionen är ännu inte allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-172">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="1a1c3-173">Support för årlig fakturering kommer snart.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-173">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="1a1c3-174">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="1a1c3-174">lineItems</span></span> | <span data-ttu-id="1a1c3-175">objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="1a1c3-175">array of objects</span></span> | <span data-ttu-id="1a1c3-176">Yes</span><span class="sxs-lookup"><span data-stu-id="1a1c3-176">Yes</span></span> | <span data-ttu-id="1a1c3-177">En matris med [**OrderLineItem**](#orderlineitem) -resurser.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-177">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="1a1c3-178">creationDate</span><span class="sxs-lookup"><span data-stu-id="1a1c3-178">creationDate</span></span> | <span data-ttu-id="1a1c3-179">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-179">string</span></span> | <span data-ttu-id="1a1c3-180">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-180">No</span></span> | <span data-ttu-id="1a1c3-181">Datumet då ordern skapades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-181">The date the order was created, in date-time format.</span></span> <span data-ttu-id="1a1c3-182">Används när beställningen har skapats.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-182">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="1a1c3-183">dokumentattribut</span><span class="sxs-lookup"><span data-stu-id="1a1c3-183">attributes</span></span> | <span data-ttu-id="1a1c3-184">objekt</span><span class="sxs-lookup"><span data-stu-id="1a1c3-184">object</span></span> | <span data-ttu-id="1a1c3-185">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-185">No</span></span> | <span data-ttu-id="1a1c3-186">Innehåller "ObjectType": "order".</span><span class="sxs-lookup"><span data-stu-id="1a1c3-186">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="1a1c3-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="1a1c3-187">OrderLineItem</span></span>

<span data-ttu-id="1a1c3-188">I den här tabellen beskrivs egenskaperna för **OrderLineItem** i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-188">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="1a1c3-189">Namn</span><span class="sxs-lookup"><span data-stu-id="1a1c3-189">Name</span></span> | <span data-ttu-id="1a1c3-190">Typ</span><span class="sxs-lookup"><span data-stu-id="1a1c3-190">Type</span></span> | <span data-ttu-id="1a1c3-191">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1a1c3-191">Required</span></span> | <span data-ttu-id="1a1c3-192">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1a1c3-192">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="1a1c3-193">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="1a1c3-193">lineItemNumber</span></span> | <span data-ttu-id="1a1c3-194">int</span><span class="sxs-lookup"><span data-stu-id="1a1c3-194">int</span></span> | <span data-ttu-id="1a1c3-195">Yes</span><span class="sxs-lookup"><span data-stu-id="1a1c3-195">Yes</span></span> | <span data-ttu-id="1a1c3-196">Varje rad objekt i samlingen får ett unikt rad nummer, räknat från 0 till count-1.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-196">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="1a1c3-197">offerId</span><span class="sxs-lookup"><span data-stu-id="1a1c3-197">offerId</span></span> | <span data-ttu-id="1a1c3-198">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-198">string</span></span> | <span data-ttu-id="1a1c3-199">Yes</span><span class="sxs-lookup"><span data-stu-id="1a1c3-199">Yes</span></span> | <span data-ttu-id="1a1c3-200">Erbjudande-ID.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-200">The offer identifier.</span></span> |
| <span data-ttu-id="1a1c3-201">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1a1c3-201">subscriptionId</span></span> | <span data-ttu-id="1a1c3-202">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-202">string</span></span> | <span data-ttu-id="1a1c3-203">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-203">No</span></span> | <span data-ttu-id="1a1c3-204">Prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-204">The subscription identifier.</span></span> |
| <span data-ttu-id="1a1c3-205">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1a1c3-205">parentSubscriptionId</span></span> | <span data-ttu-id="1a1c3-206">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-206">string</span></span> | <span data-ttu-id="1a1c3-207">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-207">No</span></span> | <span data-ttu-id="1a1c3-208">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-208">Optional.</span></span> <span data-ttu-id="1a1c3-209">ID: t för den överordnade prenumerationen i ett tilläggs erbjudande.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-209">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="1a1c3-210">Gäller enbart för korrigering.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-210">Applies to PATCH only.</span></span> |
| <span data-ttu-id="1a1c3-211">friendlyName</span><span class="sxs-lookup"><span data-stu-id="1a1c3-211">friendlyName</span></span> | <span data-ttu-id="1a1c3-212">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-212">string</span></span> | <span data-ttu-id="1a1c3-213">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-213">No</span></span> | <span data-ttu-id="1a1c3-214">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-214">Optional.</span></span> <span data-ttu-id="1a1c3-215">Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-215">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="1a1c3-216">quantity</span><span class="sxs-lookup"><span data-stu-id="1a1c3-216">quantity</span></span> | <span data-ttu-id="1a1c3-217">int</span><span class="sxs-lookup"><span data-stu-id="1a1c3-217">int</span></span> | <span data-ttu-id="1a1c3-218">Yes</span><span class="sxs-lookup"><span data-stu-id="1a1c3-218">Yes</span></span> | <span data-ttu-id="1a1c3-219">Antalet licenser för en licens baserad prenumeration.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-219">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="1a1c3-220">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="1a1c3-220">partnerIdOnRecord</span></span> | <span data-ttu-id="1a1c3-221">sträng</span><span class="sxs-lookup"><span data-stu-id="1a1c3-221">string</span></span> | <span data-ttu-id="1a1c3-222">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-222">No</span></span> | <span data-ttu-id="1a1c3-223">När en indirekt åter försäljare placerar en indirekt åter försäljare, fyller du i det här fältet med MPN-ID: t för den **indirekta åter försäljaren** (aldrig ID: t för den indirekta providern).</span><span class="sxs-lookup"><span data-stu-id="1a1c3-223">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="1a1c3-224">Detta säkerställer korrekt redovisning av incitament.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-224">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="1a1c3-225">**Det gick inte att ange MPN-ID: t för åter försäljaren. Åter försäljaren registreras dock inte, vilket innebär att incitaments beräkningar kanske inte omfattar försäljningen.**</span><span class="sxs-lookup"><span data-stu-id="1a1c3-225">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="1a1c3-226">dokumentattribut</span><span class="sxs-lookup"><span data-stu-id="1a1c3-226">attributes</span></span> | <span data-ttu-id="1a1c3-227">objekt</span><span class="sxs-lookup"><span data-stu-id="1a1c3-227">object</span></span> | <span data-ttu-id="1a1c3-228">No</span><span class="sxs-lookup"><span data-stu-id="1a1c3-228">No</span></span> | <span data-ttu-id="1a1c3-229">Innehåller "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="1a1c3-229">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="1a1c3-230">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1a1c3-230">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="1a1c3-231">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1a1c3-231">REST response</span></span>

<span data-ttu-id="1a1c3-232">Om det lyckas innehåller svars texten den ifyllda [order](order-resources.md) resursen.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-232">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1a1c3-233">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1a1c3-233">Response success and error codes</span></span>

<span data-ttu-id="1a1c3-234">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-234">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1a1c3-235">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1a1c3-235">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1a1c3-236">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1a1c3-236">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1a1c3-237">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1a1c3-237">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
