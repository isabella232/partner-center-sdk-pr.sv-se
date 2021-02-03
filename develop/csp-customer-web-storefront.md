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
# <a name="csp-customer-web-storefront"></a>Webbutik för CSP-kunder

**Gäller för:**

- Partnercenter

> [!NOTE]
> Den här exempel appen gäller endast den globala instansen av Partner Center. Den gäller inte för partner Center för Microsoft Cloud Tyskland eller till Partner Center för Microsoft Cloud för amerikanska myndigheter.

[Partner Center-butik](https://github.com/Microsoft/Partner-Center-Storefront) är en **exempel webbplats** för en onlinebutik som kunder kan använda för att köpa prenumerationer på Microsoft-produkter. Du kan ändra den här **exempel koden** för din egen användning för att [Konfigurera erbjudandena](#configure-offers), [lägga till varumärke](#configure-branding) och [lägga till en betalnings metod](#configure-payment-types).

## <a name="sample-code"></a>Exempelkod

Hämta [butik exempel kod för partner Center](https://github.com/Microsoft/Partner-Center-Storefront) från GitHub.

## <a name="configure-authentication"></a>Konfigurera autentisering

Innan du skapar programmet uppdaterar du följande värden i Web.config-filen för att avspegla den Azure AD-autentiseringsinformation som du skapade i [partner Center-autentisering](partner-center-authentication.md). Du bör använda dina konto inställningar för integration i begränsat läge vid tidig utveckling eller för testning i produktion (TiP).

- **partnerCenter. applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter. Domain**
- **webportal. clientId**
- **webportal. clientSecret**
- **webporting. Domain**
- **webportal. azureStorageConnectionString**

## <a name="configure-offers"></a>Konfigurera erbjudanden

Du kan konfigurera uppsättningen med erbjudanden (**MicrosoftOffer**) i **OfferCatalogViewModel**.

## <a name="configure-branding"></a>Konfigurera anpassning

Den här exempel webbplatsen spårar följande företags-och varumärkes information i *BrandingConfiguration.cs* och *PortalBranding.cs*:

- Organisationsnamn
- Organisations logo typ
- Sidhuvud bild
- Sekretess avtal
- E-postadress för kontakt
- Telefonnummer till kontakt
- Support-e-post
- Telefonnummer till support

### <a name="configure-payment-types"></a>Konfigurera betalnings typer

Appen använder för närvarande en PayPal-Gateway, implementerad i *PayPalGateway.cs*.