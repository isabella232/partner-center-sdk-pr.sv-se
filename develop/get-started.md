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
# <a name="get-started"></a>Kom igång

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Partner Center SDK innehåller ett hanterat API och en REST API som partner kan använda för att hantera kund-, prenumerations-och order data.

## <a name="get-the-code"></a>Hämta koden

[Ladda ned SDK för partner Center](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> API-åtkomst till Partner Center för indirekta åter försäljare är inte ett scenario som stöds.

## <a name="determine-your-version-of-partner-center"></a>Ta reda på din version av Partner Center

Vissa versioner av Partner Center har inte hela SDK tillgängligt. Mer information finns i [utveckla för partner Center för Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="get-the-samples"></a>Hämta exemplen

Mer information om C#-kodfragment, REST-exempel och exempel-appen finns i [exempel för partner Center](partner-center-samples.md).

## <a name="test-vs-production"></a>Test jämfört med produktion

När du börjar skriva och testa din kod bör du använda ditt konto för integration i begränsat läge (och motsvarande token) så att du inte av misstag debiteras nya avgifter som företaget ansvarar för att betala. Mer information om den här test miljön finns i [Konfigurera API-åtkomst i Partner Center](set-up-api-access-in-partner-center.md).

När lösningen har testats och är redo att användas på verkliga kund konton måste du uppdatera dina tokens så att du använder en Azure AD-App och en hemlighet som motsvarar ditt primära partner Center-konto.

Tips och förslag på testning och fel sökning, inklusive mer information om test-in-Production (TiP) och integration sandbox, finns i [testa och felsöka](test-and-debug.md).

## <a name="configure-your-authentication"></a>Konfigurera din autentisering

Om du vill konfigurera din Azure AD-autentisering så att du kan använda API: er för partner Center, se [partner Center-autentisering](partner-center-authentication.md).

> [!IMPORTANT]
> Microsoft presenterar ett säkert, skalbart ramverk för att autentisera leverantörer av moln lösnings leverantörer och kontroll panels leverantörer (CPV) via Microsoft Azure Multi-Factor Authentication (MFA)-arkitekturen.
Partner Center använder Azure AD för autentisering och för att använda API: er för partner Center måste du konfigurera dina autentiseringsinställningar på rätt sätt.
>
> Mer information finns i [Aktivera säker program modell](enable-secure-app-model.md).

## <a name="get-help"></a>Få hjälp

Partner kan få support i [gruppen Partner Center SDK Yammer](https://go.microsoft.com/fwlink/p/?LinkID=717360). För att få mer personligt anpassad hjälp kan utvecklare använda sina MPN-support förmåner eller Premier Support.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Gå med i Partnercenter-programmet för tidiga API- och SDK-användare

Information om hur du kan samar beta med Microsoft om utveckling av partner funktioner och funktioner finns i [delta i Partner Center API och SDK tidigt i programmet](early-adopter-program.md).
