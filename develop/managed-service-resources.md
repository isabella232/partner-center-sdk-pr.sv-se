---
title: Hanterade tjänstresurser
description: Hanterade tjänster är tjänster som en partner har delegerat administratörsbehörighet till. Partner kan ge stöd för begäranden om filtjänster och för deras hanterade tjänster.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548132"
---
# <a name="managed-service-resources"></a><span data-ttu-id="b56d4-104">Hanterade tjänstresurser</span><span class="sxs-lookup"><span data-stu-id="b56d4-104">Managed service resources</span></span>

<span data-ttu-id="b56d4-105">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b56d4-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b56d4-106">Hanterade tjänster är tjänster som en partner har delegerat administratörsbehörighet till.</span><span class="sxs-lookup"><span data-stu-id="b56d4-106">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="b56d4-107">Partner kan ge stöd för begäranden om filtjänster och för deras hanterade tjänster.</span><span class="sxs-lookup"><span data-stu-id="b56d4-107">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="b56d4-108">ManagedService</span><span class="sxs-lookup"><span data-stu-id="b56d4-108">ManagedService</span></span>

<span data-ttu-id="b56d4-109">Beskriver en hanterad tjänst.</span><span class="sxs-lookup"><span data-stu-id="b56d4-109">Describes a managed service.</span></span>

| <span data-ttu-id="b56d4-110">Egenskap</span><span class="sxs-lookup"><span data-stu-id="b56d4-110">Property</span></span>   | <span data-ttu-id="b56d4-111">Typ</span><span class="sxs-lookup"><span data-stu-id="b56d4-111">Type</span></span>                | <span data-ttu-id="b56d4-112">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b56d4-112">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="b56d4-113">Id</span><span class="sxs-lookup"><span data-stu-id="b56d4-113">Id</span></span>         | <span data-ttu-id="b56d4-114">sträng</span><span class="sxs-lookup"><span data-stu-id="b56d4-114">string</span></span>              | <span data-ttu-id="b56d4-115">Det hanterade tjänst-ID:t.</span><span class="sxs-lookup"><span data-stu-id="b56d4-115">The managed service ID.</span></span>                                  |
| <span data-ttu-id="b56d4-116">Name</span><span class="sxs-lookup"><span data-stu-id="b56d4-116">Name</span></span>       | <span data-ttu-id="b56d4-117">sträng</span><span class="sxs-lookup"><span data-stu-id="b56d4-117">string</span></span>              | <span data-ttu-id="b56d4-118">Namnet på den hanterade tjänsten.</span><span class="sxs-lookup"><span data-stu-id="b56d4-118">The name of the managed service.</span></span>                         |
| <span data-ttu-id="b56d4-119">Gruppnamn</span><span class="sxs-lookup"><span data-stu-id="b56d4-119">GroupName</span></span>  | <span data-ttu-id="b56d4-120">sträng</span><span class="sxs-lookup"><span data-stu-id="b56d4-120">string</span></span>              | <span data-ttu-id="b56d4-121">Namnet på den grupp som tjänsten tillhör.</span><span class="sxs-lookup"><span data-stu-id="b56d4-121">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="b56d4-122">Länkar</span><span class="sxs-lookup"><span data-stu-id="b56d4-122">Links</span></span>      | <span data-ttu-id="b56d4-123">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="b56d4-123">ManagedServiceLinks</span></span> | <span data-ttu-id="b56d4-124">Resursen länkar som motsvarar den hanterade tjänsten.</span><span class="sxs-lookup"><span data-stu-id="b56d4-124">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="b56d4-125">Attribut</span><span class="sxs-lookup"><span data-stu-id="b56d4-125">Attributes</span></span> | <span data-ttu-id="b56d4-126">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="b56d4-126">ResourceAttributes</span></span>  | <span data-ttu-id="b56d4-127">Metadataattributen som motsvarar avtalet.</span><span class="sxs-lookup"><span data-stu-id="b56d4-127">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="b56d4-128">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="b56d4-128">ManagedServiceLinks</span></span>

<span data-ttu-id="b56d4-129">Innehåller länkarna som gör att partnern med delegerade administratörsbehörigheter kan ge stöd för tjänsten.</span><span class="sxs-lookup"><span data-stu-id="b56d4-129">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="b56d4-130">Egenskap</span><span class="sxs-lookup"><span data-stu-id="b56d4-130">Property</span></span>      | <span data-ttu-id="b56d4-131">Typ</span><span class="sxs-lookup"><span data-stu-id="b56d4-131">Type</span></span> | <span data-ttu-id="b56d4-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b56d4-132">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="b56d4-133">AdminService</span><span class="sxs-lookup"><span data-stu-id="b56d4-133">AdminService</span></span>  | <span data-ttu-id="b56d4-134">Länk</span><span class="sxs-lookup"><span data-stu-id="b56d4-134">Link</span></span> | <span data-ttu-id="b56d4-135">Administratörstjänstens URI.</span><span class="sxs-lookup"><span data-stu-id="b56d4-135">The admin service URI.</span></span>      |
| <span data-ttu-id="b56d4-136">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="b56d4-136">ServiceHealth</span></span> | <span data-ttu-id="b56d4-137">Länk</span><span class="sxs-lookup"><span data-stu-id="b56d4-137">Link</span></span> | <span data-ttu-id="b56d4-138">Tjänstens hälso-URI.</span><span class="sxs-lookup"><span data-stu-id="b56d4-138">The service health URI.</span></span>     |
| <span data-ttu-id="b56d4-139">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="b56d4-139">ServiceTicket</span></span> | <span data-ttu-id="b56d4-140">Länk</span><span class="sxs-lookup"><span data-stu-id="b56d4-140">Link</span></span> | <span data-ttu-id="b56d4-141">URI för tjänstbiljett.</span><span class="sxs-lookup"><span data-stu-id="b56d4-141">The service ticket URI.</span></span>     |
| <span data-ttu-id="b56d4-142">Själv</span><span class="sxs-lookup"><span data-stu-id="b56d4-142">Self</span></span>          | <span data-ttu-id="b56d4-143">Länk</span><span class="sxs-lookup"><span data-stu-id="b56d4-143">Link</span></span> | <span data-ttu-id="b56d4-144">Själv-URI.</span><span class="sxs-lookup"><span data-stu-id="b56d4-144">The self-URI.</span></span>               |
| <span data-ttu-id="b56d4-145">Nästa</span><span class="sxs-lookup"><span data-stu-id="b56d4-145">Next</span></span>          | <span data-ttu-id="b56d4-146">Länk</span><span class="sxs-lookup"><span data-stu-id="b56d4-146">Link</span></span> | <span data-ttu-id="b56d4-147">Nästa sida med objekt.</span><span class="sxs-lookup"><span data-stu-id="b56d4-147">The next page of items.</span></span>     |
| <span data-ttu-id="b56d4-148">Föregående</span><span class="sxs-lookup"><span data-stu-id="b56d4-148">Previous</span></span>      | <span data-ttu-id="b56d4-149">Länk</span><span class="sxs-lookup"><span data-stu-id="b56d4-149">Link</span></span> | <span data-ttu-id="b56d4-150">Föregående sida med objekt.</span><span class="sxs-lookup"><span data-stu-id="b56d4-150">The previous page of items.</span></span> |

