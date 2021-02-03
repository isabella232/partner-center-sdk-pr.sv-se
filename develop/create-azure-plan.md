---
title: Skapa en Azure-plan
description: 'Utvecklare kan köpa, skapa och hantera Azure-planer genom programmering med hjälp av API: er för partner Center.'
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 372b94ac7217899ca560cf943bf11a7e8906872d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769315"
---
# <a name="create-an-azure-plan"></a>Skapa en Azure-plan

**Gäller för:**

* Partnercenter

Du kan köpa, skapa och hantera en Azure-prenumeration med hjälp av API: er för partner Center. Processen liknar att skapa en Microsoft Azure-prenumeration (MS-AZR-0145P). Du måste [Hämta katalog posten för Azure-planen](#get-the-catalog-item-for-azure-plan)och sedan [skapa och skicka en order](#create-and-submit-an-order).

## <a name="prerequisites"></a>Förutsättningar

* Autentiseringsuppgifter för [partner Center-autentisering](partner-center-authentication.md) . Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.
* Kund-ID. Om du inte har en kund identifierare följer du stegen i [Hämta en lista över kunder](get-a-list-of-customers.md). Du kan också logga in på Partner Center, välja kund i listan över kunder, välja **konto** och sedan spara sitt **Microsoft-ID**.
* [Bekräftelse av kundens godkännande av Microsofts kund avtal](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Hämta katalog objekt för Azure-prenumerationen

Innan du kan skapa en Azure-plan för en kund måste du hämta motsvarande katalog objekt. Du kan hämta katalog objekt med hjälp av befintliga partner-API: er för partner Center med följande resurs modeller.

* **[Produkt](product-resources.md#product)**: en grupperings konstruktion för köpbara-varor eller-tjänster. En produkt är inte ett köpbara-objekt.
* **[SKU](product-resources.md#sku)**: en köpbara lagerhållnings enhet (SKU) under en produkt. SKU: er representerar olika former av produkten.
* **[Tillgänglighet](product-resources.md#availability)**: en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta eller bransch segment).

Utför följande steg för att hämta katalog objekt för en Azure-plan:

1. Identifiera och hämta *produkt* -ID för Azure-prenumerationen. Följ stegen i [Hämta en lista över produkter](get-a-list-of-products.md) och ange **targetView** som **MicrosoftAzure**. (Om du redan känner till *produkt* -ID: t för Azure-planen kan du följa stegen i [Hämta en produkt med produkt-ID](get-a-product-by-id.md) i stället.)

2. Hämta **SKU: n** från produkten för Azure-prenumerationen. Följ stegen i [Hämta en lista över SKU: er för en produkt](get-a-list-of-skus-for-a-product.md). Om du redan känner till SKU-identifieraren för Azure-prenumerationen kan du följa stegen i [Hämta en SKU med SKU-ID](get-a-sku-by-id.md) i stället.

3. Hämta **tillgänglighet** från SKU: n för Azure-prenumerationen. Följ stegen i [Hämta en lista över tillgänglighet för en SKU](get-a-list-of-availabilities-for-a-sku.md). Om du redan känner till identifieraren för den tillgänglighet du behöver kan du följa stegen i [få en tillgänglighet med tillgänglighets-ID](get-an-availability-by-id.md) i stället. *Se till att anteckna värdet för **CatalogItemId** -egenskapen för tillgänglighet för Azure-planen. Du behöver det här värdet för att skapa en order.*

## <a name="create-and-submit-an-order"></a>Skapa och skicka en order

Följ dessa steg om du vill skicka in din beställning för en Azure-plan:

1. [Skapa en vagn](create-a-cart.md) som innehåller den samling av katalog objekt som du vill köpa. När du skapar en [varukorg](cart-resources.md#cart)grupperas [vagnens rad objekt](cart-resources.md#cartlineitem) automatiskt utifrån vad som kan köpas tillsammans i samma [ordning](order-resources.md#order). (Du kan också [Uppdatera en varukorg](update-a-cart.md).)

2. [Kolla in vagnen](checkout-a-cart.md), som leder till att en [order](order-resources.md#order)skapas.

## <a name="get-order-details"></a>Hämta beställnings information

Du kan [Hämta information om en enskild order med order-ID: t](get-an-order-by-id.md). Du kan också [Hämta en lista över alla beställningar för en specifik kund](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>När en beställning har skickats sker en fördröjning på upp till 15 minuter innan ordern visas i kund order listan.

## <a name="manage-azure-plans"></a>Hantera Azure-planer

När beställningen har bearbetats kommer en **prenumerations** resurs för partner Center att skapas för Azure-planen. Du kan använda följande metoder för att hantera **prenumerations** resurser för partner Center för att hantera Azure-planen:

* [Hämta en kunds prenumerationer](get-all-of-a-customer-s-subscriptions.md)
* [Hämta en lista över prenumerationer efter beställning](get-a-list-of-subscriptions-by-order.md)

När en Azure-plan skapas i Partner Center skapas även en motsvarande Azure-användnings prenumeration i Azure. Du kan också skapa ytterligare Azure-användnings prenumerationer i samma Azure-plan med Azure Portal och Azure API: er. Du kan hämta identifierarna för alla Azure-användnings prenumerationer som är associerade med en Azure-plan genom att följa stegen i [Hämta en lista över Azure-rättigheter för partner Center-prenumerationen](get-a-list-of-azure-entitlements-for-subscription.md)

## <a name="lifecycle-management"></a>Livs cykel hantering

Du kan pausa en befintlig Azure-plan genom att följa stegen i [pausa en prenumeration](suspend-a-subscription.md).

*Du kan bara pausa en befintlig Azure-plan om den inte längre har några aktiva användnings till gångar kopplade till sig, inklusive Azures användnings prenumerationer och Azure-reservationer.*

Mer information om hur du inaktiverar Azures användnings prenumerationer finns i [Azure API för livs cykel hantering av prenumerationer](/rest/api/resources/subscriptions).

Om du vill ta bort befintliga Azure-reservationer måste du [avbryta reservationerna](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation).
När du har pausat en Azure-prenumeration kan du återaktivera den.

Mer information om hur du återaktiverar en Azure-plan finns i återaktivera en inaktive [rad prenumeration](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Flytta över befintliga CSP-erbjudanden till en Azure-plan 

Du kan inte skapa en Azure-plan för en befintlig kund med en Microsoft Azure-prenumeration (MS-AZR-0145P). Däremot kan du [flytta över kunder från deras befintliga Azure-erbjudanden för molntjänstleverantörer (CSP) till Azure-tjänster i Azure-planen](/partner-center/azure-plan-transition) från den nya köpupplevelsen i CSP-programmet i Partnercenter. Du kan flytta över en befintlig kund genom att använda produktuppgraderings-API:erna och följa dessa steg:

* [Kontrollera om kunden kan flyttas över till en Azure-plan](get-eligibility-for-product-upgrade.md)
* [Starta en produktuppgradering för kunden](create-product-upgrade-entity.md)
* [Kontrollera statusen för en produktuppgradering](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Utgift i Azure

Du kan spåra [Azure-utgifter](azure-spending.md) genom att fråga efter användnings Sammanfattning och detaljerade användnings poster med hjälp av följande metoder:

* [Hämta användningssammanfattning för partner](get-a-partner-usage-summary.md)
* [Hämta alla kundanvändningsposter för en partner](get-a-customer-s-usage-records.md)
* [Hämta användningssammanfattning för kund](get-a-customer-usage-summary.md)
* [Hämta alla prenumerationsanvändningsposter för en kund](get-a-customer-subscription-s-usage-records.md)
* [Hämta sammanfattning av prenumerationsanvändning](get-a-customer-subscription-usage-summary.md)
* [Hämta användningsdata för prenumeration efter resurs](get-a-customer-subscription-resource-usage-records.md)
* [Hämta användningsdata för prenumeration efter mätare](get-a-customer-subscription-meter-usage-records.md)
* [Hämta postresurser för mätaranvändning](meter-usage-resources.md)
* [Hämta postresurser för resursanvändning](resource-usage-resources.md)

Du kan också ange och hantera kund användnings budget med följande metoder:

* [Hämta användningsbudget för kund](get-a-customer-s-usage-spending-budget.md)
* [Uppdatera användningsbudget för kund](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Du kan hantera fakturor och avstämnings data med följande metoder:

* [Hämta en samling fakturor](get-a-collection-of-invoices.md)
* [Hämta länkar för fakturauppskattning](get-invoice-estimate-links.md)
* [Hämta faktura efter ID](get-invoice-by-id.md)
* [Hämta fakturautdrag](get-invoice-statement.md)
* [Hämta fakturasammanfattningar](get-invoice-summaries.md)
* [Hämta radobjekt för fakturerad förbrukning](get-invoice-billed-consumption-lineitems.md)
* [Hämta radobjekt för ofakturerad förbrukning](get-invoice-unbilled-consumption-lineitems.md)
* [Hämta fakturerade rekognoseringar rad artiklar](get-invoiceline-items.md)
* [Hämta radobjekt för ofakturerad avstämning](get-invoice-unbilled-recon-lineitems.md)
