---
title: Skapa en Azure-plan
description: Utvecklare kan köpa, skapa och hantera Azure-planer programmatiskt med hjälp av Partner Center-API:er.
ms.date: 07/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: b77b067c7eb150ab1ad9904915e87c3fc55c104a
ms.sourcegitcommit: 1fce45e6cafbc4c228042523ae28aac651a73757
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/23/2021
ms.locfileid: "114483066"
---
# <a name="create-an-azure-plan"></a>Skapa en Azure-plan

Du kan köpa, skapa och hantera en Azure-plan med hjälp av Partner Center-API:er. Processen liknar att skapa en prenumeration Microsoft Azure ([MS-AZR-0145P).](https://go.microsoft.com/fwlink/p/?linkid=2164140) Du måste [hämta katalogobjektet för Azure-planen och](#get-the-catalog-item-for-azure-plan)sedan [skapa och skicka en order.](#create-and-submit-an-order)

## <a name="prerequisites"></a>Förutsättningar

* [Autentiseringsuppgifter för Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.
* Kundidentifieraren. Om du inte har en kunds identifierare följer du stegen i [Hämta en lista över kunder.](get-a-list-of-customers.md) Du kan också logga in på Partnercenter, välja kunden i listan över kunder, välja **Konto** och sedan spara sitt **Microsoft-ID.**
* [Bekräftelse av kundens godkännande av Microsoft-kundavtal](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Hämta katalogobjektet för Azure-planen

Innan du kan skapa en Azure-plan för en kund måste du hämta motsvarande katalogobjekt. Du kan hämta katalogobjektet med hjälp av befintliga API:er för Partner Center-katalogen med följande resursmodeller.

* **[Produkt](product-resources.md#product)**: En grupperingskonstruktion för köpbara varor eller tjänster. Själva produkten är inte ett köpbart objekt.
* **[SKU:](product-resources.md#sku)** En köpbar lagerhållningsenhet (SKU) under en produkt. SKU:er representerar olika former av produkten.
* **[Tillgänglighet:](product-resources.md#availability)** En konfiguration där en SKU är tillgänglig för inköp (till exempel land, valuta eller branschsegment).

Utför följande steg för att hämta katalogobjektet för en Azure-plan:

1. Identifiera och hämta *produktidentifieraren* för Azure-planen. Följ stegen i [Hämta en lista över produkter och](get-a-list-of-products.md) ange **targetView** som **MicrosoftAzure.** (Om du redan känner till *produktidentifieraren* för Azure-planen kan du följa stegen i Hämta [en produkt med produkt-ID:t i](get-a-product-by-id.md) stället.)

2. Hämta **SKU:n** från produkten för Azure-planen. Följ stegen i Hämta [en lista över SKU:er för en produkt](get-a-list-of-skus-for-a-product.md). Om du redan känner till SKU-identifieraren för Azure-planen kan du följa stegen i Hämta en SKU med [hjälp av SKU-ID:t i](get-a-sku-by-id.md) stället.

3. Hämta **tillgängligheten** från SKU:n för Azure-planen. Följ stegen i [Hämta en lista över tillgänglighet för en SKU.](get-a-list-of-availabilities-for-a-sku.md) Om du redan känner till identifieraren för den tillgänglighet du behöver kan du följa stegen i Hämta en tillgänglighet [med hjälp av tillgänglighets-ID:t](get-an-availability-by-id.md) i stället. *Se till att notera värdet för egenskapen **CatalogItemId** för tillgängligheten för Azure-planen. Du behöver det här värdet för att skapa en order.*

## <a name="create-and-submit-an-order"></a>Skapa och skicka en beställning

Följ dessa steg om du vill skicka din beställning för en Azure-plan:

1. [Skapa en kundvagn](create-a-cart.md) för den samling katalogobjekt som du tänker köpa. När du skapar [en kundvagn](cart-resources.md#cart) [grupperas kundvagnsraderna](cart-resources.md#cartlineitem) automatiskt baserat på vad som kan köpas tillsammans i samma [order.](order-resources.md#order) (Du kan också [uppdatera en kundvagn](update-a-cart.md).)

2. [Checka ut kundvagnen](checkout-a-cart.md), vilket resulterar i att en [order skapas.](order-resources.md#order)

## <a name="get-order-details"></a>Hämta beställningsinformation

Du kan [hämta information om en enskild order med hjälp av order-ID:t](get-an-order-by-id.md). Du kan också [hämta en lista över alla beställningar för en specifik kund](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>När en order har skickats uppstår en fördröjning på upp till 15 minuter innan ordern visas i kundens orderlista.

## <a name="manage-azure-plans"></a>Hantera Azure-planer

När ordern har bearbetats skapas en **prenumerationsresurs** i Partnercenter för Azure-planen. Du kan använda följande metoder för att hantera **partnercenterprenumerationsresurser** för att hantera Azure-planen:

* [Hämta en kunds prenumerationer](get-all-of-a-customer-s-subscriptions.md)
* [Hämta en lista över prenumerationer efter beställning](get-a-list-of-subscriptions-by-order.md)

När en Azure-plan skapas i Partnercenter skapas även en motsvarande Azure-användningsprenumeration i Azure. Du kan också skapa ytterligare Azure-användningsprenumerationer under samma Azure-plan med hjälp Azure Portal och Azure-API:er. Du kan hämta identifierare för alla Azure-användningsprenumerationer som är associerade med en Azure-plan genom att följa stegen i Hämta en lista över [Azure-rättigheter för Partner Center-prenumeration](get-a-list-of-azure-entitlements-for-subscription.md)

## <a name="lifecycle-management"></a>Livscykelhantering

Du kan pausa en befintlig Azure-plan genom att följa stegen i [Pausa en prenumeration.](suspend-a-subscription.md)

*Du kan bara pausa en befintlig Azure-plan om den inte längre har några associerade aktiva användningstillgångar, inklusive Azure-användningsprenumerationer och Azure-reservationer.*

Mer information om hur du inaktiverar Azure-användningsprenumerationer finns [i Azure API för livscykelhantering för prenumerationer.](/rest/api/resources/subscriptions)

Om du vill ta bort befintliga Azure-reservationer måste [du avbryta reservationerna](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation).
När du har pausat en Azure-plan kan du återaktivera den.

Mer information om hur du återaktiverar en Azure-plan finns [i Återaktivera en pausad prenumeration](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Flytta över befintliga CSP-erbjudanden till en Azure-plan 

Du kan inte skapa en Azure-plan för en befintlig kund med en Microsoft Azure-prenumeration (MS-AZR-0145P). Däremot kan du [flytta över kunder från deras befintliga Azure-erbjudanden för molntjänstleverantörer (CSP) till Azure-tjänster i Azure-planen](/partner-center/azure-plan-transition) från den nya köpupplevelsen i CSP-programmet i Partnercenter. Du kan flytta över en befintlig kund genom att använda produktuppgraderings-API:erna och följa dessa steg:

* [Kontrollera om kunden kan flyttas över till en Azure-plan](get-eligibility-for-product-upgrade.md)
* [Starta en produktuppgradering för kunden](create-product-upgrade-entity.md)
* [Kontrollera statusen för en produktuppgradering](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Utgift i Azure

Du kan spåra [Azure-utgifter](azure-spending.md) genom att fråga efter användningssammanfattning och detaljerade användningsposter med hjälp av följande metoder:

* [Hämta användningssammanfattning för partner](get-a-partner-usage-summary.md)
* [Hämta alla kundanvändningsposter för en partner](get-a-customer-s-usage-records.md)
* [Hämta användningssammanfattning för kund](get-a-customer-usage-summary.md)
* [Hämta alla prenumerationsanvändningsposter för en kund](get-a-customer-subscription-s-usage-records.md)
* [Hämta sammanfattning av prenumerationsanvändning](get-a-customer-subscription-usage-summary.md)
* [Hämta användningsdata för prenumeration efter resurs](get-a-customer-subscription-resource-usage-records.md)
* [Hämta användningsdata för prenumeration efter mätare](get-a-customer-subscription-meter-usage-records.md)
* [Hämta postresurser för mätaranvändning](meter-usage-resources.md)
* [Hämta postresurser för resursanvändning](resource-usage-resources.md)

Du kan också ange och hantera kundens användningsbudget med hjälp av följande metoder:

* [Hämta användningsbudget för kund](get-a-customer-s-usage-spending-budget.md)
* [Uppdatera användningsbudget för kund](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Du kan hantera fakturor och avstämningsdata med hjälp av följande metoder:

* [Hämta en samling fakturor](get-a-collection-of-invoices.md)
* [Hämta länkar för fakturauppskattning](get-invoice-estimate-links.md)
* [Hämta faktura efter ID](get-invoice-by-id.md)
* [Hämta fakturautdrag](get-invoice-statement.md)
* [Hämta fakturasammanfattningar](get-invoice-summaries.md)
* [Hämta radobjekt för fakturerad förbrukning](get-invoice-billed-consumption-lineitems.md)
* [Hämta radobjekt för ofakturerad förbrukning](get-invoice-unbilled-consumption-lineitems.md)
* [Hämta fakturafakturerade radobjekt](get-invoiceline-items.md)
* [Hämta radobjekt för ofakturerad avstämning](get-invoice-unbilled-recon-lineitems.md)
