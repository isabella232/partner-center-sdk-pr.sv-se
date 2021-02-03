---
title: Kom igång
description: Partner Center SDK innehåller ett hanterat API och en REST API som partner kan använda för att hantera kund-, prenumerations-och order data.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c2af1e11dbda19489a27e37c7f3de8ede90fd1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769057"
---
# <a name="get-started"></a><span data-ttu-id="76c84-103">Kom igång</span><span class="sxs-lookup"><span data-stu-id="76c84-103">Get started</span></span>

<span data-ttu-id="76c84-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="76c84-104">**Applies To**</span></span>

- <span data-ttu-id="76c84-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="76c84-105">Partner Center</span></span>
- <span data-ttu-id="76c84-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="76c84-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="76c84-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="76c84-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="76c84-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="76c84-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="76c84-109">Partner Center SDK innehåller ett hanterat API och en REST API som partner kan använda för att hantera kund-, prenumerations-och order data.</span><span class="sxs-lookup"><span data-stu-id="76c84-109">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="76c84-110">Hämta koden</span><span class="sxs-lookup"><span data-stu-id="76c84-110">Get the code</span></span>

[<span data-ttu-id="76c84-111">Ladda ned SDK för partner Center</span><span class="sxs-lookup"><span data-stu-id="76c84-111">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="76c84-112">API-åtkomst till Partner Center för indirekta åter försäljare är inte ett scenario som stöds.</span><span class="sxs-lookup"><span data-stu-id="76c84-112">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="76c84-113">Ta reda på din version av Partner Center</span><span class="sxs-lookup"><span data-stu-id="76c84-113">Determine your version of Partner Center</span></span>

<span data-ttu-id="76c84-114">Vissa versioner av Partner Center har inte hela SDK tillgängligt.</span><span class="sxs-lookup"><span data-stu-id="76c84-114">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="76c84-115">Mer information finns i [utveckla för partner Center för Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="76c84-115">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="76c84-116">Hämta exemplen</span><span class="sxs-lookup"><span data-stu-id="76c84-116">Get the samples</span></span>

<span data-ttu-id="76c84-117">Mer information om C#-kodfragment, REST-exempel och exempel-appen finns i [exempel för partner Center](partner-center-samples.md).</span><span class="sxs-lookup"><span data-stu-id="76c84-117">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="76c84-118">Test jämfört med produktion</span><span class="sxs-lookup"><span data-stu-id="76c84-118">Test vs. production</span></span>

<span data-ttu-id="76c84-119">När du börjar skriva och testa din kod bör du använda ditt konto för integration i begränsat läge (och motsvarande token) så att du inte av misstag debiteras nya avgifter som företaget ansvarar för att betala.</span><span class="sxs-lookup"><span data-stu-id="76c84-119">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="76c84-120">Mer information om den här test miljön finns i [Konfigurera API-åtkomst i Partner Center](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="76c84-120">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="76c84-121">När lösningen har testats och är redo att användas på verkliga kund konton måste du uppdatera dina tokens så att du använder en Azure AD-App och en hemlighet som motsvarar ditt primära partner Center-konto.</span><span class="sxs-lookup"><span data-stu-id="76c84-121">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="76c84-122">Tips och förslag på testning och fel sökning, inklusive mer information om test-in-Production (TiP) och integration sandbox, finns i [testa och felsöka](test-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="76c84-122">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="76c84-123">Konfigurera din autentisering</span><span class="sxs-lookup"><span data-stu-id="76c84-123">Configure your authentication</span></span>

<span data-ttu-id="76c84-124">Om du vill konfigurera din Azure AD-autentisering så att du kan använda API: er för partner Center, se [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="76c84-124">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76c84-125">Microsoft presenterar ett säkert, skalbart ramverk för att autentisera leverantörer av moln lösnings leverantörer och kontroll panels leverantörer (CPV) via Microsoft Azure Multi-Factor Authentication (MFA)-arkitekturen.</span><span class="sxs-lookup"><span data-stu-id="76c84-125">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="76c84-126">Partner Center använder Azure AD för autentisering och för att använda API: er för partner Center måste du konfigurera dina autentiseringsinställningar på rätt sätt.</span><span class="sxs-lookup"><span data-stu-id="76c84-126">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="76c84-127">Mer information finns i [Aktivera säker program modell](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="76c84-127">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="76c84-128">Få hjälp</span><span class="sxs-lookup"><span data-stu-id="76c84-128">Get help</span></span>

<span data-ttu-id="76c84-129">Partner kan få support i [gruppen Partner Center SDK Yammer](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span><span class="sxs-lookup"><span data-stu-id="76c84-129">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="76c84-130">För att få mer personligt anpassad hjälp kan utvecklare använda sina MPN-support förmåner eller Premier Support.</span><span class="sxs-lookup"><span data-stu-id="76c84-130">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="76c84-131">Gå med i Partnercenter-programmet för tidiga API- och SDK-användare</span><span class="sxs-lookup"><span data-stu-id="76c84-131">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="76c84-132">Information om hur du kan samar beta med Microsoft om utveckling av partner funktioner och funktioner finns i [delta i Partner Center API och SDK tidigt i programmet](early-adopter-program.md).</span><span class="sxs-lookup"><span data-stu-id="76c84-132">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
