---
title: Status för direkt signering (direkt godkännande) för ett kund avtal.
description: DirectSignedCustomerAgreementStatus-resursen representerar statusen för direkt signering (direkt godkännande) för ett kund avtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768796"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a><span data-ttu-id="d90c7-103">Direkt signering (direkt godkännande) status för ett kund avtal</span><span class="sxs-lookup"><span data-stu-id="d90c7-103">Direct signing (direct acceptance) status of a customer agreement</span></span>

<span data-ttu-id="d90c7-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="d90c7-104">**Applies to:**</span></span>

- <span data-ttu-id="d90c7-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d90c7-105">Partner Center</span></span>

<span data-ttu-id="d90c7-106">**DirectSignedCustomerAgreementStatus** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="d90c7-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="d90c7-107">Den här resursen är *inte tillämplig* för:</span><span class="sxs-lookup"><span data-stu-id="d90c7-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="d90c7-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d90c7-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d90c7-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="d90c7-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d90c7-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d90c7-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d90c7-111">**DirectSignedCustomerAgreementStatus** -resursen representerar statusen för det direkta godkännandet för ett kund avtal.</span><span class="sxs-lookup"><span data-stu-id="d90c7-111">The **DirectSignedCustomerAgreementStatus** resource represents the status of the direct acceptance of a customer agreement.</span></span>

## <a name="directsignedcustomeragreementstatus"></a><span data-ttu-id="d90c7-112">DirectSignedCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="d90c7-112">DirectSignedCustomerAgreementStatus</span></span>

<span data-ttu-id="d90c7-113">En **DirectSignedCustomerAgreementStatus** -resurs innehåller följande egenskaper:</span><span class="sxs-lookup"><span data-stu-id="d90c7-113">A **DirectSignedCustomerAgreementStatus** resource includes the following properties:</span></span>

| <span data-ttu-id="d90c7-114">Egenskap</span><span class="sxs-lookup"><span data-stu-id="d90c7-114">Property</span></span>       | <span data-ttu-id="d90c7-115">Typ</span><span class="sxs-lookup"><span data-stu-id="d90c7-115">Type</span></span>   | <span data-ttu-id="d90c7-116">Description</span><span class="sxs-lookup"><span data-stu-id="d90c7-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d90c7-117">isSigned</span><span class="sxs-lookup"><span data-stu-id="d90c7-117">isSigned</span></span> | <span data-ttu-id="d90c7-118">boolean</span><span class="sxs-lookup"><span data-stu-id="d90c7-118">boolean</span></span> | <span data-ttu-id="d90c7-119">Anger om kund avtalet har varit direkt signerat (accepterat) av kunden.</span><span class="sxs-lookup"><span data-stu-id="d90c7-119">Indicates if the customer agreement has been directly signed (accepted) by the customer.</span></span> |
