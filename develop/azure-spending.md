---
title: API-resurser för Azure-utgifter
description: Lär dig hur CSP-partner kan använda Partner Center-API:er för att visa och hantera Azure-utgifter och -användning för partner och kunder mot sin budget.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b51ccbcdaee18b6d5b3bd1b9531a64b22c8bac5a9d95e6cf94291ee802ed5d9
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992406"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>API-resurser för Azure-utgifter för att hantera partner- eller kundutgifter och användning mot en budget 

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Molnlösningsleverantör partner (CSP) kan visa och hantera sina Azure-utgifter via Partner Center-API:er. De kan också programmatiskt visa sina kunders utgifter mot en Azure-utgiftsbudget.

Mer information finns i scenarier där CSP-partner kan använda [Partner Center-API:er](scenarios.md)för att hantera kund- och partnerkonton och beställningar.

## <a name="partner-usage-management"></a>Hantering av partneranvändning

- [Hämta en partneranvändningssammanfattning](get-a-partner-usage-summary.md) med **hjälp av resursen PartnerUsageSummary**
- [Hämta användningsposter för alla kunder](get-a-customer-s-usage-records.md) som använder **resursen CustomerMonthlyUsageRecord**

## <a name="customer-usage-management"></a>Hantering av kundanvändning

- [Hämta en kunds användningssammanfattning](get-a-customer-usage-summary.md) med hjälp av **resursen CustomerUsageSummary**
- [Hämta alla poster för prenumerationsanvändning för en kund](get-a-customer-subscription-s-usage-records.md) med hjälp av resursen **SubscriptionMonthlyUsageRecord**

## <a name="subscription-usage-management"></a>Hantering av prenumerationsanvändning

- [Hämta en prenumerationsanvändningssammanfattning](get-a-customer-subscription-usage-summary.md) **med hjälp av resursen SubscriptionUsageSummary**
- [Hämta alla månatliga användningsposter för en prenumeration](get-all-monthly-usage-records-for-a-subscription.md) med hjälp av **resursen AzureResourceMonthlyUsageRecord**
- [Hämta användningsdata för en prenumeration med hjälp av](get-a-customer-subscription-resource-usage-records.md) resursen **ResourceUsageRecord**
- [Hämta användningsdata för en prenumeration via mätare](get-a-customer-subscription-meter-usage-records.md) med hjälp av **resursen MeterUsageRecord**

## <a name="azure-spending-budget-management"></a>Azure-utgiftsbudgethantering

- [Hämta en kunds användningsbudget med](get-a-customer-s-usage-spending-budget.md) hjälp av **resursen CustomerUsageSummary**
- [Uppdatera en kunds användningsbudget med](update-a-customer-s-usage-spending-budget.md) hjälp av **resursen CustomerUsageSummary**
