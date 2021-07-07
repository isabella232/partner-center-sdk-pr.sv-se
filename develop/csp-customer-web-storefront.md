---
title: Webbutik för CSP-kunder
description: Den här exempelwebbplatskoden visar en fungerande onlinebutik där kunder kan köpa prenumerationer på Microsoft-produkter.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d68f17d707731f426cb980a566b6478790d3507c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973340"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="04b6e-103">Webbutik för CSP-kunder</span><span class="sxs-lookup"><span data-stu-id="04b6e-103">CSP customer web storefront</span></span>

<span data-ttu-id="04b6e-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="04b6e-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="04b6e-105">**Gäller inte för:** Partner Center for Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="04b6e-105">**Does not apply to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="04b6e-106">Den här exempelappen gäller endast för den globala instansen av Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="04b6e-106">This sample app applies only to the global instance of Partner Center.</span></span>

<span data-ttu-id="04b6e-107">Butiken [i Partnercenter är](https://github.com/Microsoft/Partner-Center-Storefront) en **exempelwebbplats för en** onlinebutik som kunder kan använda för att köpa prenumerationer på Microsoft-produkter.</span><span class="sxs-lookup"><span data-stu-id="04b6e-107">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="04b6e-108">Du kan ändra den **här exempelkoden** för eget bruk för [att konfigurera erbjudandena,](#configure-offers)lägga [till varumärke](#configure-branding)och lägga till [en betalningsmetod](#configure-payment-types).</span><span class="sxs-lookup"><span data-stu-id="04b6e-108">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding), and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="04b6e-109">Exempelkod</span><span class="sxs-lookup"><span data-stu-id="04b6e-109">Sample code</span></span>

<span data-ttu-id="04b6e-110">Ladda ned [exempelkoden för Partnercenter-butiken](https://github.com/Microsoft/Partner-Center-Storefront) från GitHub.</span><span class="sxs-lookup"><span data-stu-id="04b6e-110">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="04b6e-111">Konfigurera autentisering</span><span class="sxs-lookup"><span data-stu-id="04b6e-111">Configure authentication</span></span>

<span data-ttu-id="04b6e-112">Innan du skapar programmet uppdaterar du följande värden i Web.config för att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering .](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="04b6e-112">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="04b6e-113">Du bör använda inställningarna för sandbox-kontots integrering under tidig utveckling eller för testning i produktion (TiP).</span><span class="sxs-lookup"><span data-stu-id="04b6e-113">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="04b6e-114">**partnerCenter.applicationId**</span><span class="sxs-lookup"><span data-stu-id="04b6e-114">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="04b6e-115">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="04b6e-115">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="04b6e-116">**partnerCenter.domain**</span><span class="sxs-lookup"><span data-stu-id="04b6e-116">**partnerCenter.domain**</span></span>
- <span data-ttu-id="04b6e-117">**webPortal.clientId**</span><span class="sxs-lookup"><span data-stu-id="04b6e-117">**webPortal.clientId**</span></span>
- <span data-ttu-id="04b6e-118">**webPortal.clientSecret**</span><span class="sxs-lookup"><span data-stu-id="04b6e-118">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="04b6e-119">**webPortal.domain**</span><span class="sxs-lookup"><span data-stu-id="04b6e-119">**webPortal.domain**</span></span>
- <span data-ttu-id="04b6e-120">**webPortal.azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="04b6e-120">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="04b6e-121">Konfigurera erbjudanden</span><span class="sxs-lookup"><span data-stu-id="04b6e-121">Configure offers</span></span>

<span data-ttu-id="04b6e-122">Du kan konfigurera uppsättningen med erbjudanden (**MicrosoftOffer**) i **OfferCatalogViewModel**.</span><span class="sxs-lookup"><span data-stu-id="04b6e-122">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="04b6e-123">Konfigurera varumärkesmärking</span><span class="sxs-lookup"><span data-stu-id="04b6e-123">Configure branding</span></span>

<span data-ttu-id="04b6e-124">Den här exempelwebbplatsen spårar följande företagsinformation och varumärkesinformation *i BrandingConfiguration.cs* *och PortalBranding.cs:*</span><span class="sxs-lookup"><span data-stu-id="04b6e-124">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="04b6e-125">Organisationsnamn</span><span class="sxs-lookup"><span data-stu-id="04b6e-125">Organization name</span></span>
- <span data-ttu-id="04b6e-126">Organisationens logotyp</span><span class="sxs-lookup"><span data-stu-id="04b6e-126">Organization logo</span></span>
- <span data-ttu-id="04b6e-127">Rubrikbild</span><span class="sxs-lookup"><span data-stu-id="04b6e-127">Header image</span></span>
- <span data-ttu-id="04b6e-128">Sekretessavtal</span><span class="sxs-lookup"><span data-stu-id="04b6e-128">Privacy agreement</span></span>
- <span data-ttu-id="04b6e-129">E-postadress för kontakt</span><span class="sxs-lookup"><span data-stu-id="04b6e-129">Contact email</span></span>
- <span data-ttu-id="04b6e-130">Telefonnummer till kontakt</span><span class="sxs-lookup"><span data-stu-id="04b6e-130">Contact phone number</span></span>
- <span data-ttu-id="04b6e-131">E-post för support</span><span class="sxs-lookup"><span data-stu-id="04b6e-131">Support email</span></span>
- <span data-ttu-id="04b6e-132">Telefonnummer till support</span><span class="sxs-lookup"><span data-stu-id="04b6e-132">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="04b6e-133">Konfigurera betalningstyper</span><span class="sxs-lookup"><span data-stu-id="04b6e-133">Configure payment types</span></span>

<span data-ttu-id="04b6e-134">Appen använder för närvarande en PayPal gateway, implementerad i *PayPalGateway.cs.*</span><span class="sxs-lookup"><span data-stu-id="04b6e-134">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>