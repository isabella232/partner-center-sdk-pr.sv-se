---
title: Konfigurera API-åtkomst i Partner Center
description: Konfigurera konton för utveckling mot Partner Center SDK och test i sandbox-integration.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/28/2020
ms.locfileid: "97769417"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="61ad1-103">Konfigurera API-åtkomst i Partner Center</span><span class="sxs-lookup"><span data-stu-id="61ad1-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="61ad1-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="61ad1-104">**Applies to:**</span></span>

- <span data-ttu-id="61ad1-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="61ad1-105">Partner Center</span></span>
- <span data-ttu-id="61ad1-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="61ad1-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="61ad1-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="61ad1-107">Partner Center for Microsoft Cloud for US Government</span></span>
- <span data-ttu-id="61ad1-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="61ad1-108">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="61ad1-109">I den här artikeln beskrivs de konton som du måste utveckla mot Partner Center SDK.</span><span class="sxs-lookup"><span data-stu-id="61ad1-109">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="61ad1-110">Den här artikeln beskriver också hur du skapar ett [sandbox-konto](#integration-sandbox-account) och testar det i integration sandbox.</span><span class="sxs-lookup"><span data-stu-id="61ad1-110">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="61ad1-111">För att få åtkomst till API: er måste klienten vara en CSP-klient och du måste vara antingen en indirekt provider eller en direkt fakturerings partner.</span><span class="sxs-lookup"><span data-stu-id="61ad1-111">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="61ad1-112">Konto definitioner</span><span class="sxs-lookup"><span data-stu-id="61ad1-112">Account definitions</span></span>

<span data-ttu-id="61ad1-113">För att hjälpa dig att integrera och testa API-integrering stöder Partner Center två typer av konton:</span><span class="sxs-lookup"><span data-stu-id="61ad1-113">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="61ad1-114">Primärt partner konto</span><span class="sxs-lookup"><span data-stu-id="61ad1-114">Primary Partner account</span></span>

<span data-ttu-id="61ad1-115">I det här kontot kan du skapa verkliga beställningar för riktiga kunder.</span><span class="sxs-lookup"><span data-stu-id="61ad1-115">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="61ad1-116">Om du gör ändringar eller transaktioner när du är inloggad på det primära kontot, med hjälp av antingen Partner Center SDK eller partnerns användar gränssnitt, kommer de att behandlas som officiella beställningar för riktiga kunder.</span><span class="sxs-lookup"><span data-stu-id="61ad1-116">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="61ad1-117">De kommer att avspeglas i fakturan och företaget ansvarar för att betala för dem.</span><span class="sxs-lookup"><span data-stu-id="61ad1-117">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="61ad1-118">Sandbox-konto för integrering</span><span class="sxs-lookup"><span data-stu-id="61ad1-118">Integration sandbox account</span></span>

<span data-ttu-id="61ad1-119">Det här kontot används för att testa din kod och dess integrering med API: er för partner Center innan du distribuerar den i stor ordning.</span><span class="sxs-lookup"><span data-stu-id="61ad1-119">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="61ad1-120">Ändringar och transaktioner som du gör när du är inloggad på det begränsade kontot för integration visas i fakturan, men du behöver inte betala faktura beloppet.</span><span class="sxs-lookup"><span data-stu-id="61ad1-120">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="61ad1-121">Faktura-PDF får en fri skrivning som "betala inte.</span><span class="sxs-lookup"><span data-stu-id="61ad1-121">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="61ad1-122">DETTA ÄR EN SANDBOX-FAKTURA OCH INGEN ÅTGÄRD KRÄVS. "</span><span class="sxs-lookup"><span data-stu-id="61ad1-122">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="61ad1-123">Det begränsade kontot för integration och det primära kontot fungerar oberoende av varandra och delar inte administratörs konton, användar konton, kunder, beställningar, prenumerationer eller annan information.</span><span class="sxs-lookup"><span data-stu-id="61ad1-123">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="61ad1-124">-Integrations sand boxen stöder transaktioner med ett begränsat antal kunder, order, prenumerationer, licenser osv.</span><span class="sxs-lookup"><span data-stu-id="61ad1-124">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="61ad1-125">Som princip är integrations sand Box-konton endast avsedda för integrations testning.</span><span class="sxs-lookup"><span data-stu-id="61ad1-125">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="61ad1-126">Det finns inget sandbox-konto för integrering som standard.</span><span class="sxs-lookup"><span data-stu-id="61ad1-126">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="61ad1-127">Du måste skapa en själv om du planerar att använda Partner Center SDK.</span><span class="sxs-lookup"><span data-stu-id="61ad1-127">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="61ad1-128">Konfigurera dina konton</span><span class="sxs-lookup"><span data-stu-id="61ad1-128">Set up your accounts</span></span>

<span data-ttu-id="61ad1-129">I det här avsnittet beskrivs hur du konfigurerar ett primärt partner konto och ett konto för integration i begränsat läge för partner Center SDK.</span><span class="sxs-lookup"><span data-stu-id="61ad1-129">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="61ad1-130">Skapa en integrations Sand låda</span><span class="sxs-lookup"><span data-stu-id="61ad1-130">Create an integration sandbox</span></span>

1. <span data-ttu-id="61ad1-131">Logga in på partner instrument panel med ett globalt administratörs konto (ditt primära partner konto).</span><span class="sxs-lookup"><span data-stu-id="61ad1-131">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="61ad1-132">Från menyn **Inställningar** (kugg hjuls ikon) väljer du **partner inställningar**.</span><span class="sxs-lookup"><span data-stu-id="61ad1-132">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="61ad1-133">Välj fliken **integrations-sandbox** .</span><span class="sxs-lookup"><span data-stu-id="61ad1-133">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="61ad1-134">Om du inte ser något alternativ för integrations-sandbox kanske du inte har ett globalt administratörs konto.</span><span class="sxs-lookup"><span data-stu-id="61ad1-134">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="61ad1-135">Du kanske också använder ett sandbox-konto för integration och det har redan kon figurer ATS en integrations Sand låda.</span><span class="sxs-lookup"><span data-stu-id="61ad1-135">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="61ad1-136">Ange kontakt information för administratörs kontot för integration sandbox.</span><span class="sxs-lookup"><span data-stu-id="61ad1-136">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="61ad1-137">Välj sedan **Skapa konto**.</span><span class="sxs-lookup"><span data-stu-id="61ad1-137">Then, choose **Create account**.</span></span> <span data-ttu-id="61ad1-138">Vänta några minuter för ett bekräftelse meddelande om att kontot har skapats.</span><span class="sxs-lookup"><span data-stu-id="61ad1-138">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="61ad1-139">När du ser bekräftelse meddelandet loggar du ut från partner instrument panelen.</span><span class="sxs-lookup"><span data-stu-id="61ad1-139">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="61ad1-140">Logga in igen med ditt nya administratörs konto för integration sandbox.</span><span class="sxs-lookup"><span data-stu-id="61ad1-140">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="61ad1-141">Se till att använda formatet **username@domain** för dina autentiseringsuppgifter tillsammans med det lösen ord som du nyss angav.</span><span class="sxs-lookup"><span data-stu-id="61ad1-141">Be sure to use the format **username@domain** for your credentials along with the password that you just specified.</span></span>

7. <span data-ttu-id="61ad1-142">Välj **Konfigurera ett konto** ovanför de **aktuella aktiviteterna** för att slutföra konfigurationen av Sandbox-kontot.</span><span class="sxs-lookup"><span data-stu-id="61ad1-142">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="61ad1-143">Aktivera API-åtkomst</span><span class="sxs-lookup"><span data-stu-id="61ad1-143">Enable API access</span></span>

<span data-ttu-id="61ad1-144">När ditt konto har konfigurerats måste du aktivera API-åtkomst innan du kan använda SDK:t för Partnercenter med sandbox-kontot för integrering.</span><span class="sxs-lookup"><span data-stu-id="61ad1-144">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="61ad1-145">Du måste aktivera åtkomst till API:et separat för både ditt primära partnerkonto och sandbox-kontot för integrering.</span><span class="sxs-lookup"><span data-stu-id="61ad1-145">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="61ad1-146">Logga in på partner instrument panel med ett globalt administratörs konto.</span><span class="sxs-lookup"><span data-stu-id="61ad1-146">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="61ad1-147">Från menyn **Inställningar** (kugg hjuls ikon) väljer du **partner inställningar**.</span><span class="sxs-lookup"><span data-stu-id="61ad1-147">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="61ad1-148">På sidan **konto inställningar** väljer du **program hantering**.</span><span class="sxs-lookup"><span data-stu-id="61ad1-148">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="61ad1-149">Om du inte redan har en befintlig app lägger du till en ny webbapp.</span><span class="sxs-lookup"><span data-stu-id="61ad1-149">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="61ad1-150">Om du har en befintlig webbapp väljer du knappen **Lägg till nyckel** .</span><span class="sxs-lookup"><span data-stu-id="61ad1-150">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="61ad1-151">Kopiera appens registrerings information, särskilt **nyckeln** om du skapar en webbapp, och lagra den på en säker plats.</span><span class="sxs-lookup"><span data-stu-id="61ad1-151">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="61ad1-152">Logga ut från partner instrument panel.</span><span class="sxs-lookup"><span data-stu-id="61ad1-152">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="61ad1-153">Logga in igen med ditt konto för integration sandbox.</span><span class="sxs-lookup"><span data-stu-id="61ad1-153">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="61ad1-154">Upprepa steg 2-5 för att aktivera API-åtkomst i sandbox-integration.</span><span class="sxs-lookup"><span data-stu-id="61ad1-154">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="61ad1-155">Skriv och testa kod</span><span class="sxs-lookup"><span data-stu-id="61ad1-155">Write and test code</span></span>

<span data-ttu-id="61ad1-156">Du kan skriva kod och testa kod i sandbox-integration.</span><span class="sxs-lookup"><span data-stu-id="61ad1-156">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="61ad1-157">Du behöver följande information för att [Konfigurera Partner Center-autentisering](partner-center-authentication.md) med Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61ad1-157">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="61ad1-158">Objekt namn</span><span class="sxs-lookup"><span data-stu-id="61ad1-158">Item name</span></span> | <span data-ttu-id="61ad1-159">Objekt plats</span><span class="sxs-lookup"><span data-stu-id="61ad1-159">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="61ad1-160">App-ID/klient-ID</span><span class="sxs-lookup"><span data-stu-id="61ad1-160">App ID / Client ID</span></span> | <span data-ttu-id="61ad1-161">Från menyn **Inställningar** (kugg hjuls ikon) väljer du **partner inställningar**.</span><span class="sxs-lookup"><span data-stu-id="61ad1-161">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="61ad1-162">På sidan **konto inställningar** väljer du **app Management**.</span><span class="sxs-lookup"><span data-stu-id="61ad1-162">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="61ad1-163">App-ID/klient-ID visas som det **registrerade programmets app-ID**.</span><span class="sxs-lookup"><span data-stu-id="61ad1-163">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="61ad1-164">Nyckel</span><span class="sxs-lookup"><span data-stu-id="61ad1-164">Key</span></span> | <span data-ttu-id="61ad1-165">Om du har skapat en webbapp i avsnittet [Aktivera API-åtkomst](#enable-api-access), är detta den nyckel som du sparade i steg 5.</span><span class="sxs-lookup"><span data-stu-id="61ad1-165">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="61ad1-166">Domain</span><span class="sxs-lookup"><span data-stu-id="61ad1-166">Domain</span></span> | <span data-ttu-id="61ad1-167">Domänen för integrations sand boxen.</span><span class="sxs-lookup"><span data-stu-id="61ad1-167">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="61ad1-168">Kör testad kod</span><span class="sxs-lookup"><span data-stu-id="61ad1-168">Run tested code</span></span>

<span data-ttu-id="61ad1-169">Om du vill använda din lösning med verkliga kund data måste du ändra från dina autentiseringsuppgifter för integrations-sandbox till dina primära partner konto uppgifter.</span><span class="sxs-lookup"><span data-stu-id="61ad1-169">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="61ad1-170">När du är redo att använda den testade koden i ditt primära partner konto måste du skaffa en Azure AD-säkerhetstoken.</span><span class="sxs-lookup"><span data-stu-id="61ad1-170">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="61ad1-171">Den här säkerhetstoken är baserad på din partner Center-app, nyckel och domän (i stället för din integrations-sandbox-app, nyckel och domän).</span><span class="sxs-lookup"><span data-stu-id="61ad1-171">This security token is based on your Partner Center app, key and domain (instead of your integration sandbox app, key and domain).</span></span>

1. <span data-ttu-id="61ad1-172">Följ stegen i [partner Center-autentisering](partner-center-authentication.md) för att hämta en Azure AD-säkerhetstoken med dina autentiseringsuppgifter för ditt primära partner Center.</span><span class="sxs-lookup"><span data-stu-id="61ad1-172">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="61ad1-173">(Du har tidigare följt dessa steg för att hämta en Azure AD-säkerhetstoken för din integration sandbox.)</span><span class="sxs-lookup"><span data-stu-id="61ad1-173">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="61ad1-174">Ersätt säkerhetstoken för integrering i koden med den nya säkerhetstoken för ditt primära partner konto.</span><span class="sxs-lookup"><span data-stu-id="61ad1-174">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
