---
title: Testa och felsöka med sandbox-miljön för integrering
description: Lär dig hur du använder ditt sandbox-konto för partnercenterintegrering (och relaterade token) för att testa och felsöka din kod så att du inte av misstag debiteras nya avgifter.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7a9d7755cd9f493f44f9a7bbf613e0f80cf7b4ac
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530114"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Testa och felsök med sandbox-miljön för Partner Center-integrering för att undvika att betala oväntade avgifter

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Om du vill testa din kod bör du använda ditt sandbox-konto för integrering i Partnercenter (och motsvarande token) så att du inte av misstag debiteras nya avgifter som ditt företag ansvarar för att betala. Mer information om den här Test-in-Production-miljön (TiP) finns i [Konfigurera API-åtkomst i Partnercenter.](set-up-api-access-in-partner-center.md)

## <a name="integration-sandbox-constraints"></a>Begränsningar för sandbox-miljö för integrering

Om du kör automatiska byggverifieringstester, utför testning i produktion eller utför manuell testning i sandbox-miljön för integrering kan du nå maxgränserna för sandbox-miljön för integrering. Dessa gränser är 75 kunder, 5 prenumerationer per kund och 25 licenser per prenumeration.

Gränsen på 25 licenser innebär att du inte kan skaffa ett erbjudande i sandbox-miljön som har ett minimikrav på licens som överskrider 25 licenser. Den här begränsningen omfattar utvärderingsversioner.

Det finns olika faktura- och avstämningsfiler i sandbox-miljöerna, men alla är inte tillgängliga på äldre eller moderna plattformar. Kontrollera tabellen nedan om du vill veta mer.

| **Filer**                    | **Tillgänglig i äldre** | **Tillgängligt i Modern** |
| ---------------------------- | ------------------------ | ------------------------ |
| Faktura-PDF                  | Inga                       | Ja                      |
| Fakturaavstämningsfil | Inga                       | Ja                      |
| Fakturauppskattningsfil       | Inga                       | Ja                      |
| Fil för daglig faktureringsanvändning     | Inga                       | Ja                      |
| Fil för daglig ej fakturerad användning   | Inga                       | Ja                      |


### <a name="azure-plan"></a>Azure-plan

Som standard kan partner inte etablera Azure-planer med sina sandbox-konton. Partner som behöver göra det med sitt sandbox-konto måste ansöka om åtkomst. Om du vill ansöka om åtkomst kontaktar du din Microsoft-konto chef eller företagskontakt. Partner som tidigare har sökt åtkomst för att etablera Microsoft Azure-prenumerationer (MS-AZR-0145P) i sina sandbox-konton behöver inte ansöka om åtkomst igen. De beviljas automatiskt åtkomst för att etablera Azure-planer.

Följande begränsningar gäller för partner vars sandbox-konton har godkänts för att etablera Azure-planer:

- Varje sandbox-partnerkonto kan ha upp till 10 Azure-planer för alla kundklienter (oavsett hur prenumerationerna fördelas mellan kunderna).

- En partner för direktfakturering kan skapa upp till en Azure-plan per kundklientorganisation.

- En indirekt leverantör kan skapa upp till tre Azure-planer per kundklientorganisation (för olika indirekta återförsäljare som anges som Partner-of-Record).

- Varje Azure-plan kan ha upp till tre Azure-prenumerationer.

- Varje CSP Azure-prenumeration under ditt sandbox-konto är begränsad till fyra kärnor för virtuella datorer per datacenter. Därför kan du inte etablera VM-SKU:er som kräver fler än fyra vm-kärnor. Vissa specialiserade SKU:er för virtuella datorer, till exempel GPU-kärnor, undantas också.

- Varje sandbox-partnerkonto har en utgiftsgräns på 2 000 USD per faktureringsperiod för alla Azure-planer. När en partner når maxgränsen inaktiveras alla Azure-planer tillfälligt till nästa faktureringsperiod.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Azure Molnlösningsleverantör prenumerationserbjudanden för Molnlösningsleverantör (CSP)

CSP Azure-prenumerationserbjudanden är inte längre tillgängliga som standard för sandbox-konton. Dessa inkluderar MS-AZR-0146P, MS-AZR-DE-0146P och MS-AZR-USGOV-0146P för CSP Azure-prenumerationer i Microsoft Public Cloud, tyska moln respektive Government Cloud. Partner som behöver åtkomst till dessa erbjudanden med sitt sandbox-konto måste ansöka om åtkomst. Om du vill ansöka om åtkomst kan du diskutera med Microsoft-konto chef eller företagskontakt.

För partner vars sandbox-konton har godkänts för CSP Azure-prenumerationserbjudanden gäller följande begränsningar:

- Du kan ha upp till 375 aktiva prenumerationer (75 kunder x 5 prenumerationer per kund). Men endast 10 av dessa kan vara Azure-prenumerationer för CSP.

- När en Azure-prenumeration hos CSP når 200 USD av Azure-användningen inaktiveras dess resurser tillfälligt till nästa faktureringsperiod. Det betraktas fortfarande som en aktiv prenumeration och räknas mot gränsen på 10 aktiva Azure-prenumerationer.

- Varje CSP Azure-prenumeration under ditt sandbox-konto är begränsad till fyra kärnor för virtuella datorer per datacenter. Därför kan du inte etablera VM-SKU:er som kräver fler än fyra vm-kärnor. Vissa specialiserade SKU:er för virtuella datorer, till exempel GPU-kärnor, undantas också.

> [!Important]
> Alla befintliga CSP Azure-prenumerationer som etablerats med sandbox-konton före den 1 augusti 2018 stöds inte längre och kommer att avetableras av Microsoft mellan 16 oktober och 31 oktober 2018. När prenumerationerna har avetableats kan de inte återaktiveras och associerade data är inte längre tillgängliga. Partner som har värdefulla data som lagras under dessa prenumerationer måste bladet vara tillbaka före den 16 oktober 2018.

### <a name="azure-reserved-vm-instance"></a>Azure Reserved VM-instans

Om du köper [en azure-reserverad VM-instans](purchase-azure-reservations.md) med ditt sandbox-konto är du begränsad till två VM-instanser per kund. Du är också begränsad till att bara välja från följande produkt-SKU:er för azure-reserverade VM-instanser:

| Produkttitel  | Giltighetsdatum  | Rubrik för SKU                                               | Region [ArmRegionName] | Instansnyckel [ArmSkuName] | Varaktighet | Förbrukningsmätares-ID       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, Sydkorea, södra, 1 år    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, USA, östra, 1 år     | USA, östra                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, USA, västra 2, 1 år   | USA, västra 2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, USA, norra centrala, 1 år    | usanorracentrala | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, Ca, östra, 1 år     | Kanada, västra             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Prenumerationer på produkter på den kommersiella marknadsplatsen

När du har skapat en prenumeration på Den kommersiella marknadsplatsen [för SaaS-produkter](create-subscription-azure-marketplace-products.md)i produktion måste du hämta en anpassad aktiveringslänk från Partnercenter och gå till utgivarens webbplats för att slutföra installationen. Prenumerationsfakturering börjar först när installationen är klar.

I CSP-sandbox-miljön finns det ingen integrering med ISV:er. Om du försöker hämta en aktiveringslänk från Partnercenter returneras en dummylänk. Du kan inte använda den här dummylänken för att slutföra installationen på utgivarens webbplats. Om du vill använda sandbox-kontot för integrering för att testa faktureringen för prenumerationer på SaaS-produkter på den kommersiella marknadsplatsen kan du läsa Aktivera en [sandbox-prenumeration för kommersiella marketplace-produkter i](activate-sandbox-subscription-azure-marketplace-products.md) stället. Prenumerationsfakturering börjar efter aktiveringen.

Om du vill rensa i slutet av testkörningen så att det finns utrymme för nästa testomgång kan du läsa följande artiklar:

- [Ta bort ett kundkonto från sandbox-miljön för integrering](delete-a-customer-account-from-the-integration-sandbox.md)

- [Minska kvantiteten för en prenumeration](change-the-quantity-of-a-subscription.md)

- [Pausa en prenumeration](suspend-a-subscription.md) så att du kan ta bort den.

## <a name="best-practices-for-rest-development"></a>Metodtips för REST-utveckling

- Använd ett nätverksspårningsverktyg så att du kan se din begäran, svaret och om det finns några fel i HTTP-statuskoden i svaret. Mer information om felhantering finns i [Partner Center REST-felkoder.](error-codes.md)

- Använd ett nytt korrelations-ID för varje anrop till Partnercenter REST API. Den här metoden säkerställer bättre loggning och hjälper till vid felsökning. Mer information finns i [Partner Center REST-huvuden.](headers.md)

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Felsökningstips för vanliga problem med REST

- Granska alla huvudegenskaper, inklusive URL och API-version.

- Se till att egenskaperna inkluderas vid behov och är korrekt formaterade.

- Felaktig matrisformatering är ett vanligt fel.

- **ETags** är tillfälliga och bör därför inte lagras. När ett funktionsanrop kräver **en ETags** använder du det senaste **ETags-värdet** genom att hämta resursen igen. **ETags-värden** ska inkluderas inom dubbla citattecken, till exempel en sträng:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
