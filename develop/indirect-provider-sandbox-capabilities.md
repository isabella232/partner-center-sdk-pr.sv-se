---
title: CSP Indirect-providerfunktioner i sandbox-miljön
description: Indirekta leverantörer kan skapa indirekta återförsäljare i sandbox-miljön i testsyfte.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445909"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="54f50-103">CSP Indirect provider sandbox-funktioner för att skapa konton för indirekta återförsäljare</span><span class="sxs-lookup"><span data-stu-id="54f50-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="54f50-104">**Lämpliga roller:** Indirekt leverantör</span><span class="sxs-lookup"><span data-stu-id="54f50-104">**Appropriate roles**: Indirect provider</span></span>

<span data-ttu-id="54f50-105">Indirekta CSP-leverantörer kan skapa CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.</span><span class="sxs-lookup"><span data-stu-id="54f50-105">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="54f50-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="54f50-106">Prerequisites</span></span> 

<span data-ttu-id="54f50-107">Partner Center Indirect Provider -autentiseringsuppgifter (nivå 2) för sandbox-miljö.</span><span class="sxs-lookup"><span data-stu-id="54f50-107">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="54f50-108">Sandbox-scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="54f50-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="54f50-109">Sandbox Indirect Provider – Skapa en indirekt Sandbox-återförsäljare med hjälp av Partner Center-användargränssnittet</span><span class="sxs-lookup"><span data-stu-id="54f50-109">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="54f50-110">Det här är en funktion för endast sandbox-miljö som gör att indirekta sandbox-leverantörer kan skapa ett sandbox-konto för indirekt återförsäljare via Partner Center-portalen.</span><span class="sxs-lookup"><span data-stu-id="54f50-110">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to create a Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="54f50-111">Följande scenarier är vad indirekta leverantörer kan göra för indirekta återförsäljare i sandbox-miljön via Partner Center-användargränssnittet:</span><span class="sxs-lookup"><span data-stu-id="54f50-111">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="54f50-112">Indirekta CSP-leverantörer kan skapa ett CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.</span><span class="sxs-lookup"><span data-stu-id="54f50-112">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="54f50-113">CSP Indirect Resellers kan visa kunden av indirekta leverantörer.</span><span class="sxs-lookup"><span data-stu-id="54f50-113">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="54f50-114">CSP Indirect Resellers kan hantera kundkontot med hjälp av delegerade administratörsbehörigheter.</span><span class="sxs-lookup"><span data-stu-id="54f50-114">CSP Indirect Resellers can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="54f50-115">CSP Indirect Providers kan bjuda in indirekta CSP-återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="54f50-115">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="54f50-116">Indirekta CSP-leverantörer kan ta bort CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.</span><span class="sxs-lookup"><span data-stu-id="54f50-116">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="54f50-117">a.</span><span class="sxs-lookup"><span data-stu-id="54f50-117">a.</span></span>  <span data-ttu-id="54f50-118">När sandbox-miljöns indirekta leverantör tar bort relationen med den indirekta Sandbox-återförsäljaren kontrollerar du om den indirekta återförsäljaren har någon annan relation med andra leverantörer.</span><span class="sxs-lookup"><span data-stu-id="54f50-118">When Sandbox Indirect Provider deletes the relationship with Sandbox Indirect Reseller, check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="54f50-119">I så fall tas endast relationen med den specifika indirekta providern bort.</span><span class="sxs-lookup"><span data-stu-id="54f50-119">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="54f50-120">c.</span><span class="sxs-lookup"><span data-stu-id="54f50-120">c.</span></span> <span data-ttu-id="54f50-121">Om det är den enda relationen för den indirekta återförsäljaren tas den indirekta återförsäljaren bort.</span><span class="sxs-lookup"><span data-stu-id="54f50-121">If that is the only relationship for the Indirect Reseller, then the Indirect Reseller will be deleted.</span></span>

1. <span data-ttu-id="54f50-122">CSP Indirect Providers kan ta bort en CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="54f50-122">CSP Indirect Providers can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="54f50-123">a.</span><span class="sxs-lookup"><span data-stu-id="54f50-123">a.</span></span> <span data-ttu-id="54f50-124">Det här är en funktion för endast sandbox-miljö som gör att indirekta sandbox-leverantörer kan ta bort indirekta Sandbox-återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="54f50-124">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="54f50-125">Förutsättningar för att ta bort en indirekt Sandbox-återförsäljare:</span><span class="sxs-lookup"><span data-stu-id="54f50-125">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="54f50-126">Pausa prenumerationerna för varje kund hos den indirekta Sandbox-återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="54f50-126">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="54f50-127">Ta bort alla indirekt återförsäljares kunder.</span><span class="sxs-lookup"><span data-stu-id="54f50-127">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="54f50-128">Gräns på fem indirekta Sandbox-återförsäljare per indirekt Sandbox-leverantör.</span><span class="sxs-lookup"><span data-stu-id="54f50-128">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="54f50-129">När den indirekta sandbox-återförsäljaren har tagits bort återställs kvoten.</span><span class="sxs-lookup"><span data-stu-id="54f50-129">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="54f50-130">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="54f50-130">Pre-requisites</span></span>

- <span data-ttu-id="54f50-131">Gräns på fem indirekta Sandbox-återförsäljare per indirekt Sandbox-leverantör.</span><span class="sxs-lookup"><span data-stu-id="54f50-131">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="54f50-132">Samma MPN-ID kan användas för att skapa flera sandbox-konton för indirekta återförsäljare om land för MPN-ID och sandbox-land för indirekt återförsäljare är samma.</span><span class="sxs-lookup"><span data-stu-id="54f50-132">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="54f50-133">Om du har ett tillgängligt MPN-test-ID kan du använda det eller hämta en lista över MPN-ID:n via [vår Yammer kanal]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span><span class="sxs-lookup"><span data-stu-id="54f50-133">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="54f50-134">Om du inte har åtkomst till Yammer ber Yammer dig att begära åtkomst.</span><span class="sxs-lookup"><span data-stu-id="54f50-134">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="54f50-135">Endast 75 kunder tillåts per indirekt sandbox-provider</span><span class="sxs-lookup"><span data-stu-id="54f50-135">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="54f50-136">Skapa CSP Indirect Reseller Sandbox-konto</span><span class="sxs-lookup"><span data-stu-id="54f50-136">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="54f50-137">Logga in på Partner Center via ditt sandbox-konto på nivå 2.</span><span class="sxs-lookup"><span data-stu-id="54f50-137">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="54f50-138">Gå till Indirekta återförsäljare på den vänstra menyn.</span><span class="sxs-lookup"><span data-stu-id="54f50-138">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="54f50-139">Välj knappen **Lägg till sandbox-miljö för** återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="54f50-139">Select the **Add Reseller Sandbox** button.</span></span> 

4. <span data-ttu-id="54f50-140">Fyll i formuläret för kontoregistrering.</span><span class="sxs-lookup"><span data-stu-id="54f50-140">Fill the account enrollment form.</span></span> <span data-ttu-id="54f50-141">Det är självförklarande, men kom ihåg att du skapar ett Sandbox-konto för en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="54f50-141">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="54f50-142">Det här kontot kommer inte att genomgå någon granskning och aktiveras så snart du är klar med kontoregistreringen.</span><span class="sxs-lookup"><span data-stu-id="54f50-142">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="54f50-143">När kontot har skapats får du autentiseringsuppgifterna för global administratör för sandbox-kontot för indirekt återförsäljare på portalen.</span><span class="sxs-lookup"><span data-stu-id="54f50-143">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="54f50-144">Kom ihåg att spara den omedelbart, annars kan du inte logga in som sandbox-miljö för indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="54f50-144">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="54f50-145">Logga ut och logga in igen på Partner Center med de nya autentiseringsuppgifterna för sandbox-miljön för indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="54f50-145">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="54f50-146">Utforska de funktioner som du kan göra som en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="54f50-146">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="54f50-147">Några saker är:</span><span class="sxs-lookup"><span data-stu-id="54f50-147">Some things are:</span></span>  

    - <span data-ttu-id="54f50-148">Hantera profiler</span><span class="sxs-lookup"><span data-stu-id="54f50-148">Manage profiles</span></span>  

    - <span data-ttu-id="54f50-149">Hantera användare och roller</span><span class="sxs-lookup"><span data-stu-id="54f50-149">Manage users and roles</span></span> 

    - <span data-ttu-id="54f50-150">Hantera indirekta leverantörer</span><span class="sxs-lookup"><span data-stu-id="54f50-150">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="54f50-151">Hantera CSP Sandbox-kunder</span><span class="sxs-lookup"><span data-stu-id="54f50-151">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="54f50-152">Hantera relationer</span><span class="sxs-lookup"><span data-stu-id="54f50-152">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="54f50-153">Indirekt Sandbox-provider – Ta bort indirekt Sandbox-återförsäljare med hjälp av Partner Center-användargränssnittet</span><span class="sxs-lookup"><span data-stu-id="54f50-153">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="54f50-154">Det här är en funktion endast för sandbox-miljö som gör det möjligt för indirekta sandbox-leverantörer att ta bort ett befintligt konto för indirekt sandbox-återförsäljare via Partner Center-portalen.</span><span class="sxs-lookup"><span data-stu-id="54f50-154">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="54f50-155">Förutsättningar för att ta bort indirekt sandbox-återförsäljare:</span><span class="sxs-lookup"><span data-stu-id="54f50-155">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="54f50-156">Ett befintligt CSP Indirect Reseller sandbox-konto som är associerat med ditt CSP Indirect Provider sandbox-konto på nivå 2.</span><span class="sxs-lookup"><span data-stu-id="54f50-156">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="54f50-157">Ta CSP Indirect Reseller sandbox-konto</span><span class="sxs-lookup"><span data-stu-id="54f50-157">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="54f50-158">Logga in på PartnerCenter med ditt sandbox-konto på nivå 2.</span><span class="sxs-lookup"><span data-stu-id="54f50-158">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="54f50-159">Gå till Indirekta återförsäljare på den vänstra menyn.</span><span class="sxs-lookup"><span data-stu-id="54f50-159">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="54f50-160">Välj länken **Ta bort sandbox-miljö** för återförsäljare bredvid det sandbox-konto för indirekt återförsäljare som du vill ta bort.</span><span class="sxs-lookup"><span data-stu-id="54f50-160">Select the **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="54f50-161">Sandbox-kontot för indirekt återförsäljare tas bort permanent och kan inte återställas.</span><span class="sxs-lookup"><span data-stu-id="54f50-161">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="54f50-162">API-referenser</span><span class="sxs-lookup"><span data-stu-id="54f50-162">API references</span></span>

- <span data-ttu-id="54f50-163">Skapa indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="54f50-163">Create Indirect Reseller</span></span> 
- <span data-ttu-id="54f50-164">Ta bort indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="54f50-164">Delete Indirect Reseller</span></span> 

 

 