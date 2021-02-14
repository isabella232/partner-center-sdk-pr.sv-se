---
title: Testa och felsöka med integration sandbox
description: Lär dig hur du använder ditt partner Center integration sandbox-konto (och relaterade token) för att testa och felsöka koden så att du inte råkar ta nya kostnader.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3ff4a7ec3ad984b09c60d3d820423c614fb8020d
ms.sourcegitcommit: 9f8ba784171ab4f980ed0c60ef6f2323849c4a98
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/14/2021
ms.locfileid: "100499889"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Testa och Felsök med ditt partner Center integration sandbox för att undvika att betala oväntade kostnader

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Om du vill testa din kod bör du använda ditt konto för integration i begränsat läge i Partner Center (och motsvarande token) så att du inte råkar ut för nya avgifter som företaget ansvarar för att betala. Mer information om den här test-i-produktions-miljön (TiP) finns i [Konfigurera API-åtkomst i Partner Center](set-up-api-access-in-partner-center.md).

## <a name="integration-sandbox-constraints"></a>Sandbox-begränsningar för integrering

Om du kör automatisk generering av verifierings test, utför testning i produktion eller utför manuell testning i integrations sand boxen, kan du uppnå Max gränsen för integration sandbox. Dessa gränser är 75 kunder, 5 prenumerationer per kund och 25 licenser per prenumeration.

25-licens gränsen innebär att du inte kan skaffa ett erbjudande i sand boxen som har ett lägsta licens krav som överstiger 25 licenser. Den här begränsningen omfattar test versioner.

Det finns olika fakturor och avstämnings filer som är tillgängliga i sand Box miljöer, men alla är inte tillgängliga på äldre eller moderna plattformar. Verifiera tabellen nedan om du vill veta mer.

| **Filer**                    | **Tillgänglig i äldre** | **Tillgängligt i modern** |
| ---------------------------- | ------------------------ | ------------------------ |
| Faktura-PDF                  | Inga                       | Ja                      |
| Faktura avstämnings fil | Inga                       | Ja                      |
| Faktura uppskattnings fil       | Inga                       | Ja                      |
| Daglig fakturerings användnings fil     | Inga                       | Ja                      |
| Daglig, ej fakturerad användnings fil   | Inga                       | Ja                      |


### <a name="azure-plan"></a>Azure-plan

Som standard kan partners inte etablera Azure-planer med sina sandbox-konton. Partner som behöver göra detta med sitt sandbox-konto måste gälla för åtkomst. Om du vill använda för åtkomst kontaktar du din Microsoft-konto Manager eller företags kontakt. Partner som tidigare har tillämpat för åtkomst till att etablera Microsoft Azure-prenumerationer (MS-AZR-0145P) i sina sandbox-konton behöver inte tillämpa för åtkomst igen. De kommer att beviljas åtkomst för att etablera Azure-planer automatiskt.

För partner vars sandbox-konton har godkänts för att tillhandahålla Azure-planer gäller följande begränsningar:

- Varje begränsat partner konto kan ha upp till 10 Azure-planer i alla kund klienter (oavsett hur planerna fördelas mellan kunderna).

- En direkt fakturerings partner kan skapa upp till en Azure-plan per kund klient.

- En indirekt Provider kan skapa upp till tre Azure-planer per kund klient organisation (för olika indirekta åter försäljare som anges som partner-of-Record).

- Varje Azure-plan kan ha upp till tre Azure-prenumerationer.

- Varje CSP Azure-prenumeration under ditt sandbox-konto är begränsad till fyra virtuella dator kärnor per Data Center. Därför kan du inte etablera VM-SKU: er som kräver fler än fyra VM-kärnor. Vissa specialiserade VM-SKU: er, till exempel GPU-kärnor, undantas också.

- Varje tjänst i sand Box partner har en utgifts gräns på $2000 (USD) per fakturerings period för alla Azure-planer. När en partner når ut i utgifts gränsen inaktive ras alla Azure-planer tillfälligt tills nästa fakturerings period.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Cloud Solution Provider (CSP) Azure-prenumeration erbjuder

Prenumerations erbjudanden för CSP Azure är inte längre tillgängliga som standard till sandbox-konton. Dessa inkluderar MS-AZR-0146P, MS-AZR-DE-0146P och MS-AZR-USGOV-0146P för CSP Azure-prenumerationer i Microsofts offentliga moln, tyska moln och myndighets moln. Partner som behöver åtkomst till dessa erbjudanden med sitt sandbox-konto måste gälla för åtkomst. Om du vill använda för åtkomst, diskutera med din Microsoft-konto Manager eller företags kontakt.

Följande begränsningar gäller för partner vars sandbox-konton har godkänts för CSP: er för Azure-prenumerationer:

- Du kan ha upp till högst 375 aktiva prenumerationer (75 kunder x 5 prenumerationer per kund). Men endast 10 av vilka kan vara CSP Azure-prenumerationer.

- När en CSP Azure-prenumeration når $200 av Azure-användning, inaktive ras tillfälligt resurserna tills nästa fakturerings period. Den betraktas fortfarande som en aktiv prenumeration och räknas till gränsen för 10 aktiva Azure-prenumerationer.

- Varje CSP Azure-prenumeration under ditt sandbox-konto är begränsad till fyra virtuella dator kärnor per Data Center. Därför kan du inte etablera VM-SKU: er som kräver fler än fyra VM-kärnor. Vissa specialiserade VM-SKU: er, till exempel GPU-kärnor, undantas också.

> [!Important]
> Alla befintliga CSP Azure-prenumerationer som har etablerats med sandbox-konton före den 1 augusti 2018 stöds inte längre och kommer att tas ur drift av Microsoft mellan 16 oktober 31 oktober 2018. När prenumerationerna har avetablerats kan de inte aktive ras igen och associerade data är inte längre tillgängliga. Partner som har värdefull data som lagras under dessa prenumerationer måste säkerhetskopiera data före den 16 oktober 2018.

### <a name="azure-reserved-vm-instance"></a>Azure reserverad VM-instans

Om du [köper en Azure reserverad VM-instans](purchase-azure-reservations.md) med ditt sandbox-konto är du begränsad till två VM-instanser per kund. Du är också begränsad till att endast välja från följande Azure reserverad VM instance-produkt SKU: er:

| Produkt titel  | Giltighets datum  | SKU-rubrik                                               | Region [ArmRegionName] | Instans nyckel [ArmSkuName] | Varaktighet | ID för förbruknings mätare       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, KR, södra, 1 år    | Koreasödra             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, östra USA, 1 år     | USA, östra                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, USA, väst 2, 1 år   | USA, västra 2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, norra centrala USA, 1 år    | usanorracentrala | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B-serien       | 12/1/2017 0:00  | Reserverad VM-instans, Standard_B1s, CA, öst, 1 år     | Indien             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Prenumerationer på kommersiella Marketplace-produkter

När du har [skapat en prenumeration på kommersiella Marketplace SaaS-produkter](create-subscription-azure-marketplace-products.md)måste du hämta en anpassad aktiverings länk från Partner Center och besöka utgivarens webbplats för att slutföra installationen. Prenumerations faktureringen påbörjas bara efter att installationen har slutförts.

I sandbox-miljön för KRYPTOGRAFI finns det ingen integrering med ISV: er. Om du försöker hämta en aktiverings länk från Partner Center kommer en dummy-länk att returneras. Du kan inte använda den här dummy-länken för att slutföra installations processen på utgivarens webbplats. Om du vill använda det begränsade kontot för integration för att testa faktureringen för prenumerationer på kommersiella Marketplace SaaS-produkter, se [Aktivera en Sandbox-prenumeration för kommersiella Marketplace-produkter](activate-sandbox-subscription-azure-marketplace-products.md) i stället. Prenumerations faktureringen påbörjas efter en lyckad aktivering.

Om du vill rensa i slutet av test körningen så finns det utrymme för nästa avrundnings test, se följande artiklar:

- [Ta bort ett kundkonto från sandbox-miljön för integrering](delete-a-customer-account-from-the-integration-sandbox.md)

- [Minska antalet prenumerationer](change-the-quantity-of-a-subscription.md)

- [Pausa en prenumeration](suspend-a-subscription.md) så att du kan ta bort den.

## <a name="best-practices-for-rest-development"></a>Metod tips för REST-utveckling

- Använd ett verktyg för nätverks spårning så att du kan se din begäran, svaret och om det fanns några fel i HTTP-statuskoden i svaret. Mer information om fel hantering finns i [partner Center rest-felkoder](error-codes.md).

- Använd ett nytt korrelations-ID för varje anrop som görs till Partner Center-REST API. Den här metoden ger bättre loggning och hjälper till vid fel sökning. Mer information finns i [partner Center rest-rubriker](headers.md).

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Felsökningstips för vanliga problem med REST

- Granska alla sidhuvud egenskaper, inklusive URL-och API-version.

- Se till att egenskaper tas med vid behov och korrekt formaterade.

- Felaktig mat ris formatering är ett vanligt fel.

- **ETags** är temporära och kommer därför inte att lagras. När ett funktions anrop kräver en **ETags** använder du det senaste **ETags** -värdet genom att hämta resursen igen. **ETags** -värden ska inkluderas inom dubbla citat tecken, t. ex. en sträng:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
