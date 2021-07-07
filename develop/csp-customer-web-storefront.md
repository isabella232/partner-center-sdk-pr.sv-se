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
# <a name="csp-customer-web-storefront"></a>Webbutik för CSP-kunder

**Gäller för:** Partnercenter

**Gäller inte för:** Partner Center for Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Den här exempelappen gäller endast för den globala instansen av Partnercenter.

Butiken [i Partnercenter är](https://github.com/Microsoft/Partner-Center-Storefront) en **exempelwebbplats för en** onlinebutik som kunder kan använda för att köpa prenumerationer på Microsoft-produkter. Du kan ändra den **här exempelkoden** för eget bruk för [att konfigurera erbjudandena,](#configure-offers)lägga [till varumärke](#configure-branding)och lägga till [en betalningsmetod](#configure-payment-types).

## <a name="sample-code"></a>Exempelkod

Ladda ned [exempelkoden för Partnercenter-butiken](https://github.com/Microsoft/Partner-Center-Storefront) från GitHub.

## <a name="configure-authentication"></a>Konfigurera autentisering

Innan du skapar programmet uppdaterar du följande värden i Web.config för att återspegla den Azure AD-autentiseringsinformation som du skapade i [Partnercenter-autentisering .](partner-center-authentication.md) Du bör använda inställningarna för sandbox-kontots integrering under tidig utveckling eller för testning i produktion (TiP).

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## <a name="configure-offers"></a>Konfigurera erbjudanden

Du kan konfigurera uppsättningen med erbjudanden (**MicrosoftOffer**) i **OfferCatalogViewModel**.

## <a name="configure-branding"></a>Konfigurera varumärkesmärking

Den här exempelwebbplatsen spårar följande företagsinformation och varumärkesinformation *i BrandingConfiguration.cs* *och PortalBranding.cs:*

- Organisationsnamn
- Organisationens logotyp
- Rubrikbild
- Sekretessavtal
- E-postadress för kontakt
- Telefonnummer till kontakt
- E-post för support
- Telefonnummer till support

### <a name="configure-payment-types"></a>Konfigurera betalningstyper

Appen använder för närvarande en PayPal gateway, implementerad i *PayPalGateway.cs.*