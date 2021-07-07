---
title: TransferEligibility-resurser
description: En partner kan skapa en överföring när en kund begär sin prenumeration hos partnern som ska överföras till en annan partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530216"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="891e2-103">TransferEligibility-resurser</span><span class="sxs-lookup"><span data-stu-id="891e2-103">TransferEligibility resources</span></span>

<span data-ttu-id="891e2-104">En partner kan skapa en överföring när en kund begär sin prenumeration hos partnern som ska överföras till en annan partner.</span><span class="sxs-lookup"><span data-stu-id="891e2-104">A partner can create a transfer when a customer requests their subscription with the partner to be transferred to another partner.</span></span> <span data-ttu-id="891e2-105">Använd TransferEligibility för att kontrollera om en prenumeration är berättigad att överföras.</span><span class="sxs-lookup"><span data-stu-id="891e2-105">Use TransferEligibility to check whether a subscription is eligible to be transferred.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="891e2-106">Överföringsbarhet</span><span class="sxs-lookup"><span data-stu-id="891e2-106">TransferEligibility</span></span>

<span data-ttu-id="891e2-107">Beskriver överföringEligibility.</span><span class="sxs-lookup"><span data-stu-id="891e2-107">Describes a transferEligibility.</span></span>

| <span data-ttu-id="891e2-108">Egenskap</span><span class="sxs-lookup"><span data-stu-id="891e2-108">Property</span></span>              | <span data-ttu-id="891e2-109">Typ</span><span class="sxs-lookup"><span data-stu-id="891e2-109">Type</span></span>             | <span data-ttu-id="891e2-110">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="891e2-110">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="891e2-111">id</span><span class="sxs-lookup"><span data-stu-id="891e2-111">id</span></span>                    | <span data-ttu-id="891e2-112">sträng</span><span class="sxs-lookup"><span data-stu-id="891e2-112">string</span></span>           | <span data-ttu-id="891e2-113">Kundens prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="891e2-113">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="891e2-114">isEligible</span><span class="sxs-lookup"><span data-stu-id="891e2-114">isEligible</span></span>            | <span data-ttu-id="891e2-115">boolesk</span><span class="sxs-lookup"><span data-stu-id="891e2-115">bool</span></span>             | <span data-ttu-id="891e2-116">Anger om prenumerationen är berättigad till överföringen.</span><span class="sxs-lookup"><span data-stu-id="891e2-116">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="891e2-117">Anledning</span><span class="sxs-lookup"><span data-stu-id="891e2-117">Reason</span></span>                | <span data-ttu-id="891e2-118">sträng</span><span class="sxs-lookup"><span data-stu-id="891e2-118">string</span></span>           | <span data-ttu-id="891e2-119">Orsaksegenskapen förklarar varför prenumerationen inte är berättigad till överföring.</span><span class="sxs-lookup"><span data-stu-id="891e2-119">The reason property explains why the subscription isn't eligible for transfer.</span></span> |