---
title: Partnercenter-exempel
description: För att hjälpa dig att komma igång snabbt med Partner Center-API:erna tillhandahåller vi ett exempelprogram, C\-hanterade kodfragment och REST-exempelbegäranden och -svar.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 34e269b1a0e711f82144898441c75d731b8613f70512517e12b6705990b35622
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997608"
---
# <a name="partner-center-samples"></a>Partnercenter-exempel

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

För att hjälpa dig att komma igång snabbt med Partner Center-API:erna tillhandahåller vi ett exempelprogram, C#-hanterade kodfragment och REST-exempelbegäranden och -svar.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Exempel                                                        | Information                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kodfragment                                                 | Pekare och kodfragment för .NET, Java och PowerShell som visar hur du använder det hanterade API:et i Partnercenter för att hantera kundkonton, hämta analyser, göra beställningar, hantera fakturering och prenumerationer, tillhandahålla support och hantera konton och profiler finns i [Scenarier](scenarios.md).                                                                          |
| REST-exempel                                                  | Exempelbegäranden och svar som visar hur du använder PartnerCenter REST API för att hantera kundkonton, få analyser, göra beställningar, hantera fakturering och prenumerationer, tillhandahålla support och hantera konton och profiler finns i [Scenarier](scenarios.md).                                                                                                       |
| [Konsoltestapp](console-test-app.md)                       | Den här appen är tillgänglig i C# och Java. Den innehåller kod och viss felhantering för alla scenarier som anges i avsnittet scenarier.                                                                        |
| [Webbutik för CSP-kunder](csp-customer-web-storefront.md) | Den här webbplatsen visar en fungerande onlinebutik som dina kunder kan använda för att köpa prenumerationer på Microsoft-produkter. Du kan enkelt skapa en webbplats för ditt företag med [snabbstartsguiden för CSP Customer Storefront Builder.](csp-customer-storefront-builder-quick-start-guide-.md)                                                              |
| Store-webbplats                                                | Det här programmet visar hur du skapar en webbutik baserat på katalogen med erbjudanden som är tillgängliga för Molnlösningsleverantör partner. Kunder kan skapa ett butikskonto och beställa programvaruprenumerationer via din webbplats.<br/><br/>                  **Hämta koden:**<br/> [Ladda ned exempelkoden](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Vad som ska konfigureras före lanseringen:**<br/><br/> - Autentisering: App-ID & hemlighet<br/> – Varumärke: logotyp och företagsnamn<br/> – Välkomstmeddelande<br/> – Erbjudanden, inklusive beskrivningar och priser. Appen förutsätter att listpriserna inkluderar tillämpliga skatter. Du kan också lägga till ytterligare logik för att beräkna skatt under utcheckningen.<br/> – Betalningsinformation: Ange egna kreditkortsalternativ, PayPal eller andra betalningstyper. Innan du konfigurerar den här delen bör du [läsa guiden Utebliven betalning, bedrägeri eller missbruk.](/partner-center/non-payment-fraud-misuse) |