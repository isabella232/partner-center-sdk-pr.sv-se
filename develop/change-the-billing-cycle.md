---
title: Ändra faktureringscykeln
description: 'Lär dig hur du uppdaterar en kund prenumeration på månatlig eller årlig fakturering med hjälp av API: er för partner Center. Du kan också göra detta från instrument panelen för partner Center.'
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770089"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="897e1-104">Ändra fakturerings cykel för kund prenumeration</span><span class="sxs-lookup"><span data-stu-id="897e1-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="897e1-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="897e1-105">**Applies to:**</span></span>

- <span data-ttu-id="897e1-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="897e1-106">Partner Center</span></span>
- <span data-ttu-id="897e1-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="897e1-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="897e1-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="897e1-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="897e1-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="897e1-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="897e1-110">Uppdaterar en [order](order-resources.md) från månatlig till årlig fakturering eller från årlig till månatlig fakturering.</span><span class="sxs-lookup"><span data-stu-id="897e1-110">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="897e1-111">På instrument panelen för partner Center kan du utföra den här åtgärden genom att gå till en kunds prenumerations informations sida.</span><span class="sxs-lookup"><span data-stu-id="897e1-111">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="897e1-112">Då visas ett alternativ som definierar den aktuella fakturerings perioden för prenumerationen med möjlighet att ändra och skicka den.</span><span class="sxs-lookup"><span data-stu-id="897e1-112">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="897e1-113">**Omfattas inte av** den här artikeln:</span><span class="sxs-lookup"><span data-stu-id="897e1-113">**Out of scope** for this article:</span></span>

- <span data-ttu-id="897e1-114">Ändra fakturerings perioden för utvärderings versioner</span><span class="sxs-lookup"><span data-stu-id="897e1-114">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="897e1-115">Ändra fakturerings cyklerna för eventuella icke-årliga period erbjudanden (månatligt, 6 år) & Azure-prenumerationer</span><span class="sxs-lookup"><span data-stu-id="897e1-115">Changing the billing cycles for any non-annual term offers (monthly, 6-year) & Azure subscriptions</span></span>
- <span data-ttu-id="897e1-116">Ändra fakturerings cykler för inaktiva prenumerationer</span><span class="sxs-lookup"><span data-stu-id="897e1-116">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="897e1-117">Ändra fakturerings cykler för licenserbaserade Microsoft onlinetjänster-baserade prenumerationer</span><span class="sxs-lookup"><span data-stu-id="897e1-117">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="897e1-118">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="897e1-118">Prerequisites</span></span>

- <span data-ttu-id="897e1-119">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="897e1-119">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="897e1-120">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="897e1-120">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="897e1-121">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="897e1-121">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="897e1-122">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="897e1-122">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="897e1-123">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="897e1-123">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="897e1-124">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="897e1-124">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="897e1-125">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="897e1-125">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="897e1-126">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="897e1-126">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="897e1-127">Ett order-ID.</span><span class="sxs-lookup"><span data-stu-id="897e1-127">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="897e1-128">C\#</span><span class="sxs-lookup"><span data-stu-id="897e1-128">C\#</span></span>

<span data-ttu-id="897e1-129">Om du vill ändra frekvensen för fakturerings perioden uppdaterar du egenskapen [**order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .</span><span class="sxs-lookup"><span data-stu-id="897e1-129">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a><span data-ttu-id="897e1-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="897e1-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="897e1-131">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="897e1-131">Request syntax</span></span>

| <span data-ttu-id="897e1-132">Metod</span><span class="sxs-lookup"><span data-stu-id="897e1-132">Method</span></span>    | <span data-ttu-id="897e1-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="897e1-133">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="897e1-134">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="897e1-134">**PATCH**</span></span> | <span data-ttu-id="897e1-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="897e1-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="897e1-136">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="897e1-136">URI parameter</span></span>

<span data-ttu-id="897e1-137">Den här tabellen visar den obligatoriska Frågeparametern för att ändra antalet för prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="897e1-137">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="897e1-138">Namn</span><span class="sxs-lookup"><span data-stu-id="897e1-138">Name</span></span>                   | <span data-ttu-id="897e1-139">Typ</span><span class="sxs-lookup"><span data-stu-id="897e1-139">Type</span></span> | <span data-ttu-id="897e1-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="897e1-140">Required</span></span> | <span data-ttu-id="897e1-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="897e1-141">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="897e1-142">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="897e1-142">**customer-tenant-id**</span></span> | <span data-ttu-id="897e1-143">GUID</span><span class="sxs-lookup"><span data-stu-id="897e1-143">GUID</span></span> |    <span data-ttu-id="897e1-144">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-144">Y</span></span>     | <span data-ttu-id="897e1-145">Ett GUID-formaterat **kund-Tenant-ID** som identifierar kunden</span><span class="sxs-lookup"><span data-stu-id="897e1-145">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="897e1-146">**order-ID**</span><span class="sxs-lookup"><span data-stu-id="897e1-146">**order-id**</span></span>           | <span data-ttu-id="897e1-147">GUID</span><span class="sxs-lookup"><span data-stu-id="897e1-147">GUID</span></span> |    <span data-ttu-id="897e1-148">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-148">Y</span></span>     | <span data-ttu-id="897e1-149">Order-ID</span><span class="sxs-lookup"><span data-stu-id="897e1-149">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="897e1-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="897e1-150">Request headers</span></span>

<span data-ttu-id="897e1-151">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="897e1-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="897e1-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="897e1-152">Request body</span></span>

<span data-ttu-id="897e1-153">I följande tabeller beskrivs egenskaperna i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="897e1-153">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="897e1-154">Beställning</span><span class="sxs-lookup"><span data-stu-id="897e1-154">Order</span></span>

| <span data-ttu-id="897e1-155">Egenskap</span><span class="sxs-lookup"><span data-stu-id="897e1-155">Property</span></span>           | <span data-ttu-id="897e1-156">Typ</span><span class="sxs-lookup"><span data-stu-id="897e1-156">Type</span></span>             | <span data-ttu-id="897e1-157">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="897e1-157">Required</span></span> | <span data-ttu-id="897e1-158">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="897e1-158">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="897e1-159">Id</span><span class="sxs-lookup"><span data-stu-id="897e1-159">Id</span></span>                 | <span data-ttu-id="897e1-160">sträng</span><span class="sxs-lookup"><span data-stu-id="897e1-160">string</span></span>           |    <span data-ttu-id="897e1-161">N</span><span class="sxs-lookup"><span data-stu-id="897e1-161">N</span></span>     | <span data-ttu-id="897e1-162">En beställnings identifierare som anges när beställningen har skapats</span><span class="sxs-lookup"><span data-stu-id="897e1-162">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="897e1-163">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="897e1-163">ReferenceCustomerId</span></span> | <span data-ttu-id="897e1-164">sträng</span><span class="sxs-lookup"><span data-stu-id="897e1-164">string</span></span>           |    <span data-ttu-id="897e1-165">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-165">Y</span></span>     | <span data-ttu-id="897e1-166">Kund-ID</span><span class="sxs-lookup"><span data-stu-id="897e1-166">The customer identifier</span></span>                                                    |
| <span data-ttu-id="897e1-167">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="897e1-167">BillingCycle</span></span>       | <span data-ttu-id="897e1-168">sträng</span><span class="sxs-lookup"><span data-stu-id="897e1-168">string</span></span>           |    <span data-ttu-id="897e1-169">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-169">Y</span></span>     | <span data-ttu-id="897e1-170">Anger med vilken frekvens partnern faktureras för den här ordern.</span><span class="sxs-lookup"><span data-stu-id="897e1-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="897e1-171">De värden som stöds är medlems namnen som finns i [BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="897e1-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="897e1-172">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="897e1-172">LineItems</span></span>          | <span data-ttu-id="897e1-173">objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="897e1-173">array of objects</span></span> |    <span data-ttu-id="897e1-174">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-174">Y</span></span>     | <span data-ttu-id="897e1-175">En matris med [OrderLineItem](#orderlineitem) -resurser</span><span class="sxs-lookup"><span data-stu-id="897e1-175">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="897e1-176">CreationDate</span><span class="sxs-lookup"><span data-stu-id="897e1-176">CreationDate</span></span>       | <span data-ttu-id="897e1-177">datetime</span><span class="sxs-lookup"><span data-stu-id="897e1-177">datetime</span></span>         |    <span data-ttu-id="897e1-178">N</span><span class="sxs-lookup"><span data-stu-id="897e1-178">N</span></span>     | <span data-ttu-id="897e1-179">Datumet då ordern skapades i datum-och tids format</span><span class="sxs-lookup"><span data-stu-id="897e1-179">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="897e1-180">Attribut</span><span class="sxs-lookup"><span data-stu-id="897e1-180">Attributes</span></span>         | <span data-ttu-id="897e1-181">Objekt</span><span class="sxs-lookup"><span data-stu-id="897e1-181">Object</span></span>           |    <span data-ttu-id="897e1-182">N</span><span class="sxs-lookup"><span data-stu-id="897e1-182">N</span></span>     | <span data-ttu-id="897e1-183">Innehåller "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="897e1-183">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="897e1-184">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="897e1-184">OrderLineItem</span></span>

| <span data-ttu-id="897e1-185">Egenskap</span><span class="sxs-lookup"><span data-stu-id="897e1-185">Property</span></span>             | <span data-ttu-id="897e1-186">Typ</span><span class="sxs-lookup"><span data-stu-id="897e1-186">Type</span></span>   | <span data-ttu-id="897e1-187">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="897e1-187">Required</span></span> | <span data-ttu-id="897e1-188">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="897e1-188">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="897e1-189">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="897e1-189">LineItemNumber</span></span>       | <span data-ttu-id="897e1-190">antal</span><span class="sxs-lookup"><span data-stu-id="897e1-190">number</span></span> |    <span data-ttu-id="897e1-191">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-191">Y</span></span>     | <span data-ttu-id="897e1-192">Rad objekts numret, från och med 0</span><span class="sxs-lookup"><span data-stu-id="897e1-192">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="897e1-193">OfferId</span><span class="sxs-lookup"><span data-stu-id="897e1-193">OfferId</span></span>              | <span data-ttu-id="897e1-194">sträng</span><span class="sxs-lookup"><span data-stu-id="897e1-194">string</span></span> |    <span data-ttu-id="897e1-195">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-195">Y</span></span>     | <span data-ttu-id="897e1-196">ID för erbjudandet</span><span class="sxs-lookup"><span data-stu-id="897e1-196">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="897e1-197">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="897e1-197">SubscriptionId</span></span>       | <span data-ttu-id="897e1-198">sträng</span><span class="sxs-lookup"><span data-stu-id="897e1-198">string</span></span> |    <span data-ttu-id="897e1-199">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-199">Y</span></span>     | <span data-ttu-id="897e1-200">ID för prenumerationen</span><span class="sxs-lookup"><span data-stu-id="897e1-200">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="897e1-201">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="897e1-201">FriendlyName</span></span>         | <span data-ttu-id="897e1-202">sträng</span><span class="sxs-lookup"><span data-stu-id="897e1-202">string</span></span> |    <span data-ttu-id="897e1-203">N</span><span class="sxs-lookup"><span data-stu-id="897e1-203">N</span></span>     | <span data-ttu-id="897e1-204">Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate</span><span class="sxs-lookup"><span data-stu-id="897e1-204">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="897e1-205">Antal</span><span class="sxs-lookup"><span data-stu-id="897e1-205">Quantity</span></span>             | <span data-ttu-id="897e1-206">antal</span><span class="sxs-lookup"><span data-stu-id="897e1-206">number</span></span> |    <span data-ttu-id="897e1-207">Y</span><span class="sxs-lookup"><span data-stu-id="897e1-207">Y</span></span>     | <span data-ttu-id="897e1-208">Antalet licenser eller instanser</span><span class="sxs-lookup"><span data-stu-id="897e1-208">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="897e1-209">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="897e1-209">PartnerIdOnRecord</span></span>    | <span data-ttu-id="897e1-210">sträng</span><span class="sxs-lookup"><span data-stu-id="897e1-210">string</span></span> |    <span data-ttu-id="897e1-211">N</span><span class="sxs-lookup"><span data-stu-id="897e1-211">N</span></span>     | <span data-ttu-id="897e1-212">MPN-ID för registrerad partner</span><span class="sxs-lookup"><span data-stu-id="897e1-212">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="897e1-213">Attribut</span><span class="sxs-lookup"><span data-stu-id="897e1-213">Attributes</span></span>           | <span data-ttu-id="897e1-214">Objekt</span><span class="sxs-lookup"><span data-stu-id="897e1-214">Object</span></span> |    <span data-ttu-id="897e1-215">N</span><span class="sxs-lookup"><span data-stu-id="897e1-215">N</span></span>     | <span data-ttu-id="897e1-216">Innehåller "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="897e1-216">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="897e1-217">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="897e1-217">Request example</span></span>

<span data-ttu-id="897e1-218">Uppdatera till årlig fakturering</span><span class="sxs-lookup"><span data-stu-id="897e1-218">Update to annual billing</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
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

## <a name="rest-response"></a><span data-ttu-id="897e1-219">REST-svar</span><span class="sxs-lookup"><span data-stu-id="897e1-219">REST response</span></span>

<span data-ttu-id="897e1-220">Om det lyckas returnerar den här metoden den uppdaterade prenumerations ordningen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="897e1-220">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="897e1-221">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="897e1-221">Response success and error codes</span></span>

<span data-ttu-id="897e1-222">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="897e1-222">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="897e1-223">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="897e1-223">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="897e1-224">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="897e1-224">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="897e1-225">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="897e1-225">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "Annual",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```