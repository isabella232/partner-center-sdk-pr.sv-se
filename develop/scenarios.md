---
title: Partner Center API-scenarier
description: Lär dig hur Molnlösningsleverantör-programpartner kan använda Partner Center-API:et för att programmatiskt hantera kundkonton, beställningar, support och fakturering.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a5aac400e115ef0e58452e41edd9846d683d0b6912a9f651ea49d75d5f15bbf7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989499"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>Partner Center API-scenarier som gör att du kan hantera kundkonton programmatiskt

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Center för Microsoft Cloud for US Government

I den här artikeln beskrivs några av de sätt som partner i Molnlösningsleverantör-programmet kan använda PartnerCenter-API:et för att programmatiskt hantera områden som:

- Kundkonton
- Order
- Prenumerationer
- Support
- Fakturering

Det finns olika versioner av Partnercenter som innehåller olika funktioner. Alla scenarier stöds inte i alla versioner av Partnercenter. Mer information finns i [Utveckla för Partner Center för Microsoft National Cloud.](developing-for-partner-center-for-microsoft-national-cloud.md)

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>Scenarier som stöds av Partnercenter-SDK

Alla följande scenarier kan utföras på tre olika sätt:

- Manuellt i [instrumentpanelen i Partnercenter.](https://partner.microsoft.com/dashboard)

- Programmässigt med partnercenter-hanterat API.

- Programmässigt med partnercenter-REST API.

| Mer information om dessa scenarier som stöds:  | Se den här resursen:     |
|----------------------------------|--------------------------|
| **Analys:** Lär dig hur du hämtar analysdata om Azure-användning, prenumerationer, licenser eller hänvisningar.         | [Analys](usage-analytics.md)  |
| **Granskningsåtgärder:** Lär dig hur du hämtar historiska granskningsposter för aktiviteter och åtgärder i Partnercenter. | [Granskningsåtgärder](audit.md)                     |
| **Enhetsdistributioner:** Lär dig mer om enhetskonfigurationsprinciper, arbete med enhetsbatchar och enhetsmetadata. Dessa scenarier omfattar att lägga till, ta bort, uppdatera och hämta principer för enhetskonfiguration.    | [Enhetsdistribution](device-deployment.md)  |
| **Konton och profiler:** Lär dig hur du hämtar eller uppdaterar partnerfaktureringsprofiler, juridiska profiler, MPN-profil, företagsprofiler eller supportprofiler. Du kan också hämta en lista över kunder eller indirekta återförsäljare. | [Hantera konton och profiler](manage-profiles-and-information.md)                                                                        |
| **Fakturering:** Lär dig mer om områden som att ändra faktureringscykeln, hämta Azure-priser och Azure-användningsposter, hämta fakturor, hämta partnerns aktuella kontosaldo eller få kundtjänstkostnader.  | [Hantera fakturering](manage-billing.md)   |
| **Azure-utgifter:** Få information om Azure-utgifter och partneranvändning, användning av kundprenumerationer, förbrukningsförbrukning och budgetar för kundanvändning. Scenarier omfattar även hur du uppdaterar en kundanvändningsbudget. | [Utgift i Azure](azure-spending.md)  |
| **Hantera kundkonton:** Lär dig hur du gör många aspekter av kundkontohantering, till exempel att skapa och ta bort kundkonton eller en kunds användarkonton, hantera och verifiera kundkontoinformation, hantera användarkonton och tilldela licenser.  | [Hantera kunder](manage-customers.md)  |
| **Hantera beställningar:** Lär dig hur du kan hantera kundorder och prenumerationer programmatiskt. Det här området omfattar att köpa Azure-reservationer, skapa beställningar, hämta erbjudanden från katalogen och hantera erbjudanden för utvärderingskonvertering.   | [Hantera beställningar](manage-orders.md)  |
| **Tillhandahålla support:** Lär dig hur du administrerar tjänster för en kund, hur du hämtar eller uppdaterar supportkontakter för en prenumeration och hur du hanterar tjänstbegäranden.  | [Ge support](provide-support.md)   |
| **Referenser:** Lär dig hur du skapar en referens, hämtar en lista över hänvisningar eller uppdaterar en referens.  | [Referenser](/partner/develop/referrals)  |
| **Verktyg:** Lär dig hur du verifierar en adress, hämtar adressformateringsregler efter marknad, verifierar domänens tillgänglighet, tar bort ett kundkonto från sandbox-miljön för integrering eller hämtar en post för PartnerCenter-aktiviteten. | [Verktyg](utilities.md)  |
| **Säkerhet:** Lär dig mer om REST-API:er som rör multifaktorautentisering (MFA) i Partnercenter. Dessa API:er hjälper dig att tillämpa MFA för varje användarkonto i din partnerklientorganisation.  | [Status för partnersäkerhetskrav](partner-security-requirements.md)  |

## <a name="next-steps"></a>Nästa steg

- [Se PartnerCenter-exempel](partner-center-samples.md)
- [Lär dig hur du kommer igång](get-started.md)