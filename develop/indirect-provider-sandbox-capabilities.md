---
title: CSP Indirect-providerfunktioner i sandbox-miljön
description: Indirekta leverantörer kan skapa indirekta återförsäljare i sandbox-miljön i testsyfte.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244609"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="07ea1-103">CSP Indirect provider sandbox-funktioner för att skapa konton för indirekta återförsäljare</span><span class="sxs-lookup"><span data-stu-id="07ea1-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="07ea1-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="07ea1-104">**Applies to**</span></span>

- <span data-ttu-id="07ea1-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="07ea1-105">Partner Center</span></span>

<span data-ttu-id="07ea1-106">**Lämpliga roller**</span><span class="sxs-lookup"><span data-stu-id="07ea1-106">**Appropriate roles**</span></span>

- <span data-ttu-id="07ea1-107">Indirekt leverantör</span><span class="sxs-lookup"><span data-stu-id="07ea1-107">Indirect provider</span></span>

<span data-ttu-id="07ea1-108">Indirekta CSP-leverantörer kan skapa CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.</span><span class="sxs-lookup"><span data-stu-id="07ea1-108">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="07ea1-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="07ea1-109">Prerequisites</span></span> 

<span data-ttu-id="07ea1-110">Partner Center Indirect Provider -autentiseringsuppgifter (nivå 2) för sandbox-miljö.</span><span class="sxs-lookup"><span data-stu-id="07ea1-110">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="07ea1-111">Sandbox-scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="07ea1-111">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="07ea1-112">Sandbox Indirect Provider – Skapa en indirekt Sandbox-återförsäljare med hjälp av Partner Center-användargränssnittet</span><span class="sxs-lookup"><span data-stu-id="07ea1-112">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="07ea1-113">Det här är en sandbox-funktion som gör det möjligt för indirekta sandbox-leverantörer att skapa ett sandbox-konto för indirekt återförsäljare via Partner Center-portalen.</span><span class="sxs-lookup"><span data-stu-id="07ea1-113">This is a Sandbox- only feature that allows Sandbox Indirect Providers the ability to create Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="07ea1-114">Följande scenarier är vad indirekta leverantörer kan göra för indirekta återförsäljare i sandbox-miljön via Partner Center-användargränssnittet:</span><span class="sxs-lookup"><span data-stu-id="07ea1-114">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="07ea1-115">Indirekta CSP-leverantörer kan skapa ett CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.</span><span class="sxs-lookup"><span data-stu-id="07ea1-115">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="07ea1-116">CSP Indirect Resellers kan visa kunden av indirekta leverantörer.</span><span class="sxs-lookup"><span data-stu-id="07ea1-116">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="07ea1-117">CSP Indirect Resellers kan hantera kundkontot med hjälp av delegerade administratörsbehörigheter.</span><span class="sxs-lookup"><span data-stu-id="07ea1-117">CSP Indirect Resellers  can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="07ea1-118">CSP Indirect Providers kan bjuda in indirekta CSP-återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="07ea1-118">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="07ea1-119">Indirekta CSP-leverantörer kan ta bort CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.</span><span class="sxs-lookup"><span data-stu-id="07ea1-119">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="07ea1-120">a.</span><span class="sxs-lookup"><span data-stu-id="07ea1-120">a.</span></span>  <span data-ttu-id="07ea1-121">När den indirekta Sandbox-providern tar bort relationen med den indirekta Sandbox-återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="07ea1-121">When Sandbox Indirect Provider deletes relationship with Sandbox Indirect Reseller.</span></span>

    <span data-ttu-id="07ea1-122">b.</span><span class="sxs-lookup"><span data-stu-id="07ea1-122">b.</span></span>  <span data-ttu-id="07ea1-123">Kontrollera om den indirekta återförsäljaren har någon annan relation med andra leverantörer.</span><span class="sxs-lookup"><span data-stu-id="07ea1-123">Check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="07ea1-124">I så fall tas endast relationen med den specifika indirekta providern bort.</span><span class="sxs-lookup"><span data-stu-id="07ea1-124">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="07ea1-125">c.</span><span class="sxs-lookup"><span data-stu-id="07ea1-125">c.</span></span> <span data-ttu-id="07ea1-126">Om det är den enda relationen för IR tas IR bort.</span><span class="sxs-lookup"><span data-stu-id="07ea1-126">If that is the only relationship for the IR, then the IR will be deleted.</span></span>

1. <span data-ttu-id="07ea1-127">CSP Indirect Provider kan ta bort en CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="07ea1-127">CSP Indirect Provider can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="07ea1-128">a.</span><span class="sxs-lookup"><span data-stu-id="07ea1-128">a.</span></span> <span data-ttu-id="07ea1-129">Det här är en funktion för endast sandbox-miljö som gör att indirekta sandbox-leverantörer kan ta bort indirekta sandbox-återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="07ea1-129">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="07ea1-130">Förutsättningar för att ta bort en indirekt sandbox-återförsäljare:</span><span class="sxs-lookup"><span data-stu-id="07ea1-130">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="07ea1-131">Pausa prenumerationerna för varje kund för Sandbox Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="07ea1-131">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="07ea1-132">Ta bort alla indirekta återförsäljares kunder.</span><span class="sxs-lookup"><span data-stu-id="07ea1-132">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="07ea1-133">Gräns på 5 indirekta Återförsäljare av sandbox-miljö tillåts per indirekt sandbox-leverantör.</span><span class="sxs-lookup"><span data-stu-id="07ea1-133">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="07ea1-134">När Sandbox Indirect-återförsäljaren tas bort återställs kvoten.</span><span class="sxs-lookup"><span data-stu-id="07ea1-134">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="07ea1-135">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="07ea1-135">Pre-requisites</span></span>

- <span data-ttu-id="07ea1-136">Gräns på 5 indirekta Återförsäljare av sandbox-miljö tillåts per indirekt sandbox-leverantör.</span><span class="sxs-lookup"><span data-stu-id="07ea1-136">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="07ea1-137">Samma MPN-ID kan användas för att skapa flera sandbox-konton för indirekta återförsäljare om land för MPN-ID och sandbox-land för indirekt återförsäljare är samma.</span><span class="sxs-lookup"><span data-stu-id="07ea1-137">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="07ea1-138">Om du har ett tillgängligt MPN-test-ID kan du använda det eller hämta en lista över MPN-ID:n via vår [Yammer-kanal.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 )</span><span class="sxs-lookup"><span data-stu-id="07ea1-138">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="07ea1-139">Om du inte har åtkomst till Yammer ber Yammer dig att begära åtkomst.</span><span class="sxs-lookup"><span data-stu-id="07ea1-139">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="07ea1-140">Endast 75 kunder tillåts per indirekt sandbox-provider</span><span class="sxs-lookup"><span data-stu-id="07ea1-140">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="07ea1-141">Skapa CSP Indirect Reseller Sandbox-konto</span><span class="sxs-lookup"><span data-stu-id="07ea1-141">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="07ea1-142">Logga in på Partner Center via ditt sandbox-konto på nivå 2.</span><span class="sxs-lookup"><span data-stu-id="07ea1-142">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="07ea1-143">Gå till Indirekta återförsäljare på den vänstra menyn.</span><span class="sxs-lookup"><span data-stu-id="07ea1-143">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="07ea1-144">Klicka på knappen "Lägg till sandbox-miljö för återförsäljare".</span><span class="sxs-lookup"><span data-stu-id="07ea1-144">Click on “Add Reseller Sandbox” button.</span></span> 

4. <span data-ttu-id="07ea1-145">Fyll i formuläret för kontoregistrering.</span><span class="sxs-lookup"><span data-stu-id="07ea1-145">Fill the account enrollment form.</span></span> <span data-ttu-id="07ea1-146">Det är självförklarande, men kom ihåg att du skapar ett Sandbox-konto för en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="07ea1-146">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="07ea1-147">Det här kontot genomgår ingen granskning och aktiveras när du är klar med kontoregistreringen.</span><span class="sxs-lookup"><span data-stu-id="07ea1-147">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="07ea1-148">När kontot har skapats får du autentiseringsuppgifterna för global administratör för sandbox-kontot för indirekt återförsäljare på portalen.</span><span class="sxs-lookup"><span data-stu-id="07ea1-148">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="07ea1-149">Kom ihåg att spara den omedelbart, annars kan du inte logga in som sandbox-miljö för indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="07ea1-149">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="07ea1-150">Logga ut och logga in igen på Partner Center med de nya autentiseringsuppgifterna för sandbox-miljön för indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="07ea1-150">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="07ea1-151">Utforska de funktioner som du kan göra som en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="07ea1-151">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="07ea1-152">Några saker är:</span><span class="sxs-lookup"><span data-stu-id="07ea1-152">Some things are :</span></span>  

    - <span data-ttu-id="07ea1-153">Hantera profiler</span><span class="sxs-lookup"><span data-stu-id="07ea1-153">Manage profiles</span></span>  

    - <span data-ttu-id="07ea1-154">Hantera användare och roller</span><span class="sxs-lookup"><span data-stu-id="07ea1-154">Manage users and roles</span></span> 

    - <span data-ttu-id="07ea1-155">Hantera indirekta leverantörer</span><span class="sxs-lookup"><span data-stu-id="07ea1-155">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="07ea1-156">Hantera CSP Sandbox-kunder</span><span class="sxs-lookup"><span data-stu-id="07ea1-156">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="07ea1-157">Hantera relationer</span><span class="sxs-lookup"><span data-stu-id="07ea1-157">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="07ea1-158">Sandbox Indirect Provider – Ta bort indirekt Sandbox-återförsäljare med hjälp av Partner Center-användargränssnittet</span><span class="sxs-lookup"><span data-stu-id="07ea1-158">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="07ea1-159">Det här är en sandbox-funktion som endast gör att indirekta sandbox-leverantörer kan ta bort ett befintligt konto för indirekt sandbox-återförsäljare via Partner Center-portalen.</span><span class="sxs-lookup"><span data-stu-id="07ea1-159">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="07ea1-160">Krav för att ta bort indirekt sandbox-återförsäljare:</span><span class="sxs-lookup"><span data-stu-id="07ea1-160">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="07ea1-161">Ett befintligt CSP Indirect Reseller sandbox-konto som är associerat med ditt CSP Indirect Provider sandbox-konto på nivå 2.</span><span class="sxs-lookup"><span data-stu-id="07ea1-161">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="07ea1-162">Ta bort CSP Indirect Reseller Sandbox-konto</span><span class="sxs-lookup"><span data-stu-id="07ea1-162">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="07ea1-163">Logga in på Partner Center med ditt sandbox-konto på nivå 2.</span><span class="sxs-lookup"><span data-stu-id="07ea1-163">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="07ea1-164">Gå till Indirekta återförsäljare på den vänstra menyn.</span><span class="sxs-lookup"><span data-stu-id="07ea1-164">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="07ea1-165">Klicka på **länken Ta bort sandbox-miljö** för återförsäljare bredvid sandbox-kontot för indirekt återförsäljare som du vill ta bort.</span><span class="sxs-lookup"><span data-stu-id="07ea1-165">Click on **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="07ea1-166">Sandbox-kontot för indirekt återförsäljare tas bort permanent och kan inte återställas.</span><span class="sxs-lookup"><span data-stu-id="07ea1-166">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="07ea1-167">API-referenser</span><span class="sxs-lookup"><span data-stu-id="07ea1-167">API references</span></span>

- <span data-ttu-id="07ea1-168">Skapa indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="07ea1-168">Create Indirect Reseller</span></span> 
- <span data-ttu-id="07ea1-169">Ta bort indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="07ea1-169">Delete Indirect Reseller</span></span> 

 

 