---
title: Köp katalogobjekt
description: Så här köper du katalogobjekt med partnercenter-API:et.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3e0deedff194b1c836d9266c2201a2b3a52cc1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445365"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="7cae7-103">Köp katalogobjekt</span><span class="sxs-lookup"><span data-stu-id="7cae7-103">Purchase catalog items</span></span>

<span data-ttu-id="7cae7-104">Följande scenario visar den allmänna processen för att köpa objekt från katalogen med hjälp av Partner Center-API:et.</span><span class="sxs-lookup"><span data-stu-id="7cae7-104">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="7cae7-105">Identifiering</span><span class="sxs-lookup"><span data-stu-id="7cae7-105">Discovery</span></span>

<span data-ttu-id="7cae7-106">Välj produkter och lagerhållningsenheter (SKU:er) och kontrollera deras tillgänglighet med hjälp av följande Partner Center API-modeller:</span><span class="sxs-lookup"><span data-stu-id="7cae7-106">Select products and Stock Keeping Units (SKUs) and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="7cae7-107">[Produkt](product-resources.md#product) – en grupperingskonstruktion för köpbara varor eller tjänster.</span><span class="sxs-lookup"><span data-stu-id="7cae7-107">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="7cae7-108">En produkt i sig är inte ett köpbart objekt.</span><span class="sxs-lookup"><span data-stu-id="7cae7-108">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="7cae7-109">[SKU](product-resources.md#sku) – en köpbar SKU under en produkt.</span><span class="sxs-lookup"><span data-stu-id="7cae7-109">[SKU](product-resources.md#sku) - A purchasable SKU under a product.</span></span> <span data-ttu-id="7cae7-110">De representerar olika former av produkten.</span><span class="sxs-lookup"><span data-stu-id="7cae7-110">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="7cae7-111">[Tillgänglighet](product-resources.md#availability) – En konfiguration där en SKU är tillgänglig för inköp (till exempel land, valuta och branschsegment).</span><span class="sxs-lookup"><span data-stu-id="7cae7-111">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency, and industry segment).</span></span>

<span data-ttu-id="7cae7-112">Utför följande steg för att köpa ett objekt från katalogen:</span><span class="sxs-lookup"><span data-stu-id="7cae7-112">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="7cae7-113">Identifiera och hämta den produkt och SKU som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="7cae7-113">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="7cae7-114">Hämta en lista över produkter</span><span class="sxs-lookup"><span data-stu-id="7cae7-114">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="7cae7-115">Hämta en produkt med hjälp av produkt-ID:t</span><span class="sxs-lookup"><span data-stu-id="7cae7-115">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="7cae7-116">Hämta en lista över SKU:er för en produkt</span><span class="sxs-lookup"><span data-stu-id="7cae7-116">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="7cae7-117">Hämta en SKU med hjälp av SKU-ID:t</span><span class="sxs-lookup"><span data-stu-id="7cae7-117">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="7cae7-118">Kontrollera inventeringen för en SKU.</span><span class="sxs-lookup"><span data-stu-id="7cae7-118">Check the inventory for a SKU.</span></span> <span data-ttu-id="7cae7-119">Det här steget behövs bara för SKU:er som är taggade med **ett InventoryCheck-värde** [i egenskapen purchasePrerequisites.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="7cae7-119">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="7cae7-120">Kontrollera lager</span><span class="sxs-lookup"><span data-stu-id="7cae7-120">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="7cae7-121">Hämta [tillgängligheten](product-resources.md#availability) för [SKU:n](product-resources.md#sku).</span><span class="sxs-lookup"><span data-stu-id="7cae7-121">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="7cae7-122">Du behöver **CatalogItemId för** tillgängligheten när du gör beställningen.</span><span class="sxs-lookup"><span data-stu-id="7cae7-122">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="7cae7-123">Använd något av följande API:er för att hämta det här värdet:</span><span class="sxs-lookup"><span data-stu-id="7cae7-123">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="7cae7-124">Hämta en lista över tillgänglighet för en SKU</span><span class="sxs-lookup"><span data-stu-id="7cae7-124">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="7cae7-125">Hämta en tillgänglighet med hjälp av tillgänglighets-ID:t</span><span class="sxs-lookup"><span data-stu-id="7cae7-125">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="7cae7-126">Skicka order</span><span class="sxs-lookup"><span data-stu-id="7cae7-126">Order submission</span></span>

<span data-ttu-id="7cae7-127">Gör följande om du vill skicka in katalogobjektsordningen:</span><span class="sxs-lookup"><span data-stu-id="7cae7-127">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="7cae7-128">Skapa en [kundvagn](cart-resources.md) för den samling katalogobjekt som du tänker köpa.</span><span class="sxs-lookup"><span data-stu-id="7cae7-128">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="7cae7-129">När du skapar en kundvagn [grupperas kundvagnsraderna](cart-resources.md#cartlineitem) automatiskt baserat på vad som kan köpas tillsammans i samma [order.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="7cae7-129">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="7cae7-130">Skapa en kundvagn</span><span class="sxs-lookup"><span data-stu-id="7cae7-130">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="7cae7-131">Uppdatera en kundvagn</span><span class="sxs-lookup"><span data-stu-id="7cae7-131">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="7cae7-132">Kolla in kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="7cae7-132">Check out the cart.</span></span> <span data-ttu-id="7cae7-133">När du checkar ut en kundvagn skapas en [order.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="7cae7-133">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="7cae7-134">Checka ut kundvagnen</span><span class="sxs-lookup"><span data-stu-id="7cae7-134">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="7cae7-135">Hämta beställningsinformation</span><span class="sxs-lookup"><span data-stu-id="7cae7-135">Get order details</span></span>

<span data-ttu-id="7cae7-136">Du kan hämta information om en enskild order med hjälp av order-ID:t eller hämta en lista över beställningar för en kund.</span><span class="sxs-lookup"><span data-stu-id="7cae7-136">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="7cae7-137">Det finns en fördröjning på upp till 15 minuter från det att en order skickas tills den visas i en lista över en kunds beställningar.</span><span class="sxs-lookup"><span data-stu-id="7cae7-137">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="7cae7-138">Information om en enskild order med hjälp av order-ID:n finns i Hämta en beställning per [ID.](get-an-order-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="7cae7-138">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="7cae7-139">Se [Hämta alla en kunds beställningar för att få](get-all-of-a-customer-s-orders.md) en lista över beställningar för en kund med hjälp av kund-ID:t.</span><span class="sxs-lookup"><span data-stu-id="7cae7-139">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="7cae7-140">Se [Hämta en](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) lista över beställningar efter kund och faktureringscykeltyp [](product-resources.md#billingcycletype) för att få en lista över beställningar för en kund efter faktureringsperiodstyp så att du kan visa en lista över beställningar av katalogobjekt (en gång-avgifter) och beställningar som faktureras per år eller månad separat.</span><span class="sxs-lookup"><span data-stu-id="7cae7-140">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="7cae7-141">Livscykelhantering</span><span class="sxs-lookup"><span data-stu-id="7cae7-141">Lifecycle management</span></span>

<span data-ttu-id="7cae7-142">Som en del av att hantera livscykeln för dina katalogobjekt i Partnercenter kan du hämta information om [katalogobjektets](entitlement-resources.md)berättiganden och hämta reservationsinformation med hjälp av reservationsbeställnings-ID:t.</span><span class="sxs-lookup"><span data-stu-id="7cae7-142">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="7cae7-143">Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).</span><span class="sxs-lookup"><span data-stu-id="7cae7-143">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="7cae7-144">Faktura och avstämning</span><span class="sxs-lookup"><span data-stu-id="7cae7-144">Invoice and reconciliation</span></span>

<span data-ttu-id="7cae7-145">Följande scenarier visar hur du programmatiskt visar kundens fakturor [och](invoice-resources.md)hämtar dina kontosaldon och sammanfattningar som inkluderar engångsavgifter för katalogobjekt.</span><span class="sxs-lookup"><span data-stu-id="7cae7-145">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="7cae7-146">Saldo och betalning</span><span class="sxs-lookup"><span data-stu-id="7cae7-146">Balance and payment</span></span>

<span data-ttu-id="7cae7-147">Information om hur du hämtar aktuellt kontosaldo i din standardvalutatyp som är ett saldo för både återkommande avgifter och engångsavgifter (katalogobjekt) finns i Hämta [ditt aktuella kontosaldo.](get-the-reseller-s-current-account-balance.md)</span><span class="sxs-lookup"><span data-stu-id="7cae7-147">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="7cae7-148">Saldo och betalning i flera valutor</span><span class="sxs-lookup"><span data-stu-id="7cae7-148">Multi-currency balance and payment</span></span>

<span data-ttu-id="7cae7-149">Information om hur du hämtar ditt aktuella kontosaldo och en samling fakturasammanfattningar som innehåller en fakturasammanfattning med både återkommande avgifter och engångsavgifter för var och en av kundens valutatyper finns i [Hämta fakturasammanfattningar.](get-invoice-summaries.md)</span><span class="sxs-lookup"><span data-stu-id="7cae7-149">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="7cae7-150">Fakturor</span><span class="sxs-lookup"><span data-stu-id="7cae7-150">Invoices</span></span>

<span data-ttu-id="7cae7-151">Information om hur du hämtar en samling fakturor som visar både återkommande och engångsavgifter finns i [Hämta en samling fakturor.](get-a-collection-of-invoices.md)</span><span class="sxs-lookup"><span data-stu-id="7cae7-151">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="7cae7-152">Enskild faktura</span><span class="sxs-lookup"><span data-stu-id="7cae7-152">Single Invoice</span></span>

<span data-ttu-id="7cae7-153">Information om hur du hämtar en specifik faktura med hjälp av faktura-ID:t [finns i Hämta en faktura via ID](get-invoice-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="7cae7-153">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="7cae7-154">Försoning</span><span class="sxs-lookup"><span data-stu-id="7cae7-154">Reconciliation</span></span>

<span data-ttu-id="7cae7-155">Information om en samling fakturaradsobjekt (avstämningsradsobjekt) för ett specifikt faktura-ID finns i [Hämta fakturaradsobjekt.](get-invoiceline-items.md)</span><span class="sxs-lookup"><span data-stu-id="7cae7-155">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="7cae7-156">Ladda ned en faktura som en PDF</span><span class="sxs-lookup"><span data-stu-id="7cae7-156">Download an invoice as a PDF</span></span>

<span data-ttu-id="7cae7-157">Information om hur du hämtar ett fakturautdrag i PDF-format med hjälp av ett faktura-ID finns [i Hämta ett fakturautdrag](get-invoice-statement.md).</span><span class="sxs-lookup"><span data-stu-id="7cae7-157">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
