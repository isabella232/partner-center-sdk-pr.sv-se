---
title: Skapa en kundorder
description: Lär dig hur du använder Partner Center-API:er för att skapa en order för en kund. Artikeln innehåller förutsättningar, steg och exempel.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3a86a99f43bdeec5e4c560ab59e1924b76c0636
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973560"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="a6b02-104">Skapa en order för en kund med partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="a6b02-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="a6b02-105">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a6b02-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a6b02-106">Att skapa en **order för azure-reserverade VM-instansprodukter** *gäller endast* för:</span><span class="sxs-lookup"><span data-stu-id="a6b02-106">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="a6b02-107">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a6b02-107">Partner Center</span></span>

<span data-ttu-id="a6b02-108">Information om vad som för närvarande är tillgängligt för försäljning [finns i Partnererbjudanden i Molnlösningsleverantör program](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="a6b02-108">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6b02-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a6b02-109">Prerequisites</span></span>

- <span data-ttu-id="a6b02-110">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a6b02-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a6b02-111">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a6b02-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a6b02-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a6b02-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a6b02-113">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a6b02-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a6b02-114">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="a6b02-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a6b02-115">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="a6b02-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a6b02-116">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="a6b02-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a6b02-117">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a6b02-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a6b02-118">Ett erbjudande-ID.</span><span class="sxs-lookup"><span data-stu-id="a6b02-118">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="a6b02-119">C\#</span><span class="sxs-lookup"><span data-stu-id="a6b02-119">C\#</span></span>

<span data-ttu-id="a6b02-120">Så här skapar du en order för en kund:</span><span class="sxs-lookup"><span data-stu-id="a6b02-120">To create an order for a customer:</span></span>

1. <span data-ttu-id="a6b02-121">Skapa en instans [**av ett Order-objekt**](order-resources.md) och ange **egenskapen ReferenceCustomerID** till kund-ID:t för att registrera kunden.</span><span class="sxs-lookup"><span data-stu-id="a6b02-121">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="a6b02-122">Skapa en lista [**med OrderLineItem-objekt**](order-resources.md#orderlineitem) och tilldela listan till orderns **LineItems-egenskap.**</span><span class="sxs-lookup"><span data-stu-id="a6b02-122">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="a6b02-123">Varje orderradsartikel innehåller inköpsinformationen för ett erbjudande.</span><span class="sxs-lookup"><span data-stu-id="a6b02-123">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="a6b02-124">Du måste ha minst en orderrad.</span><span class="sxs-lookup"><span data-stu-id="a6b02-124">You must have at least one order line item.</span></span>

3. <span data-ttu-id="a6b02-125">Hämta ett gränssnitt för att ordna åtgärder.</span><span class="sxs-lookup"><span data-stu-id="a6b02-125">Obtain an interface to order operations.</span></span> <span data-ttu-id="a6b02-126">Anropa först metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="a6b02-126">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="a6b02-127">Hämta sedan gränssnittet från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) Beställningar.</span><span class="sxs-lookup"><span data-stu-id="a6b02-127">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="a6b02-128">Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) och skicka in [**orderobjektet.**](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="a6b02-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

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

<span data-ttu-id="a6b02-129">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a6b02-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a6b02-130">**Project:** Partnercenter-SDK **exempelklass:** CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="a6b02-130">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a6b02-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a6b02-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a6b02-132">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="a6b02-132">Request syntax</span></span>

| <span data-ttu-id="a6b02-133">Metod</span><span class="sxs-lookup"><span data-stu-id="a6b02-133">Method</span></span>   | <span data-ttu-id="a6b02-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a6b02-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="a6b02-135">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="a6b02-135">**POST**</span></span> | <span data-ttu-id="a6b02-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a6b02-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a6b02-137">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="a6b02-137">URI parameters</span></span>

<span data-ttu-id="a6b02-138">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="a6b02-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="a6b02-139">Namn</span><span class="sxs-lookup"><span data-stu-id="a6b02-139">Name</span></span>        | <span data-ttu-id="a6b02-140">Typ</span><span class="sxs-lookup"><span data-stu-id="a6b02-140">Type</span></span>   | <span data-ttu-id="a6b02-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a6b02-141">Required</span></span> | <span data-ttu-id="a6b02-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a6b02-142">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="a6b02-143">kund-id</span><span class="sxs-lookup"><span data-stu-id="a6b02-143">customer-id</span></span> | <span data-ttu-id="a6b02-144">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-144">string</span></span> | <span data-ttu-id="a6b02-145">Ja</span><span class="sxs-lookup"><span data-stu-id="a6b02-145">Yes</span></span>      | <span data-ttu-id="a6b02-146">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="a6b02-146">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a6b02-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a6b02-147">Request headers</span></span>

<span data-ttu-id="a6b02-148">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a6b02-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a6b02-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a6b02-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="a6b02-150">Beställning</span><span class="sxs-lookup"><span data-stu-id="a6b02-150">Order</span></span>

<span data-ttu-id="a6b02-151">I den här tabellen beskrivs [orderegenskaperna](order-resources.md) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="a6b02-151">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="a6b02-152">Egenskap</span><span class="sxs-lookup"><span data-stu-id="a6b02-152">Property</span></span>             | <span data-ttu-id="a6b02-153">Typ</span><span class="sxs-lookup"><span data-stu-id="a6b02-153">Type</span></span>                        | <span data-ttu-id="a6b02-154">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a6b02-154">Required</span></span>                        | <span data-ttu-id="a6b02-155">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a6b02-155">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="a6b02-156">id</span><span class="sxs-lookup"><span data-stu-id="a6b02-156">id</span></span>                   | <span data-ttu-id="a6b02-157">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-157">string</span></span>                      | <span data-ttu-id="a6b02-158">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-158">No</span></span>                              | <span data-ttu-id="a6b02-159">En orderidentifierare som anges när ordern har skapats.</span><span class="sxs-lookup"><span data-stu-id="a6b02-159">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="a6b02-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="a6b02-160">referenceCustomerId</span></span>  | <span data-ttu-id="a6b02-161">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-161">string</span></span>                      | <span data-ttu-id="a6b02-162">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-162">No</span></span>                              | <span data-ttu-id="a6b02-163">Kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="a6b02-163">The customer identifier.</span></span> |
| <span data-ttu-id="a6b02-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="a6b02-164">billingCycle</span></span>         | <span data-ttu-id="a6b02-165">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-165">string</span></span>                      | <span data-ttu-id="a6b02-166">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-166">No</span></span>                              | <span data-ttu-id="a6b02-167">Anger med vilken frekvens partnern faktureras för den här beställningen.</span><span class="sxs-lookup"><span data-stu-id="a6b02-167">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="a6b02-168">Värden som stöds är de medlemsnamn som finns [i BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="a6b02-168">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="a6b02-169">Standardvärdet är "Varje månad" eller "OneTime" när ordern skapas.</span><span class="sxs-lookup"><span data-stu-id="a6b02-169">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="a6b02-170">Det här fältet tillämpas när ordern har skapats.</span><span class="sxs-lookup"><span data-stu-id="a6b02-170">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="a6b02-171">lineItems</span><span class="sxs-lookup"><span data-stu-id="a6b02-171">lineItems</span></span>            | <span data-ttu-id="a6b02-172">matris med [OrderLineItem-resurser](order-resources.md#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="a6b02-172">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="a6b02-173">Ja</span><span class="sxs-lookup"><span data-stu-id="a6b02-173">Yes</span></span>      | <span data-ttu-id="a6b02-174">En specificerad lista över de erbjudanden som kunden köper, inklusive kvantitet.</span><span class="sxs-lookup"><span data-stu-id="a6b02-174">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="a6b02-175">currencyCode</span><span class="sxs-lookup"><span data-stu-id="a6b02-175">currencyCode</span></span>         | <span data-ttu-id="a6b02-176">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-176">string</span></span>                      | <span data-ttu-id="a6b02-177">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-177">No</span></span>                              | <span data-ttu-id="a6b02-178">Skrivskyddade.</span><span class="sxs-lookup"><span data-stu-id="a6b02-178">Read-only.</span></span> <span data-ttu-id="a6b02-179">Den valuta som används när du gör beställningen.</span><span class="sxs-lookup"><span data-stu-id="a6b02-179">The currency used when placing the order.</span></span> <span data-ttu-id="a6b02-180">Tillämpas när ordern har skapats.</span><span class="sxs-lookup"><span data-stu-id="a6b02-180">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="a6b02-181">creationDate</span><span class="sxs-lookup"><span data-stu-id="a6b02-181">creationDate</span></span>         | <span data-ttu-id="a6b02-182">datetime</span><span class="sxs-lookup"><span data-stu-id="a6b02-182">datetime</span></span>                    | <span data-ttu-id="a6b02-183">Inga</span><span class="sxs-lookup"><span data-stu-id="a6b02-183">No</span></span>                              | <span data-ttu-id="a6b02-184">Skrivskyddade.</span><span class="sxs-lookup"><span data-stu-id="a6b02-184">Read-only.</span></span> <span data-ttu-id="a6b02-185">Det datum då ordern skapades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="a6b02-185">The date the order was created, in date-time format.</span></span> <span data-ttu-id="a6b02-186">Tillämpas när ordern har skapats.</span><span class="sxs-lookup"><span data-stu-id="a6b02-186">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="a6b02-187">status</span><span class="sxs-lookup"><span data-stu-id="a6b02-187">status</span></span>               | <span data-ttu-id="a6b02-188">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-188">string</span></span>                      | <span data-ttu-id="a6b02-189">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-189">No</span></span>                              | <span data-ttu-id="a6b02-190">Skrivskyddade.</span><span class="sxs-lookup"><span data-stu-id="a6b02-190">Read-only.</span></span> <span data-ttu-id="a6b02-191">Orderstatus.</span><span class="sxs-lookup"><span data-stu-id="a6b02-191">The status of the order.</span></span>  <span data-ttu-id="a6b02-192">Värden som stöds är de medlemsnamn som finns i [OrderStatus](order-resources.md#orderstatus).</span><span class="sxs-lookup"><span data-stu-id="a6b02-192">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="a6b02-193">Länkar</span><span class="sxs-lookup"><span data-stu-id="a6b02-193">links</span></span>                | [<span data-ttu-id="a6b02-194">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="a6b02-194">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="a6b02-195">Inga</span><span class="sxs-lookup"><span data-stu-id="a6b02-195">No</span></span>                              | <span data-ttu-id="a6b02-196">Resursen länkar som motsvarar ordern.</span><span class="sxs-lookup"><span data-stu-id="a6b02-196">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="a6b02-197">Attribut</span><span class="sxs-lookup"><span data-stu-id="a6b02-197">attributes</span></span>           | [<span data-ttu-id="a6b02-198">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="a6b02-198">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="a6b02-199">Inga</span><span class="sxs-lookup"><span data-stu-id="a6b02-199">No</span></span>                              | <span data-ttu-id="a6b02-200">Metadataattributen som motsvarar Order.</span><span class="sxs-lookup"><span data-stu-id="a6b02-200">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="a6b02-201">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="a6b02-201">OrderLineItem</span></span>

<span data-ttu-id="a6b02-202">I den här tabellen beskrivs [egenskaperna OrderLineItem](order-resources.md#orderlineitem) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="a6b02-202">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="a6b02-203">PartnerIdOnRecord bör endast tillhandahållas när en indirekt leverantör gör en beställning åt en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="a6b02-203">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="a6b02-204">Den används för att lagra den indirekta återförsäljarens Microsoft Partner Network id (aldrig DEN indirekta leverantörens ID).</span><span class="sxs-lookup"><span data-stu-id="a6b02-204">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="a6b02-205">Namn</span><span class="sxs-lookup"><span data-stu-id="a6b02-205">Name</span></span>                 | <span data-ttu-id="a6b02-206">Typ</span><span class="sxs-lookup"><span data-stu-id="a6b02-206">Type</span></span>   | <span data-ttu-id="a6b02-207">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a6b02-207">Required</span></span> | <span data-ttu-id="a6b02-208">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a6b02-208">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a6b02-209">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="a6b02-209">lineItemNumber</span></span>       | <span data-ttu-id="a6b02-210">int</span><span class="sxs-lookup"><span data-stu-id="a6b02-210">int</span></span>    | <span data-ttu-id="a6b02-211">Ja</span><span class="sxs-lookup"><span data-stu-id="a6b02-211">Yes</span></span>      | <span data-ttu-id="a6b02-212">Varje radobjekt i samlingen får ett unikt radnummer som räknas upp från 0 till count-1.</span><span class="sxs-lookup"><span data-stu-id="a6b02-212">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="a6b02-213">offerId</span><span class="sxs-lookup"><span data-stu-id="a6b02-213">offerId</span></span>              | <span data-ttu-id="a6b02-214">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-214">string</span></span> | <span data-ttu-id="a6b02-215">Ja</span><span class="sxs-lookup"><span data-stu-id="a6b02-215">Yes</span></span>      | <span data-ttu-id="a6b02-216">Erbjudandeidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="a6b02-216">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="a6b02-217">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a6b02-217">subscriptionId</span></span>       | <span data-ttu-id="a6b02-218">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-218">string</span></span> | <span data-ttu-id="a6b02-219">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-219">No</span></span>       | <span data-ttu-id="a6b02-220">Prenumerationsidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="a6b02-220">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="a6b02-221">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a6b02-221">parentSubscriptionId</span></span> | <span data-ttu-id="a6b02-222">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-222">string</span></span> | <span data-ttu-id="a6b02-223">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-223">No</span></span>       | <span data-ttu-id="a6b02-224">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="a6b02-224">Optional.</span></span> <span data-ttu-id="a6b02-225">ID:t för den överordnade prenumerationen i ett tilläggserbjudande.</span><span class="sxs-lookup"><span data-stu-id="a6b02-225">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="a6b02-226">Gäller endast PATCH.</span><span class="sxs-lookup"><span data-stu-id="a6b02-226">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="a6b02-227">friendlyName</span><span class="sxs-lookup"><span data-stu-id="a6b02-227">friendlyName</span></span>         | <span data-ttu-id="a6b02-228">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-228">string</span></span> | <span data-ttu-id="a6b02-229">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-229">No</span></span>       | <span data-ttu-id="a6b02-230">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="a6b02-230">Optional.</span></span> <span data-ttu-id="a6b02-231">Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydighet.</span><span class="sxs-lookup"><span data-stu-id="a6b02-231">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="a6b02-232">quantity</span><span class="sxs-lookup"><span data-stu-id="a6b02-232">quantity</span></span>             | <span data-ttu-id="a6b02-233">int</span><span class="sxs-lookup"><span data-stu-id="a6b02-233">int</span></span>    | <span data-ttu-id="a6b02-234">Ja</span><span class="sxs-lookup"><span data-stu-id="a6b02-234">Yes</span></span>      | <span data-ttu-id="a6b02-235">Antalet licenser för en licensbaserad prenumeration.</span><span class="sxs-lookup"><span data-stu-id="a6b02-235">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="a6b02-236">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="a6b02-236">partnerIdOnRecord</span></span>    | <span data-ttu-id="a6b02-237">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-237">string</span></span> | <span data-ttu-id="a6b02-238">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-238">No</span></span>       | <span data-ttu-id="a6b02-239">När en indirekt leverantör gör en beställning åt en indirekt återförsäljare fyller du i det här fältet med MPN-ID:t för den indirekta återförsäljaren **(aldrig** DEN indirekta leverantörens ID).</span><span class="sxs-lookup"><span data-stu-id="a6b02-239">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="a6b02-240">Detta säkerställer korrekt redovisning av incitament.</span><span class="sxs-lookup"><span data-stu-id="a6b02-240">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="a6b02-241">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="a6b02-241">provisioningContext</span></span>  | <span data-ttu-id="a6b02-242">Ordlista<sträng, sträng></span><span class="sxs-lookup"><span data-stu-id="a6b02-242">Dictionary<string, string></span></span>                | <span data-ttu-id="a6b02-243">Inga</span><span class="sxs-lookup"><span data-stu-id="a6b02-243">No</span></span>       |  <span data-ttu-id="a6b02-244">Information som krävs för etablering för vissa objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="a6b02-244">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="a6b02-245">Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för specifika objekt i katalogen.</span><span class="sxs-lookup"><span data-stu-id="a6b02-245">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="a6b02-246">Länkar</span><span class="sxs-lookup"><span data-stu-id="a6b02-246">links</span></span>                | [<span data-ttu-id="a6b02-247">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="a6b02-247">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="a6b02-248">Inga</span><span class="sxs-lookup"><span data-stu-id="a6b02-248">No</span></span>       |  <span data-ttu-id="a6b02-249">Skrivskyddade.</span><span class="sxs-lookup"><span data-stu-id="a6b02-249">Read-only.</span></span> <span data-ttu-id="a6b02-250">Resursen länkar som motsvarar orderradobjektet.</span><span class="sxs-lookup"><span data-stu-id="a6b02-250">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="a6b02-251">Attribut</span><span class="sxs-lookup"><span data-stu-id="a6b02-251">attributes</span></span>           | [<span data-ttu-id="a6b02-252">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="a6b02-252">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="a6b02-253">Inga</span><span class="sxs-lookup"><span data-stu-id="a6b02-253">No</span></span>       | <span data-ttu-id="a6b02-254">Metadataattributen som motsvarar OrderLineItem.</span><span class="sxs-lookup"><span data-stu-id="a6b02-254">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="a6b02-255">renewsTo</span><span class="sxs-lookup"><span data-stu-id="a6b02-255">renewsTo</span></span>             | <span data-ttu-id="a6b02-256">Matris med objekt</span><span class="sxs-lookup"><span data-stu-id="a6b02-256">Array of objects</span></span>                          | <span data-ttu-id="a6b02-257">Inga</span><span class="sxs-lookup"><span data-stu-id="a6b02-257">No</span></span>    |<span data-ttu-id="a6b02-258">En matris med [RenewsTo-resurser.](order-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="a6b02-258">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="a6b02-259">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="a6b02-259">RenewsTo</span></span>

<span data-ttu-id="a6b02-260">I den här tabellen beskrivs [egenskaperna RenewsTo](order-resources.md#renewsto) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="a6b02-260">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="a6b02-261">Egenskap</span><span class="sxs-lookup"><span data-stu-id="a6b02-261">Property</span></span>              | <span data-ttu-id="a6b02-262">Typ</span><span class="sxs-lookup"><span data-stu-id="a6b02-262">Type</span></span>             | <span data-ttu-id="a6b02-263">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a6b02-263">Required</span></span>        | <span data-ttu-id="a6b02-264">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a6b02-264">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a6b02-265">termDuration</span><span class="sxs-lookup"><span data-stu-id="a6b02-265">termDuration</span></span>          | <span data-ttu-id="a6b02-266">sträng</span><span class="sxs-lookup"><span data-stu-id="a6b02-266">string</span></span>           | <span data-ttu-id="a6b02-267">No</span><span class="sxs-lookup"><span data-stu-id="a6b02-267">No</span></span>              | <span data-ttu-id="a6b02-268">En ISO 8601-representation av förnyelseperiodens varaktighet.</span><span class="sxs-lookup"><span data-stu-id="a6b02-268">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="a6b02-269">De aktuella värdena som stöds **är P1M** (1 månad) och **P1Y** (1 år).</span><span class="sxs-lookup"><span data-stu-id="a6b02-269">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="a6b02-270">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a6b02-270">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a6b02-271">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a6b02-271">REST response</span></span>

<span data-ttu-id="a6b02-272">Om det lyckas returnerar metoden en [Order-resurs](order-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="a6b02-272">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a6b02-273">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a6b02-273">Response success and error codes</span></span>

<span data-ttu-id="a6b02-274">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="a6b02-274">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a6b02-275">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a6b02-275">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a6b02-276">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a6b02-276">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a6b02-277">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a6b02-277">Response example</span></span>

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
