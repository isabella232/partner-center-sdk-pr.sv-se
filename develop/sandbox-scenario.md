---
title: Sandbox-funktioner för återförsäljarrelation
description: Sandbox-miljön för partner har möjlighet att stödja relationer mellan partnern och kunden
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9bef4a15685ebbdc2212988f5ac5724b946cfd54
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2021
ms.locfileid: "110243392"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="e669e-103">Sandbox-funktioner för återförsäljarrelation</span><span class="sxs-lookup"><span data-stu-id="e669e-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="e669e-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="e669e-104">**Applies to:**</span></span>

- <span data-ttu-id="e669e-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e669e-105">Partner Center</span></span>
- <span data-ttu-id="e669e-106">Partnercenter drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e669e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e669e-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="e669e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e669e-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e669e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e669e-109">Den här artikeln förklarar vad som stöds i sandbox-miljön för återförsäljarrelationer mellan partnern och kunden.</span><span class="sxs-lookup"><span data-stu-id="e669e-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e669e-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e669e-110">Prerequisites</span></span>

- <span data-ttu-id="e669e-111">Autentiseringsuppgifter för Partnercenter-konto.</span><span class="sxs-lookup"><span data-stu-id="e669e-111">Partner Center account credentials.</span></span> <span data-ttu-id="e669e-112">Sandbox-scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e669e-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="e669e-113">Ett kund-ID (kund-klient-ID).</span><span class="sxs-lookup"><span data-stu-id="e669e-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="e669e-114">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard/home)</span><span class="sxs-lookup"><span data-stu-id="e669e-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="e669e-115">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="e669e-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e669e-116">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="e669e-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e669e-117">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="e669e-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e669e-118">Microsoft-ID:t är samma som kund-ID:t (kund-klient-ID).</span><span class="sxs-lookup"><span data-stu-id="e669e-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="e669e-119">Alla Azure Reserved Virtual Machine Instances och programvaruinköpsorder måste avbrytas innan du tar bort en kund från sandbox-miljön för Tip-integrering.</span><span class="sxs-lookup"><span data-stu-id="e669e-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="e669e-120">Scenarier som stöder återförsäljarrelation</span><span class="sxs-lookup"><span data-stu-id="e669e-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="e669e-121">Direktfaktureringspartner och indirekta leverantörer i sandbox-miljön kan skapa relationer med Sandbox-kunden.</span><span class="sxs-lookup"><span data-stu-id="e669e-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="e669e-122">Sandbox-direktfaktureringspartner och indirekta leverantörer kan inte bjuda in Sandbox-kunder.</span><span class="sxs-lookup"><span data-stu-id="e669e-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="e669e-123">Direktfaktureringspartner och indirekta leverantörer i sandbox-miljö kan ta bort återförsäljarrelationer från Partner Center-gränssnittet och API:et.</span><span class="sxs-lookup"><span data-stu-id="e669e-123">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="e669e-124">Sandbox Remove Reseller Relationship anropar Ta bort kund-AP.</span><span class="sxs-lookup"><span data-stu-id="e669e-124">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="e669e-125">Detta tar bort relationen samt kundens klientorganisation.</span><span class="sxs-lookup"><span data-stu-id="e669e-125">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="e669e-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="e669e-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="e669e-127">I sandbox-miljön</span><span class="sxs-lookup"><span data-stu-id="e669e-127">In the Sandbox</span></span>

    <span data-ttu-id="e669e-128">**Partner för direktfakturering:**</span><span class="sxs-lookup"><span data-stu-id="e669e-128">**Direct bill partners**:</span></span>

    - <span data-ttu-id="e669e-129">Kan lägga till befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-129">Can add existing customers</span></span>

    - <span data-ttu-id="e669e-130">Det går inte att begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-130">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="e669e-131">**Indirekta leverantörer:**</span><span class="sxs-lookup"><span data-stu-id="e669e-131">**Indirect providers**:</span></span>

    - <span data-ttu-id="e669e-132">Kan lägga till befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-132">Can add existing customers</span></span>

    - <span data-ttu-id="e669e-133">Det går inte att begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-133">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="e669e-134">Det går inte att ha en relation med en indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="e669e-134">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="e669e-135">**Indirekt återförsäljare:**</span><span class="sxs-lookup"><span data-stu-id="e669e-135">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="e669e-136">Kan ha en relation med befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-136">Can have a relationships with existing customers</span></span>

    -   <span data-ttu-id="e669e-137">Det går inte att begära nya relationer eller lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-137">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="e669e-138">I Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e669e-138">In Partner Center</span></span>

    <span data-ttu-id="e669e-139">**Partner för direktfakturering:**</span><span class="sxs-lookup"><span data-stu-id="e669e-139">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="e669e-140">Kan lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-140">Can add new customers</span></span>

    -   <span data-ttu-id="e669e-141">Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-141">Can request relationships with new customers</span></span>

    <span data-ttu-id="e669e-142">**Indirekta leverantörer:**</span><span class="sxs-lookup"><span data-stu-id="e669e-142">**Indirect providers**:</span></span>

    -   <span data-ttu-id="e669e-143">Kan lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-143">Can add new customers</span></span>

    -   <span data-ttu-id="e669e-144">Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-144">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="e669e-145">Kan ha relationer med indirekta återförsäljare</span><span class="sxs-lookup"><span data-stu-id="e669e-145">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="e669e-146">**Indirekta återförsäljare:**</span><span class="sxs-lookup"><span data-stu-id="e669e-146">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="e669e-147">Det går inte att lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-147">Can’t add new customers</span></span>

    -   <span data-ttu-id="e669e-148">Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="e669e-148">Can request relationships with new customers</span></span>


<span data-ttu-id="e669e-149">Mer information [finns i Ta](remove-a-reseller-relationship-with-a-customer.md) bort återförsäljarrelation för kunden.</span><span class="sxs-lookup"><span data-stu-id="e669e-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="e669e-150">Det finns dock vissa skillnader mellan funktionerna Product och Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e669e-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e669e-151">BEGÄRANDESYNTAX</span><span class="sxs-lookup"><span data-stu-id="e669e-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="e669e-152">**Metod**</span><span class="sxs-lookup"><span data-stu-id="e669e-152">**Method**</span></span>|<span data-ttu-id="e669e-153">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="e669e-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="e669e-154">Ta bort</span><span class="sxs-lookup"><span data-stu-id="e669e-154">Delete</span></span>|<span data-ttu-id="e669e-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="e669e-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="e669e-156">Begärandetext Ingen</span><span class="sxs-lookup"><span data-stu-id="e669e-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e669e-157">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e669e-157">Response success and error codes</span></span>

<span data-ttu-id="e669e-158">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e669e-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e669e-159">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e669e-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e669e-160">En fullständig lista finns i [Partner Center REST-felkoder.](./error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e669e-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e669e-161">Nästa steg</span><span class="sxs-lookup"><span data-stu-id="e669e-161">Next steps</span></span>

- [<span data-ttu-id="e669e-162">Aktivera Sandbox-prenumerationer för Azure Marketplace produkter</span><span class="sxs-lookup"><span data-stu-id="e669e-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="e669e-163">Avbryta en beställning från sandbox-miljön</span><span class="sxs-lookup"><span data-stu-id="e669e-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="e669e-164">Testa och felsök</span><span class="sxs-lookup"><span data-stu-id="e669e-164">Test and debug</span></span>](test-and-debug.md)