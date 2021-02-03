---
title: Skapa en kund order
description: 'Lär dig hur du använder API: er för partner Center för att skapa en order för en kund. Artikeln innehåller krav, steg och exempel.'
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770125"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="4d3fc-104">Skapa en order för en kund med hjälp av API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="4d3fc-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="4d3fc-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="4d3fc-105">**Applies to:**</span></span>

- <span data-ttu-id="4d3fc-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="4d3fc-106">Partner Center</span></span>
- <span data-ttu-id="4d3fc-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="4d3fc-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4d3fc-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4d3fc-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4d3fc-109">Att skapa en **beställning för reserverade produkter från virtuella Azure-datorer** gäller *endast* för:</span><span class="sxs-lookup"><span data-stu-id="4d3fc-109">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="4d3fc-110">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="4d3fc-110">Partner Center</span></span>

<span data-ttu-id="4d3fc-111">Information om vad som för närvarande är tillgängligt för försäljning finns [i partner erbjudanden i Cloud Solution Provider-programmet](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-111">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d3fc-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="4d3fc-112">Prerequisites</span></span>

- <span data-ttu-id="4d3fc-113">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4d3fc-114">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4d3fc-115">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4d3fc-116">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4d3fc-117">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4d3fc-118">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4d3fc-119">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="4d3fc-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4d3fc-120">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4d3fc-121">Ett erbjudande-ID.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-121">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="4d3fc-122">C\#</span><span class="sxs-lookup"><span data-stu-id="4d3fc-122">C\#</span></span>

<span data-ttu-id="4d3fc-123">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="4d3fc-123">To create an order for a customer:</span></span>

1. <span data-ttu-id="4d3fc-124">Instansiera ett [**order**](order-resources.md) -objekt och ange **ReferenceCustomerID** -egenskapen till kund-ID: t för att registrera kunden.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-124">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="4d3fc-125">Skapa en lista med [**OrderLineItem**](order-resources.md#orderlineitem) -objekt och tilldela listan till orderns **rad objekt** -egenskap.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-125">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="4d3fc-126">Varje order rads objekt innehåller inköps information för ett erbjudande.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="4d3fc-127">Du måste ha minst ett order rads objekt.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-127">You must have at least one order line item.</span></span>

3. <span data-ttu-id="4d3fc-128">Hämta ett gränssnitt för att beställa åtgärder.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-128">Obtain an interface to order operations.</span></span> <span data-ttu-id="4d3fc-129">Anropa först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-129">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="4d3fc-130">Hämta sedan gränssnittet från egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .</span><span class="sxs-lookup"><span data-stu-id="4d3fc-130">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="4d3fc-131">Anropa metoden [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) och skicka det till [**order**](order-resources.md) -objektet.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-131">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="4d3fc-132">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4d3fc-133">**Projekt**: Partner Center SDK-exempel **klass**: CreateOrder.CS</span><span class="sxs-lookup"><span data-stu-id="4d3fc-133">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4d3fc-134">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="4d3fc-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4d3fc-135">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="4d3fc-135">Request syntax</span></span>

| <span data-ttu-id="4d3fc-136">Metod</span><span class="sxs-lookup"><span data-stu-id="4d3fc-136">Method</span></span>   | <span data-ttu-id="4d3fc-137">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="4d3fc-137">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="4d3fc-138">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="4d3fc-138">**POST**</span></span> | <span data-ttu-id="4d3fc-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="4d3fc-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4d3fc-140">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="4d3fc-140">URI parameters</span></span>

<span data-ttu-id="4d3fc-141">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-141">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="4d3fc-142">Namn</span><span class="sxs-lookup"><span data-stu-id="4d3fc-142">Name</span></span>        | <span data-ttu-id="4d3fc-143">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3fc-143">Type</span></span>   | <span data-ttu-id="4d3fc-144">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4d3fc-144">Required</span></span> | <span data-ttu-id="4d3fc-145">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4d3fc-145">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="4d3fc-146">kund-ID</span><span class="sxs-lookup"><span data-stu-id="4d3fc-146">customer-id</span></span> | <span data-ttu-id="4d3fc-147">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-147">string</span></span> | <span data-ttu-id="4d3fc-148">Yes</span><span class="sxs-lookup"><span data-stu-id="4d3fc-148">Yes</span></span>      | <span data-ttu-id="4d3fc-149">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-149">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4d3fc-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="4d3fc-150">Request headers</span></span>

<span data-ttu-id="4d3fc-151">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4d3fc-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="4d3fc-152">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="4d3fc-153">Beställning</span><span class="sxs-lookup"><span data-stu-id="4d3fc-153">Order</span></span>

<span data-ttu-id="4d3fc-154">I den här tabellen beskrivs [beställnings](order-resources.md) egenskaperna i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-154">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="4d3fc-155">Egenskap</span><span class="sxs-lookup"><span data-stu-id="4d3fc-155">Property</span></span>             | <span data-ttu-id="4d3fc-156">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3fc-156">Type</span></span>                        | <span data-ttu-id="4d3fc-157">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4d3fc-157">Required</span></span>                        | <span data-ttu-id="4d3fc-158">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4d3fc-158">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="4d3fc-159">id</span><span class="sxs-lookup"><span data-stu-id="4d3fc-159">id</span></span>                   | <span data-ttu-id="4d3fc-160">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-160">string</span></span>                      | <span data-ttu-id="4d3fc-161">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-161">No</span></span>                              | <span data-ttu-id="4d3fc-162">En beställnings identifierare som anges när beställningen har skapats.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-162">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="4d3fc-163">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="4d3fc-163">referenceCustomerId</span></span>  | <span data-ttu-id="4d3fc-164">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-164">string</span></span>                      | <span data-ttu-id="4d3fc-165">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-165">No</span></span>                              | <span data-ttu-id="4d3fc-166">Kund-ID.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-166">The customer identifier.</span></span> |
| <span data-ttu-id="4d3fc-167">billingCycle</span><span class="sxs-lookup"><span data-stu-id="4d3fc-167">billingCycle</span></span>         | <span data-ttu-id="4d3fc-168">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-168">string</span></span>                      | <span data-ttu-id="4d3fc-169">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-169">No</span></span>                              | <span data-ttu-id="4d3fc-170">Anger med vilken frekvens partnern faktureras för den här ordern.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="4d3fc-171">De värden som stöds är medlems namnen som finns i [BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="4d3fc-172">Standardvärdet är "Monthly" eller "Databasmigrering" när ordern skapas.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-172">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="4d3fc-173">Det här fältet används när beställningen har skapats.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-173">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="4d3fc-174">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="4d3fc-174">lineItems</span></span>            | <span data-ttu-id="4d3fc-175">matris med [OrderLineItem](order-resources.md#orderlineitem) -resurser</span><span class="sxs-lookup"><span data-stu-id="4d3fc-175">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="4d3fc-176">Yes</span><span class="sxs-lookup"><span data-stu-id="4d3fc-176">Yes</span></span>      | <span data-ttu-id="4d3fc-177">En lista med specificerade erbjudanden som kunden köper inklusive kvantiteten.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-177">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="4d3fc-178">currencyCode</span><span class="sxs-lookup"><span data-stu-id="4d3fc-178">currencyCode</span></span>         | <span data-ttu-id="4d3fc-179">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-179">string</span></span>                      | <span data-ttu-id="4d3fc-180">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-180">No</span></span>                              | <span data-ttu-id="4d3fc-181">Skrivskyddad.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-181">Read-only.</span></span> <span data-ttu-id="4d3fc-182">Den valuta som används när ordern placeras.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-182">The currency used when placing the order.</span></span> <span data-ttu-id="4d3fc-183">Används när beställningen har skapats.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-183">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="4d3fc-184">creationDate</span><span class="sxs-lookup"><span data-stu-id="4d3fc-184">creationDate</span></span>         | <span data-ttu-id="4d3fc-185">datetime</span><span class="sxs-lookup"><span data-stu-id="4d3fc-185">datetime</span></span>                    | <span data-ttu-id="4d3fc-186">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-186">No</span></span>                              | <span data-ttu-id="4d3fc-187">Skrivskyddad.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-187">Read-only.</span></span> <span data-ttu-id="4d3fc-188">Datumet då ordern skapades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-188">The date the order was created, in date-time format.</span></span> <span data-ttu-id="4d3fc-189">Används när beställningen har skapats.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-189">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="4d3fc-190">status</span><span class="sxs-lookup"><span data-stu-id="4d3fc-190">status</span></span>               | <span data-ttu-id="4d3fc-191">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-191">string</span></span>                      | <span data-ttu-id="4d3fc-192">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-192">No</span></span>                              | <span data-ttu-id="4d3fc-193">Skrivskyddad.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-193">Read-only.</span></span> <span data-ttu-id="4d3fc-194">Status för ordern.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-194">The status of the order.</span></span>  <span data-ttu-id="4d3fc-195">De värden som stöds är medlems namnen som finns i [OrderStatus](order-resources.md#orderstatus).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-195">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="4d3fc-196">Länkar</span><span class="sxs-lookup"><span data-stu-id="4d3fc-196">links</span></span>                | [<span data-ttu-id="4d3fc-197">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="4d3fc-197">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="4d3fc-198">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-198">No</span></span>                              | <span data-ttu-id="4d3fc-199">Resurs länkarna som motsvarar beställningen.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-199">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="4d3fc-200">dokumentattribut</span><span class="sxs-lookup"><span data-stu-id="4d3fc-200">attributes</span></span>           | [<span data-ttu-id="4d3fc-201">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="4d3fc-201">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="4d3fc-202">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-202">No</span></span>                              | <span data-ttu-id="4d3fc-203">De metadata-attribut som motsvarar beställningen.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-203">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="4d3fc-204">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="4d3fc-204">OrderLineItem</span></span>

<span data-ttu-id="4d3fc-205">I den här tabellen beskrivs egenskaperna för [OrderLineItem](order-resources.md#orderlineitem) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-205">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="4d3fc-206">PartnerIdOnRecord bör endast anges när en indirekt leverantör placerar en order på uppdrag av en indirekt åter försäljare.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-206">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="4d3fc-207">Den används endast för att lagra Microsoft Partner Network-ID: t för den indirekta åter försäljaren (aldrig ID: t för den indirekta providern).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-207">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="4d3fc-208">Namn</span><span class="sxs-lookup"><span data-stu-id="4d3fc-208">Name</span></span>                 | <span data-ttu-id="4d3fc-209">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3fc-209">Type</span></span>   | <span data-ttu-id="4d3fc-210">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4d3fc-210">Required</span></span> | <span data-ttu-id="4d3fc-211">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4d3fc-211">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4d3fc-212">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="4d3fc-212">lineItemNumber</span></span>       | <span data-ttu-id="4d3fc-213">int</span><span class="sxs-lookup"><span data-stu-id="4d3fc-213">int</span></span>    | <span data-ttu-id="4d3fc-214">Yes</span><span class="sxs-lookup"><span data-stu-id="4d3fc-214">Yes</span></span>      | <span data-ttu-id="4d3fc-215">Varje rad objekt i samlingen får ett unikt rad nummer, räknat från 0 till count-1.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-215">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="4d3fc-216">offerId</span><span class="sxs-lookup"><span data-stu-id="4d3fc-216">offerId</span></span>              | <span data-ttu-id="4d3fc-217">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-217">string</span></span> | <span data-ttu-id="4d3fc-218">Yes</span><span class="sxs-lookup"><span data-stu-id="4d3fc-218">Yes</span></span>      | <span data-ttu-id="4d3fc-219">Erbjudande-ID.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-219">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="4d3fc-220">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4d3fc-220">subscriptionId</span></span>       | <span data-ttu-id="4d3fc-221">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-221">string</span></span> | <span data-ttu-id="4d3fc-222">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-222">No</span></span>       | <span data-ttu-id="4d3fc-223">Prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-223">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="4d3fc-224">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4d3fc-224">parentSubscriptionId</span></span> | <span data-ttu-id="4d3fc-225">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-225">string</span></span> | <span data-ttu-id="4d3fc-226">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-226">No</span></span>       | <span data-ttu-id="4d3fc-227">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-227">Optional.</span></span> <span data-ttu-id="4d3fc-228">ID: t för den överordnade prenumerationen i ett tilläggs erbjudande.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-228">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="4d3fc-229">Gäller enbart för korrigering.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-229">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="4d3fc-230">friendlyName</span><span class="sxs-lookup"><span data-stu-id="4d3fc-230">friendlyName</span></span>         | <span data-ttu-id="4d3fc-231">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-231">string</span></span> | <span data-ttu-id="4d3fc-232">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-232">No</span></span>       | <span data-ttu-id="4d3fc-233">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-233">Optional.</span></span> <span data-ttu-id="4d3fc-234">Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-234">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="4d3fc-235">quantity</span><span class="sxs-lookup"><span data-stu-id="4d3fc-235">quantity</span></span>             | <span data-ttu-id="4d3fc-236">int</span><span class="sxs-lookup"><span data-stu-id="4d3fc-236">int</span></span>    | <span data-ttu-id="4d3fc-237">Yes</span><span class="sxs-lookup"><span data-stu-id="4d3fc-237">Yes</span></span>      | <span data-ttu-id="4d3fc-238">Antalet licenser för en licens baserad prenumeration.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-238">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="4d3fc-239">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="4d3fc-239">partnerIdOnRecord</span></span>    | <span data-ttu-id="4d3fc-240">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-240">string</span></span> | <span data-ttu-id="4d3fc-241">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-241">No</span></span>       | <span data-ttu-id="4d3fc-242">När en indirekt åter försäljare placerar en indirekt åter försäljare, fyller du i det här fältet med MPN-ID: t för den **indirekta åter försäljaren** (aldrig ID: t för den indirekta providern).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-242">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="4d3fc-243">Detta säkerställer korrekt redovisning av incitament.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-243">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="4d3fc-244">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="4d3fc-244">provisioningContext</span></span>  | <span data-ttu-id="4d3fc-245">Ord listans<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="4d3fc-245">Dictionary<string, string></span></span>                | <span data-ttu-id="4d3fc-246">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-246">No</span></span>       |  <span data-ttu-id="4d3fc-247">Information krävs för etablering av vissa objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-247">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="4d3fc-248">Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för vissa objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-248">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="4d3fc-249">Länkar</span><span class="sxs-lookup"><span data-stu-id="4d3fc-249">links</span></span>                | [<span data-ttu-id="4d3fc-250">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="4d3fc-250">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="4d3fc-251">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-251">No</span></span>       |  <span data-ttu-id="4d3fc-252">Skrivskyddad.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-252">Read-only.</span></span> <span data-ttu-id="4d3fc-253">Resurs länkarna som motsvarar order rads objektet.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-253">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="4d3fc-254">dokumentattribut</span><span class="sxs-lookup"><span data-stu-id="4d3fc-254">attributes</span></span>           | [<span data-ttu-id="4d3fc-255">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="4d3fc-255">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="4d3fc-256">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-256">No</span></span>       | <span data-ttu-id="4d3fc-257">De metadata-attribut som motsvarar OrderLineItem.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-257">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="4d3fc-258">renewsTo</span><span class="sxs-lookup"><span data-stu-id="4d3fc-258">renewsTo</span></span>             | <span data-ttu-id="4d3fc-259">Objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="4d3fc-259">Array of objects</span></span>                          | <span data-ttu-id="4d3fc-260">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-260">No</span></span>    |<span data-ttu-id="4d3fc-261">En matris med [RenewsTo](order-resources.md#renewsto) -resurser.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-261">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="4d3fc-262">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="4d3fc-262">RenewsTo</span></span>

<span data-ttu-id="4d3fc-263">I den här tabellen beskrivs egenskaperna för [RenewsTo](order-resources.md#renewsto) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-263">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="4d3fc-264">Egenskap</span><span class="sxs-lookup"><span data-stu-id="4d3fc-264">Property</span></span>              | <span data-ttu-id="4d3fc-265">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3fc-265">Type</span></span>             | <span data-ttu-id="4d3fc-266">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4d3fc-266">Required</span></span>        | <span data-ttu-id="4d3fc-267">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4d3fc-267">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4d3fc-268">termDuration</span><span class="sxs-lookup"><span data-stu-id="4d3fc-268">termDuration</span></span>          | <span data-ttu-id="4d3fc-269">sträng</span><span class="sxs-lookup"><span data-stu-id="4d3fc-269">string</span></span>           | <span data-ttu-id="4d3fc-270">No</span><span class="sxs-lookup"><span data-stu-id="4d3fc-270">No</span></span>              | <span data-ttu-id="4d3fc-271">En ISO 8601-representation av förnyelse periodens varaktighet.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-271">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="4d3fc-272">De aktuella värdena som stöds är **P1M** (1 månad) och **P1Y** (1 år).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-272">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="4d3fc-273">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="4d3fc-273">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="4d3fc-274">REST-svar</span><span class="sxs-lookup"><span data-stu-id="4d3fc-274">REST response</span></span>

<span data-ttu-id="4d3fc-275">Om det lyckas returnerar metoden en [order](order-resources.md) resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-275">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4d3fc-276">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="4d3fc-276">Response success and error codes</span></span>

<span data-ttu-id="4d3fc-277">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-277">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4d3fc-278">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="4d3fc-278">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4d3fc-279">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4d3fc-279">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4d3fc-280">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="4d3fc-280">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
