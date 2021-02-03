---
title: Azure utgifts-API-resurser
description: 'Lär dig hur CSP-partner kan använda API: er för partner Center för att visa och hantera partner och kunds Azure-utgifter och användning mot deras budget.'
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a2995a06473cc6990d1234acd522a3b38a03d3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97769996"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Azure utgifts-API-resurser för att hantera partner eller kund utgifter och användning mot en budget 

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Leverantörer av moln lösningar (CSP) kan visa och hantera sina Azure-utgifter via API: er för partner Center. De kan också program mässigt Visa sina kunders utgifter mot en Azure utgifts budget.

Mer information finns [i scenarier där CSP-partner kan använda API: er för partner Center för att hantera kund-och partner konton och order](scenarios.md).

## <a name="partner-usage-management"></a>Hantering av partner användning

- [Få en översikt över användning av partner](get-a-partner-usage-summary.md) med hjälp av **PartnerUsageSummary** -resursen
- [Hämta användnings poster för alla kunder som](get-a-customer-s-usage-records.md) använder **CustomerMonthlyUsageRecord** -resursen

## <a name="customer-usage-management"></a>Hantering av kund användning

- [Få en kunds användnings översikt](get-a-customer-usage-summary.md) med hjälp av **CustomerUsageSummary** -resursen
- [Hämta alla prenumerations användnings poster för en kund](get-a-customer-subscription-s-usage-records.md) med hjälp av **SubscriptionMonthlyUsageRecord** -resursen

## <a name="subscription-usage-management"></a>Hantering av prenumerations användning

- [Hämta en översikt över prenumerations användning](get-a-customer-subscription-usage-summary.md) med **SubscriptionUsageSummary** -resursen
- [Hämta alla månatliga användnings poster för en prenumeration](get-all-monthly-usage-records-for-a-subscription.md) med hjälp av **AzureResourceMonthlyUsageRecord** -resursen
- [Hämta användnings data för en prenumeration per resurs](get-a-customer-subscription-resource-usage-records.md) med hjälp av **ResourceUsageRecord** -resursen
- [Hämta användnings data för en prenumeration efter mätare](get-a-customer-subscription-meter-usage-records.md) med hjälp av **MeterUsageRecord** -resursen

## <a name="azure-spending-budget-management"></a>Budget hantering för Azure-utgifter

- [Hämta en kunds användnings budget](get-a-customer-s-usage-spending-budget.md) med hjälp av **CustomerUsageSummary** -resursen
- [Uppdatera en kunds användnings budget](update-a-customer-s-usage-spending-budget.md) med hjälp av **CustomerUsageSummary** -resursen
