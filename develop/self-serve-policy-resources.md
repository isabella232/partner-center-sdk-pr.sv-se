---
title: Självbetjänings princip resurser
description: En partner ställer in självbetjänings principer för en kund.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768952"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="87e16-103">SelfServePolicy-resurs</span><span class="sxs-lookup"><span data-stu-id="87e16-103">SelfServePolicy resource</span></span>

<span data-ttu-id="87e16-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="87e16-104">**Applies to:**</span></span>

- <span data-ttu-id="87e16-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="87e16-105">Partner Center</span></span>

<span data-ttu-id="87e16-106">En partner ställer in självbetjänings principer för en kund.</span><span class="sxs-lookup"><span data-stu-id="87e16-106">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="87e16-107">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="87e16-107">SelfServePolicy</span></span>

<span data-ttu-id="87e16-108">Beskriver en varukorg.</span><span class="sxs-lookup"><span data-stu-id="87e16-108">Describes a cart.</span></span>

| <span data-ttu-id="87e16-109">Egenskap</span><span class="sxs-lookup"><span data-stu-id="87e16-109">Property</span></span>              | <span data-ttu-id="87e16-110">Typ</span><span class="sxs-lookup"><span data-stu-id="87e16-110">Type</span></span>             | <span data-ttu-id="87e16-111">Description</span><span class="sxs-lookup"><span data-stu-id="87e16-111">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="87e16-112">id</span><span class="sxs-lookup"><span data-stu-id="87e16-112">id</span></span>                    | <span data-ttu-id="87e16-113">sträng</span><span class="sxs-lookup"><span data-stu-id="87e16-113">string</span></span>           | <span data-ttu-id="87e16-114">En princip identifierare för egen installation som anges när du skapar den själv fungerande principen.</span><span class="sxs-lookup"><span data-stu-id="87e16-114">A self serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="87e16-115">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="87e16-115">SelfServeEntity</span></span>       | <span data-ttu-id="87e16-116">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="87e16-116">SelfServeEntity</span></span>  | <span data-ttu-id="87e16-117">Den själv betjänande entitet som beviljas åtkomst.</span><span class="sxs-lookup"><span data-stu-id="87e16-117">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="87e16-118">Den beviljande användaren</span><span class="sxs-lookup"><span data-stu-id="87e16-118">Grantor</span></span>               | <span data-ttu-id="87e16-119">Den beviljande användaren</span><span class="sxs-lookup"><span data-stu-id="87e16-119">Grantor</span></span>          | <span data-ttu-id="87e16-120">Den beviljande behörighet som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="87e16-120">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="87e16-121">Behörigheter</span><span class="sxs-lookup"><span data-stu-id="87e16-121">Permissions</span></span>           | <span data-ttu-id="87e16-122">Behörighets mat ris</span><span class="sxs-lookup"><span data-stu-id="87e16-122">Array of Permission</span></span>| <span data-ttu-id="87e16-123">En matris med [behörighets](#permission) resurser.</span><span class="sxs-lookup"><span data-stu-id="87e16-123">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="87e16-124">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="87e16-124">SelfServeEntity</span></span>

<span data-ttu-id="87e16-125">Representerar den entitet som beviljats behörigheter.</span><span class="sxs-lookup"><span data-stu-id="87e16-125">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="87e16-126">Egenskap</span><span class="sxs-lookup"><span data-stu-id="87e16-126">Property</span></span>             | <span data-ttu-id="87e16-127">Typ</span><span class="sxs-lookup"><span data-stu-id="87e16-127">Type</span></span>|<span data-ttu-id="87e16-128">Description</span><span class="sxs-lookup"><span data-stu-id="87e16-128">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="87e16-129">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="87e16-129">SelfServeEntityType</span></span>  | <span data-ttu-id="87e16-130">sträng</span><span class="sxs-lookup"><span data-stu-id="87e16-130">string</span></span>                           | <span data-ttu-id="87e16-131">Entiteten beviljas åtkomst, godkända värden: kund.</span><span class="sxs-lookup"><span data-stu-id="87e16-131">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="87e16-132">TenantID</span><span class="sxs-lookup"><span data-stu-id="87e16-132">TenantID</span></span>             | <span data-ttu-id="87e16-133">sträng</span><span class="sxs-lookup"><span data-stu-id="87e16-133">string</span></span>                           | <span data-ttu-id="87e16-134">Klient-ID: n för den entitet som har beviljats åtkomst.</span><span class="sxs-lookup"><span data-stu-id="87e16-134">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="87e16-135">Den beviljande användaren</span><span class="sxs-lookup"><span data-stu-id="87e16-135">Grantor</span></span>

<span data-ttu-id="87e16-136">Representerar den beviljande behörighet som beviljar behörighet.</span><span class="sxs-lookup"><span data-stu-id="87e16-136">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="87e16-137">Egenskap</span><span class="sxs-lookup"><span data-stu-id="87e16-137">Property</span></span>             | <span data-ttu-id="87e16-138">Typ</span><span class="sxs-lookup"><span data-stu-id="87e16-138">Type</span></span>|<span data-ttu-id="87e16-139">Description</span><span class="sxs-lookup"><span data-stu-id="87e16-139">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="87e16-140">GrantorType</span><span class="sxs-lookup"><span data-stu-id="87e16-140">GrantorType</span></span>          | <span data-ttu-id="87e16-141">sträng</span><span class="sxs-lookup"><span data-stu-id="87e16-141">string</span></span>                           | <span data-ttu-id="87e16-142">Den beviljande användaren beviljar åtkomst, godkända värden: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="87e16-142">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="87e16-143">TenantID</span><span class="sxs-lookup"><span data-stu-id="87e16-143">TenantID</span></span>             | <span data-ttu-id="87e16-144">sträng</span><span class="sxs-lookup"><span data-stu-id="87e16-144">string</span></span>                           | <span data-ttu-id="87e16-145">Klient-ID för entiteten som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="87e16-145">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="87e16-146">Behörighet</span><span class="sxs-lookup"><span data-stu-id="87e16-146">Permission</span></span>

<span data-ttu-id="87e16-147">Representerar en behörighet i den självbetjänings principen.</span><span class="sxs-lookup"><span data-stu-id="87e16-147">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="87e16-148">Egenskap</span><span class="sxs-lookup"><span data-stu-id="87e16-148">Property</span></span>             | <span data-ttu-id="87e16-149">Typ</span><span class="sxs-lookup"><span data-stu-id="87e16-149">Type</span></span>|<span data-ttu-id="87e16-150">Description</span><span class="sxs-lookup"><span data-stu-id="87e16-150">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="87e16-151">Resurs</span><span class="sxs-lookup"><span data-stu-id="87e16-151">Resource</span></span>             | <span data-ttu-id="87e16-152">sträng</span><span class="sxs-lookup"><span data-stu-id="87e16-152">string</span></span>                           | <span data-ttu-id="87e16-153">Resurs åtkomsten beviljas för: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="87e16-153">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="87e16-154">Action</span><span class="sxs-lookup"><span data-stu-id="87e16-154">Action</span></span>               | <span data-ttu-id="87e16-155">sträng</span><span class="sxs-lookup"><span data-stu-id="87e16-155">string</span></span>                           | <span data-ttu-id="87e16-156">Åtkomst till åtgärden beviljas för: Köp</span><span class="sxs-lookup"><span data-stu-id="87e16-156">The action access is being granted for: Purchase</span></span>                                           |
