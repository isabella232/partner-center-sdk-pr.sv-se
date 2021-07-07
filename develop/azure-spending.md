---
title: API-resurser för Azure-utgifter
description: Lär dig hur CSP-partner kan använda Partner Center-API:er för att visa och hantera Azure-utgifter och -användning för partner och kunder mot sin budget.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 472554de1c354559d5bc4b21959c109467891806
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974326"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="8b42e-103">API-resurser för Azure-utgifter för att hantera partner- eller kundutgifter och användning mot en budget</span><span class="sxs-lookup"><span data-stu-id="8b42e-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="8b42e-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8b42e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8b42e-105">Molnlösningsleverantör partner (CSP) kan visa och hantera sina Azure-utgifter via Partner Center-API:er.</span><span class="sxs-lookup"><span data-stu-id="8b42e-105">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="8b42e-106">De kan också programmatiskt visa sina kunders utgifter mot en Azure-utgiftsbudget.</span><span class="sxs-lookup"><span data-stu-id="8b42e-106">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="8b42e-107">Mer information finns i scenarier där CSP-partner kan använda [Partner Center-API:er](scenarios.md)för att hantera kund- och partnerkonton och beställningar.</span><span class="sxs-lookup"><span data-stu-id="8b42e-107">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="8b42e-108">Hantering av partneranvändning</span><span class="sxs-lookup"><span data-stu-id="8b42e-108">Partner usage management</span></span>

- <span data-ttu-id="8b42e-109">[Hämta en partneranvändningssammanfattning](get-a-partner-usage-summary.md) med **hjälp av resursen PartnerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="8b42e-109">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="8b42e-110">[Hämta användningsposter för alla kunder](get-a-customer-s-usage-records.md) som använder **resursen CustomerMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="8b42e-110">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="8b42e-111">Hantering av kundanvändning</span><span class="sxs-lookup"><span data-stu-id="8b42e-111">Customer usage management</span></span>

- <span data-ttu-id="8b42e-112">[Hämta en kunds användningssammanfattning](get-a-customer-usage-summary.md) med hjälp av **resursen CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="8b42e-112">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="8b42e-113">[Hämta alla poster för prenumerationsanvändning för en kund](get-a-customer-subscription-s-usage-records.md) med hjälp av resursen **SubscriptionMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="8b42e-113">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="8b42e-114">Hantering av prenumerationsanvändning</span><span class="sxs-lookup"><span data-stu-id="8b42e-114">Subscription usage management</span></span>

- <span data-ttu-id="8b42e-115">[Hämta en prenumerationsanvändningssammanfattning](get-a-customer-subscription-usage-summary.md) **med hjälp av resursen SubscriptionUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="8b42e-115">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="8b42e-116">[Hämta alla månatliga användningsposter för en prenumeration](get-all-monthly-usage-records-for-a-subscription.md) med hjälp av **resursen AzureResourceMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="8b42e-116">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="8b42e-117">[Hämta användningsdata för en prenumeration med hjälp av](get-a-customer-subscription-resource-usage-records.md) resursen **ResourceUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="8b42e-117">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="8b42e-118">[Hämta användningsdata för en prenumeration via mätare](get-a-customer-subscription-meter-usage-records.md) med hjälp av **resursen MeterUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="8b42e-118">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="8b42e-119">Azure-utgiftsbudgethantering</span><span class="sxs-lookup"><span data-stu-id="8b42e-119">Azure spending budget management</span></span>

- <span data-ttu-id="8b42e-120">[Hämta en kunds användningsbudget med](get-a-customer-s-usage-spending-budget.md) hjälp av **resursen CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="8b42e-120">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="8b42e-121">[Uppdatera en kunds användningsbudget med](update-a-customer-s-usage-spending-budget.md) hjälp av **resursen CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="8b42e-121">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
