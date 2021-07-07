---
title: Resurser för självbetjäningsprincipen
description: En partner anger självbetjäningsprinciper för en kund.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446725"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="e4b17-103">SelfServePolicy-resurs</span><span class="sxs-lookup"><span data-stu-id="e4b17-103">SelfServePolicy resource</span></span>

<span data-ttu-id="e4b17-104">En partner anger självbetjäningsprinciper för en kund.</span><span class="sxs-lookup"><span data-stu-id="e4b17-104">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="e4b17-105">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="e4b17-105">SelfServePolicy</span></span>

<span data-ttu-id="e4b17-106">Beskriver en kundvagn.</span><span class="sxs-lookup"><span data-stu-id="e4b17-106">Describes a cart.</span></span>

| <span data-ttu-id="e4b17-107">Egenskap</span><span class="sxs-lookup"><span data-stu-id="e4b17-107">Property</span></span>              | <span data-ttu-id="e4b17-108">Typ</span><span class="sxs-lookup"><span data-stu-id="e4b17-108">Type</span></span>             | <span data-ttu-id="e4b17-109">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e4b17-109">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4b17-110">id</span><span class="sxs-lookup"><span data-stu-id="e4b17-110">id</span></span>                    | <span data-ttu-id="e4b17-111">sträng</span><span class="sxs-lookup"><span data-stu-id="e4b17-111">string</span></span>           | <span data-ttu-id="e4b17-112">En principidentifierare med självbetjäning som tillhandahålls när självbetjäningsprincipen har skapats.</span><span class="sxs-lookup"><span data-stu-id="e4b17-112">A self-serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="e4b17-113">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="e4b17-113">SelfServeEntity</span></span>       | <span data-ttu-id="e4b17-114">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="e4b17-114">SelfServeEntity</span></span>  | <span data-ttu-id="e4b17-115">Entiteten med självbetjäning som beviljas åtkomst.</span><span class="sxs-lookup"><span data-stu-id="e4b17-115">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="e4b17-116">Beviljaren</span><span class="sxs-lookup"><span data-stu-id="e4b17-116">Grantor</span></span>               | <span data-ttu-id="e4b17-117">Beviljaren</span><span class="sxs-lookup"><span data-stu-id="e4b17-117">Grantor</span></span>          | <span data-ttu-id="e4b17-118">Den beviljande som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="e4b17-118">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="e4b17-119">Behörigheter</span><span class="sxs-lookup"><span data-stu-id="e4b17-119">Permissions</span></span>           | <span data-ttu-id="e4b17-120">Behörighetsmatris</span><span class="sxs-lookup"><span data-stu-id="e4b17-120">Array of Permission</span></span>| <span data-ttu-id="e4b17-121">En matris med [behörighetsresurser.](#permission)</span><span class="sxs-lookup"><span data-stu-id="e4b17-121">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="e4b17-122">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="e4b17-122">SelfServeEntity</span></span>

<span data-ttu-id="e4b17-123">Representerar den entitet som beviljas behörigheter.</span><span class="sxs-lookup"><span data-stu-id="e4b17-123">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="e4b17-124">Egenskap</span><span class="sxs-lookup"><span data-stu-id="e4b17-124">Property</span></span>             | <span data-ttu-id="e4b17-125">Typ</span><span class="sxs-lookup"><span data-stu-id="e4b17-125">Type</span></span>|<span data-ttu-id="e4b17-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e4b17-126">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4b17-127">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="e4b17-127">SelfServeEntityType</span></span>  | <span data-ttu-id="e4b17-128">sträng</span><span class="sxs-lookup"><span data-stu-id="e4b17-128">string</span></span>                           | <span data-ttu-id="e4b17-129">Entiteten beviljas åtkomst, godkända värden: Kund.</span><span class="sxs-lookup"><span data-stu-id="e4b17-129">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="e4b17-130">TenantID</span><span class="sxs-lookup"><span data-stu-id="e4b17-130">TenantID</span></span>             | <span data-ttu-id="e4b17-131">sträng</span><span class="sxs-lookup"><span data-stu-id="e4b17-131">string</span></span>                           | <span data-ttu-id="e4b17-132">Klient-ID för den entitet som beviljas åtkomst.</span><span class="sxs-lookup"><span data-stu-id="e4b17-132">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="e4b17-133">Beviljaren</span><span class="sxs-lookup"><span data-stu-id="e4b17-133">Grantor</span></span>

<span data-ttu-id="e4b17-134">Representerar den beviljande som beviljar behörigheterna.</span><span class="sxs-lookup"><span data-stu-id="e4b17-134">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="e4b17-135">Egenskap</span><span class="sxs-lookup"><span data-stu-id="e4b17-135">Property</span></span>             | <span data-ttu-id="e4b17-136">Typ</span><span class="sxs-lookup"><span data-stu-id="e4b17-136">Type</span></span>|<span data-ttu-id="e4b17-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e4b17-137">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4b17-138">GrantorType</span><span class="sxs-lookup"><span data-stu-id="e4b17-138">GrantorType</span></span>          | <span data-ttu-id="e4b17-139">sträng</span><span class="sxs-lookup"><span data-stu-id="e4b17-139">string</span></span>                           | <span data-ttu-id="e4b17-140">Den beviljande som beviljar åtkomst, godkända värden: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="e4b17-140">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="e4b17-141">TenantID</span><span class="sxs-lookup"><span data-stu-id="e4b17-141">TenantID</span></span>             | <span data-ttu-id="e4b17-142">sträng</span><span class="sxs-lookup"><span data-stu-id="e4b17-142">string</span></span>                           | <span data-ttu-id="e4b17-143">Klient-ID för den entitet som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="e4b17-143">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="e4b17-144">Behörighet</span><span class="sxs-lookup"><span data-stu-id="e4b17-144">Permission</span></span>

<span data-ttu-id="e4b17-145">Representerar en behörighet i självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="e4b17-145">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="e4b17-146">Egenskap</span><span class="sxs-lookup"><span data-stu-id="e4b17-146">Property</span></span>             | <span data-ttu-id="e4b17-147">Typ</span><span class="sxs-lookup"><span data-stu-id="e4b17-147">Type</span></span>|<span data-ttu-id="e4b17-148">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e4b17-148">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4b17-149">Resurs</span><span class="sxs-lookup"><span data-stu-id="e4b17-149">Resource</span></span>             | <span data-ttu-id="e4b17-150">sträng</span><span class="sxs-lookup"><span data-stu-id="e4b17-150">string</span></span>                           | <span data-ttu-id="e4b17-151">Resursåtkomsten beviljas också: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="e4b17-151">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="e4b17-152">Action</span><span class="sxs-lookup"><span data-stu-id="e4b17-152">Action</span></span>               | <span data-ttu-id="e4b17-153">sträng</span><span class="sxs-lookup"><span data-stu-id="e4b17-153">string</span></span>                           | <span data-ttu-id="e4b17-154">Åtgärdsåtkomst beviljas för: Köp</span><span class="sxs-lookup"><span data-stu-id="e4b17-154">The action access is being granted for: Purchase</span></span>                                           |
