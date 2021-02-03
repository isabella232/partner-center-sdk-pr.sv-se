---
title: API-scenarier för partner Center
description: Lär dig hur Cloud Solution Provider-programpartner kan använda Partner Center API för att hantera kund konton, beställningar, support och fakturering program mässigt.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14dbd501e3d075c3880fae6f362feef797cba133
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769957"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>Partner Center API-scenarier som låter dig hantera kund konton program mässigt

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

I den här artikeln beskrivs några av de sätt som partners i Cloud Solution Provider-programmet kan använda Partner Center API för att hantera områden som:

- Kund konton
- Order
- Prenumerationer
- Support
- Fakturering

Det finns olika versioner av Partner Center som innehåller olika funktioner. Alla scenarier stöds inte i alla versioner av Partner Center. Mer information finns i [utveckla för partner Center för Microsofts nationella moln](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>Scenarier som stöds av Partner Center SDK

Alla följande scenarier kan utföras på tre olika sätt:

- Manuellt på instrument panelen för [partner Center](https://partner.microsoft.com/dashboard) .

- Via programmering med hjälp av Partner Center Managed API.

- Via programmering med hjälp av Partner Center REST API.

| Lär dig mer om dessa scenarier som stöds:  | Se den här resursen:     |
|----------------------------------|--------------------------|
| **Analys:** Lär dig hur du hämtar analys data om Azure-användning, prenumerationer, licenser eller hänvisningar.         | [Analys](usage-analytics.md)  |
| **Gransknings åtgärder:** Lär dig hur du hämtar historiska gransknings poster för aktivitet och åtgärder i Partner Center. | [Granskningsåtgärder](audit.md)                     |
| **Enhets distributioner:** Lär dig mer om enhets konfigurations principer, arbeta med enhets batchar och metadata för enheten. I dessa scenarier ingår att lägga till, ta bort, uppdatera och hämta enhets konfigurations principer.    | [Enhetsdistribution](device-deployment.md)  |
| **Konton och profiler:** Lär dig hur du hämtar eller uppdaterar partner fakturerings profiler, juridiska profiler, MPN profil, affärs profiler eller support profiler. Du kan också få en lista över kunder eller indirekta åter försäljare. | [Hantera konton och profiler](manage-profiles-and-information.md)                                                                        |
| **Fakturering:** Lär dig mer om områden som att ändra fakturerings cykeln, få Azure-priser och Azures användnings poster, få fakturor, få partners aktuella konto balans eller få kund tjänst kostnader.  | [Hantera fakturering](manage-billing.md)   |
| **Azure-utgifter:** Få information om Azure-utgifter och partner användning, användning av kund prenumerationer, mätnings användning och kund användnings budgetar. Scenarier innehåller också information om hur du uppdaterar en kund användnings budget. | [Utgift i Azure](azure-spending.md)  |
| **Hantera kund konton:** Lär dig hur du utför många aspekter av kund konto hantering, till exempel att skapa och ta bort kund konton eller kund användar konton, hantera och verifiera kund konto information, hantera användar konton och tilldela licenser.  | [Hantera kunder](manage-customers.md)  |
| **Hantera order:** Lär dig allt du kan använda för att hantera kund beställningar och prenumerationer program mässigt. Det här området omfattar att köpa Azure-reservationer, skapa order, Hämta erbjudanden från katalogen och hantera utvärderings versioner av utvärderings versioner.   | [Hantera beställningar](manage-orders.md)  |
| **Tillhandahålla support:** Lär dig hur du administrerar tjänster för en kund, hur du hämtar eller uppdaterar support kontakter för en prenumeration och hur du hanterar tjänst begär Anden.  | [Ge support](provide-support.md)   |
| **Hänvisningar:** Lär dig hur du skapar en hänvisning, hämtar en lista över referenser eller uppdaterar en hänvisning.  | [Referenser](/partner/develop/referrals)  |
| **Verktyg:** Lär dig hur du verifierar en adress, hämtar regler för adress formatering per marknad, kontrollerar domänens tillgänglighet, tar bort ett kund konto från sandbox-integrering eller hämtar en post för partner Center-aktivitet. | [Verktyg](utilities.md)  |
| **Säkerhet:** Lär dig mer om REST-API: er relaterade till Multi-Factor Authentication (MFA) i Partner Center. Dessa API: er hjälper dig att genomdriva MFA för varje användar konto i din partner klient.  | [Status för partner säkerhets krav](partner-security-requirements.md)  |

## <a name="next-steps"></a>Nästa steg

- [Se exempel för partner Center](partner-center-samples.md)
- [Lär dig hur du kommer igång](get-started.md)