---
title: Skapa en prenumeration för produkter på den kommersiella marknadsplatsen
description: Utvecklare kan skapa och hantera en prenumeration för produkter på den kommersiella marknadsplatsen med partnercenter-API:er.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ae2e4b0a1ffa2e63e68864887093673e32079d9f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973374"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Skapa en prenumeration för produkter på den kommersiella marknadsplatsen

Du kan skapa en prenumeration för produkter på den kommersiella marknadsplatsen med hjälp av PartnerCenter-API:er. Du måste [hämta en lista över erbjudanden för en marknad,](#get-a-list-of-offers-for-a-market)skapa och skicka en [beställning](#create-and-submit-an-order) för en prenumeration på den kommersiella marknadsplatsen och sedan hämta [en aktiveringslänk.](#get-activation-link)

Du kan också [utföra livscykelhantering och](#lifecycle-management) [hantera fakturor för](#invoice-and-reconciliation) dessa prenumerationer.

## <a name="prerequisites"></a>Förutsättningar

* [Autentiseringsuppgifter för Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.
* Kundidentifieraren. Om du inte har en kunds identifierare följer du stegen i [Hämta en lista över kunder.](get-a-list-of-customers.md) Du kan också logga in på Partnercenter, välja kunden i listan över kunder, välja **Konto** och sedan spara sitt **Microsoft-ID.**

## <a name="get-a-list-of-offers-for-a-market"></a>Hämta en lista över erbjudanden för en marknad

Du kan kontrollera de tillgängliga erbjudandena för en marknad med hjälp av följande Partner Center API-modeller:

* **[Produkt:](product-resources.md#product)** En grupperingskonstruktion för köpbara varor eller tjänster. Själva produkten är inte ett köpbart objekt.
* **[SKU:](product-resources.md#sku)** En köpbar lagerhållningsenhet (SKU) under en produkt. Dessa representerar olika former av produkten.
* **[Tillgänglighet:](product-resources.md#availability)** En konfiguration där en SKU kan köpas (till exempel land, valuta eller branschsegment).

Slutför följande steg innan du köper en Azure-reservation:

1. Identifiera och hämta den produkt och SKU som du vill köpa. Om du redan känner till produkt-ID och SKU-ID väljer du dem.

    * [Hämta en lista över produkter](get-a-list-of-products.md)
    * [Hämta en produkt med produkt-ID:t](get-a-product-by-id.md)
    * [Hämta en lista över SKU:er för en produkt](get-a-list-of-skus-for-a-product.md)
    * [Hämta en SKU med hjälp av SKU-ID:t](get-a-sku-by-id.md)

    > [!NOTE]
    > Du kan identifiera produkter på den kommersiella marknadsplatsen med deras **ProductType-egenskap** **"Azure"** och deras **SubType-egenskap** **"SaaS".**

2. Om SKU:erna är taggade med **en InventoryCheck-förutsättning** [kontrollerar du inventeringen för en SKU.](check-inventory.md)

    > [!NOTE]
    > För stunden finns det inga produkter från den kommersiella marknadsplatsen som stöder inventeringskontroll eller taggas med krav **för InventoryCheck.**

3. Hämta tillgängligheten för SKU:n. Du behöver **CatalogItemId för** tillgängligheten när du gör beställningen, som du kan hämta via följande API:er:

    * [Hämta en lista över tillgänglighet för en SKU](get-a-list-of-availabilities-for-a-sku.md)
    * [Hämta en tillgänglighet med hjälp av tillgänglighets-ID:t](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Skapa och skicka en beställning

Följ dessa steg om du vill skicka din Azure-reservationsbeställning:

1. [Skapa en kundvagn](create-a-cart.md) för den samling katalogobjekt som du tänker köpa. När du skapar [en kundvagn](cart-resources.md#cart) [grupperas kundvagnsradsobjekten](cart-resources.md#cartlineitem) automatiskt baserat på vad som kan köpas tillsammans i samma [order.](order-resources.md#order) (Du kan också [uppdatera en kundvagn](update-a-cart.md).)
2. [Checka ut kundvagnen](checkout-a-cart.md), vilket resulterar i att en [order skapas.](order-resources.md#order)

### <a name="get-order-details"></a>Hämta orderinformation

Du kan [hämta information om en enskild order med hjälp av order-ID:t](get-an-order-by-id.md). Du kan också [hämta en lista över alla beställningar för en specifik kund](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> När en order har skickats uppstår en fördröjning på upp till 15 minuter innan ordern visas i kundens orderlista.

## <a name="get-activation-link"></a>Hämta aktiveringslänk

Partnern eller kunden måste aktivera prenumerationer för att Azure Marketplace produkter. Du kan [få en aktiveringslänk via orderradobjektet](get-activation-link-by-order-line-item.md). Du kan också [hämta en prenumeration per ID](get-a-subscription-by-id.md)och sedan räkna upp dess Egenskap **Länkar** för att skapa en aktiveringslänk.

## <a name="lifecycle-management"></a>Livscykelhantering

Du kan hantera livscykeln för dina prenumerationer på produkter från den kommersiella marknadsplatsen med hjälp av följande metoder:

* [Avbryta en prenumeration på kommersiell marknadsplats](cancel-an-azure-marketplace-subscription.md)
* [Aktivera eller inaktivera automatisk förnyelse för en prenumeration på den kommersiella marknadsplatsen](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Kvantitetshantering

Kvantiteten för en prenumeration på den kommersiella marknadsplatsen måste vara inom de gränser som definieras av dess associerade [SKU](product-resources.md#sku) (se **attributen minimumQuantity** och **maximumQuantity).** Om du vill uppdatera kvantiteten för en prenumeration på den kommersiella marknadsplatsen använder du följande metod:

* [Ändra kvantiteten för en prenumeration](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Du kan hantera [kundfakturor](invoice-resources.md) (inklusive avgifter för prenumerationer på produkter på den kommersiella marknadsplatsen) med hjälp av följande metoder:

* [Hämta fakturafakturerade förbrukningsradsobjekt på den kommersiella marknadsplatsen](get-invoice-billed-consumption-lineitems.md)
* [Hämta länkar för fakturauppskattning](get-invoice-estimate-links.md)
* [Hämta förbrukningsradartiklar för faktura som inte fakturerats på den kommersiella marknadsplatsen](get-invoice-unbilled-consumption-lineitems.md)
* [Hämta ej fakturerade avstämningsradsobjekt](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Testa med hjälp av sandbox-integrationskonto

När du har skapat en prenumeration på SaaS-produkter på den kommersiella marknadsplatsen i produktion måste du hämta en anpassad aktiveringslänk från Partnercenter och besöka utgivarens webbplats för att slutföra installationen. Prenumerationsfakturering börjar först när installationen är klar.

I CSP-sandbox-miljön finns det ingen integrering med ISV:er. Om du försöker hämta en aktiveringslänk från Partnercenter returneras en dummylänk. Du kan inte använda den här dummylänken för att slutföra installationen på utgivarens webbplats. Om du vill använda sandbox-kontot för integrering för att testa faktureringen för prenumerationer på SaaS-produkter på den kommersiella marknadsplatsen använder du följande metod för att aktivera prenumerationen i stället. Prenumerationsfakturering börjar efter aktiveringen:

* [Aktivera en sandbox-prenumeration för produkter på den kommersiella marknadsplatsen](activate-sandbox-subscription-azure-marketplace-products.md)

