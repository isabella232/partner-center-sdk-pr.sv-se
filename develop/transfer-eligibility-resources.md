---
title: TransferEligibility-resurser
description: En partner skapar en överföring när en kund vill att prenumerationen på partnern ska överföras till en annan partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768961"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="00635-103">TransferEligibility-resurser</span><span class="sxs-lookup"><span data-stu-id="00635-103">TransferEligibility resources</span></span>

<span data-ttu-id="00635-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="00635-104">**Applies to:**</span></span>

- <span data-ttu-id="00635-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="00635-105">Partner Center</span></span>

<span data-ttu-id="00635-106">En partner skapar en överföring när en kund vill att prenumerationen på partnern ska överföras till en annan partner.</span><span class="sxs-lookup"><span data-stu-id="00635-106">A partner creates a transfer when a customer wants their subscription with the partner to be transferred to another partner.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="00635-107">TransferEligibility</span><span class="sxs-lookup"><span data-stu-id="00635-107">TransferEligibility</span></span>

<span data-ttu-id="00635-108">Beskriver en transferEligibility.</span><span class="sxs-lookup"><span data-stu-id="00635-108">Describes a transferEligibility.</span></span>

| <span data-ttu-id="00635-109">Egenskap</span><span class="sxs-lookup"><span data-stu-id="00635-109">Property</span></span>              | <span data-ttu-id="00635-110">Typ</span><span class="sxs-lookup"><span data-stu-id="00635-110">Type</span></span>             | <span data-ttu-id="00635-111">Description</span><span class="sxs-lookup"><span data-stu-id="00635-111">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="00635-112">id</span><span class="sxs-lookup"><span data-stu-id="00635-112">id</span></span>                    | <span data-ttu-id="00635-113">sträng</span><span class="sxs-lookup"><span data-stu-id="00635-113">string</span></span>           | <span data-ttu-id="00635-114">Kundens prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="00635-114">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="00635-115">isEligible</span><span class="sxs-lookup"><span data-stu-id="00635-115">isEligible</span></span>            | <span data-ttu-id="00635-116">boolesk</span><span class="sxs-lookup"><span data-stu-id="00635-116">bool</span></span>             | <span data-ttu-id="00635-117">Anger om prenumerationen är giltig för överföringen.</span><span class="sxs-lookup"><span data-stu-id="00635-117">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="00635-118">Orsak</span><span class="sxs-lookup"><span data-stu-id="00635-118">Reason</span></span>                | <span data-ttu-id="00635-119">sträng</span><span class="sxs-lookup"><span data-stu-id="00635-119">string</span></span>           | <span data-ttu-id="00635-120">Egenskapen orsak förklarar varför prenumerationen inte är berättigad till överföring.</span><span class="sxs-lookup"><span data-stu-id="00635-120">The reason property explains why the subscription isn't eligible for transfer.</span></span> |