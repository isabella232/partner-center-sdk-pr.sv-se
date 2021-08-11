---
title: Köp katalogobjekt
description: Så här köper du katalogobjekt med partnercenter-API:et.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 34560ceff2721a805d50cd4bf0702f6e7cf6f473db3f38ee52ea439b7355b786
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997352"
---
# <a name="purchase-catalog-items"></a>Köp katalogobjekt

Följande scenario visar den allmänna processen för att köpa objekt från katalogen med hjälp av Partner Center-API:et.

## <a name="discovery"></a>Identifiering

Välj produkter och lagerhållningsenheter (SKU:er) och kontrollera deras tillgänglighet med hjälp av följande Partner Center API-modeller:

- [Produkt](product-resources.md#product) – en grupperingskonstruktion för köpbara varor eller tjänster. En produkt i sig är inte ett köpbart objekt.
- [SKU](product-resources.md#sku) – en köpbar SKU under en produkt. De representerar olika former av produkten.
- [Tillgänglighet](product-resources.md#availability) – En konfiguration där en SKU är tillgänglig för inköp (till exempel land, valuta och branschsegment).

Utför följande steg för att köpa ett objekt från katalogen:

1. Identifiera och hämta den produkt och SKU som du vill köpa.

   - [Hämta en lista över produkter](get-a-list-of-products.md)
   - [Hämta en produkt med hjälp av produkt-ID:t](get-a-product-by-id.md)
   - [Hämta en lista över SKU:er för en produkt](get-a-list-of-skus-for-a-product.md)
   - [Hämta en SKU med hjälp av SKU-ID:t](get-a-sku-by-id.md)

2. Kontrollera inventeringen för en SKU. Det här steget behövs bara för SKU:er som är taggade med **ett InventoryCheck-värde** [i egenskapen purchasePrerequisites.](product-resources.md#sku)

   - [Kontrollera lager](check-inventory.md)

3. Hämta [tillgängligheten](product-resources.md#availability) för [SKU:n](product-resources.md#sku). Du behöver **CatalogItemId för** tillgängligheten när du gör beställningen. Använd något av följande API:er för att hämta det här värdet:

   - [Hämta en lista över tillgänglighet för en SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Hämta en tillgänglighet med hjälp av tillgänglighets-ID:t](get-an-availability-by-id.md)

## <a name="order-submission"></a>Skicka order

Gör följande om du vill skicka in katalogobjektsordningen:

1. Skapa en [kundvagn](cart-resources.md) för den samling katalogobjekt som du tänker köpa. När du skapar en kundvagn [grupperas kundvagnsraderna](cart-resources.md#cartlineitem) automatiskt baserat på vad som kan köpas tillsammans i samma [order.](order-resources.md)

   - [Skapa en kundvagn](create-a-cart.md)
   - [Uppdatera en kundvagn](update-a-cart.md)

2. Kolla in kundvagnen. När du checkar ut en kundvagn skapas en [order.](order-resources.md)

   - [Checka ut kundvagnen](checkout-a-cart.md)

## <a name="get-order-details"></a>Hämta beställningsinformation

Du kan hämta information om en enskild order med hjälp av order-ID:t eller hämta en lista över beställningar för en kund. Det finns en fördröjning på upp till 15 minuter från det att en order skickas tills den visas i en lista över en kunds beställningar.

- Information om en enskild order med hjälp av order-ID:n finns i Hämta en beställning per [ID.](get-an-order-by-id.md)

- Se [Hämta alla en kunds beställningar för att få](get-all-of-a-customer-s-orders.md) en lista över beställningar för en kund med hjälp av kund-ID:t.

- Se [Hämta en](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) lista över beställningar efter kund och faktureringscykeltyp [](product-resources.md#billingcycletype) för att få en lista över beställningar för en kund efter faktureringsperiodstyp så att du kan visa en lista över beställningar av katalogobjekt (en gång-avgifter) och beställningar som faktureras per år eller månad separat.

## <a name="lifecycle-management"></a>Livscykelhantering

Som en del av att hantera livscykeln för dina katalogobjekt i Partnercenter kan du hämta information om [katalogobjektets](entitlement-resources.md)berättiganden och hämta reservationsinformation med hjälp av reservationsbeställnings-ID:t. Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Följande scenarier visar hur du programmatiskt visar kundens fakturor [och](invoice-resources.md)hämtar dina kontosaldon och sammanfattningar som inkluderar engångsavgifter för katalogobjekt.

### <a name="balance-and-payment"></a>Saldo och betalning

Information om hur du hämtar aktuellt kontosaldo i din standardvalutatyp som är ett saldo för både återkommande avgifter och engångsavgifter (katalogobjekt) finns i Hämta [ditt aktuella kontosaldo.](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo och betalning i flera valutor

Information om hur du hämtar ditt aktuella kontosaldo och en samling fakturasammanfattningar som innehåller en fakturasammanfattning med både återkommande avgifter och engångsavgifter för var och en av kundens valutatyper finns i [Hämta fakturasammanfattningar.](get-invoice-summaries.md)

### <a name="invoices"></a>Fakturor

Information om hur du hämtar en samling fakturor som visar både återkommande och engångsavgifter finns i [Hämta en samling fakturor.](get-a-collection-of-invoices.md) 

### <a name="single-invoice"></a>Enskild faktura

Information om hur du hämtar en specifik faktura med hjälp av faktura-ID:t [finns i Hämta en faktura via ID](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Försoning

Information om en samling fakturaradsobjekt (avstämningsradsobjekt) för ett specifikt faktura-ID finns i [Hämta fakturaradsobjekt.](get-invoiceline-items.md)  

### <a name="download-an-invoice-as-a-pdf"></a>Ladda ned en faktura som en PDF

Information om hur du hämtar ett fakturautdrag i PDF-format med hjälp av ett faktura-ID finns [i Hämta ett fakturautdrag](get-invoice-statement.md).
