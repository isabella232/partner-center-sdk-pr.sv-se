---
title: Hanterade tjänst resurser
description: Hanterade tjänster är tjänster som en partner har delegerat administratörs privilegier för. Partner kan ge support för och fil tjänst begär Anden för de hanterade tjänsternas räkning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768862"
---
# <a name="managed-service-resources"></a><span data-ttu-id="5000c-104">Hanterade tjänst resurser</span><span class="sxs-lookup"><span data-stu-id="5000c-104">Managed service resources</span></span>

<span data-ttu-id="5000c-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="5000c-105">**Applies To**</span></span>

- <span data-ttu-id="5000c-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="5000c-106">Partner Center</span></span>
- <span data-ttu-id="5000c-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="5000c-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5000c-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="5000c-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5000c-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5000c-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5000c-110">Hanterade tjänster är tjänster som en partner har delegerat administratörs privilegier för.</span><span class="sxs-lookup"><span data-stu-id="5000c-110">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="5000c-111">Partner kan ge support för och fil tjänst begär Anden för de hanterade tjänsternas räkning.</span><span class="sxs-lookup"><span data-stu-id="5000c-111">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="5000c-112">ManagedService</span><span class="sxs-lookup"><span data-stu-id="5000c-112">ManagedService</span></span>

<span data-ttu-id="5000c-113">Beskriver en hanterad tjänst.</span><span class="sxs-lookup"><span data-stu-id="5000c-113">Describes a managed service.</span></span>

| <span data-ttu-id="5000c-114">Egenskap</span><span class="sxs-lookup"><span data-stu-id="5000c-114">Property</span></span>   | <span data-ttu-id="5000c-115">Typ</span><span class="sxs-lookup"><span data-stu-id="5000c-115">Type</span></span>                | <span data-ttu-id="5000c-116">Description</span><span class="sxs-lookup"><span data-stu-id="5000c-116">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="5000c-117">Id</span><span class="sxs-lookup"><span data-stu-id="5000c-117">Id</span></span>         | <span data-ttu-id="5000c-118">sträng</span><span class="sxs-lookup"><span data-stu-id="5000c-118">string</span></span>              | <span data-ttu-id="5000c-119">ID för hanterad tjänst.</span><span class="sxs-lookup"><span data-stu-id="5000c-119">The managed service id.</span></span>                                  |
| <span data-ttu-id="5000c-120">Name</span><span class="sxs-lookup"><span data-stu-id="5000c-120">Name</span></span>       | <span data-ttu-id="5000c-121">sträng</span><span class="sxs-lookup"><span data-stu-id="5000c-121">string</span></span>              | <span data-ttu-id="5000c-122">Namnet på den hanterade tjänsten.</span><span class="sxs-lookup"><span data-stu-id="5000c-122">The name of the managed service.</span></span>                         |
| <span data-ttu-id="5000c-123">Namn</span><span class="sxs-lookup"><span data-stu-id="5000c-123">GroupName</span></span>  | <span data-ttu-id="5000c-124">sträng</span><span class="sxs-lookup"><span data-stu-id="5000c-124">string</span></span>              | <span data-ttu-id="5000c-125">Namnet på den grupp som tjänsten tillhör.</span><span class="sxs-lookup"><span data-stu-id="5000c-125">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="5000c-126">Länkar</span><span class="sxs-lookup"><span data-stu-id="5000c-126">Links</span></span>      | <span data-ttu-id="5000c-127">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="5000c-127">ManagedServiceLinks</span></span> | <span data-ttu-id="5000c-128">Resurs länkarna som motsvarar den hanterade tjänsten.</span><span class="sxs-lookup"><span data-stu-id="5000c-128">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="5000c-129">Attribut</span><span class="sxs-lookup"><span data-stu-id="5000c-129">Attributes</span></span> | <span data-ttu-id="5000c-130">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="5000c-130">ResourceAttributes</span></span>  | <span data-ttu-id="5000c-131">De metadata-attribut som motsvarar avtalet.</span><span class="sxs-lookup"><span data-stu-id="5000c-131">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="5000c-132">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="5000c-132">ManagedServiceLinks</span></span>

<span data-ttu-id="5000c-133">Innehåller de länkar som tillåter partnern med delegerade administratörs behörigheter att tillhandahålla stöd för tjänsten.</span><span class="sxs-lookup"><span data-stu-id="5000c-133">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="5000c-134">Egenskap</span><span class="sxs-lookup"><span data-stu-id="5000c-134">Property</span></span>      | <span data-ttu-id="5000c-135">Typ</span><span class="sxs-lookup"><span data-stu-id="5000c-135">Type</span></span> | <span data-ttu-id="5000c-136">Description</span><span class="sxs-lookup"><span data-stu-id="5000c-136">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="5000c-137">AdminService</span><span class="sxs-lookup"><span data-stu-id="5000c-137">AdminService</span></span>  | <span data-ttu-id="5000c-138">Länk</span><span class="sxs-lookup"><span data-stu-id="5000c-138">Link</span></span> | <span data-ttu-id="5000c-139">Admin-tjänstens URI.</span><span class="sxs-lookup"><span data-stu-id="5000c-139">The admin service URI.</span></span>      |
| <span data-ttu-id="5000c-140">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="5000c-140">ServiceHealth</span></span> | <span data-ttu-id="5000c-141">Länk</span><span class="sxs-lookup"><span data-stu-id="5000c-141">Link</span></span> | <span data-ttu-id="5000c-142">URI för tjänste hälsa.</span><span class="sxs-lookup"><span data-stu-id="5000c-142">The service health URI.</span></span>     |
| <span data-ttu-id="5000c-143">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="5000c-143">ServiceTicket</span></span> | <span data-ttu-id="5000c-144">Länk</span><span class="sxs-lookup"><span data-stu-id="5000c-144">Link</span></span> | <span data-ttu-id="5000c-145">URI för tjänst biljett.</span><span class="sxs-lookup"><span data-stu-id="5000c-145">The service ticket URI.</span></span>     |
| <span data-ttu-id="5000c-146">Själv</span><span class="sxs-lookup"><span data-stu-id="5000c-146">Self</span></span>          | <span data-ttu-id="5000c-147">Länk</span><span class="sxs-lookup"><span data-stu-id="5000c-147">Link</span></span> | <span data-ttu-id="5000c-148">Själv URI.</span><span class="sxs-lookup"><span data-stu-id="5000c-148">The self URI.</span></span>               |
| <span data-ttu-id="5000c-149">Nästa</span><span class="sxs-lookup"><span data-stu-id="5000c-149">Next</span></span>          | <span data-ttu-id="5000c-150">Länk</span><span class="sxs-lookup"><span data-stu-id="5000c-150">Link</span></span> | <span data-ttu-id="5000c-151">Nästa sida med objekt.</span><span class="sxs-lookup"><span data-stu-id="5000c-151">The next page of items.</span></span>     |
| <span data-ttu-id="5000c-152">Föregående</span><span class="sxs-lookup"><span data-stu-id="5000c-152">Previous</span></span>      | <span data-ttu-id="5000c-153">Länk</span><span class="sxs-lookup"><span data-stu-id="5000c-153">Link</span></span> | <span data-ttu-id="5000c-154">Föregående sida med objekt.</span><span class="sxs-lookup"><span data-stu-id="5000c-154">The previous page of items.</span></span> |

