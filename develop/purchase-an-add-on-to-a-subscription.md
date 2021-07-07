---
title: Köp ett tillägg till en prenumeration
description: Så här köper du ett tillägg till en befintlig prenumeration.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547690"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="38de9-103">Köp ett tillägg till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="38de9-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="38de9-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="38de9-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="38de9-105">Så här köper du ett tillägg till en befintlig prenumeration.</span><span class="sxs-lookup"><span data-stu-id="38de9-105">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38de9-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="38de9-106">Prerequisites</span></span>

- <span data-ttu-id="38de9-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="38de9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="38de9-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="38de9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="38de9-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="38de9-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="38de9-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="38de9-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="38de9-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="38de9-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="38de9-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="38de9-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="38de9-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="38de9-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="38de9-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="38de9-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="38de9-115">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="38de9-115">A subscription ID.</span></span> <span data-ttu-id="38de9-116">Det här är den befintliga prenumeration som du kan köpa ett tilläggserbjudande för.</span><span class="sxs-lookup"><span data-stu-id="38de9-116">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="38de9-117">Ett erbjudande-ID som identifierar tilläggserbjudandet att köpa.</span><span class="sxs-lookup"><span data-stu-id="38de9-117">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="38de9-118">Köpa ett tillägg via kod</span><span class="sxs-lookup"><span data-stu-id="38de9-118">Purchasing an add-on through code</span></span>

<span data-ttu-id="38de9-119">När du köper ett tillägg till en prenumeration uppdaterar du den ursprungliga prenumerationsbeställningen med ordern för tillägget.</span><span class="sxs-lookup"><span data-stu-id="38de9-119">When you purchase an add-on to a subscription, you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="38de9-120">I följande är customerId kund-ID, subscriptionId är prenumerations-ID och addOnOfferId är erbjudandets ID för tillägget.</span><span class="sxs-lookup"><span data-stu-id="38de9-120">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="38de9-121">Här är stegen:</span><span class="sxs-lookup"><span data-stu-id="38de9-121">Here are the steps:</span></span>

1.  <span data-ttu-id="38de9-122">Hämta ett gränssnitt för åtgärderna för prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="38de9-122">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="38de9-123">Använd det gränssnittet för att instansiera ett prenumerationsobjekt.</span><span class="sxs-lookup"><span data-stu-id="38de9-123">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="38de9-124">Då får du information om den överordnade prenumerationen, inklusive order-ID:t.</span><span class="sxs-lookup"><span data-stu-id="38de9-124">This gets you the parent subscription details, including the order ID.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="38de9-125">Skapa en instans av ett nytt [**Order-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order)</span><span class="sxs-lookup"><span data-stu-id="38de9-125">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="38de9-126">Den här orderinstansen används för att uppdatera den ursprungliga order som användes för att köpa prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="38de9-126">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="38de9-127">Lägg till ett objekt med en rad i den ordning som representerar tillägget.</span><span class="sxs-lookup"><span data-stu-id="38de9-127">Add a single-line item to the order that represents the add-on.</span></span>
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

4.  <span data-ttu-id="38de9-128">Uppdatera den ursprungliga beställningen för prenumerationen med den nya ordern för tillägget.</span><span class="sxs-lookup"><span data-stu-id="38de9-128">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="38de9-129">C\#</span><span class="sxs-lookup"><span data-stu-id="38de9-129">C\#</span></span>

<span data-ttu-id="38de9-130">Om du vill köpa ett tillägg börjar du med att hämta ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och [**metoden Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera prenumerationen som har tilläggserbjudandet.</span><span class="sxs-lookup"><span data-stu-id="38de9-130">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="38de9-131">Använd det [**gränssnittet för**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) att hämta prenumerationsinformationen genom att anropa [**Hämta**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="38de9-131">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="38de9-132">Prenumerationsinformationen innehåller order-ID:t för prenumerationsordern, vilket är ordern som ska uppdateras med tillägget.</span><span class="sxs-lookup"><span data-stu-id="38de9-132">The subscription details contain the order ID of the subscription order, which is the order to be updated with the add-on.</span></span>

<span data-ttu-id="38de9-133">Skapa sedan en instans av ett nytt [**Order-objekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) och fyll i det med en enda [**LineItem-instans**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) som innehåller informationen för att identifiera tillägget, enligt följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="38de9-133">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="38de9-134">Du använder det här nya objektet för att uppdatera prenumerationsordningen med tillägget.</span><span class="sxs-lookup"><span data-stu-id="38de9-134">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="38de9-135">Anropa slutligen [**Patch-metoden**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) för att uppdatera prenumerationsordningen, efter att först ha identifierat kunden [**med IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) och [**ordern med Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span><span class="sxs-lookup"><span data-stu-id="38de9-135">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

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

<span data-ttu-id="38de9-136">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="38de9-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="38de9-137">**Project:** Partnercenter-SDK **exempelklass:** AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="38de9-137">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="38de9-138">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="38de9-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="38de9-139">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="38de9-139">Request syntax</span></span>

| <span data-ttu-id="38de9-140">Metod</span><span class="sxs-lookup"><span data-stu-id="38de9-140">Method</span></span>    | <span data-ttu-id="38de9-141">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="38de9-141">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="38de9-142">**Patch**</span><span class="sxs-lookup"><span data-stu-id="38de9-142">**PATCH**</span></span> | <span data-ttu-id="38de9-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="38de9-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="38de9-144">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="38de9-144">URI parameters</span></span>

<span data-ttu-id="38de9-145">Använd följande parametrar för att identifiera kunden och ordern.</span><span class="sxs-lookup"><span data-stu-id="38de9-145">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="38de9-146">Namn</span><span class="sxs-lookup"><span data-stu-id="38de9-146">Name</span></span>                   | <span data-ttu-id="38de9-147">Typ</span><span class="sxs-lookup"><span data-stu-id="38de9-147">Type</span></span>     | <span data-ttu-id="38de9-148">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="38de9-148">Required</span></span> | <span data-ttu-id="38de9-149">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="38de9-149">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="38de9-150">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="38de9-150">**customer-tenant-id**</span></span> | <span data-ttu-id="38de9-151">**guid**</span><span class="sxs-lookup"><span data-stu-id="38de9-151">**guid**</span></span> | <span data-ttu-id="38de9-152">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-152">Y</span></span>        | <span data-ttu-id="38de9-153">Värdet är ett GUID-formaterat **kundklient-ID** som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="38de9-153">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="38de9-154">**order-id**</span><span class="sxs-lookup"><span data-stu-id="38de9-154">**order-id**</span></span>           | <span data-ttu-id="38de9-155">**guid**</span><span class="sxs-lookup"><span data-stu-id="38de9-155">**guid**</span></span> | <span data-ttu-id="38de9-156">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-156">Y</span></span>        | <span data-ttu-id="38de9-157">Orderidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="38de9-157">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="38de9-158">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="38de9-158">Request headers</span></span>

<span data-ttu-id="38de9-159">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="38de9-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="38de9-160">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="38de9-160">Request body</span></span>

<span data-ttu-id="38de9-161">I följande tabeller beskrivs egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="38de9-161">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="38de9-162">Beställning</span><span class="sxs-lookup"><span data-stu-id="38de9-162">Order</span></span>

| <span data-ttu-id="38de9-163">Namn</span><span class="sxs-lookup"><span data-stu-id="38de9-163">Name</span></span>                | <span data-ttu-id="38de9-164">Typ</span><span class="sxs-lookup"><span data-stu-id="38de9-164">Type</span></span>             | <span data-ttu-id="38de9-165">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="38de9-165">Required</span></span> | <span data-ttu-id="38de9-166">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="38de9-166">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="38de9-167">Id</span><span class="sxs-lookup"><span data-stu-id="38de9-167">Id</span></span>                  | <span data-ttu-id="38de9-168">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-168">string</span></span>           | <span data-ttu-id="38de9-169">N</span><span class="sxs-lookup"><span data-stu-id="38de9-169">N</span></span>        | <span data-ttu-id="38de9-170">Order-ID:t.</span><span class="sxs-lookup"><span data-stu-id="38de9-170">The order ID.</span></span>                                        |
| <span data-ttu-id="38de9-171">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="38de9-171">ReferenceCustomerId</span></span> | <span data-ttu-id="38de9-172">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-172">string</span></span>           | <span data-ttu-id="38de9-173">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-173">Y</span></span>        | <span data-ttu-id="38de9-174">Kund-ID: t.</span><span class="sxs-lookup"><span data-stu-id="38de9-174">The customer ID.</span></span>                                     |
| <span data-ttu-id="38de9-175">LineItems</span><span class="sxs-lookup"><span data-stu-id="38de9-175">LineItems</span></span>           | <span data-ttu-id="38de9-176">matris med objekt</span><span class="sxs-lookup"><span data-stu-id="38de9-176">array of objects</span></span> | <span data-ttu-id="38de9-177">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-177">Y</span></span>        | <span data-ttu-id="38de9-178">En matris med [OrderLineItem-objekt.](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="38de9-178">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="38de9-179">CreationDate</span><span class="sxs-lookup"><span data-stu-id="38de9-179">CreationDate</span></span>        | <span data-ttu-id="38de9-180">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-180">string</span></span>           | <span data-ttu-id="38de9-181">N</span><span class="sxs-lookup"><span data-stu-id="38de9-181">N</span></span>        | <span data-ttu-id="38de9-182">Det datum då ordern skapades i datum/tid-format.</span><span class="sxs-lookup"><span data-stu-id="38de9-182">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="38de9-183">Attribut</span><span class="sxs-lookup"><span data-stu-id="38de9-183">Attributes</span></span>          | <span data-ttu-id="38de9-184">objekt</span><span class="sxs-lookup"><span data-stu-id="38de9-184">object</span></span>           | <span data-ttu-id="38de9-185">N</span><span class="sxs-lookup"><span data-stu-id="38de9-185">N</span></span>        | <span data-ttu-id="38de9-186">Innehåller "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="38de9-186">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="38de9-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="38de9-187">OrderLineItem</span></span>

| <span data-ttu-id="38de9-188">Namn</span><span class="sxs-lookup"><span data-stu-id="38de9-188">Name</span></span>                 | <span data-ttu-id="38de9-189">Typ</span><span class="sxs-lookup"><span data-stu-id="38de9-189">Type</span></span>   | <span data-ttu-id="38de9-190">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="38de9-190">Required</span></span> | <span data-ttu-id="38de9-191">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="38de9-191">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="38de9-192">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="38de9-192">LineItemNumber</span></span>       | <span data-ttu-id="38de9-193">antal</span><span class="sxs-lookup"><span data-stu-id="38de9-193">number</span></span> | <span data-ttu-id="38de9-194">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-194">Y</span></span>        | <span data-ttu-id="38de9-195">Radobjektets nummer, som börjar med 0.</span><span class="sxs-lookup"><span data-stu-id="38de9-195">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="38de9-196">OfferId</span><span class="sxs-lookup"><span data-stu-id="38de9-196">OfferId</span></span>              | <span data-ttu-id="38de9-197">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-197">string</span></span> | <span data-ttu-id="38de9-198">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-198">Y</span></span>        | <span data-ttu-id="38de9-199">Erbjudandets ID för tillägget.</span><span class="sxs-lookup"><span data-stu-id="38de9-199">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="38de9-200">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="38de9-200">SubscriptionId</span></span>       | <span data-ttu-id="38de9-201">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-201">string</span></span> | <span data-ttu-id="38de9-202">N</span><span class="sxs-lookup"><span data-stu-id="38de9-202">N</span></span>        | <span data-ttu-id="38de9-203">ID för tilläggsprenumerationen som köpts.</span><span class="sxs-lookup"><span data-stu-id="38de9-203">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="38de9-204">ParentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="38de9-204">ParentSubscriptionId</span></span> | <span data-ttu-id="38de9-205">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-205">string</span></span> | <span data-ttu-id="38de9-206">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-206">Y</span></span>        | <span data-ttu-id="38de9-207">ID:t för den överordnade prenumeration som har tilläggserbjudandet.</span><span class="sxs-lookup"><span data-stu-id="38de9-207">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="38de9-208">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="38de9-208">FriendlyName</span></span>         | <span data-ttu-id="38de9-209">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-209">string</span></span> | <span data-ttu-id="38de9-210">N</span><span class="sxs-lookup"><span data-stu-id="38de9-210">N</span></span>        | <span data-ttu-id="38de9-211">Det egna namnet för det här radobjektet.</span><span class="sxs-lookup"><span data-stu-id="38de9-211">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="38de9-212">Kvantitet</span><span class="sxs-lookup"><span data-stu-id="38de9-212">Quantity</span></span>             | <span data-ttu-id="38de9-213">antal</span><span class="sxs-lookup"><span data-stu-id="38de9-213">number</span></span> | <span data-ttu-id="38de9-214">Y</span><span class="sxs-lookup"><span data-stu-id="38de9-214">Y</span></span>        | <span data-ttu-id="38de9-215">Antalet licenser.</span><span class="sxs-lookup"><span data-stu-id="38de9-215">The number of licenses.</span></span>                                      |
| <span data-ttu-id="38de9-216">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="38de9-216">PartnerIdOnRecord</span></span>    | <span data-ttu-id="38de9-217">sträng</span><span class="sxs-lookup"><span data-stu-id="38de9-217">string</span></span> | <span data-ttu-id="38de9-218">N</span><span class="sxs-lookup"><span data-stu-id="38de9-218">N</span></span>        | <span data-ttu-id="38de9-219">MPN-ID:t för postpartnern.</span><span class="sxs-lookup"><span data-stu-id="38de9-219">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="38de9-220">Attribut</span><span class="sxs-lookup"><span data-stu-id="38de9-220">Attributes</span></span>           | <span data-ttu-id="38de9-221">objekt</span><span class="sxs-lookup"><span data-stu-id="38de9-221">object</span></span> | <span data-ttu-id="38de9-222">N</span><span class="sxs-lookup"><span data-stu-id="38de9-222">N</span></span>        | <span data-ttu-id="38de9-223">Innehåller "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="38de9-223">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="38de9-224">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="38de9-224">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="38de9-225">REST-svar</span><span class="sxs-lookup"><span data-stu-id="38de9-225">REST response</span></span>

<span data-ttu-id="38de9-226">Om det lyckas returnerar den här metoden den uppdaterade prenumerationsordningen i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="38de9-226">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="38de9-227">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="38de9-227">Response success and error codes</span></span>

<span data-ttu-id="38de9-228">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="38de9-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="38de9-229">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="38de9-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="38de9-230">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="38de9-230">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="38de9-231">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="38de9-231">Response example</span></span>

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
