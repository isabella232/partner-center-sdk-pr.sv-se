---
title: Köp ett tillägg till en prenumeration
description: Så här köper du ett tillägg till en befintlig prenumeration.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769657"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="3243e-103">Köp ett tillägg till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="3243e-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="3243e-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="3243e-104">**Applies To**</span></span>

- <span data-ttu-id="3243e-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="3243e-105">Partner Center</span></span>
- <span data-ttu-id="3243e-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="3243e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3243e-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3243e-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3243e-108">Så här köper du ett tillägg till en befintlig prenumeration.</span><span class="sxs-lookup"><span data-stu-id="3243e-108">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3243e-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3243e-109">Prerequisites</span></span>

- <span data-ttu-id="3243e-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3243e-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3243e-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3243e-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3243e-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3243e-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3243e-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="3243e-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3243e-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="3243e-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3243e-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="3243e-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3243e-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="3243e-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3243e-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3243e-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3243e-118">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="3243e-118">A subscription ID.</span></span> <span data-ttu-id="3243e-119">Det här är den befintliga prenumerationen för vilken du kan köpa ett tilläggs erbjudande.</span><span class="sxs-lookup"><span data-stu-id="3243e-119">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="3243e-120">Ett erbjudande-ID som identifierar tilläggs erbjudandet för köp.</span><span class="sxs-lookup"><span data-stu-id="3243e-120">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="3243e-121">Köpa ett tillägg via kod</span><span class="sxs-lookup"><span data-stu-id="3243e-121">Purchasing an add-on through code</span></span>

<span data-ttu-id="3243e-122">När du köper ett tillägg till en prenumeration uppdaterar du den ursprungliga prenumerations ordningen med ordern för tillägget.</span><span class="sxs-lookup"><span data-stu-id="3243e-122">When you purchase an add-on to a subscription you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="3243e-123">I följande är customerId kund-ID: t, subscriptionId är prenumerations-ID och addOnOfferId är erbjudande-ID för tillägget.</span><span class="sxs-lookup"><span data-stu-id="3243e-123">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="3243e-124">Här är stegen:</span><span class="sxs-lookup"><span data-stu-id="3243e-124">Here are the steps:</span></span>

1.  <span data-ttu-id="3243e-125">Hämta ett gränssnitt till prenumerationens åtgärder.</span><span class="sxs-lookup"><span data-stu-id="3243e-125">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="3243e-126">Använd det gränssnittet för att instansiera ett prenumerations objekt.</span><span class="sxs-lookup"><span data-stu-id="3243e-126">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="3243e-127">Detta hämtar information om överordnad prenumeration, inklusive order-ID.</span><span class="sxs-lookup"><span data-stu-id="3243e-127">This gets you the parent subscription details, including the order id.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="3243e-128">Instansiera ett nytt [**order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objekt.</span><span class="sxs-lookup"><span data-stu-id="3243e-128">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="3243e-129">Den här order instansen används för att uppdatera den ursprungliga order som används för att köpa prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="3243e-129">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="3243e-130">Lägg till ett enskilt rad objekt i den ordning som representerar tillägget.</span><span class="sxs-lookup"><span data-stu-id="3243e-130">Add a single line item to the order that represents the add-on.</span></span>
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  <span data-ttu-id="3243e-131">Uppdatera den ursprungliga ordningen för prenumerationen med den nya ordern för tillägget.</span><span class="sxs-lookup"><span data-stu-id="3243e-131">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="3243e-132">C\#</span><span class="sxs-lookup"><span data-stu-id="3243e-132">C\#</span></span>

<span data-ttu-id="3243e-133">Om du vill köpa ett tillägg börjar du med att hämta ett gränssnitt till prenumerations åtgärderna genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera den prenumeration som har tilläggs erbjudandet.</span><span class="sxs-lookup"><span data-stu-id="3243e-133">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="3243e-134">Använd det [**gränssnittet**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) för att hämta prenumerations informationen genom att anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="3243e-134">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="3243e-135">Varför behöver du prenumerations informationen?</span><span class="sxs-lookup"><span data-stu-id="3243e-135">Why do you need the subscription details?</span></span> <span data-ttu-id="3243e-136">Eftersom du behöver order-ID: t för prenumerations ordern.</span><span class="sxs-lookup"><span data-stu-id="3243e-136">Because you need the order id of the subscription order.</span></span> <span data-ttu-id="3243e-137">Det är den ordning som ska uppdateras med tillägget.</span><span class="sxs-lookup"><span data-stu-id="3243e-137">That's the order to be updated with the add-on.</span></span>

<span data-ttu-id="3243e-138">Sedan instansierar du ett nytt [**order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) -objekt och fyller det med en enda [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -instans som innehåller informationen för att identifiera tillägget, som du ser i följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="3243e-138">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="3243e-139">Du använder det här nya objektet för att uppdatera prenumerations ordningen med tillägget.</span><span class="sxs-lookup"><span data-stu-id="3243e-139">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="3243e-140">Slutligen kan du anropa [**korrigerings**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) metoden för att uppdatera prenumerations ordningen, efter att först ha identifierat kunden med [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) och ordern med [**Orders. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span><span class="sxs-lookup"><span data-stu-id="3243e-140">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

<span data-ttu-id="3243e-141">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3243e-141">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3243e-142">**Projekt**: Partner Center SDK-exempel **klass**: AddSubscriptionAddOn.CS</span><span class="sxs-lookup"><span data-stu-id="3243e-142">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3243e-143">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3243e-143">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3243e-144">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="3243e-144">Request syntax</span></span>

| <span data-ttu-id="3243e-145">Metod</span><span class="sxs-lookup"><span data-stu-id="3243e-145">Method</span></span>    | <span data-ttu-id="3243e-146">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3243e-146">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3243e-147">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="3243e-147">**PATCH**</span></span> | <span data-ttu-id="3243e-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3243e-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3243e-149">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="3243e-149">URI parameters</span></span>

<span data-ttu-id="3243e-150">Använd följande parametrar för att identifiera kunden och ordern.</span><span class="sxs-lookup"><span data-stu-id="3243e-150">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="3243e-151">Namn</span><span class="sxs-lookup"><span data-stu-id="3243e-151">Name</span></span>                   | <span data-ttu-id="3243e-152">Typ</span><span class="sxs-lookup"><span data-stu-id="3243e-152">Type</span></span>     | <span data-ttu-id="3243e-153">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3243e-153">Required</span></span> | <span data-ttu-id="3243e-154">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3243e-154">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="3243e-155">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="3243e-155">**customer-tenant-id**</span></span> | <span data-ttu-id="3243e-156">**guid**</span><span class="sxs-lookup"><span data-stu-id="3243e-156">**guid**</span></span> | <span data-ttu-id="3243e-157">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-157">Y</span></span>        | <span data-ttu-id="3243e-158">Värdet är ett GUID-formaterat **kund-Tenant-ID** som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="3243e-158">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="3243e-159">**order-ID**</span><span class="sxs-lookup"><span data-stu-id="3243e-159">**order-id**</span></span>           | <span data-ttu-id="3243e-160">**guid**</span><span class="sxs-lookup"><span data-stu-id="3243e-160">**guid**</span></span> | <span data-ttu-id="3243e-161">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-161">Y</span></span>        | <span data-ttu-id="3243e-162">Order-ID.</span><span class="sxs-lookup"><span data-stu-id="3243e-162">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="3243e-163">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3243e-163">Request headers</span></span>

<span data-ttu-id="3243e-164">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3243e-164">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3243e-165">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3243e-165">Request body</span></span>

<span data-ttu-id="3243e-166">I följande tabeller beskrivs egenskaperna i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="3243e-166">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="3243e-167">Beställning</span><span class="sxs-lookup"><span data-stu-id="3243e-167">Order</span></span>

| <span data-ttu-id="3243e-168">Namn</span><span class="sxs-lookup"><span data-stu-id="3243e-168">Name</span></span>                | <span data-ttu-id="3243e-169">Typ</span><span class="sxs-lookup"><span data-stu-id="3243e-169">Type</span></span>             | <span data-ttu-id="3243e-170">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3243e-170">Required</span></span> | <span data-ttu-id="3243e-171">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3243e-171">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="3243e-172">Id</span><span class="sxs-lookup"><span data-stu-id="3243e-172">Id</span></span>                  | <span data-ttu-id="3243e-173">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-173">string</span></span>           | <span data-ttu-id="3243e-174">N</span><span class="sxs-lookup"><span data-stu-id="3243e-174">N</span></span>        | <span data-ttu-id="3243e-175">Order-ID.</span><span class="sxs-lookup"><span data-stu-id="3243e-175">The order ID.</span></span>                                        |
| <span data-ttu-id="3243e-176">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="3243e-176">ReferenceCustomerId</span></span> | <span data-ttu-id="3243e-177">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-177">string</span></span>           | <span data-ttu-id="3243e-178">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-178">Y</span></span>        | <span data-ttu-id="3243e-179">Kund-ID.</span><span class="sxs-lookup"><span data-stu-id="3243e-179">The customer ID.</span></span>                                     |
| <span data-ttu-id="3243e-180">Rad objekt</span><span class="sxs-lookup"><span data-stu-id="3243e-180">LineItems</span></span>           | <span data-ttu-id="3243e-181">objekt mat ris</span><span class="sxs-lookup"><span data-stu-id="3243e-181">array of objects</span></span> | <span data-ttu-id="3243e-182">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-182">Y</span></span>        | <span data-ttu-id="3243e-183">En matris med [OrderLineItem](#orderlineitem) -objekt.</span><span class="sxs-lookup"><span data-stu-id="3243e-183">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="3243e-184">CreationDate</span><span class="sxs-lookup"><span data-stu-id="3243e-184">CreationDate</span></span>        | <span data-ttu-id="3243e-185">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-185">string</span></span>           | <span data-ttu-id="3243e-186">N</span><span class="sxs-lookup"><span data-stu-id="3243e-186">N</span></span>        | <span data-ttu-id="3243e-187">Datumet då ordern skapades i datum-/tids format.</span><span class="sxs-lookup"><span data-stu-id="3243e-187">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="3243e-188">Attribut</span><span class="sxs-lookup"><span data-stu-id="3243e-188">Attributes</span></span>          | <span data-ttu-id="3243e-189">objekt</span><span class="sxs-lookup"><span data-stu-id="3243e-189">object</span></span>           | <span data-ttu-id="3243e-190">N</span><span class="sxs-lookup"><span data-stu-id="3243e-190">N</span></span>        | <span data-ttu-id="3243e-191">Innehåller "ObjectType": "order".</span><span class="sxs-lookup"><span data-stu-id="3243e-191">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="3243e-192">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="3243e-192">OrderLineItem</span></span>

| <span data-ttu-id="3243e-193">Namn</span><span class="sxs-lookup"><span data-stu-id="3243e-193">Name</span></span>                 | <span data-ttu-id="3243e-194">Typ</span><span class="sxs-lookup"><span data-stu-id="3243e-194">Type</span></span>   | <span data-ttu-id="3243e-195">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3243e-195">Required</span></span> | <span data-ttu-id="3243e-196">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3243e-196">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="3243e-197">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="3243e-197">LineItemNumber</span></span>       | <span data-ttu-id="3243e-198">antal</span><span class="sxs-lookup"><span data-stu-id="3243e-198">number</span></span> | <span data-ttu-id="3243e-199">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-199">Y</span></span>        | <span data-ttu-id="3243e-200">Rad objekts numret, från och med 0.</span><span class="sxs-lookup"><span data-stu-id="3243e-200">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="3243e-201">OfferId</span><span class="sxs-lookup"><span data-stu-id="3243e-201">OfferId</span></span>              | <span data-ttu-id="3243e-202">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-202">string</span></span> | <span data-ttu-id="3243e-203">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-203">Y</span></span>        | <span data-ttu-id="3243e-204">Erbjudande-ID för tillägget.</span><span class="sxs-lookup"><span data-stu-id="3243e-204">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="3243e-205">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="3243e-205">SubscriptionId</span></span>       | <span data-ttu-id="3243e-206">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-206">string</span></span> | <span data-ttu-id="3243e-207">N</span><span class="sxs-lookup"><span data-stu-id="3243e-207">N</span></span>        | <span data-ttu-id="3243e-208">ID: t för den tilläggs prenumeration som har köpts.</span><span class="sxs-lookup"><span data-stu-id="3243e-208">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="3243e-209">ParentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="3243e-209">ParentSubscriptionId</span></span> | <span data-ttu-id="3243e-210">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-210">string</span></span> | <span data-ttu-id="3243e-211">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-211">Y</span></span>        | <span data-ttu-id="3243e-212">ID för den överordnade prenumeration som har tilläggs erbjudandet.</span><span class="sxs-lookup"><span data-stu-id="3243e-212">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="3243e-213">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="3243e-213">FriendlyName</span></span>         | <span data-ttu-id="3243e-214">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-214">string</span></span> | <span data-ttu-id="3243e-215">N</span><span class="sxs-lookup"><span data-stu-id="3243e-215">N</span></span>        | <span data-ttu-id="3243e-216">Det egna namnet för det här rad objektet.</span><span class="sxs-lookup"><span data-stu-id="3243e-216">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="3243e-217">Antal</span><span class="sxs-lookup"><span data-stu-id="3243e-217">Quantity</span></span>             | <span data-ttu-id="3243e-218">antal</span><span class="sxs-lookup"><span data-stu-id="3243e-218">number</span></span> | <span data-ttu-id="3243e-219">Y</span><span class="sxs-lookup"><span data-stu-id="3243e-219">Y</span></span>        | <span data-ttu-id="3243e-220">Antalet licenser.</span><span class="sxs-lookup"><span data-stu-id="3243e-220">The number of licenses.</span></span>                                      |
| <span data-ttu-id="3243e-221">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="3243e-221">PartnerIdOnRecord</span></span>    | <span data-ttu-id="3243e-222">sträng</span><span class="sxs-lookup"><span data-stu-id="3243e-222">string</span></span> | <span data-ttu-id="3243e-223">N</span><span class="sxs-lookup"><span data-stu-id="3243e-223">N</span></span>        | <span data-ttu-id="3243e-224">MPN-ID: t för post partnern.</span><span class="sxs-lookup"><span data-stu-id="3243e-224">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="3243e-225">Attribut</span><span class="sxs-lookup"><span data-stu-id="3243e-225">Attributes</span></span>           | <span data-ttu-id="3243e-226">objekt</span><span class="sxs-lookup"><span data-stu-id="3243e-226">object</span></span> | <span data-ttu-id="3243e-227">N</span><span class="sxs-lookup"><span data-stu-id="3243e-227">N</span></span>        | <span data-ttu-id="3243e-228">Innehåller "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="3243e-228">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="3243e-229">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3243e-229">Request example</span></span>

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
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
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

## <a name="rest-response"></a><span data-ttu-id="3243e-230">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3243e-230">REST response</span></span>

<span data-ttu-id="3243e-231">Om det lyckas returnerar den här metoden den uppdaterade prenumerations ordningen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="3243e-231">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3243e-232">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3243e-232">Response success and error codes</span></span>

<span data-ttu-id="3243e-233">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="3243e-233">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3243e-234">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3243e-234">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3243e-235">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3243e-235">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3243e-236">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3243e-236">Response example</span></span>

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
    "billingCycle": "none",
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
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
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
