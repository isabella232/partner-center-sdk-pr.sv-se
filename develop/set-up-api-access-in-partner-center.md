---
title: Konfigurera API-åtkomst i Partner Center
description: Konfigurera konton för utveckling mot Partnercenter-SDK och testa i sandbox-miljön för integrering.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2c564baa9b626ff6ce21f9bcc517902d7cf99244
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547435"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="b7eb1-103">Konfigurera API-åtkomst i Partner Center</span><span class="sxs-lookup"><span data-stu-id="b7eb1-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="b7eb1-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government | Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="b7eb1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="b7eb1-105">I den här artikeln beskrivs de konton som du behöver utveckla mot Partnercenter-SDK.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-105">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="b7eb1-106">Den här artikeln förklarar också hur du skapar ett [sandbox-konto för integrering och](#integration-sandbox-account) testar i sandbox-miljön för integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-106">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="b7eb1-107">För att få åtkomst till API:er måste din klient vara en CSP-klient och du måste vara antingen en indirekt leverantör eller en partner för direktfakturering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-107">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="b7eb1-108">Kontodefinitioner</span><span class="sxs-lookup"><span data-stu-id="b7eb1-108">Account definitions</span></span>

<span data-ttu-id="b7eb1-109">Partner Center har stöd för två typer av konton som hjälper dig att integrera och testa API-integreringen:</span><span class="sxs-lookup"><span data-stu-id="b7eb1-109">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="b7eb1-110">Primärt partnerkonto</span><span class="sxs-lookup"><span data-stu-id="b7eb1-110">Primary Partner account</span></span>

<span data-ttu-id="b7eb1-111">På det här kontot skapar du verkliga beställningar för verkliga kunder.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-111">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="b7eb1-112">Om du gör ändringar eller transaktioner när du är inloggad på det primära kontot, med hjälp av antingen Partnercenter-SDK eller partnerinstrumentpanelens användargränssnitt, behandlas de som officiella beställningar för verkliga kunder.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-112">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="b7eb1-113">De visas på din faktura och ditt företag ansvarar för att betala för dem.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-113">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="b7eb1-114">Sandbox-konto för integrering</span><span class="sxs-lookup"><span data-stu-id="b7eb1-114">Integration sandbox account</span></span>

<span data-ttu-id="b7eb1-115">Det här kontot används för att testa din kod och dess integrering med Partner Center-API:erna innan du distribuerar den brett.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-115">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="b7eb1-116">Ändringar och transaktioner som du gör när du är inloggad på sandbox-kontot för integrering visas på din faktura, men du behöver inte betala fakturabeloppet.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-116">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="b7eb1-117">Faktura-PDF har en ansvarsfriskrivning som "BETALA INTE.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-117">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="b7eb1-118">DET HÄR ÄR EN SANDBOX-FAKTURA OCH INGEN ÅTGÄRD KRÄVS."</span><span class="sxs-lookup"><span data-stu-id="b7eb1-118">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="b7eb1-119">Sandbox-kontot för integrering och det primära kontot fungerar oberoende och delar inte administratörskonton, användarkonton, kunder, beställningar, prenumerationer eller andra data.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-119">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="b7eb1-120">Sandbox-miljön för integrering stöder transaktioner med ett begränsat antal kunder, beställningar, prenumerationer, licenser osv.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-120">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="b7eb1-121">Enligt principen är integrations-sandbox-konton endast avsedda för integreringstestning.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-121">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="b7eb1-122">Det finns inget sandbox-konto för integrering som standard.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-122">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="b7eb1-123">Du måste skapa en själv om du planerar att använda Partnercenter-SDK.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-123">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="b7eb1-124">Konfigurera dina konton</span><span class="sxs-lookup"><span data-stu-id="b7eb1-124">Set up your accounts</span></span>

<span data-ttu-id="b7eb1-125">I det här avsnittet beskrivs hur du ställer in ett primärt partnerkonto och ett sandbox-konto för integrering för Partnercenter-SDK.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-125">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="b7eb1-126">Skapa en sandbox-miljö för integrering</span><span class="sxs-lookup"><span data-stu-id="b7eb1-126">Create an integration sandbox</span></span>

1. <span data-ttu-id="b7eb1-127">Logga in på partnerinstrumentpanelen med ett globalt administratörskonto (ditt primära partnerkonto.)</span><span class="sxs-lookup"><span data-stu-id="b7eb1-127">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="b7eb1-128">På **Inställningar** (kugghjulsikonen) väljer du **Partnerinställningar.**</span><span class="sxs-lookup"><span data-stu-id="b7eb1-128">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="b7eb1-129">Välj **fliken Sandbox-miljö för** integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-129">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b7eb1-130">Om du inte ser alternativet Sandbox-miljö för integrering kanske du inte har något globalt administratörskonto.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-130">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="b7eb1-131">Du kanske också använder ett sandbox-konto för integrering och en sandbox-miljö för integrering har redan ställts in.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-131">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="b7eb1-132">Ange kontaktinformationen för administratörskontot för sandbox-integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-132">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="b7eb1-133">Välj sedan **Skapa konto.**</span><span class="sxs-lookup"><span data-stu-id="b7eb1-133">Then, choose **Create account**.</span></span> <span data-ttu-id="b7eb1-134">Vänta några minuter på ett bekräftelsemeddelande om att kontot har skapats.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-134">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="b7eb1-135">När du ser bekräftelsemeddelandet loggar du ut från Partnerinstrumentpanel.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-135">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="b7eb1-136">Logga in igen med ditt nya administratörskonto för sandbox-integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-136">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="b7eb1-137">Se till att använda formatet för **username@domain** dina autentiseringsuppgifter tillsammans med det lösenord som du har angett.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-137">Be sure to use the format **username@domain** for your credentials along with the password that you specified.</span></span>

7. <span data-ttu-id="b7eb1-138">Välj **Konfigurera konto ovanför Aktuella** uppgifter för **att** slutföra konfigurationen av sandbox-kontot.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-138">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="b7eb1-139">Aktivera API-åtkomst</span><span class="sxs-lookup"><span data-stu-id="b7eb1-139">Enable API access</span></span>

<span data-ttu-id="b7eb1-140">När ditt konto har konfigurerats måste du aktivera API-åtkomst innan du kan använda SDK:t för Partnercenter med sandbox-kontot för integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-140">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="b7eb1-141">Du måste aktivera åtkomst till API:et separat för både ditt primära partnerkonto och sandbox-kontot för integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-141">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="b7eb1-142">Logga in på partnerinstrumentpanelen med ett globalt administratörskonto.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-142">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="b7eb1-143">På **Inställningar** (kugghjulsikonen) väljer du **Partnerinställningar.**</span><span class="sxs-lookup"><span data-stu-id="b7eb1-143">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="b7eb1-144">På sidan **Kontoinställningar** väljer du **Apphantering.**</span><span class="sxs-lookup"><span data-stu-id="b7eb1-144">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="b7eb1-145">Om du inte redan har en befintlig app lägger du till en ny webbapp.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-145">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="b7eb1-146">Om du har en befintlig webbapp väljer du knappen **Lägg till** nyckel.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-146">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="b7eb1-147">Kopiera appregistreringsinformationen, särskilt **nyckeln** om du skapar en webbapp och lagra den på en säker plats.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-147">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="b7eb1-148">Logga ut från partnerinstrumentpanelen.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-148">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="b7eb1-149">Logga in igen med ditt sandbox-konto för integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-149">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="b7eb1-150">Upprepa steg 2–5 för att aktivera API-åtkomst i sandbox-miljön för integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-150">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="b7eb1-151">Skriva och testa kod</span><span class="sxs-lookup"><span data-stu-id="b7eb1-151">Write and test code</span></span>

<span data-ttu-id="b7eb1-152">Du kan skriva kod och testa kod i sandbox-miljön för integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-152">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="b7eb1-153">Du behöver följande information för att konfigurera [Partner Center-autentisering](partner-center-authentication.md) med Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-153">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="b7eb1-154">Objektnamn</span><span class="sxs-lookup"><span data-stu-id="b7eb1-154">Item name</span></span> | <span data-ttu-id="b7eb1-155">Objektplats</span><span class="sxs-lookup"><span data-stu-id="b7eb1-155">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="b7eb1-156">App-ID/klient-ID</span><span class="sxs-lookup"><span data-stu-id="b7eb1-156">App ID / Client ID</span></span> | <span data-ttu-id="b7eb1-157">På **Inställningar** (kugghjulsikonen) väljer du **Partnerinställningar.**</span><span class="sxs-lookup"><span data-stu-id="b7eb1-157">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="b7eb1-158">På sidan **Kontoinställningar** väljer du **Apphantering.**</span><span class="sxs-lookup"><span data-stu-id="b7eb1-158">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="b7eb1-159">App-ID/klient-ID visas som **det registrerade app-ID:t.**</span><span class="sxs-lookup"><span data-stu-id="b7eb1-159">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="b7eb1-160">Nyckel</span><span class="sxs-lookup"><span data-stu-id="b7eb1-160">Key</span></span> | <span data-ttu-id="b7eb1-161">Om du skapade en webbapp i avsnittet [Aktivera API-åtkomst](#enable-api-access)är det här nyckeln som du sparade i steg 5.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-161">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="b7eb1-162">Domain</span><span class="sxs-lookup"><span data-stu-id="b7eb1-162">Domain</span></span> | <span data-ttu-id="b7eb1-163">Domänen för sandbox-miljön för integrering.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-163">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="b7eb1-164">Köra testad kod</span><span class="sxs-lookup"><span data-stu-id="b7eb1-164">Run tested code</span></span>

<span data-ttu-id="b7eb1-165">Om du vill använda din lösning med verkliga kunddata måste du ändra från dina autentiseringsuppgifter för sandbox-integrering till autentiseringsuppgifterna för ditt primära partnerkonto.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-165">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="b7eb1-166">När du är redo att använda din testade kod i ditt primära partnerkonto måste du hämta en Azure AD-säkerhetstoken.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-166">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="b7eb1-167">Den här säkerhetstoken baseras på din Partner Center-app, nyckel och domän (i stället för din integrerings-sandbox-app, nyckel och domän).</span><span class="sxs-lookup"><span data-stu-id="b7eb1-167">This security token is based on your Partner Center app, key, and domain (instead of your integration sandbox app, key, and domain).</span></span>

1. <span data-ttu-id="b7eb1-168">Följ stegen i Partner [Center-autentisering för att hämta](partner-center-authentication.md) en Azure AD-säkerhetstoken med dina primära Autentiseringsuppgifter för Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-168">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="b7eb1-169">(Du har tidigare följt de här stegen för att hämta en Azure AD-säkerhetstoken för din sandbox-miljö för integrering.)</span><span class="sxs-lookup"><span data-stu-id="b7eb1-169">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="b7eb1-170">Ersätt integrationssäkerhetstoken i koden med den nya säkerhetstoken för ditt primära partnerkonto.</span><span class="sxs-lookup"><span data-stu-id="b7eb1-170">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
