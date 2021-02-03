---
title: Konsoltestapp
description: 'Den här konsolens testapp innehåller exempel kod för alla scenarier som stöds av API: er för partner Center. Du kan också använda den för testning.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769180"
---
# <a name="console-test-app"></a><span data-ttu-id="91a31-104">Konsoltestapp</span><span class="sxs-lookup"><span data-stu-id="91a31-104">Console test app</span></span>

<span data-ttu-id="91a31-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="91a31-105">**Applies to:**</span></span>

- <span data-ttu-id="91a31-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="91a31-106">Partner Center</span></span>
- <span data-ttu-id="91a31-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="91a31-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="91a31-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="91a31-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="91a31-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="91a31-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="91a31-110">-Test-appen finns i C# och Java innehåller exempel koder för alla scenarier som stöds av API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="91a31-110">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="91a31-111">Du kan också använda den för testning.</span><span class="sxs-lookup"><span data-stu-id="91a31-111">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="91a31-112">Hämta koden</span><span class="sxs-lookup"><span data-stu-id="91a31-112">Get the code</span></span>

<span data-ttu-id="91a31-113">Hämta exempel koden för konsolens test app.</span><span class="sxs-lookup"><span data-stu-id="91a31-113">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="91a31-114">.NET</span><span class="sxs-lookup"><span data-stu-id="91a31-114">.NET</span></span>

<span data-ttu-id="91a31-115">[Hämta exempel koden](https://go.microsoft.com/fwlink/p/?LinkId=746682) och ändra den efter behov.</span><span class="sxs-lookup"><span data-stu-id="91a31-115">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91a31-116">Innan du skapar programmet uppdaterar du värdena i *App.config* -filen så att den återspeglar den Azure AD-autentiseringsinformation som du skapade i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="91a31-116">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="91a31-117">Mer specifikt bör du använda konto inställningarna för integration i begränsat läge vid tidig utveckling eller för testning i produktion.</span><span class="sxs-lookup"><span data-stu-id="91a31-117">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="91a31-118">Under **ScenarioSettings** i *App.config* -filen kan du ange parametrar som ska skickas automatiskt till de scenarier som du kör.</span><span class="sxs-lookup"><span data-stu-id="91a31-118">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="91a31-119">För att ändra listan över scenarier som körs, kommentera ut rader i **IPartnerScenario \[ \] mainScenarios** eller i en enskild metod för att **Hämta scenarier** i *program.cs* -filen.</span><span class="sxs-lookup"><span data-stu-id="91a31-119">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="91a31-120">Java</span><span class="sxs-lookup"><span data-stu-id="91a31-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="91a31-121">[Hämta exempel koden](https://go.microsoft.com/fwlink/p/?LinkId=2026887) och ändra den efter behov.</span><span class="sxs-lookup"><span data-stu-id="91a31-121">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91a31-122">Innan du skapar programmet uppdaterar du värdena i *SamplesConfigurations.jspå* filen för att avspegla den Azure AD-autentiseringsinformation som du skapade i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="91a31-122">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="91a31-123">Mer specifikt bör du använda konto inställningarna för integration i begränsat läge vid tidig utveckling eller för testning i produktion.</span><span class="sxs-lookup"><span data-stu-id="91a31-123">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="91a31-124">Under **ScenarioSettings** i *SamplesConfiguration.jspå* fil kan du ange parametrar som ska skickas automatiskt till de scenarier som du kör.</span><span class="sxs-lookup"><span data-stu-id="91a31-124">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="91a31-125">För att ändra listan över scenarier som körs, kommentera ut rader i **IPartnerScenario \[ \] mainScenarios** eller i en enskild metod för att **Hämta scenarier** i filen *program. java* .</span><span class="sxs-lookup"><span data-stu-id="91a31-125">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="91a31-126">Ändra</span><span class="sxs-lookup"><span data-stu-id="91a31-126">What to change</span></span>

<span data-ttu-id="91a31-127">Använd följande listor för att avgöra vad som ska ändras eller inte ändras i exempel koden.</span><span class="sxs-lookup"><span data-stu-id="91a31-127">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="91a31-128">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="91a31-128">PartnerServiceSettings</span></span>

<span data-ttu-id="91a31-129">Ändra inte för **PartnerServiceSettings**:</span><span class="sxs-lookup"><span data-stu-id="91a31-129">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="91a31-130">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="91a31-130">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="91a31-131">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="91a31-131">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="91a31-132">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="91a31-132">**GraphEndpoint**</span></span>
- <span data-ttu-id="91a31-133">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="91a31-133">**CommonDomain**</span></span>

<span data-ttu-id="91a31-134">Alla de här inställningarna krävs för att exempel-API-anropen ska fungera korrekt.</span><span class="sxs-lookup"><span data-stu-id="91a31-134">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="91a31-135">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="91a31-135">UserAuthentication</span></span>

<span data-ttu-id="91a31-136">För **UserAuthentication** är du tvungen att ändra:</span><span class="sxs-lookup"><span data-stu-id="91a31-136">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="91a31-137">**ApplicationId** (ditt Azure Active Directory program-ID används för inloggning)</span><span class="sxs-lookup"><span data-stu-id="91a31-137">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="91a31-138">**Användar namn** (ditt Active Directory-användarnamn)</span><span class="sxs-lookup"><span data-stu-id="91a31-138">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="91a31-139">**Lösen ord** (ditt Active Directory-lösenord).</span><span class="sxs-lookup"><span data-stu-id="91a31-139">**Password** (your active directory password).</span></span>

<span data-ttu-id="91a31-140">Ändra inte:</span><span class="sxs-lookup"><span data-stu-id="91a31-140">Don't change:</span></span>

- <span data-ttu-id="91a31-141">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="91a31-141">**ResourceUrl**</span></span>
- <span data-ttu-id="91a31-142">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="91a31-142">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="91a31-143">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="91a31-143">AppAuthentication</span></span>

<span data-ttu-id="91a31-144">För **AppAuthentication** är du tvungen att ändra:</span><span class="sxs-lookup"><span data-stu-id="91a31-144">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="91a31-145">**ApplicationId** (ditt Active Directory-program-ID som används för program inloggning)</span><span class="sxs-lookup"><span data-stu-id="91a31-145">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="91a31-146">**ApplicationSecret** (din Active Directory-programhemlighet som används för program inloggning)</span><span class="sxs-lookup"><span data-stu-id="91a31-146">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="91a31-147">**Domän** (din Active Directory-domän som programmet finns på)</span><span class="sxs-lookup"><span data-stu-id="91a31-147">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="91a31-148">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="91a31-148">ScenarioSettings</span></span>

<span data-ttu-id="91a31-149">Ändra inte för **ScenarioSettings**:</span><span class="sxs-lookup"><span data-stu-id="91a31-149">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="91a31-150">**CustomerDomainSuffix** (domänsuffix som används för att skapa en ny kund)</span><span class="sxs-lookup"><span data-stu-id="91a31-150">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="91a31-151">Valfria inställningar.</span><span class="sxs-lookup"><span data-stu-id="91a31-151">Optional settings.</span></span> <span data-ttu-id="91a31-152">Om detta lämnas tomt måste den här informationen anges när du kör ett scenario där det behövs):</span><span class="sxs-lookup"><span data-stu-id="91a31-152">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="91a31-153">**CustomerIdToDelete** (ID för den kund som används för borttagning)</span><span class="sxs-lookup"><span data-stu-id="91a31-153">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="91a31-154">**DefaultCustomerId** (kund-ID: t som ska användas i kundrelaterade scenarier)</span><span class="sxs-lookup"><span data-stu-id="91a31-154">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="91a31-155">**DefaultInvoiceID** (faktura-ID som ska användas i faktura scenarier)</span><span class="sxs-lookup"><span data-stu-id="91a31-155">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="91a31-156">**PartnerMpnId** (partner MPN-ID som ska användas i indirekta partner scenarier)</span><span class="sxs-lookup"><span data-stu-id="91a31-156">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="91a31-157">**DefaultServiceRequestId** (ID för tjänst förfrågan som ska användas i scenarier med tjänstbegäran)</span><span class="sxs-lookup"><span data-stu-id="91a31-157">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="91a31-158">**DefaultSupportTopicID** (ID för support avsnittet som ska användas i tjänst begär ande scenarier)</span><span class="sxs-lookup"><span data-stu-id="91a31-158">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="91a31-159">**DefaultOfferID** (erbjudande-ID som ska användas i erbjudande scenarier)</span><span class="sxs-lookup"><span data-stu-id="91a31-159">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="91a31-160">**DefaultOrderID** (order-ID som ska användas i ordnings scenarier)</span><span class="sxs-lookup"><span data-stu-id="91a31-160">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="91a31-161">**DefaultSubscriptionID** (PRENUMERATIONS-ID som ska användas i prenumerations scenarier)</span><span class="sxs-lookup"><span data-stu-id="91a31-161">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="91a31-162">Valfritt att ändra.</span><span class="sxs-lookup"><span data-stu-id="91a31-162">Optional to change.</span></span> <span data-ttu-id="91a31-163">Alla de här inställningarna anger mängden poster per sida vid hämtning av växlat innehåll:</span><span class="sxs-lookup"><span data-stu-id="91a31-163">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="91a31-164">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="91a31-164">**CustomerPageSize**</span></span>
- <span data-ttu-id="91a31-165">**InvoicePageSize**</span><span class="sxs-lookup"><span data-stu-id="91a31-165">**InvoicePageSize**</span></span>
- <span data-ttu-id="91a31-166">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="91a31-166">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="91a31-167">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="91a31-167">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="91a31-168">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="91a31-168">**SubscriptionPageSize**</span></span>
