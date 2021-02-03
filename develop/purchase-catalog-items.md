---
title: Köp katalogobjekt
description: Så här köper du katalog objekt med API för partner Center.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768883"
---
# <a name="purchase-catalog-items"></a>Köp katalogobjekt

**Gäller för**

- Partnercenter

Följande scenario visar den allmänna processen för att köpa objekt från katalogen med hjälp av Partner Center-API: et.

## <a name="discovery"></a>Identifiering

Välj produkter och SKU: er och kontrol lera deras tillgänglighet med hjälp av följande Partner Center API-modeller:

- [Produkt](product-resources.md#product) – en grupperings konstruktion för köpbara-varor eller-tjänster. En produkt som själva är inte ett köpbara-objekt.
- [SKU](product-resources.md#sku) – en köpbara lagerhållnings enhet (SKU) under en produkt. Dessa representerar olika former av produkten.
- [Tillgänglighet](product-resources.md#availability) – en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta och bransch segment).

Utför följande steg för att köpa ett objekt från katalogen:

1. Identifiera och hämta den produkt och SKU som du vill köpa.

   - [Hämta en lista över produkter](get-a-list-of-products.md)
   - [Hämta en produkt med produkt-ID](get-a-product-by-id.md)
   - [Hämta en lista över SKU: er för en produkt](get-a-list-of-skus-for-a-product.md)
   - [Hämta en SKU med SKU-ID](get-a-sku-by-id.md)

2. Kontrol lera inventeringen för en SKU. Det här steget behövs bara för SKU: er som är taggade med ett **InventoryCheck** -värde i egenskapen [purchasePrerequisites](product-resources.md#sku) .

   - [Kontrollera lager](check-inventory.md)

3. Hämta [tillgänglighet](product-resources.md#availability) för SKU: [n](product-resources.md#sku). Du behöver **CatalogItemId** av tillgängligheten när du placerar ordern. Använd något av följande API: er för att hämta det här värdet:

   - [Hämta en lista över tillgänglighet för en SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Få en tillgänglighet med tillgänglighets-ID: t](get-an-availability-by-id.md)

## <a name="order-submission"></a>Order överföring

Gör så här för att skicka in din katalog objekts ordning:

1. Skapa en [vagn](cart-resources.md) som innehåller den samling av katalog objekt som du vill köpa. När du skapar en varukorg grupperas [vagnens rad objekt](cart-resources.md#cartlineitem) automatiskt utifrån vad som kan köpas tillsammans i samma [ordning](order-resources.md).

   - [Skapa en Shopping vagn](create-a-cart.md)
   - [Uppdatera en Shopping vagn](update-a-cart.md)

2. Kolla in vagnen. Att checka ut en vagns resultat i skapandet av en [order](order-resources.md).

   - [Checka ut vagnen](checkout-a-cart.md)

## <a name="get-order-details"></a>Hämta beställnings information

Du kan hämta information om en enskild order med order-ID: t eller hämta en lista över beställningar för en kund. Det finns en fördröjning på upp till 15 minuter mellan tiden som en beställning skickas och när den visas i en lista över en kunds beställningar.

- Se [Hämta en order efter ID](get-an-order-by-id.md) för att få information om en enskild order med hjälp av order-ID: n.

- Se [Hämta alla kund order](get-all-of-a-customer-s-orders.md) för att få en lista över beställningar för en kund med kund-ID.

- Se [Hämta en lista över beställningar efter kund-och fakturerings cykel typ](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) för att få en lista över beställningar för en kund via [fakturerings cykel typ](product-resources.md#billingcycletype) , så att du kan visa en lista över katalog objekts beställningar (engångs avgifter) och årliga eller månatliga fakturerade beställningar separat.

## <a name="lifecycle-management"></a>Livs cykel hantering

Som en del av att hantera livs cykeln för dina katalog objekt i Partner Center kan du hämta information om dina katalog objekts [rättigheter](entitlement-resources.md)och hämta reservations information med hjälp av reservations orderns ID. Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Följande scenarier visar hur du program mässigt visar din kunds [fakturor](invoice-resources.md)och hur du får dina konto balanser och sammanfattningar som innehåller engångs avgifter för katalog objekt.

### <a name="balance-and-payment"></a>Saldo och betalning

Om du vill hämta aktuellt konto saldo i din standard valuta typ som är en balans mellan både återkommande och engångs kostnader (katalog objekt), se [Hämta ditt aktuella konto saldo](get-the-reseller-s-current-account-balance.md).

### <a name="multi-currency-balance-and-payment"></a>Saldo och betalning för flera valutor

Om du vill hämta ditt aktuella konto saldo och en samling av faktura sammanfattningar som innehåller en faktura sammanfattning med både återkommande och engångs kostnader för var och en av kundens valuta typer, se [Hämta faktura sammanfattningar](get-invoice-summaries.md).

### <a name="invoices"></a>Fakturor

Om du vill hämta en samling fakturor som visar både återkommande och engångs kostnader, se [Hämta en samling fakturor](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Enskild faktura

Information om hur du hämtar en speciell faktura med hjälp av faktura-ID finns i [Hämta en faktura efter ID](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Konto

Information om hur du hämtar information om faktura rads objekt (avstämnings rad objekt) för ett angivet faktura-ID finns i [Hämta faktura rads objekt](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Ladda ned en faktura som en PDF

Information om hur du hämtar ett faktura uttryck i PDF-formulär med hjälp av ett faktura-ID finns i [Hämta en faktura instruktion](get-invoice-statement.md).
