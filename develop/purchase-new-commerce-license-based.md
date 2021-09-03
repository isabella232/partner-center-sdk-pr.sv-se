---
title: Köpa nya handelslicensbaserade tjänster
description: Utvecklare kan köpa, skapa och hantera nya handelslicensbaserade tjänster med hjälp av Partner Center-API:erna.
ms.date: 02/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: dd3aebdb0a670449d3a39f67fc2ad6c7ef8df8e5
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457335"
---
# <a name="purchasing-new-commerce-license-based-services"></a>Köpa nya handelslicensbaserade tjänster

**Gäller för:**

* Partnercenter

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365.

Du kan köpa, skapa och hantera nya handelsupplevelselicensbaserade tjänster med hjälp av Partner Center-API:er. Processen påminner om till exempel Azure-plan och Marketplace-erbjudanden.

## <a name="prerequisites"></a>Förutsättningar

* [Autentiseringsuppgifter för Partnercenter.](partner-center-authentication.md) Den nya handelsupplevelsen stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.
* Kundidentifieraren. Om du inte har en kunds identifierare följer du stegen i [Hämta en lista över kunder.](get-a-list-of-customers.md) Du kan också logga in på Partnercenter, välja kunden i listan över kunder, välja **Konto** och sedan spara sitt **Microsoft-ID.**
* [Bekräftelse av kundens godkännande av Microsoft-kundavtal](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-new-commerce-license-based-services"></a>Hämta katalogobjektet för nya handelslicensbaserade tjänster

Du måste hämta nya katalogobjekt för handelslicensbaserade tjänster. Hämta katalogobjekt med hjälp av befintliga API:er för Partner Center-katalogen med följande resursmodeller:

* **[Produkt:](product-resources.md#product)** En grupperingskonstruktion för köpbara varor eller tjänster. Själva produkten är inte ett köpbart objekt.
* **[SKU:](product-resources.md#sku)** En köpbar lagerhållningsenhet (SKU) under en produkt. SKU:er representerar olika former av produkten.
* **[Tillgänglighet:](product-resources.md#availability)** En konfiguration där en SKU kan köpas (till exempel land, valuta eller branschsegment).

Så här hämtar du katalogobjekten för nya erbjudanden om handelslicensbaserade tjänster:

1. Följ stegen i [Hämta en lista över produkter](get-a-list-of-products.md) för produkter och ange **targetView** som **OnlineServices**. (Om du redan känner till produktidentifieraren för det erbjudande som du vill köpa kan du följa stegen i Hämta en produkt med [produkt-ID:t](get-a-product-by-id.md) i stället.)

2. Hämta **SKU:n** från produkten för det erbjudande du letar efter. Följ stegen i Hämta [en lista över SKU:er för en produkt](get-a-list-of-skus-for-a-product.md). (Om du redan känner till SKU-identifieraren för det erbjudande du vill ha kan du följa stegen i Hämta en SKU med hjälp av [SKU-ID:t](get-a-sku-by-id.md) i stället.)

3. Hämta **tillgängligheten** från SKU:n för erbjudandet. Olika erbjudanden har specifika villkor. Vissa SKU:er har mer än en tillgänglighet. Följ stegen i [Hämta en lista över tillgänglighet för en SKU.](get-a-list-of-availabilities-for-a-sku.md) (Om du redan känner till identifieraren för den tillgänglighet du behöver kan du följa stegen i Hämta en tillgänglighet med hjälp av [tillgänglighets-ID:t](get-an-availability-by-id.md) i stället.) *Se till att notera värdet för **egenskapen CatalogItemId** för tillgängligheten för erbjudandet. Du behöver det här värdet för att skapa en order*.

## <a name="create-and-submit-an-order"></a>Skapa och skicka en beställning

Följ dessa steg om du vill skicka din beställning för en Azure-plan (inklusive nya handelsordrar):

1. [Skapa en kundvagn](create-a-cart.md) för den samling katalogobjekt som du tänker köpa. När du skapar [en kundvagn](cart-resources.md#cart) [grupperas kundvagnsradsobjekten](cart-resources.md#cartlineitem) automatiskt baserat på vad som kan köpas tillsammans i samma [order.](order-resources.md#order) (Du kan också [uppdatera en kundvagn](update-a-cart.md).)

2. [Checka ut kundvagnen](checkout-a-cart.md), vilket resulterar i att en [order skapas.](order-resources.md#order)

## <a name="get-order-details"></a>Hämta orderinformation

Du kan [hämta information om en enskild order med hjälp av order-ID:t](get-an-order-by-id.md). Du kan också [hämta en lista över alla beställningar för en specifik kund](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>När du har skickat en beställning tar det upp till 15 minuter innan ordern visas i kundens orderlista. För närvarande kan EU-partner bara köpa nya handelserbjudanden för: 1. Nya kunder 2. Befintliga kunder som inte har en befintlig Azure-plan, marknadsplats, programvaruprenumerationer eller permanent programvara i en annan valuta än partnerns landsvaluta.

## <a name="manage-new-commerce-subscriptions"></a>Hantera nya handelsprenumerationer

När ordern har bearbetats  skapas en partnercenterprenumerationsresurs för Azure-planen. Du kan använda följande metoder för att hantera Partner **Center-prenumerationsresurser** för att hantera Azure-planen:

* [Hämta en kunds prenumerationer](get-all-of-a-customer-s-subscriptions.md)
* [Hämta en lista över prenumerationer efter beställning](get-a-list-of-subscriptions-by-order.md)

Det finns skillnader och nya funktioner som är specifika för ny handel.

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Du kan hantera fakturor och avstämningsdata med hjälp av följande metoder:

* [Hämta en samling fakturor](get-a-collection-of-invoices.md)
* [Hämta länkar för fakturauppskattning](get-invoice-estimate-links.md)
* [Hämta faktura efter ID](get-invoice-by-id.md)
* [Hämta fakturautdrag](get-invoice-statement.md)
* [Hämta fakturasammanfattningar](get-invoice-summaries.md)
* [Hämta radobjekt för fakturerad förbrukning](get-invoice-billed-consumption-lineitems.md)
* [Hämta radobjekt för ofakturerad förbrukning](get-invoice-unbilled-consumption-lineitems.md)
* [Hämta fakturerade rekognoserade radobjekt](get-invoiceline-items.md)
* [Hämta radobjekt för ofakturerad avstämning](get-invoice-unbilled-recon-lineitems.md)
