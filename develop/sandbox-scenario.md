---
title: Partnerfunktioner för sandbox-miljö som stöder återförsäljarrelation
description: Partner sand Box har möjlighet att stödja relationer mellan partnern och kunden
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711873"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a><span data-ttu-id="9e4ad-103">Partnerfunktioner för sandbox-miljö som stöder återförsäljarrelation</span><span class="sxs-lookup"><span data-stu-id="9e4ad-103">Partner sandbox capabilities that support reseller relationship</span></span>

<span data-ttu-id="9e4ad-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="9e4ad-104">**Applies to:**</span></span>

- <span data-ttu-id="9e4ad-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9e4ad-105">Partner Center</span></span>
- <span data-ttu-id="9e4ad-106">Partnercenter drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="9e4ad-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9e4ad-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="9e4ad-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9e4ad-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9e4ad-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9e4ad-109">Den här artikeln förklarar vad som stöds i sand boxen för åter försäljares relationer mellan partnern och kunden.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e4ad-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9e4ad-110">Prerequisites</span></span>

- <span data-ttu-id="9e4ad-111">Autentiseringsuppgifter för partner Center-kontot.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-111">Partner Center account credentials.</span></span> <span data-ttu-id="9e4ad-112">Sandbox-scenariot stöder autentisering med både den fristående appen och appens och användarens autentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="9e4ad-113">Ett kund-ID (kund-Tenant-ID).</span><span class="sxs-lookup"><span data-stu-id="9e4ad-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="9e4ad-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard/home)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="9e4ad-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9e4ad-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9e4ad-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="9e4ad-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9e4ad-118">Microsoft-ID: t är detsamma som kund-ID (kund-Tenant-ID).</span><span class="sxs-lookup"><span data-stu-id="9e4ad-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="9e4ad-119">Alla Azure Reserved Virtual Machine Instances-och program inköps order måste annulleras innan du tar bort en kund från sandbox-tipset.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="9e4ad-120">Scenarier som stöder åter försäljarens relation</span><span class="sxs-lookup"><span data-stu-id="9e4ad-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="9e4ad-121">I sand Box Direct Bill partners och indirekta leverantörer kan du skapa relationer med den begränsade kunden.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="9e4ad-122">Sand Box Direct Bill partners och indirekta leverantörer kan inte bjuda in sandbox-kunder.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>



### <a name="in-the-sandbox"></a><span data-ttu-id="9e4ad-123">I sandbox</span><span class="sxs-lookup"><span data-stu-id="9e4ad-123">In the Sandbox</span></span>

<span data-ttu-id="9e4ad-124">**Direkta fakturerings partner**:</span><span class="sxs-lookup"><span data-stu-id="9e4ad-124">**Direct bill partners**:</span></span>

<span data-ttu-id="9e4ad-125">• Kan lägga till befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-125">•   Can add existing customers</span></span>

<span data-ttu-id="9e4ad-126">• Det går inte att begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-126">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="9e4ad-127">**Indirekta leverantörer**:</span><span class="sxs-lookup"><span data-stu-id="9e4ad-127">**Indirect providers**:</span></span>

<span data-ttu-id="9e4ad-128">• Kan lägga till befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-128">•   Can add existing customers</span></span>

<span data-ttu-id="9e4ad-129">• Det går inte att begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-129">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="9e4ad-130">• Det går inte att ha en relation med en indirekt åter försäljare</span><span class="sxs-lookup"><span data-stu-id="9e4ad-130">•   Cannot have a relationship with an Indirect reseller</span></span>

<span data-ttu-id="9e4ad-131">**Indirekt åter försäljare**: (kommer snart)</span><span class="sxs-lookup"><span data-stu-id="9e4ad-131">**Indirect reseller**: (coming soon)</span></span>

<span data-ttu-id="9e4ad-132">• Kan ha relationer med befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-132">•   Can have a relationships with existing customers</span></span>

<span data-ttu-id="9e4ad-133">• Det går inte att begära nya relationer eller lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-133">•   Cannot request new relationships or add new customers</span></span>

### <a name="in-partner-center"></a><span data-ttu-id="9e4ad-134">I Partner Center</span><span class="sxs-lookup"><span data-stu-id="9e4ad-134">In Partner Center</span></span>

<span data-ttu-id="9e4ad-135">**Direkta fakturerings partner**:</span><span class="sxs-lookup"><span data-stu-id="9e4ad-135">**Direct bill partners**:</span></span>

<span data-ttu-id="9e4ad-136">• Kan lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-136">•   Can add new customers</span></span>

<span data-ttu-id="9e4ad-137">• Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-137">•   Can request relationships with new customers</span></span>

<span data-ttu-id="9e4ad-138">**Indirekta leverantörer**:</span><span class="sxs-lookup"><span data-stu-id="9e4ad-138">**Indirect providers**:</span></span>

<span data-ttu-id="9e4ad-139">• Kan lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-139">•   Can add new customers</span></span>

<span data-ttu-id="9e4ad-140">• Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-140">•   Can request relationships with new customers</span></span>

<span data-ttu-id="9e4ad-141">• Kan ha relationer med indirekta åter försäljare</span><span class="sxs-lookup"><span data-stu-id="9e4ad-141">•   Can have relationships with indirect resellers</span></span>

<span data-ttu-id="9e4ad-142">**Indirekta åter försäljare**:</span><span class="sxs-lookup"><span data-stu-id="9e4ad-142">**Indirect resellers**:</span></span>

<span data-ttu-id="9e4ad-143">• Det går inte att lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-143">•   Can’t add new customers</span></span>

<span data-ttu-id="9e4ad-144">• Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-144">•   Can request relationships with new customers</span></span>

3. <span data-ttu-id="9e4ad-145">I sandbox direkt fakturerings partner och indirekta leverantörer kan du ta bort åter försäljarens relation från användar gränssnittet och API: t för partner Center.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-145">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="9e4ad-146">Den begränsade åter försäljarens relation kommer att anropa ta bort kund-AP.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-146">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="9e4ad-147">Detta tar bort relationen och tar bort kund klienten.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-147">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="9e4ad-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="9e4ad-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>

<span data-ttu-id="9e4ad-149">Följ den [ta bort åter försäljarens relation](remove-a-reseller-relationship-with-a-customer.md) för kunden för mer information.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="9e4ad-150">Det finns dock vissa skillnader mellan produkt-och sandbox-funktionerna.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e4ad-151">SYNTAX FÖR BEGÄRAN</span><span class="sxs-lookup"><span data-stu-id="9e4ad-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="9e4ad-152">**Metod**</span><span class="sxs-lookup"><span data-stu-id="9e4ad-152">**Method**</span></span>|<span data-ttu-id="9e4ad-153">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="9e4ad-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="9e4ad-154">Ta bort</span><span class="sxs-lookup"><span data-stu-id="9e4ad-154">Delete</span></span>|<span data-ttu-id="9e4ad-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="9e4ad-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="9e4ad-156">Begär ande texten none</span><span class="sxs-lookup"><span data-stu-id="9e4ad-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e4ad-157">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9e4ad-157">Response success and error codes</span></span>

<span data-ttu-id="9e4ad-158">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e4ad-159">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9e4ad-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e4ad-160">En fullständig lista finns i [partner Center rest-felkoder](./error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9e4ad-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e4ad-161">Nästa steg</span><span class="sxs-lookup"><span data-stu-id="9e4ad-161">Next steps</span></span>

- [<span data-ttu-id="9e4ad-162">Aktivera sandbox-prenumerationer för Azure Marketplace-produkter</span><span class="sxs-lookup"><span data-stu-id="9e4ad-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="9e4ad-163">Avbryta en order från sandbox</span><span class="sxs-lookup"><span data-stu-id="9e4ad-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="9e4ad-164">Testa och felsök</span><span class="sxs-lookup"><span data-stu-id="9e4ad-164">Test and debug</span></span>](test-and-debug.md)