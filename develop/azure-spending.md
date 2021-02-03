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
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="30b6b-103">Azure utgifts-API-resurser för att hantera partner eller kund utgifter och användning mot en budget</span><span class="sxs-lookup"><span data-stu-id="30b6b-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="30b6b-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="30b6b-104">**Applies to:**</span></span>

- <span data-ttu-id="30b6b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="30b6b-105">Partner Center</span></span>
- <span data-ttu-id="30b6b-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="30b6b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="30b6b-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="30b6b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="30b6b-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="30b6b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="30b6b-109">Leverantörer av moln lösningar (CSP) kan visa och hantera sina Azure-utgifter via API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="30b6b-109">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="30b6b-110">De kan också program mässigt Visa sina kunders utgifter mot en Azure utgifts budget.</span><span class="sxs-lookup"><span data-stu-id="30b6b-110">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="30b6b-111">Mer information finns [i scenarier där CSP-partner kan använda API: er för partner Center för att hantera kund-och partner konton och order](scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="30b6b-111">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="30b6b-112">Hantering av partner användning</span><span class="sxs-lookup"><span data-stu-id="30b6b-112">Partner usage management</span></span>

- <span data-ttu-id="30b6b-113">[Få en översikt över användning av partner](get-a-partner-usage-summary.md) med hjälp av **PartnerUsageSummary** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-113">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="30b6b-114">[Hämta användnings poster för alla kunder som](get-a-customer-s-usage-records.md) använder **CustomerMonthlyUsageRecord** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-114">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="30b6b-115">Hantering av kund användning</span><span class="sxs-lookup"><span data-stu-id="30b6b-115">Customer usage management</span></span>

- <span data-ttu-id="30b6b-116">[Få en kunds användnings översikt](get-a-customer-usage-summary.md) med hjälp av **CustomerUsageSummary** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-116">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="30b6b-117">[Hämta alla prenumerations användnings poster för en kund](get-a-customer-subscription-s-usage-records.md) med hjälp av **SubscriptionMonthlyUsageRecord** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-117">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="30b6b-118">Hantering av prenumerations användning</span><span class="sxs-lookup"><span data-stu-id="30b6b-118">Subscription usage management</span></span>

- <span data-ttu-id="30b6b-119">[Hämta en översikt över prenumerations användning](get-a-customer-subscription-usage-summary.md) med **SubscriptionUsageSummary** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-119">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="30b6b-120">[Hämta alla månatliga användnings poster för en prenumeration](get-all-monthly-usage-records-for-a-subscription.md) med hjälp av **AzureResourceMonthlyUsageRecord** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-120">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="30b6b-121">[Hämta användnings data för en prenumeration per resurs](get-a-customer-subscription-resource-usage-records.md) med hjälp av **ResourceUsageRecord** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-121">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="30b6b-122">[Hämta användnings data för en prenumeration efter mätare](get-a-customer-subscription-meter-usage-records.md) med hjälp av **MeterUsageRecord** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-122">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="30b6b-123">Budget hantering för Azure-utgifter</span><span class="sxs-lookup"><span data-stu-id="30b6b-123">Azure spending budget management</span></span>

- <span data-ttu-id="30b6b-124">[Hämta en kunds användnings budget](get-a-customer-s-usage-spending-budget.md) med hjälp av **CustomerUsageSummary** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-124">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="30b6b-125">[Uppdatera en kunds användnings budget](update-a-customer-s-usage-spending-budget.md) med hjälp av **CustomerUsageSummary** -resursen</span><span class="sxs-lookup"><span data-stu-id="30b6b-125">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
