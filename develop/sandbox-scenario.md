---
title: Partnerfunktioner för sandbox-miljö som stöder återförsäljarrelation
description: Partner sand Box har möjlighet att stödja relationer mellan partnern och kunden
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711873"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a>Partnerfunktioner för sandbox-miljö som stöder återförsäljarrelation

**Gäller för:**

- Partnercenter
- Partnercenter drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Den här artikeln förklarar vad som stöds i sand boxen för åter försäljares relationer mellan partnern och kunden. 

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter för partner Center-kontot. Sandbox-scenariot stöder autentisering med både den fristående appen och appens och användarens autentiseringsuppgifter.
- Ett kund-ID (kund-Tenant-ID). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard/home)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID (kund-Tenant-ID).
- Alla Azure Reserved Virtual Machine Instances-och program inköps order måste annulleras innan du tar bort en kund från sandbox-tipset.

## <a name="scenarios-supporting-reseller-relationship"></a>Scenarier som stöder åter försäljarens relation

1.  I sand Box Direct Bill partners och indirekta leverantörer kan du skapa relationer med den begränsade kunden. 
2.  Sand Box Direct Bill partners och indirekta leverantörer kan inte bjuda in sandbox-kunder.



### <a name="in-the-sandbox"></a>I sandbox

**Direkta fakturerings partner**:

• Kan lägga till befintliga kunder

• Det går inte att begära relationer med nya kunder

**Indirekta leverantörer**:

• Kan lägga till befintliga kunder

• Det går inte att begära relationer med nya kunder

• Det går inte att ha en relation med en indirekt åter försäljare

**Indirekt åter försäljare**: (kommer snart)

• Kan ha relationer med befintliga kunder

• Det går inte att begära nya relationer eller lägga till nya kunder

### <a name="in-partner-center"></a>I Partner Center

**Direkta fakturerings partner**:

• Kan lägga till nya kunder

• Kan begära relationer med nya kunder

**Indirekta leverantörer**:

• Kan lägga till nya kunder

• Kan begära relationer med nya kunder

• Kan ha relationer med indirekta åter försäljare

**Indirekta åter försäljare**:

• Det går inte att lägga till nya kunder

• Kan begära relationer med nya kunder

3. I sandbox direkt fakturerings partner och indirekta leverantörer kan du ta bort åter försäljarens relation från användar gränssnittet och API: t för partner Center.

4. Den begränsade åter försäljarens relation kommer att anropa ta bort kund-AP. Detta tar bort relationen och tar bort kund klienten. {baseURL}/v1/Customers/{customer-Tenant-id}

Följ den [ta bort åter försäljarens relation](remove-a-reseller-relationship-with-a-customer.md) för kunden för mer information. Det finns dock vissa skillnader mellan produkt-och sandbox-funktionerna.

### <a name="request-syntax"></a>SYNTAX FÖR BEGÄRAN

|**Metod**|**Ta bort**|
|-------------|------------|
|Ta bort|{baseURL}/v1/Customers/{customer-Tenant-id} |

Begär ande texten none

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](./error-codes.md).

## <a name="next-steps"></a>Nästa steg

- [Aktivera sandbox-prenumerationer för Azure Marketplace-produkter](activate-sandbox-subscription-azure-marketplace-products.md)

- [Avbryta en order från sandbox](cancel-an-order-from-the-integration-sandbox.md)

- [Testa och felsök](test-and-debug.md)