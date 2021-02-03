---
title: Webbutik för CSP-kunder
description: Den här exempel webbplats koden visar en fungerande onlinebutik för kunder som köper prenumerationer på Microsoft-produkter.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768799"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="8f345-103">Webbutik för CSP-kunder</span><span class="sxs-lookup"><span data-stu-id="8f345-103">CSP customer web storefront</span></span>

<span data-ttu-id="8f345-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="8f345-104">**Applies to:**</span></span>

- <span data-ttu-id="8f345-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="8f345-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="8f345-106">Den här exempel appen gäller endast den globala instansen av Partner Center.</span><span class="sxs-lookup"><span data-stu-id="8f345-106">This sample app applies only to the global instance of Partner Center.</span></span> <span data-ttu-id="8f345-107">Den gäller inte för partner Center för Microsoft Cloud Tyskland eller till Partner Center för Microsoft Cloud för amerikanska myndigheter.</span><span class="sxs-lookup"><span data-stu-id="8f345-107">It does not apply to Partner Center for Microsoft Cloud Germany or to Partner Center for Microsoft Cloud for US Government.</span></span>

<span data-ttu-id="8f345-108">[Partner Center-butik](https://github.com/Microsoft/Partner-Center-Storefront) är en **exempel webbplats** för en onlinebutik som kunder kan använda för att köpa prenumerationer på Microsoft-produkter.</span><span class="sxs-lookup"><span data-stu-id="8f345-108">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="8f345-109">Du kan ändra den här **exempel koden** för din egen användning för att [Konfigurera erbjudandena](#configure-offers), [lägga till varumärke](#configure-branding) och [lägga till en betalnings metod](#configure-payment-types).</span><span class="sxs-lookup"><span data-stu-id="8f345-109">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding) and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="8f345-110">Exempelkod</span><span class="sxs-lookup"><span data-stu-id="8f345-110">Sample code</span></span>

<span data-ttu-id="8f345-111">Hämta [butik exempel kod för partner Center](https://github.com/Microsoft/Partner-Center-Storefront) från GitHub.</span><span class="sxs-lookup"><span data-stu-id="8f345-111">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="8f345-112">Konfigurera autentisering</span><span class="sxs-lookup"><span data-stu-id="8f345-112">Configure authentication</span></span>

<span data-ttu-id="8f345-113">Innan du skapar programmet uppdaterar du följande värden i Web.config-filen för att avspegla den Azure AD-autentiseringsinformation som du skapade i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8f345-113">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f345-114">Du bör använda dina konto inställningar för integration i begränsat läge vid tidig utveckling eller för testning i produktion (TiP).</span><span class="sxs-lookup"><span data-stu-id="8f345-114">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="8f345-115">**partnerCenter. applicationId**</span><span class="sxs-lookup"><span data-stu-id="8f345-115">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="8f345-116">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="8f345-116">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="8f345-117">**partnerCenter. Domain**</span><span class="sxs-lookup"><span data-stu-id="8f345-117">**partnerCenter.domain**</span></span>
- <span data-ttu-id="8f345-118">**webportal. clientId**</span><span class="sxs-lookup"><span data-stu-id="8f345-118">**webPortal.clientId**</span></span>
- <span data-ttu-id="8f345-119">**webportal. clientSecret**</span><span class="sxs-lookup"><span data-stu-id="8f345-119">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="8f345-120">**webporting. Domain**</span><span class="sxs-lookup"><span data-stu-id="8f345-120">**webPortal.domain**</span></span>
- <span data-ttu-id="8f345-121">**webportal. azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="8f345-121">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="8f345-122">Konfigurera erbjudanden</span><span class="sxs-lookup"><span data-stu-id="8f345-122">Configure offers</span></span>

<span data-ttu-id="8f345-123">Du kan konfigurera uppsättningen med erbjudanden (**MicrosoftOffer**) i **OfferCatalogViewModel**.</span><span class="sxs-lookup"><span data-stu-id="8f345-123">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="8f345-124">Konfigurera anpassning</span><span class="sxs-lookup"><span data-stu-id="8f345-124">Configure branding</span></span>

<span data-ttu-id="8f345-125">Den här exempel webbplatsen spårar följande företags-och varumärkes information i *BrandingConfiguration.cs* och *PortalBranding.cs*:</span><span class="sxs-lookup"><span data-stu-id="8f345-125">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="8f345-126">Organisationsnamn</span><span class="sxs-lookup"><span data-stu-id="8f345-126">Organization name</span></span>
- <span data-ttu-id="8f345-127">Organisations logo typ</span><span class="sxs-lookup"><span data-stu-id="8f345-127">Organization logo</span></span>
- <span data-ttu-id="8f345-128">Sidhuvud bild</span><span class="sxs-lookup"><span data-stu-id="8f345-128">Header image</span></span>
- <span data-ttu-id="8f345-129">Sekretess avtal</span><span class="sxs-lookup"><span data-stu-id="8f345-129">Privacy agreement</span></span>
- <span data-ttu-id="8f345-130">E-postadress för kontakt</span><span class="sxs-lookup"><span data-stu-id="8f345-130">Contact email</span></span>
- <span data-ttu-id="8f345-131">Telefonnummer till kontakt</span><span class="sxs-lookup"><span data-stu-id="8f345-131">Contact phone number</span></span>
- <span data-ttu-id="8f345-132">Support-e-post</span><span class="sxs-lookup"><span data-stu-id="8f345-132">Support email</span></span>
- <span data-ttu-id="8f345-133">Telefonnummer till support</span><span class="sxs-lookup"><span data-stu-id="8f345-133">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="8f345-134">Konfigurera betalnings typer</span><span class="sxs-lookup"><span data-stu-id="8f345-134">Configure payment types</span></span>

<span data-ttu-id="8f345-135">Appen använder för närvarande en PayPal-Gateway, implementerad i *PayPalGateway.cs*.</span><span class="sxs-lookup"><span data-stu-id="8f345-135">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>