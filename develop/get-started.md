---
title: Kom igång
description: I Partnercenter-SDK ett hanterat API och en REST API som partner kan använda för att hantera kund-, prenumerations- och beställningsdata.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b5d05f26d63574ef876519091dc1c33c05f36e25
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548761"
---
# <a name="get-started"></a><span data-ttu-id="1aa6d-103">Kom igång</span><span class="sxs-lookup"><span data-stu-id="1aa6d-103">Get started</span></span>

<span data-ttu-id="1aa6d-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1aa6d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1aa6d-105">I Partnercenter-SDK ett hanterat API och en REST API som partner kan använda för att hantera kund-, prenumerations- och beställningsdata.</span><span class="sxs-lookup"><span data-stu-id="1aa6d-105">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="1aa6d-106">Hämta koden</span><span class="sxs-lookup"><span data-stu-id="1aa6d-106">Get the code</span></span>

[<span data-ttu-id="1aa6d-107">Ladda ned Partnercenter-SDK</span><span class="sxs-lookup"><span data-stu-id="1aa6d-107">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="1aa6d-108">API-åtkomst till Partner Center för indirekta återförsäljare stöds inte.</span><span class="sxs-lookup"><span data-stu-id="1aa6d-108">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="1aa6d-109">Fastställ din version av Partnercenter</span><span class="sxs-lookup"><span data-stu-id="1aa6d-109">Determine your version of Partner Center</span></span>

<span data-ttu-id="1aa6d-110">I vissa versioner av Partnercenter finns inte hela SDK:n tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="1aa6d-110">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="1aa6d-111">Mer information finns i [Utveckla för Partner Center för Microsoft National Cloud.](developing-for-partner-center-for-microsoft-national-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="1aa6d-111">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="1aa6d-112">Hämta exemplen</span><span class="sxs-lookup"><span data-stu-id="1aa6d-112">Get the samples</span></span>

<span data-ttu-id="1aa6d-113">Mer information om C#-kodfragment, REST-exempel och exempelappen finns i [Partner Center-exempel.](partner-center-samples.md)</span><span class="sxs-lookup"><span data-stu-id="1aa6d-113">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="1aa6d-114">Test jämfört med produktion</span><span class="sxs-lookup"><span data-stu-id="1aa6d-114">Test vs. production</span></span>

<span data-ttu-id="1aa6d-115">När du först skriver och testar din kod bör du använda ditt sandbox-konto för integrering (och motsvarande token) så att du inte av misstag debiteras nya avgifter som ditt företag är ansvarigt för att betala.</span><span class="sxs-lookup"><span data-stu-id="1aa6d-115">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="1aa6d-116">Mer information om den här testmiljön finns i [Konfigurera API-åtkomst i Partnercenter.](set-up-api-access-in-partner-center.md)</span><span class="sxs-lookup"><span data-stu-id="1aa6d-116">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="1aa6d-117">När din lösning har testats och är redo att användas på verkliga kundkonton måste du uppdatera dina token så att du använder en Azure AD-klientapp och en hemlighet som motsvarar ditt primära Partnercenter-konto.</span><span class="sxs-lookup"><span data-stu-id="1aa6d-117">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="1aa6d-118">Tips och förslag om testning och felsökning, inklusive mer information om Test-in-Production (TiP) och sandbox-miljön för integrering finns [i Testa och felsöka](test-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="1aa6d-118">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="1aa6d-119">Konfigurera din autentisering</span><span class="sxs-lookup"><span data-stu-id="1aa6d-119">Configure your authentication</span></span>

<span data-ttu-id="1aa6d-120">Information om hur du konfigurerar din Azure AD-autentisering så att du kan använda Partner Center-API:er finns [i Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1aa6d-120">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1aa6d-121">Microsoft introducerar ett säkert, skalbart ramverk för autentisering av molnlösningsleverantörer (CSP) och leverantörer av kontrollpanelen (CPV) via arkitekturen för Microsoft Azure multifaktorautentisering (MFA).</span><span class="sxs-lookup"><span data-stu-id="1aa6d-121">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="1aa6d-122">Partnercenter använder Azure AD för autentisering och för att använda Partner Center-API:er måste du konfigurera autentiseringsinställningarna korrekt.</span><span class="sxs-lookup"><span data-stu-id="1aa6d-122">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="1aa6d-123">Mer information finns i [Aktivera säker programmodell.](enable-secure-app-model.md)</span><span class="sxs-lookup"><span data-stu-id="1aa6d-123">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="1aa6d-124">Få hjälp</span><span class="sxs-lookup"><span data-stu-id="1aa6d-124">Get help</span></span>

<span data-ttu-id="1aa6d-125">Partner kan få support på [Partnercenter-SDK Yammer grupp](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span><span class="sxs-lookup"><span data-stu-id="1aa6d-125">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="1aa6d-126">För att få mer anpassad hjälp kan utvecklare använda sina MPN-supportförmåner eller Premier Support.</span><span class="sxs-lookup"><span data-stu-id="1aa6d-126">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="1aa6d-127">Gå med i Partnercenter-programmet för tidiga API- och SDK-användare</span><span class="sxs-lookup"><span data-stu-id="1aa6d-127">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="1aa6d-128">Information om hur du kan samarbeta med Microsoft när det gäller utveckling av partnerfunktioner finns i Join the Partner Center API and SDK Early Adopter Program (Gå med i Partner Center-API:et och [SDK Early Adopter Program).](early-adopter-program.md)</span><span class="sxs-lookup"><span data-stu-id="1aa6d-128">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
