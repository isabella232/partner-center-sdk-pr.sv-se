---
title: Skapa en prenumeration på kommersiella Marketplace-produkter
description: 'Utvecklare kan skapa och hantera en prenumeration på kommersiella Marketplace-produkter med hjälp av API: er för partner Center.'
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df2a3707e00ba36a11c404b102304c08d105244e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768811"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a><span data-ttu-id="8b685-103">Skapa en prenumeration på kommersiella Marketplace-produkter</span><span class="sxs-lookup"><span data-stu-id="8b685-103">Create a subscription for commercial marketplace products</span></span>

<span data-ttu-id="8b685-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="8b685-104">**Applies to:**</span></span>

* <span data-ttu-id="8b685-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="8b685-105">Partner Center</span></span>

<span data-ttu-id="8b685-106">Du kan skapa en prenumeration på kommersiella Marketplace-produkter med hjälp av API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="8b685-106">You can create a subscription for commercial marketplace products using Partner Center APIs.</span></span> <span data-ttu-id="8b685-107">Du måste [få en lista över erbjudanden för en marknad](#get-a-list-of-offers-for-a-market), [skapa och skicka in en order](#create-and-submit-an-order) för en prenumeration på en kommersiell marknads plats och sedan [Hämta en aktiverings länk](#get-activation-link).</span><span class="sxs-lookup"><span data-stu-id="8b685-107">You must [get a list of offers for a market](#get-a-list-of-offers-for-a-market), [create and submit an order](#create-and-submit-an-order) for a commercial marketplace subscription, then [retrieve an activation link](#get-activation-link).</span></span>

<span data-ttu-id="8b685-108">Du kan också [utföra livs cykel hantering](#lifecycle-management) och [hantera fakturor](#invoice-and-reconciliation) för dessa prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="8b685-108">You can also [perform lifecycle management](#lifecycle-management) and [manage invoices](#invoice-and-reconciliation) for these subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b685-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8b685-109">Prerequisites</span></span>

* <span data-ttu-id="8b685-110">Autentiseringsuppgifter för [partner Center-autentisering](partner-center-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="8b685-110">[Partner Center authentication](partner-center-authentication.md) credentials.</span></span> <span data-ttu-id="8b685-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8b685-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>
* <span data-ttu-id="8b685-112">Kund-ID.</span><span class="sxs-lookup"><span data-stu-id="8b685-112">The customer identifier.</span></span> <span data-ttu-id="8b685-113">Om du inte har en kund identifierare följer du stegen i [Hämta en lista över kunder](get-a-list-of-customers.md).</span><span class="sxs-lookup"><span data-stu-id="8b685-113">If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md).</span></span> <span data-ttu-id="8b685-114">Du kan också logga in på Partner Center, välja kund i listan över kunder, välja **konto** och sedan spara sitt **Microsoft-ID**.</span><span class="sxs-lookup"><span data-stu-id="8b685-114">Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.</span></span>

## <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="8b685-115">Hämta en lista över erbjudanden för en marknad</span><span class="sxs-lookup"><span data-stu-id="8b685-115">Get a list of offers for a market</span></span>

<span data-ttu-id="8b685-116">Du kan kontrol lera tillgängliga erbjudanden för en marknad med hjälp av följande Partner Center API-modeller:</span><span class="sxs-lookup"><span data-stu-id="8b685-116">You can check the available offers for a market using the following Partner Center API models:</span></span>

* <span data-ttu-id="8b685-117">**[Produkt](product-resources.md#product)**: en grupperings konstruktion för köpbara-varor eller-tjänster.</span><span class="sxs-lookup"><span data-stu-id="8b685-117">**[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="8b685-118">En produkt är inte ett köpbara-objekt.</span><span class="sxs-lookup"><span data-stu-id="8b685-118">A product itself isn't a purchasable item.</span></span>
* <span data-ttu-id="8b685-119">**[SKU](product-resources.md#sku)**: en köpbara lagerhållnings enhet (SKU) under en produkt.</span><span class="sxs-lookup"><span data-stu-id="8b685-119">**[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="8b685-120">Dessa representerar olika former av produkten.</span><span class="sxs-lookup"><span data-stu-id="8b685-120">These represent the different shapes of the product.</span></span>
* <span data-ttu-id="8b685-121">**[Tillgänglighet](product-resources.md#availability)**: en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta eller bransch segment).</span><span class="sxs-lookup"><span data-stu-id="8b685-121">**[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).</span></span>

<span data-ttu-id="8b685-122">Innan du köper en Azure-reservation utför du följande steg:</span><span class="sxs-lookup"><span data-stu-id="8b685-122">Before you purchase an Azure reservation, complete the following steps:</span></span>

1. <span data-ttu-id="8b685-123">Identifiera och hämta den produkt och SKU som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="8b685-123">Identify and retrieve the product and SKU that you want to purchase.</span></span> <span data-ttu-id="8b685-124">Om du redan känner till produkt-ID och SKU-ID väljer du dem.</span><span class="sxs-lookup"><span data-stu-id="8b685-124">If you already know the Product ID and SKU ID, select them.</span></span>

    * [<span data-ttu-id="8b685-125">Hämta en lista över produkter</span><span class="sxs-lookup"><span data-stu-id="8b685-125">Get a list of products</span></span>](get-a-list-of-products.md)
    * [<span data-ttu-id="8b685-126">Hämta en produkt med produkt-ID</span><span class="sxs-lookup"><span data-stu-id="8b685-126">Get a product using the product ID</span></span>](get-a-product-by-id.md)
    * [<span data-ttu-id="8b685-127">Hämta en lista över SKU: er för en produkt</span><span class="sxs-lookup"><span data-stu-id="8b685-127">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
    * [<span data-ttu-id="8b685-128">Hämta en SKU med SKU-ID</span><span class="sxs-lookup"><span data-stu-id="8b685-128">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

    > [!NOTE]
    > <span data-ttu-id="8b685-129">Du kan identifiera kommersiella Marketplace-produkter med deras **ProductType** -egenskap för **"Azure"** och deras **SubType** -egenskap för **"SaaS"**.</span><span class="sxs-lookup"><span data-stu-id="8b685-129">You can identify commercial marketplace products by their **ProductType** property of **"Azure"** and their **SubType** property of **"SaaS"**.</span></span>

2. <span data-ttu-id="8b685-130">Om SKU: erna är taggade med en **InventoryCheck** -förutsättning [kontrollerar du inventeringen för en SKU](check-inventory.md).</span><span class="sxs-lookup"><span data-stu-id="8b685-130">If the SKUs are tagged with an **InventoryCheck** prerequisite, [check the inventory for a SKU](check-inventory.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="8b685-131">För närvarande finns det inga kommersiella Marketplace-produkter som stöder inventerings kontroll eller som är taggade med en **InventoryCheck** -förutsättning.</span><span class="sxs-lookup"><span data-stu-id="8b685-131">At this time, there are no commercial marketplace products that support inventory check or are tagged with an **InventoryCheck** prerequisite.</span></span>

3. <span data-ttu-id="8b685-132">Hämta tillgänglighet för SKU: n.</span><span class="sxs-lookup"><span data-stu-id="8b685-132">Retrieve the availability for the SKU.</span></span> <span data-ttu-id="8b685-133">Du behöver **CatalogItemId** av tillgängligheten när du placerar ordern, som du kan hämta via följande API: er:</span><span class="sxs-lookup"><span data-stu-id="8b685-133">You will need the **CatalogItemId** of the availability when placing the order, which you can retrieve through the following APIs:</span></span>

    * [<span data-ttu-id="8b685-134">Hämta en lista över tillgänglighet för en SKU</span><span class="sxs-lookup"><span data-stu-id="8b685-134">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
    * [<span data-ttu-id="8b685-135">Få en tillgänglighet med tillgänglighets-ID: t</span><span class="sxs-lookup"><span data-stu-id="8b685-135">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a><span data-ttu-id="8b685-136">Skapa och skicka en order</span><span class="sxs-lookup"><span data-stu-id="8b685-136">Create and submit an order</span></span>

<span data-ttu-id="8b685-137">Följ dessa steg om du vill skicka in din Azure reservations ordning:</span><span class="sxs-lookup"><span data-stu-id="8b685-137">To submit your Azure reservation order, follow these steps:</span></span>

1. <span data-ttu-id="8b685-138">[Skapa en vagn](create-a-cart.md) som innehåller den samling av katalog objekt som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="8b685-138">[Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="8b685-139">När du skapar en [varukorg](cart-resources.md#cart)grupperas [vagnens rad objekt](cart-resources.md#cartlineitem) automatiskt utifrån vad som kan köpas tillsammans i samma [ordning](order-resources.md#order).</span><span class="sxs-lookup"><span data-stu-id="8b685-139">When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order).</span></span> <span data-ttu-id="8b685-140">(Du kan också [Uppdatera en varukorg](update-a-cart.md).)</span><span class="sxs-lookup"><span data-stu-id="8b685-140">(You can also [update a cart](update-a-cart.md).)</span></span>
2. <span data-ttu-id="8b685-141">[Kolla in vagnen](checkout-a-cart.md), som leder till att en [order](order-resources.md#order)skapas.</span><span class="sxs-lookup"><span data-stu-id="8b685-141">[Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).</span></span>

### <a name="get-order-details"></a><span data-ttu-id="8b685-142">Hämta beställnings information</span><span class="sxs-lookup"><span data-stu-id="8b685-142">Get order details</span></span>

<span data-ttu-id="8b685-143">Du kan [Hämta information om en enskild order med order-ID: t](get-an-order-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="8b685-143">You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md).</span></span> <span data-ttu-id="8b685-144">Du kan också [Hämta en lista över alla beställningar för en specifik kund](get-all-of-a-customer-s-orders.md).</span><span class="sxs-lookup"><span data-stu-id="8b685-144">You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8b685-145">När en beställning har skickats sker en fördröjning på upp till 15 minuter innan ordern visas i kund order listan.</span><span class="sxs-lookup"><span data-stu-id="8b685-145">After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list.</span></span>

## <a name="get-activation-link"></a><span data-ttu-id="8b685-146">Hämta aktiverings länk</span><span class="sxs-lookup"><span data-stu-id="8b685-146">Get activation link</span></span>

<span data-ttu-id="8b685-147">Partnern eller kunden måste aktivera prenumerationer på Azure Marketplace-produkter.</span><span class="sxs-lookup"><span data-stu-id="8b685-147">The partner or customer must activate subscriptions to Azure Marketplace products.</span></span> <span data-ttu-id="8b685-148">Du kan [Hämta en aktiverings länk per order rads objekt](get-activation-link-by-order-line-item.md).</span><span class="sxs-lookup"><span data-stu-id="8b685-148">You can [get an activation link by order line item](get-activation-link-by-order-line-item.md).</span></span> <span data-ttu-id="8b685-149">Du kan också [få en prenumeration efter ID](get-a-subscription-by-id.md)och sedan räkna upp dess **länkar** -egenskap för att skapa en aktiverings länk.</span><span class="sxs-lookup"><span data-stu-id="8b685-149">You can also [get a subscription by ID](get-a-subscription-by-id.md), then enumerate its **Links** property to create an activation link.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="8b685-150">Livs cykel hantering</span><span class="sxs-lookup"><span data-stu-id="8b685-150">Lifecycle management</span></span>

<span data-ttu-id="8b685-151">Du kan hantera livs cykeln för dina prenumerationer på kommersiella Marketplace-produkter på följande sätt:</span><span class="sxs-lookup"><span data-stu-id="8b685-151">You can manage the lifecycle of your subscriptions to commercial marketplace products using the following methods:</span></span>

* [<span data-ttu-id="8b685-152">Avbryta en prenumeration på kommersiell marknadsplats</span><span class="sxs-lookup"><span data-stu-id="8b685-152">Cancel a commercial marketplace subscription</span></span>](cancel-an-azure-marketplace-subscription.md)
* [<span data-ttu-id="8b685-153">Aktivera eller inaktivera autoförnyelse för en prenumeration på kommersiell marknads plats</span><span class="sxs-lookup"><span data-stu-id="8b685-153">Enable or disable autorenew for a commercial marketplace subscription</span></span>](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a><span data-ttu-id="8b685-154">Hantering av kvantitet</span><span class="sxs-lookup"><span data-stu-id="8b685-154">Quantity management</span></span>

<span data-ttu-id="8b685-155">Antalet prenumerationer på en extern marknads plats måste ligga inom de gränser som definieras av den associerade [SKU: n](product-resources.md#sku) (se attributet **minimumQuantity** och **maximumQuantity** ).</span><span class="sxs-lookup"><span data-stu-id="8b685-155">The quantity of a commercial marketplace subscription must be within the limits defined by its associated [SKU](product-resources.md#sku) (see the **minimumQuantity** and **maximumQuantity** attributes).</span></span> <span data-ttu-id="8b685-156">Använd följande metod för att uppdatera antalet för en prenumeration på en extern marknads plats:</span><span class="sxs-lookup"><span data-stu-id="8b685-156">To update the quantity of a commercial marketplace subscription, use the following method:</span></span>

* [<span data-ttu-id="8b685-157">Ändra kvantiteten för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="8b685-157">Change the quantity of a subscription</span></span>](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="8b685-158">Faktura och avstämning</span><span class="sxs-lookup"><span data-stu-id="8b685-158">Invoice and reconciliation</span></span>

<span data-ttu-id="8b685-159">Du kan hantera kund [fakturor](invoice-resources.md) (inklusive avgifter för prenumerationer på kommersiella Marketplace-produkter) på följande sätt:</span><span class="sxs-lookup"><span data-stu-id="8b685-159">You can manage customer [invoices](invoice-resources.md) (including charges for subscriptions to commercial marketplace products) using the following methods:</span></span>

* [<span data-ttu-id="8b685-160">Hämta försäljnings objekt för försäljnings fakturor på försäljnings platser</span><span class="sxs-lookup"><span data-stu-id="8b685-160">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
* [<span data-ttu-id="8b685-161">Hämta länkar för fakturauppskattning</span><span class="sxs-lookup"><span data-stu-id="8b685-161">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
* [<span data-ttu-id="8b685-162">Hämta fakturor för ej fakturerade kommersiella marknads platser på marknaden</span><span class="sxs-lookup"><span data-stu-id="8b685-162">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
* [<span data-ttu-id="8b685-163">Hämta faktura poster för ej fakturerade faktura rader</span><span class="sxs-lookup"><span data-stu-id="8b685-163">Get invoice unbilled reconciliation line items</span></span>](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a><span data-ttu-id="8b685-164">Testa att använda sandbox-konto för integration</span><span class="sxs-lookup"><span data-stu-id="8b685-164">Test using integration sandbox account</span></span>

<span data-ttu-id="8b685-165">När du har skapat en prenumeration på kommersiella Marketplace SaaS-produkter måste du hämta en anpassad aktiverings länk från Partner Center och besöka utgivarens webbplats för att slutföra installationen.</span><span class="sxs-lookup"><span data-stu-id="8b685-165">In production, after you have created a subscription to commercial marketplace SaaS products, you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="8b685-166">Prenumerations faktureringen påbörjas bara efter att installationen har slutförts.</span><span class="sxs-lookup"><span data-stu-id="8b685-166">Subscription billing will begin only after setup is complete.</span></span>

<span data-ttu-id="8b685-167">I sandbox-miljön för KRYPTOGRAFI finns det ingen integrering med ISV: er.</span><span class="sxs-lookup"><span data-stu-id="8b685-167">In the CSP sandbox environment, there is no integration with ISVs.</span></span> <span data-ttu-id="8b685-168">Om du försöker hämta en aktiverings länk från Partner Center kommer en dummy-länk att returneras.</span><span class="sxs-lookup"><span data-stu-id="8b685-168">If you try to retrieve an activation link from Partner Center, a dummy link will be returned.</span></span> <span data-ttu-id="8b685-169">Du kan inte använda den här dummy-länken för att slutföra installations processen på utgivarens webbplats.</span><span class="sxs-lookup"><span data-stu-id="8b685-169">You cannot use this dummy link to complete the setup process at the publisher's site.</span></span> <span data-ttu-id="8b685-170">Använd följande metod för att aktivera prenumerationen i stället för att använda det begränsade kontot för integration för att testa faktureringen för prenumerationer på kommersiella Marketplace-SaaS produkter.</span><span class="sxs-lookup"><span data-stu-id="8b685-170">To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, use the following method to activate the subscription instead.</span></span> <span data-ttu-id="8b685-171">Prenumerations faktureringen påbörjas efter lyckad aktivering:</span><span class="sxs-lookup"><span data-stu-id="8b685-171">Subscription billing will begin after successful activation:</span></span>

* [<span data-ttu-id="8b685-172">Aktivera en Sandbox-prenumeration för kommersiella Marketplace-produkter</span><span class="sxs-lookup"><span data-stu-id="8b685-172">Activate a sandbox subscription for commercial marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

