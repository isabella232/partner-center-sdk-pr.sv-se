---
title: Sandbox-funktioner för återförsäljarrelation
description: Sandbox-miljön för partner har möjlighet att stödja relationer mellan partnern och kunden
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14133627a607c6e4151a90c37565e5f62823345e007eb55d87100de25d1f161a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996860"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a>Sandbox-funktioner för återförsäljarrelation

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Den här artikeln förklarar vad som stöds i sandbox-miljön för återförsäljarrelationer mellan partnern och kunden. 

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter för Partnercenter-konto. Sandbox-scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.
- Ett kund-ID (kund-klient-ID). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard/home) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t (kund-klient-ID).
- Alla Azure Reserved Virtual Machine Instances och programvaruinköpsorder måste avbrytas innan du tar bort en kund från sandbox-miljön för Tip-integrering.

## <a name="scenarios-supporting-reseller-relationship"></a>Scenarier som stöder återförsäljarrelation

1.  Direktfaktureringspartner och indirekta leverantörer i sandbox-miljön kan skapa relationer med Sandbox-kunden. 
2.  Sandbox-direktfaktureringspartner och indirekta leverantörer kan inte bjuda in Sandbox-kunder.

3. Direktfaktureringspartner och indirekta leverantörer i sandbox-miljö kan ta bort återförsäljarrelationer från Partner Center-gränssnittet och API:et.

4. Sandbox Remove Reseller Relationship anropar Ta bort kund-AP. Detta tar bort relationen och kundklientorganisationen. {baseURL}/v1/Customers/{customer-Tenant-id}


    ### <a name="in-the-sandbox"></a>I sandbox-miljön

    **Direktfaktureringspartner:**

    - Kan lägga till befintliga kunder

    - Det går inte att begära relationer med nya kunder

    **Indirekta leverantörer:**

    - Kan lägga till befintliga kunder

    - Det går inte att begära relationer med nya kunder

    - Det går inte att ha en relation med en indirekt återförsäljare

    **Indirekt återförsäljare:** 

    -   Kan ha relationer med befintliga kunder

    -   Det går inte att begära nya relationer eller lägga till nya kunder

    ### <a name="in-partner-center"></a>I Partnercenter

    **Direktfaktureringspartner:**

    -   Kan lägga till nya kunder

    -   Kan begära relationer med nya kunder

    **Indirekta leverantörer:**

    -   Kan lägga till nya kunder

    -   Kan begära relationer med nya kunder

    -   Kan ha relationer med indirekta återförsäljare

    **Indirekta återförsäljare:**

    -   Det går inte att lägga till nya kunder

    -   Kan begära relationer med nya kunder


Mer information [finns i Ta](remove-a-reseller-relationship-with-a-customer.md) bort återförsäljarrelation för kunden. Det finns dock vissa skillnader mellan funktionerna Product och Sandbox.

### <a name="request-syntax"></a>BEGÄRANDESYNTAX

|**Metod**|**Ta bort**|
|-------------|------------|
|Ta bort|{baseURL}/v1/Customers/{customer-Tenant-id} |

Begärandetexten Ingen

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](./error-codes.md)

## <a name="next-steps"></a>Nästa steg

- [Aktivera Sandbox-prenumerationer för Azure Marketplace produkter](activate-sandbox-subscription-azure-marketplace-products.md)

- [Avbryta en beställning från sandbox-miljön](cancel-an-order-from-the-integration-sandbox.md)

- [Testa och felsök](test-and-debug.md)