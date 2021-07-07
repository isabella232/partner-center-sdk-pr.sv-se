---
title: Ändra faktureringscykeln
description: Lär dig hur du uppdaterar en kundprenumeration till månatlig eller årlig fakturering med partnercenter-API:er. Du kan också göra detta från instrumentpanelen i Partnercenter.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 435309229e2cb038c936028943f4c2cf27b032a7
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974122"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="cda45-104">Ändra faktureringsperioden för en kundprenumeration</span><span class="sxs-lookup"><span data-stu-id="cda45-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="cda45-105">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cda45-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cda45-106">Uppdaterar en [order från](order-resources.md) månatlig till årlig fakturering eller från årlig till månatlig fakturering.</span><span class="sxs-lookup"><span data-stu-id="cda45-106">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="cda45-107">Den här åtgärden kan utföras på Partnercenter-instrumentpanelen genom att gå till sidan med prenumerationsinformation för en kund.</span><span class="sxs-lookup"><span data-stu-id="cda45-107">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="cda45-108">När du är där ser du ett alternativ som definierar den aktuella faktureringsperioden för prenumerationen med möjlighet att ändra och skicka den.</span><span class="sxs-lookup"><span data-stu-id="cda45-108">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="cda45-109">**Utanför omfånget** för den här artikeln:</span><span class="sxs-lookup"><span data-stu-id="cda45-109">**Out of scope** for this article:</span></span>

- <span data-ttu-id="cda45-110">Ändra faktureringsperioden för utvärderingsversioner</span><span class="sxs-lookup"><span data-stu-id="cda45-110">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="cda45-111">Ändra faktureringscyklerna för icke-årliga erbjudanden (månadsvis, sex år) & Azure-prenumerationer</span><span class="sxs-lookup"><span data-stu-id="cda45-111">Changing the billing cycles for any non-annual term offers (monthly, six-year) & Azure subscriptions</span></span>
- <span data-ttu-id="cda45-112">Ändra faktureringscykler för inaktiva prenumerationer</span><span class="sxs-lookup"><span data-stu-id="cda45-112">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="cda45-113">Ändra faktureringscykler för Microsoft onlinetjänster-licensbaserade prenumerationer</span><span class="sxs-lookup"><span data-stu-id="cda45-113">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cda45-114">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cda45-114">Prerequisites</span></span>

- <span data-ttu-id="cda45-115">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cda45-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cda45-116">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cda45-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cda45-117">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cda45-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cda45-118">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="cda45-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cda45-119">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="cda45-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cda45-120">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="cda45-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cda45-121">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="cda45-121">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cda45-122">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cda45-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="cda45-123">Ett order-ID.</span><span class="sxs-lookup"><span data-stu-id="cda45-123">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="cda45-124">C\#</span><span class="sxs-lookup"><span data-stu-id="cda45-124">C\#</span></span>

<span data-ttu-id="cda45-125">Om du vill ändra frekvensen för faktureringsperioden uppdaterar du egenskapen [**Order.BillingCycle.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)</span><span class="sxs-lookup"><span data-stu-id="cda45-125">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="cda45-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cda45-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cda45-127">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="cda45-127">Request syntax</span></span>

| <span data-ttu-id="cda45-128">Metod</span><span class="sxs-lookup"><span data-stu-id="cda45-128">Method</span></span>    | <span data-ttu-id="cda45-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cda45-129">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cda45-130">**Patch**</span><span class="sxs-lookup"><span data-stu-id="cda45-130">**PATCH**</span></span> | <span data-ttu-id="cda45-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cda45-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cda45-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="cda45-132">URI parameter</span></span>

<span data-ttu-id="cda45-133">I den här tabellen visas den frågeparameter som krävs för att ändra antalet för prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cda45-133">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="cda45-134">Namn</span><span class="sxs-lookup"><span data-stu-id="cda45-134">Name</span></span>                   | <span data-ttu-id="cda45-135">Typ</span><span class="sxs-lookup"><span data-stu-id="cda45-135">Type</span></span> | <span data-ttu-id="cda45-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cda45-136">Required</span></span> | <span data-ttu-id="cda45-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cda45-137">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="cda45-138">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="cda45-138">**customer-tenant-id**</span></span> | <span data-ttu-id="cda45-139">GUID</span><span class="sxs-lookup"><span data-stu-id="cda45-139">GUID</span></span> |    <span data-ttu-id="cda45-140">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-140">Y</span></span>     | <span data-ttu-id="cda45-141">Ett **GUID-formaterat kundklient-ID** som identifierar kunden</span><span class="sxs-lookup"><span data-stu-id="cda45-141">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="cda45-142">**order-id**</span><span class="sxs-lookup"><span data-stu-id="cda45-142">**order-id**</span></span>           | <span data-ttu-id="cda45-143">GUID</span><span class="sxs-lookup"><span data-stu-id="cda45-143">GUID</span></span> |    <span data-ttu-id="cda45-144">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-144">Y</span></span>     | <span data-ttu-id="cda45-145">Orderidentifieraren</span><span class="sxs-lookup"><span data-stu-id="cda45-145">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="cda45-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cda45-146">Request headers</span></span>

<span data-ttu-id="cda45-147">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cda45-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cda45-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cda45-148">Request body</span></span>

<span data-ttu-id="cda45-149">I följande tabeller beskrivs egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="cda45-149">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="cda45-150">Beställning</span><span class="sxs-lookup"><span data-stu-id="cda45-150">Order</span></span>

| <span data-ttu-id="cda45-151">Egenskap</span><span class="sxs-lookup"><span data-stu-id="cda45-151">Property</span></span>           | <span data-ttu-id="cda45-152">Typ</span><span class="sxs-lookup"><span data-stu-id="cda45-152">Type</span></span>             | <span data-ttu-id="cda45-153">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cda45-153">Required</span></span> | <span data-ttu-id="cda45-154">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cda45-154">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="cda45-155">Id</span><span class="sxs-lookup"><span data-stu-id="cda45-155">Id</span></span>                 | <span data-ttu-id="cda45-156">sträng</span><span class="sxs-lookup"><span data-stu-id="cda45-156">string</span></span>           |    <span data-ttu-id="cda45-157">N</span><span class="sxs-lookup"><span data-stu-id="cda45-157">N</span></span>     | <span data-ttu-id="cda45-158">En orderidentifierare som anges när ordern har skapats</span><span class="sxs-lookup"><span data-stu-id="cda45-158">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="cda45-159">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="cda45-159">ReferenceCustomerId</span></span> | <span data-ttu-id="cda45-160">sträng</span><span class="sxs-lookup"><span data-stu-id="cda45-160">string</span></span>           |    <span data-ttu-id="cda45-161">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-161">Y</span></span>     | <span data-ttu-id="cda45-162">Kundidentifieraren</span><span class="sxs-lookup"><span data-stu-id="cda45-162">The customer identifier</span></span>                                                    |
| <span data-ttu-id="cda45-163">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="cda45-163">BillingCycle</span></span>       | <span data-ttu-id="cda45-164">sträng</span><span class="sxs-lookup"><span data-stu-id="cda45-164">string</span></span>           |    <span data-ttu-id="cda45-165">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-165">Y</span></span>     | <span data-ttu-id="cda45-166">Anger med vilken frekvens partnern faktureras för den här beställningen.</span><span class="sxs-lookup"><span data-stu-id="cda45-166">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="cda45-167">Värden som stöds är de medlemsnamn som finns [i BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="cda45-167">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="cda45-168">LineItems</span><span class="sxs-lookup"><span data-stu-id="cda45-168">LineItems</span></span>          | <span data-ttu-id="cda45-169">matris med objekt</span><span class="sxs-lookup"><span data-stu-id="cda45-169">array of objects</span></span> |    <span data-ttu-id="cda45-170">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-170">Y</span></span>     | <span data-ttu-id="cda45-171">En matris med [OrderLineItem-resurser](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="cda45-171">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="cda45-172">CreationDate</span><span class="sxs-lookup"><span data-stu-id="cda45-172">CreationDate</span></span>       | <span data-ttu-id="cda45-173">datetime</span><span class="sxs-lookup"><span data-stu-id="cda45-173">datetime</span></span>         |    <span data-ttu-id="cda45-174">N</span><span class="sxs-lookup"><span data-stu-id="cda45-174">N</span></span>     | <span data-ttu-id="cda45-175">Det datum då ordern skapades, i datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="cda45-175">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="cda45-176">Attribut</span><span class="sxs-lookup"><span data-stu-id="cda45-176">Attributes</span></span>         | <span data-ttu-id="cda45-177">Objekt</span><span class="sxs-lookup"><span data-stu-id="cda45-177">Object</span></span>           |    <span data-ttu-id="cda45-178">N</span><span class="sxs-lookup"><span data-stu-id="cda45-178">N</span></span>     | <span data-ttu-id="cda45-179">Innehåller "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="cda45-179">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="cda45-180">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="cda45-180">OrderLineItem</span></span>

| <span data-ttu-id="cda45-181">Egenskap</span><span class="sxs-lookup"><span data-stu-id="cda45-181">Property</span></span>             | <span data-ttu-id="cda45-182">Typ</span><span class="sxs-lookup"><span data-stu-id="cda45-182">Type</span></span>   | <span data-ttu-id="cda45-183">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cda45-183">Required</span></span> | <span data-ttu-id="cda45-184">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cda45-184">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="cda45-185">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="cda45-185">LineItemNumber</span></span>       | <span data-ttu-id="cda45-186">antal</span><span class="sxs-lookup"><span data-stu-id="cda45-186">number</span></span> |    <span data-ttu-id="cda45-187">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-187">Y</span></span>     | <span data-ttu-id="cda45-188">Radobjektets nummer, som börjar med 0</span><span class="sxs-lookup"><span data-stu-id="cda45-188">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="cda45-189">OfferId</span><span class="sxs-lookup"><span data-stu-id="cda45-189">OfferId</span></span>              | <span data-ttu-id="cda45-190">sträng</span><span class="sxs-lookup"><span data-stu-id="cda45-190">string</span></span> |    <span data-ttu-id="cda45-191">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-191">Y</span></span>     | <span data-ttu-id="cda45-192">ID för erbjudandet</span><span class="sxs-lookup"><span data-stu-id="cda45-192">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="cda45-193">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="cda45-193">SubscriptionId</span></span>       | <span data-ttu-id="cda45-194">sträng</span><span class="sxs-lookup"><span data-stu-id="cda45-194">string</span></span> |    <span data-ttu-id="cda45-195">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-195">Y</span></span>     | <span data-ttu-id="cda45-196">ID för prenumerationen</span><span class="sxs-lookup"><span data-stu-id="cda45-196">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="cda45-197">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="cda45-197">FriendlyName</span></span>         | <span data-ttu-id="cda45-198">sträng</span><span class="sxs-lookup"><span data-stu-id="cda45-198">string</span></span> |    <span data-ttu-id="cda45-199">N</span><span class="sxs-lookup"><span data-stu-id="cda45-199">N</span></span>     | <span data-ttu-id="cda45-200">Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydigheter</span><span class="sxs-lookup"><span data-stu-id="cda45-200">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="cda45-201">Kvantitet</span><span class="sxs-lookup"><span data-stu-id="cda45-201">Quantity</span></span>             | <span data-ttu-id="cda45-202">antal</span><span class="sxs-lookup"><span data-stu-id="cda45-202">number</span></span> |    <span data-ttu-id="cda45-203">Y</span><span class="sxs-lookup"><span data-stu-id="cda45-203">Y</span></span>     | <span data-ttu-id="cda45-204">Antalet licenser eller instanser</span><span class="sxs-lookup"><span data-stu-id="cda45-204">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="cda45-205">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="cda45-205">PartnerIdOnRecord</span></span>    | <span data-ttu-id="cda45-206">sträng</span><span class="sxs-lookup"><span data-stu-id="cda45-206">string</span></span> |    <span data-ttu-id="cda45-207">N</span><span class="sxs-lookup"><span data-stu-id="cda45-207">N</span></span>     | <span data-ttu-id="cda45-208">MPN-ID för partnern i posten</span><span class="sxs-lookup"><span data-stu-id="cda45-208">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="cda45-209">Attribut</span><span class="sxs-lookup"><span data-stu-id="cda45-209">Attributes</span></span>           | <span data-ttu-id="cda45-210">Objekt</span><span class="sxs-lookup"><span data-stu-id="cda45-210">Object</span></span> |    <span data-ttu-id="cda45-211">N</span><span class="sxs-lookup"><span data-stu-id="cda45-211">N</span></span>     | <span data-ttu-id="cda45-212">Innehåller "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="cda45-212">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="cda45-213">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cda45-213">Request example</span></span>

<span data-ttu-id="cda45-214">Uppdatera till årlig fakturering</span><span class="sxs-lookup"><span data-stu-id="cda45-214">Update to annual billing</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cda45-215">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cda45-215">REST response</span></span>

<span data-ttu-id="cda45-216">Om det lyckas returnerar den här metoden den uppdaterade prenumerationsordningen i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="cda45-216">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cda45-217">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cda45-217">Response success and error codes</span></span>

<span data-ttu-id="cda45-218">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="cda45-218">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cda45-219">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cda45-219">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cda45-220">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="cda45-220">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cda45-221">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cda45-221">Response example</span></span>

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