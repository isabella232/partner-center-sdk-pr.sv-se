---
title: Kom igång
description: I Partnercenter-SDK ett hanterat API och en REST API som partner kan använda för att hantera kund-, prenumerations- och beställningsdata.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 340b46978d71bdf5fa6f6795d69fe0721d808c4eb2650744e82510c208dd5b8f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989703"
---
# <a name="get-started"></a>Kom igång

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

I Partnercenter-SDK ett hanterat API och en REST API som partner kan använda för att hantera kund-, prenumerations- och beställningsdata.

## <a name="get-the-code"></a>Hämta koden

[Ladda ned Partnercenter-SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> API-åtkomst till Partner center för indirekta återförsäljare stöds inte.

## <a name="determine-your-version-of-partner-center"></a>Fastställ din version av Partnercenter

I vissa versioner av PartnerCenter finns inte hela SDK:n tillgänglig. Mer information finns i [Utveckla för Partner Center för Microsoft National Cloud.](developing-for-partner-center-for-microsoft-national-cloud.md)

## <a name="get-the-samples"></a>Hämta exemplen

Mer information om C#-kodfragment, REST-exempel och exempelappen finns i [PartnerCenter-exempel.](partner-center-samples.md)

## <a name="test-vs-production"></a>Test jämfört med produktion

När du först skriver och testar din kod bör du använda ditt sandbox-konto för integrering (och motsvarande token) så att du inte av misstag debiteras nya avgifter som ditt företag är ansvarigt för att betala. Mer information om den här testmiljön finns i [Konfigurera API-åtkomst i Partnercenter.](set-up-api-access-in-partner-center.md)

När din lösning har testats och är redo att användas på verkliga kundkonton måste du uppdatera dina token så att du använder en Azure AD-klientapp och en hemlighet som motsvarar ditt primära Partnercenter-konto.

Tips och förslag om testning och felsökning, inklusive mer information om Test-in-Production (TiP) och Integration Sandbox, finns i [Testa och felsöka](test-and-debug.md).

## <a name="configure-your-authentication"></a>Konfigurera din autentisering

Information om hur du konfigurerar din Azure AD-autentisering så att du kan använda Partner Center-API:er finns [i Partner center-autentisering](partner-center-authentication.md).

> [!IMPORTANT]
> Microsoft introducerar ett säkert, skalbart ramverk för autentisering av molnlösningsleverantörer (CSP) och leverantörer av kontrollpaneler (CPV) via arkitekturen för Microsoft Azure multifaktorautentisering (MFA).
Partner center använder Azure AD för autentisering och för att använda Partner Center-API:er måste du konfigurera autentiseringsinställningarna korrekt.
>
> Mer information finns i [Aktivera säker programmodell.](enable-secure-app-model.md)

## <a name="get-help"></a>Få hjälp

Partner kan få support Partnercenter-SDK Yammer [gruppen](https://go.microsoft.com/fwlink/p/?LinkID=717360). För att få mer personlig hjälp kan utvecklare använda sina MPN-supportförmåner eller Premier Support.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Gå med i Partnercenter-programmet för tidiga API- och SDK-användare

Information om hur du kan samarbeta med Microsoft när det gäller utveckling av partnerfunktioner finns i Join the Partner Center API and SDK Early Adopter Program (Gå med i [Partner Center-API:et och SDK Early Adopter Program).](early-adopter-program.md)
