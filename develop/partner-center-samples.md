---
title: Partnercenter-exempel
description: 'För att hjälpa dig att snabbt komma igång med API: er för partner Center tillhandahåller vi ett exempel program, C \ hanterade kodfragment och REST-exempel förfrågningar och svar.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2098544e8607eabc4d25d90dcd7cad41510778a9
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769495"
---
# <a name="partner-center-samples"></a>Partnercenter-exempel

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

För att hjälpa dig att snabbt komma igång med API: er för partner Center tillhandahåller vi ett exempel program, C#-hanterade kodfragment och REST-exempel förfrågningar och svar.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Exempel                                                        | Information                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kodfragment                                                 | För pekare och .NET-, Java-och PowerShell-kodfragment som visar hur du använder det hanterade API: t för partner Center för att hantera kund konton, få analyser, placera order, hantera fakturering och prenumerationer, ge support och hantera konton och profiler, se [scenarier](scenarios.md).                                                                          |
| REST-exempel                                                  | För exempel förfrågningar och svar som visar hur du använder Partner Center REST API för att hantera kund konton, få analyser, placera order, hantera fakturering och prenumerationer, ge support och hantera konton och profiler, se [scenarier](scenarios.md).                                                                                                       |
| [Konsoltestapp](console-test-app.md)                       | Den här appen är tillgänglig i C# och Java, och innehåller kod och viss fel hantering för alla scenarier som anges i avsnittet scenarier.                                                                        |
| [Webbutik för CSP-kunder](csp-customer-web-storefront.md) | Den här platsen visar en onlinebutik som dina kunder kan använda för att köpa prenumerationer på Microsoft-produkter. Du kan enkelt skapa en webbplats för ditt företag med [hjälp av snabb starts guiden för CSP-kund butik Builder](csp-customer-storefront-builder-quick-start-guide-.md).                                                              |
| Store-webbplats                                                | Det här programmet visar hur du skapar ett webb Arkiv baserat på katalogen med erbjudanden som är tillgängliga för leverantörer av moln lösningar. Kunder kan skapa ett lagrings konto och beställa program varu prenumerationer via din webbplats.<br/><br/>                  **Hämta koden:**<br/> [Hämta exempel koden](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Vad du ska konfigurera innan du släpper:**<br/><br/> -Autentisering: app-ID & hemlighet<br/> -Varumärke: Logo typ och företags namn<br/> – Välkomst meddelande<br/> – Erbjudanden, inklusive beskrivningar och priser. Appen förutsätter att List priserna innehåller alla tillämpliga skatter. Alternativt kan du lägga till ytterligare logik för att beräkna skatt under kassan.<br/> – Betalnings information: ange egna kreditkorts alternativ, PayPal eller andra betalnings typer. Innan du konfigurerar den här delen bör du läsa hand boken [utan betalning, bedrägerier eller missbruk](/partner-center/non-payment-fraud-misuse). |