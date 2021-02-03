---
title: Köp katalogobjekt
description: Så här köper du katalog objekt med API för partner Center.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768883"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="c38b3-103">Köp katalogobjekt</span><span class="sxs-lookup"><span data-stu-id="c38b3-103">Purchase catalog items</span></span>

<span data-ttu-id="c38b3-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="c38b3-104">**Applies To**</span></span>

- <span data-ttu-id="c38b3-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="c38b3-105">Partner Center</span></span>

<span data-ttu-id="c38b3-106">Följande scenario visar den allmänna processen för att köpa objekt från katalogen med hjälp av Partner Center-API: et.</span><span class="sxs-lookup"><span data-stu-id="c38b3-106">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="c38b3-107">Identifiering</span><span class="sxs-lookup"><span data-stu-id="c38b3-107">Discovery</span></span>

<span data-ttu-id="c38b3-108">Välj produkter och SKU: er och kontrol lera deras tillgänglighet med hjälp av följande Partner Center API-modeller:</span><span class="sxs-lookup"><span data-stu-id="c38b3-108">Select products and SKUs and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="c38b3-109">[Produkt](product-resources.md#product) – en grupperings konstruktion för köpbara-varor eller-tjänster.</span><span class="sxs-lookup"><span data-stu-id="c38b3-109">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="c38b3-110">En produkt som själva är inte ett köpbara-objekt.</span><span class="sxs-lookup"><span data-stu-id="c38b3-110">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="c38b3-111">[SKU](product-resources.md#sku) – en köpbara lagerhållnings enhet (SKU) under en produkt.</span><span class="sxs-lookup"><span data-stu-id="c38b3-111">[SKU](product-resources.md#sku) - A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="c38b3-112">Dessa representerar olika former av produkten.</span><span class="sxs-lookup"><span data-stu-id="c38b3-112">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="c38b3-113">[Tillgänglighet](product-resources.md#availability) – en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta och bransch segment).</span><span class="sxs-lookup"><span data-stu-id="c38b3-113">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency and industry segment).</span></span>

<span data-ttu-id="c38b3-114">Utför följande steg för att köpa ett objekt från katalogen:</span><span class="sxs-lookup"><span data-stu-id="c38b3-114">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="c38b3-115">Identifiera och hämta den produkt och SKU som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="c38b3-115">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="c38b3-116">Hämta en lista över produkter</span><span class="sxs-lookup"><span data-stu-id="c38b3-116">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="c38b3-117">Hämta en produkt med produkt-ID</span><span class="sxs-lookup"><span data-stu-id="c38b3-117">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="c38b3-118">Hämta en lista över SKU: er för en produkt</span><span class="sxs-lookup"><span data-stu-id="c38b3-118">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="c38b3-119">Hämta en SKU med SKU-ID</span><span class="sxs-lookup"><span data-stu-id="c38b3-119">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="c38b3-120">Kontrol lera inventeringen för en SKU.</span><span class="sxs-lookup"><span data-stu-id="c38b3-120">Check the inventory for a SKU.</span></span> <span data-ttu-id="c38b3-121">Det här steget behövs bara för SKU: er som är taggade med ett **InventoryCheck** -värde i egenskapen [purchasePrerequisites](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="c38b3-121">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="c38b3-122">Kontrollera lager</span><span class="sxs-lookup"><span data-stu-id="c38b3-122">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="c38b3-123">Hämta [tillgänglighet](product-resources.md#availability) för SKU: [n](product-resources.md#sku).</span><span class="sxs-lookup"><span data-stu-id="c38b3-123">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="c38b3-124">Du behöver **CatalogItemId** av tillgängligheten när du placerar ordern.</span><span class="sxs-lookup"><span data-stu-id="c38b3-124">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="c38b3-125">Använd något av följande API: er för att hämta det här värdet:</span><span class="sxs-lookup"><span data-stu-id="c38b3-125">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="c38b3-126">Hämta en lista över tillgänglighet för en SKU</span><span class="sxs-lookup"><span data-stu-id="c38b3-126">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="c38b3-127">Få en tillgänglighet med tillgänglighets-ID: t</span><span class="sxs-lookup"><span data-stu-id="c38b3-127">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="c38b3-128">Order överföring</span><span class="sxs-lookup"><span data-stu-id="c38b3-128">Order submission</span></span>

<span data-ttu-id="c38b3-129">Gör så här för att skicka in din katalog objekts ordning:</span><span class="sxs-lookup"><span data-stu-id="c38b3-129">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="c38b3-130">Skapa en [vagn](cart-resources.md) som innehåller den samling av katalog objekt som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="c38b3-130">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="c38b3-131">När du skapar en varukorg grupperas [vagnens rad objekt](cart-resources.md#cartlineitem) automatiskt utifrån vad som kan köpas tillsammans i samma [ordning](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-131">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="c38b3-132">Skapa en Shopping vagn</span><span class="sxs-lookup"><span data-stu-id="c38b3-132">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="c38b3-133">Uppdatera en Shopping vagn</span><span class="sxs-lookup"><span data-stu-id="c38b3-133">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="c38b3-134">Kolla in vagnen.</span><span class="sxs-lookup"><span data-stu-id="c38b3-134">Check out the cart.</span></span> <span data-ttu-id="c38b3-135">Att checka ut en vagns resultat i skapandet av en [order](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-135">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="c38b3-136">Checka ut vagnen</span><span class="sxs-lookup"><span data-stu-id="c38b3-136">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="c38b3-137">Hämta beställnings information</span><span class="sxs-lookup"><span data-stu-id="c38b3-137">Get order details</span></span>

<span data-ttu-id="c38b3-138">Du kan hämta information om en enskild order med order-ID: t eller hämta en lista över beställningar för en kund.</span><span class="sxs-lookup"><span data-stu-id="c38b3-138">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="c38b3-139">Det finns en fördröjning på upp till 15 minuter mellan tiden som en beställning skickas och när den visas i en lista över en kunds beställningar.</span><span class="sxs-lookup"><span data-stu-id="c38b3-139">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="c38b3-140">Se [Hämta en order efter ID](get-an-order-by-id.md) för att få information om en enskild order med hjälp av order-ID: n.</span><span class="sxs-lookup"><span data-stu-id="c38b3-140">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="c38b3-141">Se [Hämta alla kund order](get-all-of-a-customer-s-orders.md) för att få en lista över beställningar för en kund med kund-ID.</span><span class="sxs-lookup"><span data-stu-id="c38b3-141">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="c38b3-142">Se [Hämta en lista över beställningar efter kund-och fakturerings cykel typ](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) för att få en lista över beställningar för en kund via [fakturerings cykel typ](product-resources.md#billingcycletype) , så att du kan visa en lista över katalog objekts beställningar (engångs avgifter) och årliga eller månatliga fakturerade beställningar separat.</span><span class="sxs-lookup"><span data-stu-id="c38b3-142">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="c38b3-143">Livs cykel hantering</span><span class="sxs-lookup"><span data-stu-id="c38b3-143">Lifecycle management</span></span>

<span data-ttu-id="c38b3-144">Som en del av att hantera livs cykeln för dina katalog objekt i Partner Center kan du hämta information om dina katalog objekts [rättigheter](entitlement-resources.md)och hämta reservations information med hjälp av reservations orderns ID.</span><span class="sxs-lookup"><span data-stu-id="c38b3-144">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="c38b3-145">Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-145">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="c38b3-146">Faktura och avstämning</span><span class="sxs-lookup"><span data-stu-id="c38b3-146">Invoice and reconciliation</span></span>

<span data-ttu-id="c38b3-147">Följande scenarier visar hur du program mässigt visar din kunds [fakturor](invoice-resources.md)och hur du får dina konto balanser och sammanfattningar som innehåller engångs avgifter för katalog objekt.</span><span class="sxs-lookup"><span data-stu-id="c38b3-147">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="c38b3-148">Saldo och betalning</span><span class="sxs-lookup"><span data-stu-id="c38b3-148">Balance and payment</span></span>

<span data-ttu-id="c38b3-149">Om du vill hämta aktuellt konto saldo i din standard valuta typ som är en balans mellan både återkommande och engångs kostnader (katalog objekt), se [Hämta ditt aktuella konto saldo](get-the-reseller-s-current-account-balance.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-149">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="c38b3-150">Saldo och betalning för flera valutor</span><span class="sxs-lookup"><span data-stu-id="c38b3-150">Multi-currency balance and payment</span></span>

<span data-ttu-id="c38b3-151">Om du vill hämta ditt aktuella konto saldo och en samling av faktura sammanfattningar som innehåller en faktura sammanfattning med både återkommande och engångs kostnader för var och en av kundens valuta typer, se [Hämta faktura sammanfattningar](get-invoice-summaries.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-151">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="c38b3-152">Fakturor</span><span class="sxs-lookup"><span data-stu-id="c38b3-152">Invoices</span></span>

<span data-ttu-id="c38b3-153">Om du vill hämta en samling fakturor som visar både återkommande och engångs kostnader, se [Hämta en samling fakturor](get-a-collection-of-invoices.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-153">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="c38b3-154">Enskild faktura</span><span class="sxs-lookup"><span data-stu-id="c38b3-154">Single Invoice</span></span>

<span data-ttu-id="c38b3-155">Information om hur du hämtar en speciell faktura med hjälp av faktura-ID finns i [Hämta en faktura efter ID](get-invoice-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-155">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="c38b3-156">Konto</span><span class="sxs-lookup"><span data-stu-id="c38b3-156">Reconciliation</span></span>

<span data-ttu-id="c38b3-157">Information om hur du hämtar information om faktura rads objekt (avstämnings rad objekt) för ett angivet faktura-ID finns i [Hämta faktura rads objekt](get-invoiceline-items.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-157">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="c38b3-158">Ladda ned en faktura som en PDF</span><span class="sxs-lookup"><span data-stu-id="c38b3-158">Download an invoice as a PDF</span></span>

<span data-ttu-id="c38b3-159">Information om hur du hämtar ett faktura uttryck i PDF-formulär med hjälp av ett faktura-ID finns i [Hämta en faktura instruktion](get-invoice-statement.md).</span><span class="sxs-lookup"><span data-stu-id="c38b3-159">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
