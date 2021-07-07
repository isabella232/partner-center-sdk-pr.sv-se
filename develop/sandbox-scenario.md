---
title: Sandbox-funktioner för återförsäljarrelation
description: Sandbox-miljön för partner har möjlighet att stödja relationer mellan partnern och kunden
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aa6c4fb9ef71bacfad7e0f1510fec15f6af60a05
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547401"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="eccb5-103">Sandbox-funktioner för återförsäljarrelation</span><span class="sxs-lookup"><span data-stu-id="eccb5-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="eccb5-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="eccb5-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="eccb5-105">Den här artikeln förklarar vad som stöds i sandbox-miljön för återförsäljarrelationer mellan partnern och kunden.</span><span class="sxs-lookup"><span data-stu-id="eccb5-105">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eccb5-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="eccb5-106">Prerequisites</span></span>

- <span data-ttu-id="eccb5-107">Autentiseringsuppgifter för Partnercenter-konto.</span><span class="sxs-lookup"><span data-stu-id="eccb5-107">Partner Center account credentials.</span></span> <span data-ttu-id="eccb5-108">Sandbox-scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="eccb5-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="eccb5-109">Ett kund-ID (kund-klient-ID).</span><span class="sxs-lookup"><span data-stu-id="eccb5-109">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="eccb5-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard/home)</span><span class="sxs-lookup"><span data-stu-id="eccb5-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="eccb5-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="eccb5-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="eccb5-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="eccb5-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="eccb5-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="eccb5-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="eccb5-114">Microsoft-ID:t är samma som kund-ID:t (kund-klient-ID).</span><span class="sxs-lookup"><span data-stu-id="eccb5-114">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="eccb5-115">Alla Azure Reserved Virtual Machine Instances och programvaruköpordrar måste avbrytas innan du tar bort en kund från sandbox-miljön för Tipsintegrering.</span><span class="sxs-lookup"><span data-stu-id="eccb5-115">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="eccb5-116">Scenarier som stöder återförsäljarrelation</span><span class="sxs-lookup"><span data-stu-id="eccb5-116">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="eccb5-117">Direktfaktureringspartner och indirekta leverantörer i sandbox-miljön kan skapa relationer med sandbox-kunden.</span><span class="sxs-lookup"><span data-stu-id="eccb5-117">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="eccb5-118">Faktureringspartner och indirekta leverantörer i sandbox-miljön kan inte bjuda in Sandbox-kunder.</span><span class="sxs-lookup"><span data-stu-id="eccb5-118">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="eccb5-119">Faktureringspartner och indirekta leverantörer i sandbox-miljön kan ta bort återförsäljarrelationer från Partner Center-gränssnittet och API:et.</span><span class="sxs-lookup"><span data-stu-id="eccb5-119">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="eccb5-120">Sandbox Remove Reseller Relationship (Ta bort återförsäljarrelation) anropar Delete customer AP (Ta bort kund-AP).</span><span class="sxs-lookup"><span data-stu-id="eccb5-120">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="eccb5-121">Detta tar bort relationen och kundklientorganisationen.</span><span class="sxs-lookup"><span data-stu-id="eccb5-121">This will remove the relationship and delete the customer tenant.</span></span> <span data-ttu-id="eccb5-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="eccb5-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="eccb5-123">I sandbox-miljön</span><span class="sxs-lookup"><span data-stu-id="eccb5-123">In the Sandbox</span></span>

    <span data-ttu-id="eccb5-124">**Partner för direktfakturering:**</span><span class="sxs-lookup"><span data-stu-id="eccb5-124">**Direct bill partners**:</span></span>

    - <span data-ttu-id="eccb5-125">Kan lägga till befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-125">Can add existing customers</span></span>

    - <span data-ttu-id="eccb5-126">Det går inte att begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-126">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="eccb5-127">**Indirekta leverantörer:**</span><span class="sxs-lookup"><span data-stu-id="eccb5-127">**Indirect providers**:</span></span>

    - <span data-ttu-id="eccb5-128">Kan lägga till befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-128">Can add existing customers</span></span>

    - <span data-ttu-id="eccb5-129">Det går inte att begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-129">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="eccb5-130">Det går inte att ha en relation med en indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="eccb5-130">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="eccb5-131">**Indirekt återförsäljare:**</span><span class="sxs-lookup"><span data-stu-id="eccb5-131">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="eccb5-132">Kan ha relationer med befintliga kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-132">Can have relationships with existing customers</span></span>

    -   <span data-ttu-id="eccb5-133">Det går inte att begära nya relationer eller lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-133">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="eccb5-134">I Partnercenter</span><span class="sxs-lookup"><span data-stu-id="eccb5-134">In Partner Center</span></span>

    <span data-ttu-id="eccb5-135">**Partner för direktfakturering:**</span><span class="sxs-lookup"><span data-stu-id="eccb5-135">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="eccb5-136">Kan lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-136">Can add new customers</span></span>

    -   <span data-ttu-id="eccb5-137">Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-137">Can request relationships with new customers</span></span>

    <span data-ttu-id="eccb5-138">**Indirekta leverantörer:**</span><span class="sxs-lookup"><span data-stu-id="eccb5-138">**Indirect providers**:</span></span>

    -   <span data-ttu-id="eccb5-139">Kan lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-139">Can add new customers</span></span>

    -   <span data-ttu-id="eccb5-140">Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-140">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="eccb5-141">Kan ha relationer med indirekta återförsäljare</span><span class="sxs-lookup"><span data-stu-id="eccb5-141">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="eccb5-142">**Indirekta återförsäljare:**</span><span class="sxs-lookup"><span data-stu-id="eccb5-142">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="eccb5-143">Det går inte att lägga till nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-143">Can’t add new customers</span></span>

    -   <span data-ttu-id="eccb5-144">Kan begära relationer med nya kunder</span><span class="sxs-lookup"><span data-stu-id="eccb5-144">Can request relationships with new customers</span></span>


<span data-ttu-id="eccb5-145">Mer information [finns i Ta](remove-a-reseller-relationship-with-a-customer.md) bort återförsäljarrelation för kunden.</span><span class="sxs-lookup"><span data-stu-id="eccb5-145">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="eccb5-146">Det finns dock vissa skillnader mellan funktionerna Product och Sandbox.</span><span class="sxs-lookup"><span data-stu-id="eccb5-146">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="eccb5-147">BEGÄRANDESYNTAX</span><span class="sxs-lookup"><span data-stu-id="eccb5-147">REQUEST SYNTAX</span></span>

|<span data-ttu-id="eccb5-148">**Metod**</span><span class="sxs-lookup"><span data-stu-id="eccb5-148">**Method**</span></span>|<span data-ttu-id="eccb5-149">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="eccb5-149">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="eccb5-150">Ta bort</span><span class="sxs-lookup"><span data-stu-id="eccb5-150">Delete</span></span>|<span data-ttu-id="eccb5-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="eccb5-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="eccb5-152">Begärandetext Ingen</span><span class="sxs-lookup"><span data-stu-id="eccb5-152">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="eccb5-153">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="eccb5-153">Response success and error codes</span></span>

<span data-ttu-id="eccb5-154">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="eccb5-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="eccb5-155">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="eccb5-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="eccb5-156">En fullständig lista finns i [Partner Center REST-felkoder.](./error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="eccb5-156">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eccb5-157">Nästa steg</span><span class="sxs-lookup"><span data-stu-id="eccb5-157">Next steps</span></span>

- [<span data-ttu-id="eccb5-158">Aktivera Sandbox-prenumerationer för Azure Marketplace produkter</span><span class="sxs-lookup"><span data-stu-id="eccb5-158">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="eccb5-159">Avbryta en beställning från sandbox-miljön</span><span class="sxs-lookup"><span data-stu-id="eccb5-159">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="eccb5-160">Testa och felsök</span><span class="sxs-lookup"><span data-stu-id="eccb5-160">Test and debug</span></span>](test-and-debug.md)