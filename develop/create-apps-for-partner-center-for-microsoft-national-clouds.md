---
title: Registrera information om appar för partner Center för Microsoft National Cloud
description: Lär dig hur och varför Apps-utvecklare för partner Center för Microsoft National Cloud måste registrera information om sin app med Azure AD via Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770145"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="584bb-103">Registrera information om appar för partner Center för Microsoft National Cloud via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="584bb-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="584bb-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="584bb-104">**Applies to:**</span></span>

- <span data-ttu-id="584bb-105">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="584bb-105">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="584bb-106">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="584bb-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="584bb-107">Utvecklare måste registrera information om sin app med Azure AD via Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="584bb-107">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="584bb-108">Detta säkerställer att endast angivna appar kan ansluta till partner-och kund information.</span><span class="sxs-lookup"><span data-stu-id="584bb-108">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="584bb-109">För partner Center för Microsoft Cloud för amerikanska myndigheter måste du för närvarande hantera appar via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="584bb-109">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="584bb-110">Mer information finns i [referens dokumentationen för Azure PowerShell](/powershell/module/Azuread/#applications).</span><span class="sxs-lookup"><span data-stu-id="584bb-110">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="584bb-111">Tänk på följande ytterligare krav när du skapar en app för partner Center för Microsoft Cloud Tyskland eller partner Center för Microsoft Cloud för amerikanska myndigheter.</span><span class="sxs-lookup"><span data-stu-id="584bb-111">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="584bb-112">Webbappar</span><span class="sxs-lookup"><span data-stu-id="584bb-112">Web apps</span></span>

<span data-ttu-id="584bb-113">För webbappar använder du följande procedurer för att registrera ditt program-ID.</span><span class="sxs-lookup"><span data-stu-id="584bb-113">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="584bb-114">Skapa eller uppdatera en webbapp</span><span class="sxs-lookup"><span data-stu-id="584bb-114">Create or update web app</span></span>

1. <span data-ttu-id="584bb-115">Gå till sidan [Azure Portal-Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app.</span><span class="sxs-lookup"><span data-stu-id="584bb-115">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="584bb-116">Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.</span><span class="sxs-lookup"><span data-stu-id="584bb-116">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="584bb-117">Välj **ny registrering**.</span><span class="sxs-lookup"><span data-stu-id="584bb-117">Select **New registration**.</span></span> <span data-ttu-id="584bb-118">Mer information finns i [snabb start: registrera ett program med Microsoft Identity Platform](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="584bb-118">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="584bb-119">Konfigurera API-åtkomst behörigheter för webb program</span><span class="sxs-lookup"><span data-stu-id="584bb-119">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="584bb-120">Välj din app.</span><span class="sxs-lookup"><span data-stu-id="584bb-120">Choose your app.</span></span> <span data-ttu-id="584bb-121">Gå till **Inställningar** för webbappen.</span><span class="sxs-lookup"><span data-stu-id="584bb-121">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="584bb-122">I avsnittet **API-åtkomst** väljer du **nödvändiga behörigheter**</span><span class="sxs-lookup"><span data-stu-id="584bb-122">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="584bb-123">För Windows Azure Active Directory-behörigheter:</span><span class="sxs-lookup"><span data-stu-id="584bb-123">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="584bb-124">Välj **Windows Azure Active Directory-behörigheter**.</span><span class="sxs-lookup"><span data-stu-id="584bb-124">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="584bb-125">I **program behörigheter** väljer du läsa katalog data.</span><span class="sxs-lookup"><span data-stu-id="584bb-125">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="584bb-126">Spara behörigheterna.</span><span class="sxs-lookup"><span data-stu-id="584bb-126">Save the permissions.</span></span>

4. <span data-ttu-id="584bb-127">Notera program-ID i avsnittet **Egenskaper** i din webbapp.</span><span class="sxs-lookup"><span data-stu-id="584bb-127">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="584bb-128">Lägg till en hemlig nyckel i appen</span><span class="sxs-lookup"><span data-stu-id="584bb-128">Add a secret key to your app</span></span>

1. <span data-ttu-id="584bb-129">Gå till avsnittet **nycklar** i din webbapp.</span><span class="sxs-lookup"><span data-stu-id="584bb-129">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="584bb-130">Ange nyckel beskrivning och välj varaktighet som 1 eller 2 år efter behov.</span><span class="sxs-lookup"><span data-stu-id="584bb-130">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="584bb-131">Spara och kopiera värdet för den hemliga nyckeln.</span><span class="sxs-lookup"><span data-stu-id="584bb-131">Save and copy the secret key value.</span></span> <span data-ttu-id="584bb-132">**Det här värdet visas inte igen när du lämnar den här sidan.**</span><span class="sxs-lookup"><span data-stu-id="584bb-132">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="584bb-133">Du bör ha följande information från Web App-konfigurationen:</span><span class="sxs-lookup"><span data-stu-id="584bb-133">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="584bb-134">Program-ID</span><span class="sxs-lookup"><span data-stu-id="584bb-134">Application ID</span></span>
- <span data-ttu-id="584bb-135">Apphemlighet</span><span class="sxs-lookup"><span data-stu-id="584bb-135">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="584bb-136">Registrera webb programmet i Partner Center</span><span class="sxs-lookup"><span data-stu-id="584bb-136">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="584bb-137">Logga in på [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="584bb-137">Log in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="584bb-138">Välj **instrument panel**, välj sedan **konto inställningar** och sedan **app Management**.</span><span class="sxs-lookup"><span data-stu-id="584bb-138">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="584bb-139">I avsnittet **webbapp** väljer du **Registrera befintlig app**.</span><span class="sxs-lookup"><span data-stu-id="584bb-139">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="584bb-140">Välj den webbapp som du skapade i Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="584bb-140">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="584bb-141">Välj **Registrera din app**.</span><span class="sxs-lookup"><span data-stu-id="584bb-141">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="584bb-142">Inbyggda appar</span><span class="sxs-lookup"><span data-stu-id="584bb-142">Native apps</span></span>

<span data-ttu-id="584bb-143">Inbyggda appar behöver inte registreras på Partner Center.</span><span class="sxs-lookup"><span data-stu-id="584bb-143">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="584bb-144">Men de här apparna måste konfigureras för att ge åtkomst till API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="584bb-144">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="584bb-145">Innan du skapar en intern app i Azure Portal loggar du in på Partner Center med administratörs användarens autentiseringsuppgifter från partner klient organisationen.</span><span class="sxs-lookup"><span data-stu-id="584bb-145">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="584bb-146">Detta skapar inställningarna på klienten för att aktivera program behörigheter.</span><span class="sxs-lookup"><span data-stu-id="584bb-146">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="584bb-147">Skapa inbyggd app</span><span class="sxs-lookup"><span data-stu-id="584bb-147">Create native app</span></span>

1. <span data-ttu-id="584bb-148">Gå till sidan [Azure Portal-Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app.</span><span class="sxs-lookup"><span data-stu-id="584bb-148">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="584bb-149">Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.</span><span class="sxs-lookup"><span data-stu-id="584bb-149">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="584bb-150">Välj **ny registrering**.</span><span class="sxs-lookup"><span data-stu-id="584bb-150">Select **New registration**.</span></span> <span data-ttu-id="584bb-151">Mer information finns i [snabb start: registrera ett program med Microsoft Identity Platform](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="584bb-151">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="584bb-152">Konfigurera API-åtkomst behörigheter för inbyggd app</span><span class="sxs-lookup"><span data-stu-id="584bb-152">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="584bb-153">Välj din app.</span><span class="sxs-lookup"><span data-stu-id="584bb-153">Choose your app.</span></span> <span data-ttu-id="584bb-154">Gå till **Inställningar**.</span><span class="sxs-lookup"><span data-stu-id="584bb-154">Go to **Settings**.</span></span>

2. <span data-ttu-id="584bb-155">I API-åtkomst väljer du **nödvändiga behörigheter**.</span><span class="sxs-lookup"><span data-stu-id="584bb-155">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="584bb-156">Välj **Windows Azure Active Directory-behörigheter**.</span><span class="sxs-lookup"><span data-stu-id="584bb-156">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="584bb-157">I **delegerade behörigheter** väljer du följande behörigheter:</span><span class="sxs-lookup"><span data-stu-id="584bb-157">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="584bb-158">**Logga in och läsa användarprofil**</span><span class="sxs-lookup"><span data-stu-id="584bb-158">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="584bb-159">**Läs katalogdata**</span><span class="sxs-lookup"><span data-stu-id="584bb-159">**Read directory data**</span></span>
    - <span data-ttu-id="584bb-160">**Gå till katalogen som den inloggade användaren**</span><span class="sxs-lookup"><span data-stu-id="584bb-160">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="584bb-161">**Läs alla grupper**</span><span class="sxs-lookup"><span data-stu-id="584bb-161">**Read all groups**</span></span>

4. <span data-ttu-id="584bb-162">Spara behörigheterna.</span><span class="sxs-lookup"><span data-stu-id="584bb-162">Save the permissions.</span></span>

5. <span data-ttu-id="584bb-163">Välj **Lägg till** i de **behörigheter som krävs**.</span><span class="sxs-lookup"><span data-stu-id="584bb-163">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="584bb-164">Välj **Välj ett API**.</span><span class="sxs-lookup"><span data-stu-id="584bb-164">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="584bb-165">I sökrutan anger du **Microsoft Partner Center** och väljer den i listan resultat.</span><span class="sxs-lookup"><span data-stu-id="584bb-165">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="584bb-166">Välj **Välj**.</span><span class="sxs-lookup"><span data-stu-id="584bb-166">Choose **Select**.</span></span>

7. <span data-ttu-id="584bb-167">Välj **Välj behörigheter**.</span><span class="sxs-lookup"><span data-stu-id="584bb-167">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="584bb-168">Välj **åtkomst till Partner Center-skyddsutrustning**.</span><span class="sxs-lookup"><span data-stu-id="584bb-168">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="584bb-169">Välj **Välj**.</span><span class="sxs-lookup"><span data-stu-id="584bb-169">Choose **Select**.</span></span>

8. <span data-ttu-id="584bb-170">Välj alternativet som anger att du är **klar**.</span><span class="sxs-lookup"><span data-stu-id="584bb-170">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="584bb-171">Notera program-ID i appens egenskaper.</span><span class="sxs-lookup"><span data-stu-id="584bb-171">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="584bb-172">Du behöver inte registrera interna appar i Partner Center, men den inbyggda appen måste vara administratör godkänd.</span><span class="sxs-lookup"><span data-stu-id="584bb-172">You do not need to register native apps in Partner Center, however the native app must be admin consented .</span></span> <span data-ttu-id="584bb-173">Notera program-ID för din inbyggda app.</span><span class="sxs-lookup"><span data-stu-id="584bb-173">Note the application ID of your native app.</span></span>
