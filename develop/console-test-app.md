---
title: Konsoltestapp
description: Den här konsoltestappen innehåller exempelkod för alla scenarier som stöds av Partner Center-API:erna. Du kan också använda den för testning.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974037"
---
# <a name="console-test-app"></a><span data-ttu-id="44203-104">Konsoltestapp</span><span class="sxs-lookup"><span data-stu-id="44203-104">Console test app</span></span>

<span data-ttu-id="44203-105">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44203-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="44203-106">Konsoltestappen finns i C# och Java. Den innehåller exempelkoder för alla scenarier som stöds av Partner Center-API:erna.</span><span class="sxs-lookup"><span data-stu-id="44203-106">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="44203-107">Du kan också använda den för testning.</span><span class="sxs-lookup"><span data-stu-id="44203-107">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="44203-108">Hämta koden</span><span class="sxs-lookup"><span data-stu-id="44203-108">Get the code</span></span>

<span data-ttu-id="44203-109">Ladda ned exempelkoden för konsoltestappen.</span><span class="sxs-lookup"><span data-stu-id="44203-109">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="44203-110">.NET</span><span class="sxs-lookup"><span data-stu-id="44203-110">.NET</span></span>

<span data-ttu-id="44203-111">[Ladda ned exempelkoden](https://go.microsoft.com/fwlink/p/?LinkId=746682) och ändra den efter behov.</span><span class="sxs-lookup"><span data-stu-id="44203-111">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44203-112">Innan du skapar programmet uppdaterar du värdena i filen *App.config* för att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="44203-112">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44203-113">Mer specifikt bör du använda inställningarna för sandbox-integrationskontot under tidig utveckling eller för testning i produktion.</span><span class="sxs-lookup"><span data-stu-id="44203-113">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="44203-114">Under **ScenarioInställningar** i *App.config* kan du ange parametrar som skickas automatiskt till de scenarier som du kör.</span><span class="sxs-lookup"><span data-stu-id="44203-114">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="44203-115">Om du vill ändra listan över scenarier som körs kommenterar du ut rader **i IPartnerScenario \[ \] mainScenarios** eller i en enskild **metod** för att hämta scenarier som finns *i filen Program.cs.*</span><span class="sxs-lookup"><span data-stu-id="44203-115">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="44203-116">Java</span><span class="sxs-lookup"><span data-stu-id="44203-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="44203-117">[Ladda ned exempelkoden](https://go.microsoft.com/fwlink/p/?LinkId=2026887) och ändra den efter behov.</span><span class="sxs-lookup"><span data-stu-id="44203-117">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44203-118">Innan du skapar programmet uppdaterar du värdena i filen *SamplesConfigurations.jsför* att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering .](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="44203-118">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44203-119">Mer specifikt bör du använda inställningarna för sandbox-integrationskontot under tidig utveckling eller för testning i produktion.</span><span class="sxs-lookup"><span data-stu-id="44203-119">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="44203-120">Under **ScenarioInställningar i** SamplesConfiguration.js *på* filen kan du ange parametrar som skickas automatiskt till de scenarier som du kör.</span><span class="sxs-lookup"><span data-stu-id="44203-120">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="44203-121">Om du vill ändra listan över scenarier som körs kommenterar du ut rader **i IPartnerScenario \[ \] mainScenarios** eller i en enskild **metod** för att hämta scenarier som finns i *filen Program.java.*</span><span class="sxs-lookup"><span data-stu-id="44203-121">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="44203-122">Vad som ska ändras</span><span class="sxs-lookup"><span data-stu-id="44203-122">What to change</span></span>

<span data-ttu-id="44203-123">Använd följande listor för att avgöra vad som ska ändras eller inte ändras i exempelkoden.</span><span class="sxs-lookup"><span data-stu-id="44203-123">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="44203-124">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="44203-124">PartnerServiceSettings</span></span>

<span data-ttu-id="44203-125">För **PartnerServiceSettings** ändrar du inte:</span><span class="sxs-lookup"><span data-stu-id="44203-125">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="44203-126">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="44203-126">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="44203-127">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="44203-127">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="44203-128">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="44203-128">**GraphEndpoint**</span></span>
- <span data-ttu-id="44203-129">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="44203-129">**CommonDomain**</span></span>

<span data-ttu-id="44203-130">Alla dessa inställningar är nödvändiga för att exempel-API-anropen ska fungera korrekt.</span><span class="sxs-lookup"><span data-stu-id="44203-130">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="44203-131">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="44203-131">UserAuthentication</span></span>

<span data-ttu-id="44203-132">För **UserAuthentication** måste du ändra:</span><span class="sxs-lookup"><span data-stu-id="44203-132">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="44203-133">**ApplicationId** (ditt Azure Active Directory-ID som används för inloggning)</span><span class="sxs-lookup"><span data-stu-id="44203-133">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="44203-134">**UserName** (ditt active directory-användarnamn)</span><span class="sxs-lookup"><span data-stu-id="44203-134">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="44203-135">**Lösenord** (ditt Active Directory-lösenord).</span><span class="sxs-lookup"><span data-stu-id="44203-135">**Password** (your active directory password).</span></span>

<span data-ttu-id="44203-136">Ändra inte:</span><span class="sxs-lookup"><span data-stu-id="44203-136">Don't change:</span></span>

- <span data-ttu-id="44203-137">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="44203-137">**ResourceUrl**</span></span>
- <span data-ttu-id="44203-138">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="44203-138">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="44203-139">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="44203-139">AppAuthentication</span></span>

<span data-ttu-id="44203-140">För **AppAuthentication** måste du ändra:</span><span class="sxs-lookup"><span data-stu-id="44203-140">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="44203-141">**ApplicationId** (ditt Active Directory-program-ID som används för programinloggning)</span><span class="sxs-lookup"><span data-stu-id="44203-141">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="44203-142">**ApplicationSecret** (din Active Directory-programhemlighet som används för programinloggning)</span><span class="sxs-lookup"><span data-stu-id="44203-142">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="44203-143">**Domän** (active directory-domänen där programmet finns)</span><span class="sxs-lookup"><span data-stu-id="44203-143">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="44203-144">ScenarioInställningar</span><span class="sxs-lookup"><span data-stu-id="44203-144">ScenarioSettings</span></span>

<span data-ttu-id="44203-145">För **ScenarioSettings** ändrar du inte:</span><span class="sxs-lookup"><span data-stu-id="44203-145">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="44203-146">**CustomerDomainSuffix** (domänsuffixet som används när du skapar en ny kund)</span><span class="sxs-lookup"><span data-stu-id="44203-146">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="44203-147">Valfria inställningar.</span><span class="sxs-lookup"><span data-stu-id="44203-147">Optional settings.</span></span> <span data-ttu-id="44203-148">Om den lämnas tom måste den här informationen matas in när du kör ett scenario där det behövs):</span><span class="sxs-lookup"><span data-stu-id="44203-148">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="44203-149">**CustomerIdToDelete** (ID:t för kunden som användes för borttagning)</span><span class="sxs-lookup"><span data-stu-id="44203-149">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="44203-150">**DefaultCustomerId** (det kund-ID som ska användas i kundrelaterade scenarier)</span><span class="sxs-lookup"><span data-stu-id="44203-150">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="44203-151">**DefaultInvoiceID (det** faktura-ID som ska användas i fakturascenarier)</span><span class="sxs-lookup"><span data-stu-id="44203-151">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="44203-152">**PartnerMpnId** (partnerns MPN-ID som ska användas i indirekta partnerscenarier)</span><span class="sxs-lookup"><span data-stu-id="44203-152">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="44203-153">**DefaultServiceRequestId (det** tjänstbegärande-ID som ska användas i scenarier med tjänstbegäran)</span><span class="sxs-lookup"><span data-stu-id="44203-153">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="44203-154">**DefaultSupportTopicID** (supportämnes-ID som ska användas i scenarier med tjänstbegäran)</span><span class="sxs-lookup"><span data-stu-id="44203-154">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="44203-155">**DefaultOfferID (det** erbjudande-ID som ska användas i erbjudandescenarier)</span><span class="sxs-lookup"><span data-stu-id="44203-155">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="44203-156">**DefaultOrderID** (order-ID:t som ska användas i ordningsscenarier)</span><span class="sxs-lookup"><span data-stu-id="44203-156">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="44203-157">**DefaultSubscriptionID** (prenumerations-ID:t som ska användas i prenumerationsscenarier)</span><span class="sxs-lookup"><span data-stu-id="44203-157">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="44203-158">Valfritt att ändra.</span><span class="sxs-lookup"><span data-stu-id="44203-158">Optional to change.</span></span> <span data-ttu-id="44203-159">Alla dessa inställningar anger hur många poster per sida som ska hämtas vid hämtning av sidindelade innehåll:</span><span class="sxs-lookup"><span data-stu-id="44203-159">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="44203-160">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="44203-160">**CustomerPageSize**</span></span>
- <span data-ttu-id="44203-161">**InvoicePageSize**</span><span class="sxs-lookup"><span data-stu-id="44203-161">**InvoicePageSize**</span></span>
- <span data-ttu-id="44203-162">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="44203-162">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="44203-163">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="44203-163">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="44203-164">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="44203-164">**SubscriptionPageSize**</span></span>
