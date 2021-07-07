---
title: Registrera appinformation för Partner Center for Microsoft National Cloud
description: Lär dig hur och varför apputvecklare för Partner Center for Microsoft National Cloud måste registrera information om sin app med Azure AD via Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973459"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="7fe14-103">Registrera appinformation för Partner Center for Microsoft National Cloud via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7fe14-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="7fe14-104">**Gäller för:** Partner Center for Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7fe14-104">**Applies to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7fe14-105">Utvecklare måste registrera information om sin app med Azure AD via Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7fe14-105">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="7fe14-106">Detta säkerställer att endast angivna appar kan ansluta till partner- och kunddata.</span><span class="sxs-lookup"><span data-stu-id="7fe14-106">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="7fe14-107">För Partnercenter för Microsoft Cloud for US Government måste du för närvarande hantera appar via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7fe14-107">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="7fe14-108">Mer information finns i Azure PowerShell [referensdokumentationen](/powershell/module/Azuread/#applications).</span><span class="sxs-lookup"><span data-stu-id="7fe14-108">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="7fe14-109">Tänk på följande ytterligare krav när du skapar en app för Partner center för Microsoft Cloud Tyskland eller Partnercenter för Microsoft Cloud for US Government.</span><span class="sxs-lookup"><span data-stu-id="7fe14-109">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="7fe14-110">Webbappar</span><span class="sxs-lookup"><span data-stu-id="7fe14-110">Web apps</span></span>

<span data-ttu-id="7fe14-111">För webbappar använder du följande procedurer för att registrera ditt program-ID.</span><span class="sxs-lookup"><span data-stu-id="7fe14-111">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="7fe14-112">Skapa eller uppdatera webbapp</span><span class="sxs-lookup"><span data-stu-id="7fe14-112">Create or update web app</span></span>

1. <span data-ttu-id="7fe14-113">Gå till [sidan Azure Portal – Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app.</span><span class="sxs-lookup"><span data-stu-id="7fe14-113">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="7fe14-114">Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.</span><span class="sxs-lookup"><span data-stu-id="7fe14-114">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="7fe14-115">Välj **Ny registrering.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-115">Select **New registration**.</span></span> <span data-ttu-id="7fe14-116">Mer information finns i [Snabbstart: Registrera ett program med Microsofts identitetsplattform](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="7fe14-116">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="7fe14-117">Konfigurera API-åtkomstbehörigheter för webbapp</span><span class="sxs-lookup"><span data-stu-id="7fe14-117">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="7fe14-118">Välj din app.</span><span class="sxs-lookup"><span data-stu-id="7fe14-118">Choose your app.</span></span> <span data-ttu-id="7fe14-119">Gå **till Inställningar** av webbappen.</span><span class="sxs-lookup"><span data-stu-id="7fe14-119">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="7fe14-120">I **avsnittet API-åtkomst** väljer du **Nödvändiga behörigheter**</span><span class="sxs-lookup"><span data-stu-id="7fe14-120">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="7fe14-121">För Windows Azure Active Directory-behörigheter:</span><span class="sxs-lookup"><span data-stu-id="7fe14-121">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="7fe14-122">Välj **Windows Azure Active Directory behörigheter**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-122">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="7fe14-123">I **Programbehörigheter** väljer du Läsa katalogdata.</span><span class="sxs-lookup"><span data-stu-id="7fe14-123">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="7fe14-124">Spara behörigheterna.</span><span class="sxs-lookup"><span data-stu-id="7fe14-124">Save the permissions.</span></span>

4. <span data-ttu-id="7fe14-125">Observera program-ID:t **i avsnittet** Egenskaper för webbappen.</span><span class="sxs-lookup"><span data-stu-id="7fe14-125">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="7fe14-126">Lägga till en hemlig nyckel i din app</span><span class="sxs-lookup"><span data-stu-id="7fe14-126">Add a secret key to your app</span></span>

1. <span data-ttu-id="7fe14-127">Gå till **avsnittet Nycklar** i webbappen.</span><span class="sxs-lookup"><span data-stu-id="7fe14-127">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="7fe14-128">Ange nyckelbeskrivning och välj varaktighet som 1 eller 2 år, efter behov.</span><span class="sxs-lookup"><span data-stu-id="7fe14-128">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="7fe14-129">Spara och kopiera värdet för den hemliga nyckeln.</span><span class="sxs-lookup"><span data-stu-id="7fe14-129">Save and copy the secret key value.</span></span> <span data-ttu-id="7fe14-130">**Det här värdet visas inte igen när du lämnar den här sidan.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-130">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="7fe14-131">Du bör ha följande information från webbappskonfigurationen:</span><span class="sxs-lookup"><span data-stu-id="7fe14-131">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="7fe14-132">Program-ID:t</span><span class="sxs-lookup"><span data-stu-id="7fe14-132">Application ID</span></span>
- <span data-ttu-id="7fe14-133">Apphemlighet</span><span class="sxs-lookup"><span data-stu-id="7fe14-133">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="7fe14-134">Registrera webbappen i Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7fe14-134">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="7fe14-135">Logga in på [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7fe14-135">Sign in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="7fe14-136">Välj **Instrumentpanel,** välj **sedan Konto Inställningar** och välj sedan **Apphantering.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-136">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="7fe14-137">I avsnittet **Webbapp** väljer du **Registrera befintlig app.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-137">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="7fe14-138">Välj den webbapp som du skapade Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7fe14-138">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="7fe14-139">Välj **Registrera din app.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-139">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="7fe14-140">Inbyggda appar</span><span class="sxs-lookup"><span data-stu-id="7fe14-140">Native apps</span></span>

<span data-ttu-id="7fe14-141">Inbyggda appar behöver inte vara registrerade i Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="7fe14-141">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="7fe14-142">Men de här apparna måste konfigureras för att ge åtkomst till Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="7fe14-142">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="7fe14-143">Innan du skapar en inbyggd app i Azure Portal loggar du in på Partnercenter med autentiseringsuppgifterna för administratörsanvändaren från partnerklientorganisationen.</span><span class="sxs-lookup"><span data-stu-id="7fe14-143">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="7fe14-144">Detta skapar inställningarna för klientorganisationen för att aktivera appbehörigheter.</span><span class="sxs-lookup"><span data-stu-id="7fe14-144">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="7fe14-145">Skapa inbyggd app</span><span class="sxs-lookup"><span data-stu-id="7fe14-145">Create native app</span></span>

1. <span data-ttu-id="7fe14-146">Gå till [sidan Azure Portal – Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app.</span><span class="sxs-lookup"><span data-stu-id="7fe14-146">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="7fe14-147">Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.</span><span class="sxs-lookup"><span data-stu-id="7fe14-147">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="7fe14-148">Välj **Ny registrering.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-148">Select **New registration**.</span></span> <span data-ttu-id="7fe14-149">Mer information finns i [Snabbstart: Registrera ett program med Microsofts identitetsplattform](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="7fe14-149">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="7fe14-150">Konfigurera API-åtkomstbehörigheter för inbyggd app</span><span class="sxs-lookup"><span data-stu-id="7fe14-150">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="7fe14-151">Välj din app.</span><span class="sxs-lookup"><span data-stu-id="7fe14-151">Choose your app.</span></span> <span data-ttu-id="7fe14-152">Gå till **Inställningar**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-152">Go to **Settings**.</span></span>

2. <span data-ttu-id="7fe14-153">I API-åtkomst väljer du **Nödvändiga behörigheter.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-153">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="7fe14-154">Välj **Windows Azure Active Directory behörigheter**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-154">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="7fe14-155">I **Delegerade behörigheter** väljer du följande behörigheter:</span><span class="sxs-lookup"><span data-stu-id="7fe14-155">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="7fe14-156">**Logga in och läsa användarprofil**</span><span class="sxs-lookup"><span data-stu-id="7fe14-156">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="7fe14-157">**Läs katalogdata**</span><span class="sxs-lookup"><span data-stu-id="7fe14-157">**Read directory data**</span></span>
    - <span data-ttu-id="7fe14-158">**Gå till katalogen som den inloggade användaren**</span><span class="sxs-lookup"><span data-stu-id="7fe14-158">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="7fe14-159">**Läs alla grupper**</span><span class="sxs-lookup"><span data-stu-id="7fe14-159">**Read all groups**</span></span>

4. <span data-ttu-id="7fe14-160">Spara behörigheterna.</span><span class="sxs-lookup"><span data-stu-id="7fe14-160">Save the permissions.</span></span>

5. <span data-ttu-id="7fe14-161">Välj **Lägg till** i Nödvändiga **behörigheter.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-161">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="7fe14-162">Välj **Välj ett API**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-162">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="7fe14-163">I sökrutan anger du **Microsoft Partner Center** och väljer det i resultatlistan.</span><span class="sxs-lookup"><span data-stu-id="7fe14-163">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="7fe14-164">Välj **Välj**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-164">Choose **Select**.</span></span>

7. <span data-ttu-id="7fe14-165">Välj **Välj behörigheter**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-165">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="7fe14-166">Välj **Access Partner Center PPE.**</span><span class="sxs-lookup"><span data-stu-id="7fe14-166">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="7fe14-167">Välj **Välj**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-167">Choose **Select**.</span></span>

8. <span data-ttu-id="7fe14-168">Välj alternativet som anger att du är **klar**.</span><span class="sxs-lookup"><span data-stu-id="7fe14-168">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="7fe14-169">Observera program-ID:t i Egenskaper för din app.</span><span class="sxs-lookup"><span data-stu-id="7fe14-169">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="7fe14-170">Du behöver inte registrera inbyggda appar i Partnercenter, men den interna appen måste godkännas av administratören.</span><span class="sxs-lookup"><span data-stu-id="7fe14-170">You do not need to register native apps in Partner Center, however the native app must be admin consented.</span></span> <span data-ttu-id="7fe14-171">Observera program-ID:t för din interna app.</span><span class="sxs-lookup"><span data-stu-id="7fe14-171">Note the application ID of your native app.</span></span>
