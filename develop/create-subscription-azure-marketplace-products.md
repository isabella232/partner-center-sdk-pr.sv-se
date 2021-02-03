---
title: Skapa en prenumeration på kommersiella Marketplace-produkter
description: 'Utvecklare kan skapa och hantera en prenumeration på kommersiella Marketplace-produkter med hjälp av API: er för partner Center.'
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df2a3707e00ba36a11c404b102304c08d105244e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768811"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Skapa en prenumeration på kommersiella Marketplace-produkter

**Gäller för:**

* Partnercenter

Du kan skapa en prenumeration på kommersiella Marketplace-produkter med hjälp av API: er för partner Center. Du måste [få en lista över erbjudanden för en marknad](#get-a-list-of-offers-for-a-market), [skapa och skicka in en order](#create-and-submit-an-order) för en prenumeration på en kommersiell marknads plats och sedan [Hämta en aktiverings länk](#get-activation-link).

Du kan också [utföra livs cykel hantering](#lifecycle-management) och [hantera fakturor](#invoice-and-reconciliation) för dessa prenumerationer.

## <a name="prerequisites"></a>Förutsättningar

* Autentiseringsuppgifter för [partner Center-autentisering](partner-center-authentication.md) . Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.
* Kund-ID. Om du inte har en kund identifierare följer du stegen i [Hämta en lista över kunder](get-a-list-of-customers.md). Du kan också logga in på Partner Center, välja kund i listan över kunder, välja **konto** och sedan spara sitt **Microsoft-ID**.

## <a name="get-a-list-of-offers-for-a-market"></a>Hämta en lista över erbjudanden för en marknad

Du kan kontrol lera tillgängliga erbjudanden för en marknad med hjälp av följande Partner Center API-modeller:

* **[Produkt](product-resources.md#product)**: en grupperings konstruktion för köpbara-varor eller-tjänster. En produkt är inte ett köpbara-objekt.
* **[SKU](product-resources.md#sku)**: en köpbara lagerhållnings enhet (SKU) under en produkt. Dessa representerar olika former av produkten.
* **[Tillgänglighet](product-resources.md#availability)**: en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta eller bransch segment).

Innan du köper en Azure-reservation utför du följande steg:

1. Identifiera och hämta den produkt och SKU som du vill köpa. Om du redan känner till produkt-ID och SKU-ID väljer du dem.

    * [Hämta en lista över produkter](get-a-list-of-products.md)
    * [Hämta en produkt med produkt-ID](get-a-product-by-id.md)
    * [Hämta en lista över SKU: er för en produkt](get-a-list-of-skus-for-a-product.md)
    * [Hämta en SKU med SKU-ID](get-a-sku-by-id.md)

    > [!NOTE]
    > Du kan identifiera kommersiella Marketplace-produkter med deras **ProductType** -egenskap för **"Azure"** och deras **SubType** -egenskap för **"SaaS"**.

2. Om SKU: erna är taggade med en **InventoryCheck** -förutsättning [kontrollerar du inventeringen för en SKU](check-inventory.md).

    > [!NOTE]
    > För närvarande finns det inga kommersiella Marketplace-produkter som stöder inventerings kontroll eller som är taggade med en **InventoryCheck** -förutsättning.

3. Hämta tillgänglighet för SKU: n. Du behöver **CatalogItemId** av tillgängligheten när du placerar ordern, som du kan hämta via följande API: er:

    * [Hämta en lista över tillgänglighet för en SKU](get-a-list-of-availabilities-for-a-sku.md)
    * [Få en tillgänglighet med tillgänglighets-ID: t](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Skapa och skicka en order

Följ dessa steg om du vill skicka in din Azure reservations ordning:

1. [Skapa en vagn](create-a-cart.md) som innehåller den samling av katalog objekt som du vill köpa. När du skapar en [varukorg](cart-resources.md#cart)grupperas [vagnens rad objekt](cart-resources.md#cartlineitem) automatiskt utifrån vad som kan köpas tillsammans i samma [ordning](order-resources.md#order). (Du kan också [Uppdatera en varukorg](update-a-cart.md).)
2. [Kolla in vagnen](checkout-a-cart.md), som leder till att en [order](order-resources.md#order)skapas.

### <a name="get-order-details"></a>Hämta beställnings information

Du kan [Hämta information om en enskild order med order-ID: t](get-an-order-by-id.md). Du kan också [Hämta en lista över alla beställningar för en specifik kund](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> När en beställning har skickats sker en fördröjning på upp till 15 minuter innan ordern visas i kund order listan.

## <a name="get-activation-link"></a>Hämta aktiverings länk

Partnern eller kunden måste aktivera prenumerationer på Azure Marketplace-produkter. Du kan [Hämta en aktiverings länk per order rads objekt](get-activation-link-by-order-line-item.md). Du kan också [få en prenumeration efter ID](get-a-subscription-by-id.md)och sedan räkna upp dess **länkar** -egenskap för att skapa en aktiverings länk.

## <a name="lifecycle-management"></a>Livs cykel hantering

Du kan hantera livs cykeln för dina prenumerationer på kommersiella Marketplace-produkter på följande sätt:

* [Avbryta en prenumeration på kommersiell marknadsplats](cancel-an-azure-marketplace-subscription.md)
* [Aktivera eller inaktivera autoförnyelse för en prenumeration på kommersiell marknads plats](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Hantering av kvantitet

Antalet prenumerationer på en extern marknads plats måste ligga inom de gränser som definieras av den associerade [SKU: n](product-resources.md#sku) (se attributet **minimumQuantity** och **maximumQuantity** ). Använd följande metod för att uppdatera antalet för en prenumeration på en extern marknads plats:

* [Ändra kvantiteten för en prenumeration](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Du kan hantera kund [fakturor](invoice-resources.md) (inklusive avgifter för prenumerationer på kommersiella Marketplace-produkter) på följande sätt:

* [Hämta försäljnings objekt för försäljnings fakturor på försäljnings platser](get-invoice-billed-consumption-lineitems.md)
* [Hämta länkar för fakturauppskattning](get-invoice-estimate-links.md)
* [Hämta fakturor för ej fakturerade kommersiella marknads platser på marknaden](get-invoice-unbilled-consumption-lineitems.md)
* [Hämta faktura poster för ej fakturerade faktura rader](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Testa att använda sandbox-konto för integration

När du har skapat en prenumeration på kommersiella Marketplace SaaS-produkter måste du hämta en anpassad aktiverings länk från Partner Center och besöka utgivarens webbplats för att slutföra installationen. Prenumerations faktureringen påbörjas bara efter att installationen har slutförts.

I sandbox-miljön för KRYPTOGRAFI finns det ingen integrering med ISV: er. Om du försöker hämta en aktiverings länk från Partner Center kommer en dummy-länk att returneras. Du kan inte använda den här dummy-länken för att slutföra installations processen på utgivarens webbplats. Använd följande metod för att aktivera prenumerationen i stället för att använda det begränsade kontot för integration för att testa faktureringen för prenumerationer på kommersiella Marketplace-SaaS produkter. Prenumerations faktureringen påbörjas efter lyckad aktivering:

* [Aktivera en Sandbox-prenumeration för kommersiella Marketplace-produkter](activate-sandbox-subscription-azure-marketplace-products.md)

