---
title: Skapa kundorder för indirekt återförsäljare
description: Lär dig hur du använder Partner Center-API:er för att skapa en order för en kund till en indirekt återförsäljare. Artikeln innehåller krav, steg och exempel.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973559"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="b30cf-104">Skapa en beställning för en kund till en indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="b30cf-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="b30cf-105">Hur du skapar en order för en kund till en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="b30cf-105">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b30cf-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b30cf-106">Prerequisites</span></span>

- <span data-ttu-id="b30cf-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b30cf-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b30cf-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b30cf-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b30cf-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b30cf-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b30cf-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b30cf-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b30cf-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="b30cf-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b30cf-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="b30cf-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b30cf-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="b30cf-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b30cf-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b30cf-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b30cf-115">Erbjudandeidentifieraren för objektet som ska köpas.</span><span class="sxs-lookup"><span data-stu-id="b30cf-115">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="b30cf-116">Klient-ID för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="b30cf-116">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="b30cf-117">C\#</span><span class="sxs-lookup"><span data-stu-id="b30cf-117">C\#</span></span>

<span data-ttu-id="b30cf-118">Så här skapar du en order för en kund till en indirekt återförsäljare:</span><span class="sxs-lookup"><span data-stu-id="b30cf-118">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="b30cf-119">Hämta en samling av indirekta återförsäljare som har en relation med den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="b30cf-119">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="b30cf-120">Hämta en lokal variabel till objektet i samlingen som matchar det indirekta återförsäljar-ID:t.</span><span class="sxs-lookup"><span data-stu-id="b30cf-120">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="b30cf-121">Det här steget hjälper dig att komma åt återförsäljarens [**MpnId-egenskap**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) när du skapar ordern.</span><span class="sxs-lookup"><span data-stu-id="b30cf-121">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="b30cf-122">Instansiera [**ett Order-objekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) och ange [**egenskapen ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) till kundidentifieraren för att registrera kunden.</span><span class="sxs-lookup"><span data-stu-id="b30cf-122">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="b30cf-123">Skapa en lista [**med OrderLineItem-objekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) och tilldela listan till orderns [**LineItems-egenskap.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems)</span><span class="sxs-lookup"><span data-stu-id="b30cf-123">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="b30cf-124">Varje orderradsartikel innehåller inköpsinformationen för ett erbjudande.</span><span class="sxs-lookup"><span data-stu-id="b30cf-124">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="b30cf-125">Se till att fylla i egenskapen [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) i varje radobjekt med MPN-ID:t för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="b30cf-125">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="b30cf-126">Du måste ha minst en orderrad.</span><span class="sxs-lookup"><span data-stu-id="b30cf-126">You must have at least one order line item.</span></span>

5. <span data-ttu-id="b30cf-127">Hämta ett gränssnitt för att beställa åtgärder genom att anropa [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och hämta sedan gränssnittet från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) Orders.</span><span class="sxs-lookup"><span data-stu-id="b30cf-127">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="b30cf-128">Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) för att skapa ordern.</span><span class="sxs-lookup"><span data-stu-id="b30cf-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="b30cf-129">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="b30cf-129">C\# example</span></span>

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

<span data-ttu-id="b30cf-130">**Exempel:** [Konsoltestapp med](console-test-app.md)**Project:** Partnercenter-SDK **Samples-klass:** PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="b30cf-130">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b30cf-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b30cf-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b30cf-132">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b30cf-132">Request syntax</span></span>

| <span data-ttu-id="b30cf-133">Metod</span><span class="sxs-lookup"><span data-stu-id="b30cf-133">Method</span></span>   | <span data-ttu-id="b30cf-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b30cf-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b30cf-135">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="b30cf-135">**POST**</span></span> | <span data-ttu-id="b30cf-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b30cf-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b30cf-137">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b30cf-137">URI parameters</span></span>

<span data-ttu-id="b30cf-138">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="b30cf-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="b30cf-139">Namn</span><span class="sxs-lookup"><span data-stu-id="b30cf-139">Name</span></span>        | <span data-ttu-id="b30cf-140">Typ</span><span class="sxs-lookup"><span data-stu-id="b30cf-140">Type</span></span>   | <span data-ttu-id="b30cf-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b30cf-141">Required</span></span> | <span data-ttu-id="b30cf-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b30cf-142">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="b30cf-143">kund-ID</span><span class="sxs-lookup"><span data-stu-id="b30cf-143">customer-id</span></span> | <span data-ttu-id="b30cf-144">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-144">string</span></span> | <span data-ttu-id="b30cf-145">Ja</span><span class="sxs-lookup"><span data-stu-id="b30cf-145">Yes</span></span>      | <span data-ttu-id="b30cf-146">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="b30cf-146">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b30cf-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b30cf-147">Request headers</span></span>

<span data-ttu-id="b30cf-148">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b30cf-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b30cf-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b30cf-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="b30cf-150">Beställning</span><span class="sxs-lookup"><span data-stu-id="b30cf-150">Order</span></span>

<span data-ttu-id="b30cf-151">I den här tabellen beskrivs **orderegenskaperna** i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="b30cf-151">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="b30cf-152">Namn</span><span class="sxs-lookup"><span data-stu-id="b30cf-152">Name</span></span> | <span data-ttu-id="b30cf-153">Typ</span><span class="sxs-lookup"><span data-stu-id="b30cf-153">Type</span></span> | <span data-ttu-id="b30cf-154">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b30cf-154">Required</span></span> | <span data-ttu-id="b30cf-155">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b30cf-155">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="b30cf-156">id</span><span class="sxs-lookup"><span data-stu-id="b30cf-156">id</span></span> | <span data-ttu-id="b30cf-157">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-157">string</span></span> | <span data-ttu-id="b30cf-158">No</span><span class="sxs-lookup"><span data-stu-id="b30cf-158">No</span></span> | <span data-ttu-id="b30cf-159">En orderidentifierare som anges när ordern har skapats.</span><span class="sxs-lookup"><span data-stu-id="b30cf-159">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="b30cf-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="b30cf-160">referenceCustomerId</span></span> | <span data-ttu-id="b30cf-161">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-161">string</span></span> | <span data-ttu-id="b30cf-162">Ja</span><span class="sxs-lookup"><span data-stu-id="b30cf-162">Yes</span></span> | <span data-ttu-id="b30cf-163">Kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="b30cf-163">The customer identifier.</span></span> |
| <span data-ttu-id="b30cf-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="b30cf-164">billingCycle</span></span> | <span data-ttu-id="b30cf-165">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-165">string</span></span> | <span data-ttu-id="b30cf-166">No</span><span class="sxs-lookup"><span data-stu-id="b30cf-166">No</span></span> | <span data-ttu-id="b30cf-167">Frekvensen som partnern debiteras med för den här beställningen.</span><span class="sxs-lookup"><span data-stu-id="b30cf-167">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="b30cf-168">Standardvärdet är &quot; Varje månad och tillämpas när &quot; ordern har skapats.</span><span class="sxs-lookup"><span data-stu-id="b30cf-168">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="b30cf-169">Värden som stöds är de medlemsnamn som finns [**i BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="b30cf-169">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="b30cf-170">Obs! Den årliga faktureringsfunktionen är ännu inte allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="b30cf-170">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="b30cf-171">Stöd för årlig fakturering kommer snart.</span><span class="sxs-lookup"><span data-stu-id="b30cf-171">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="b30cf-172">lineItems</span><span class="sxs-lookup"><span data-stu-id="b30cf-172">lineItems</span></span> | <span data-ttu-id="b30cf-173">matris med objekt</span><span class="sxs-lookup"><span data-stu-id="b30cf-173">array of objects</span></span> | <span data-ttu-id="b30cf-174">Ja</span><span class="sxs-lookup"><span data-stu-id="b30cf-174">Yes</span></span> | <span data-ttu-id="b30cf-175">En matris med [**OrderLineItem-resurser.**](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="b30cf-175">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="b30cf-176">creationDate</span><span class="sxs-lookup"><span data-stu-id="b30cf-176">creationDate</span></span> | <span data-ttu-id="b30cf-177">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-177">string</span></span> | <span data-ttu-id="b30cf-178">No</span><span class="sxs-lookup"><span data-stu-id="b30cf-178">No</span></span> | <span data-ttu-id="b30cf-179">Det datum då ordern skapades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="b30cf-179">The date the order was created, in date-time format.</span></span> <span data-ttu-id="b30cf-180">Tillämpas när ordern har skapats.</span><span class="sxs-lookup"><span data-stu-id="b30cf-180">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="b30cf-181">Attribut</span><span class="sxs-lookup"><span data-stu-id="b30cf-181">attributes</span></span> | <span data-ttu-id="b30cf-182">objekt</span><span class="sxs-lookup"><span data-stu-id="b30cf-182">object</span></span> | <span data-ttu-id="b30cf-183">Inga</span><span class="sxs-lookup"><span data-stu-id="b30cf-183">No</span></span> | <span data-ttu-id="b30cf-184">Innehåller "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="b30cf-184">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="b30cf-185">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="b30cf-185">OrderLineItem</span></span>

<span data-ttu-id="b30cf-186">I den här tabellen beskrivs **egenskaperna OrderLineItem** i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="b30cf-186">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="b30cf-187">Namn</span><span class="sxs-lookup"><span data-stu-id="b30cf-187">Name</span></span> | <span data-ttu-id="b30cf-188">Typ</span><span class="sxs-lookup"><span data-stu-id="b30cf-188">Type</span></span> | <span data-ttu-id="b30cf-189">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b30cf-189">Required</span></span> | <span data-ttu-id="b30cf-190">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b30cf-190">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="b30cf-191">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="b30cf-191">lineItemNumber</span></span> | <span data-ttu-id="b30cf-192">int</span><span class="sxs-lookup"><span data-stu-id="b30cf-192">int</span></span> | <span data-ttu-id="b30cf-193">Ja</span><span class="sxs-lookup"><span data-stu-id="b30cf-193">Yes</span></span> | <span data-ttu-id="b30cf-194">Varje radobjekt i samlingen får ett unikt radnummer som räknas upp från 0 till count-1.</span><span class="sxs-lookup"><span data-stu-id="b30cf-194">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="b30cf-195">offerId</span><span class="sxs-lookup"><span data-stu-id="b30cf-195">offerId</span></span> | <span data-ttu-id="b30cf-196">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-196">string</span></span> | <span data-ttu-id="b30cf-197">Ja</span><span class="sxs-lookup"><span data-stu-id="b30cf-197">Yes</span></span> | <span data-ttu-id="b30cf-198">Erbjudandeidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="b30cf-198">The offer identifier.</span></span> |
| <span data-ttu-id="b30cf-199">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b30cf-199">subscriptionId</span></span> | <span data-ttu-id="b30cf-200">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-200">string</span></span> | <span data-ttu-id="b30cf-201">No</span><span class="sxs-lookup"><span data-stu-id="b30cf-201">No</span></span> | <span data-ttu-id="b30cf-202">Prenumerationsidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="b30cf-202">The subscription identifier.</span></span> |
| <span data-ttu-id="b30cf-203">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="b30cf-203">parentSubscriptionId</span></span> | <span data-ttu-id="b30cf-204">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-204">string</span></span> | <span data-ttu-id="b30cf-205">No</span><span class="sxs-lookup"><span data-stu-id="b30cf-205">No</span></span> | <span data-ttu-id="b30cf-206">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="b30cf-206">Optional.</span></span> <span data-ttu-id="b30cf-207">ID:t för den överordnade prenumerationen i ett tilläggserbjudande.</span><span class="sxs-lookup"><span data-stu-id="b30cf-207">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="b30cf-208">Gäller endast PATCH.</span><span class="sxs-lookup"><span data-stu-id="b30cf-208">Applies to PATCH only.</span></span> |
| <span data-ttu-id="b30cf-209">friendlyName</span><span class="sxs-lookup"><span data-stu-id="b30cf-209">friendlyName</span></span> | <span data-ttu-id="b30cf-210">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-210">string</span></span> | <span data-ttu-id="b30cf-211">No</span><span class="sxs-lookup"><span data-stu-id="b30cf-211">No</span></span> | <span data-ttu-id="b30cf-212">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="b30cf-212">Optional.</span></span> <span data-ttu-id="b30cf-213">Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydighet.</span><span class="sxs-lookup"><span data-stu-id="b30cf-213">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="b30cf-214">quantity</span><span class="sxs-lookup"><span data-stu-id="b30cf-214">quantity</span></span> | <span data-ttu-id="b30cf-215">int</span><span class="sxs-lookup"><span data-stu-id="b30cf-215">int</span></span> | <span data-ttu-id="b30cf-216">Ja</span><span class="sxs-lookup"><span data-stu-id="b30cf-216">Yes</span></span> | <span data-ttu-id="b30cf-217">Antalet licenser för en licensbaserad prenumeration.</span><span class="sxs-lookup"><span data-stu-id="b30cf-217">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="b30cf-218">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="b30cf-218">partnerIdOnRecord</span></span> | <span data-ttu-id="b30cf-219">sträng</span><span class="sxs-lookup"><span data-stu-id="b30cf-219">string</span></span> | <span data-ttu-id="b30cf-220">No</span><span class="sxs-lookup"><span data-stu-id="b30cf-220">No</span></span> | <span data-ttu-id="b30cf-221">När en indirekt leverantör gör en beställning åt en indirekt återförsäljare fyller du i det här fältet med mpn-ID:t för den indirekta **återförsäljaren** (aldrig ID för den indirekta leverantören).</span><span class="sxs-lookup"><span data-stu-id="b30cf-221">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="b30cf-222">Detta säkerställer korrekt redovisning av incitament.</span><span class="sxs-lookup"><span data-stu-id="b30cf-222">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="b30cf-223">**Om du inte anger återförsäljarens MPN-ID misslyckas inte beställningen. Återförsäljaren registreras dock inte och därför kanske inte försäljningen ingår i incitamentberäkningarna.**</span><span class="sxs-lookup"><span data-stu-id="b30cf-223">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="b30cf-224">Attribut</span><span class="sxs-lookup"><span data-stu-id="b30cf-224">attributes</span></span> | <span data-ttu-id="b30cf-225">objekt</span><span class="sxs-lookup"><span data-stu-id="b30cf-225">object</span></span> | <span data-ttu-id="b30cf-226">Inga</span><span class="sxs-lookup"><span data-stu-id="b30cf-226">No</span></span> | <span data-ttu-id="b30cf-227">Innehåller "ObjectType":"OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="b30cf-227">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="b30cf-228">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b30cf-228">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b30cf-229">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b30cf-229">REST response</span></span>

<span data-ttu-id="b30cf-230">Om det lyckas innehåller svarstexten den ifyllda [orderresursen.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="b30cf-230">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b30cf-231">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b30cf-231">Response success and error codes</span></span>

<span data-ttu-id="b30cf-232">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b30cf-232">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b30cf-233">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b30cf-233">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b30cf-234">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b30cf-234">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b30cf-235">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b30cf-235">Response example</span></span>

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
