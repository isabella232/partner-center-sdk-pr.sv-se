---
title: Relationer resurser
description: Beskriver resurser som är relaterade till relationer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768877"
---
# <a name="relationships-resources"></a><span data-ttu-id="ca73b-103">Relationer resurser</span><span class="sxs-lookup"><span data-stu-id="ca73b-103">Relationships resources</span></span>

<span data-ttu-id="ca73b-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="ca73b-104">**Applies To**</span></span>

- <span data-ttu-id="ca73b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="ca73b-105">Partner Center</span></span>

<span data-ttu-id="ca73b-106">Beskriver resurser som är relaterade till relationer.</span><span class="sxs-lookup"><span data-stu-id="ca73b-106">Describes resources related to relationships.</span></span>

## <a name="partnerrelationship"></a><span data-ttu-id="ca73b-107">PartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="ca73b-107">PartnerRelationship</span></span>

<span data-ttu-id="ca73b-108">Representerar en relation mellan två partner.</span><span class="sxs-lookup"><span data-stu-id="ca73b-108">Represents a relationship between two partners.</span></span>

| <span data-ttu-id="ca73b-109">Egenskap</span><span class="sxs-lookup"><span data-stu-id="ca73b-109">Property</span></span>         | <span data-ttu-id="ca73b-110">Typ</span><span class="sxs-lookup"><span data-stu-id="ca73b-110">Type</span></span>                                                           | <span data-ttu-id="ca73b-111">Description</span><span class="sxs-lookup"><span data-stu-id="ca73b-111">Description</span></span>                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ca73b-112">id</span><span class="sxs-lookup"><span data-stu-id="ca73b-112">id</span></span>               | <span data-ttu-id="ca73b-113">sträng</span><span class="sxs-lookup"><span data-stu-id="ca73b-113">string</span></span>                                                         | <span data-ttu-id="ca73b-114">Partner-ID.</span><span class="sxs-lookup"><span data-stu-id="ca73b-114">The partner identifier.</span></span> <span data-ttu-id="ca73b-115">Partner-ID: t anger klient-ID för den partner som finns på mottagar sidan i relationen.</span><span class="sxs-lookup"><span data-stu-id="ca73b-115">The partner identifier specifies the tenant id of the partner who is in the recipient (from) side of the relationship.</span></span> |
| <span data-ttu-id="ca73b-116">location</span><span class="sxs-lookup"><span data-stu-id="ca73b-116">location</span></span>         | <span data-ttu-id="ca73b-117">sträng</span><span class="sxs-lookup"><span data-stu-id="ca73b-117">string</span></span>                                                         | <span data-ttu-id="ca73b-118">Partnerns plats.</span><span class="sxs-lookup"><span data-stu-id="ca73b-118">The location of the partner.</span></span>                                                                                                                   |
| <span data-ttu-id="ca73b-119">mpnId</span><span class="sxs-lookup"><span data-stu-id="ca73b-119">mpnId</span></span>            | <span data-ttu-id="ca73b-120">sträng</span><span class="sxs-lookup"><span data-stu-id="ca73b-120">string</span></span>                                                         | <span data-ttu-id="ca73b-121">Partnerns Microsoft Partner Network-ID (MPN).</span><span class="sxs-lookup"><span data-stu-id="ca73b-121">The Microsoft Partner Network (MPN) identifier of the partner.</span></span>                                                                                 |
| <span data-ttu-id="ca73b-122">name</span><span class="sxs-lookup"><span data-stu-id="ca73b-122">name</span></span>             | <span data-ttu-id="ca73b-123">sträng</span><span class="sxs-lookup"><span data-stu-id="ca73b-123">string</span></span>                                                         | <span data-ttu-id="ca73b-124">Namnet på partnern.</span><span class="sxs-lookup"><span data-stu-id="ca73b-124">The name of the partner.</span></span>                                                                                                                       |
| <span data-ttu-id="ca73b-125">relationshipType</span><span class="sxs-lookup"><span data-stu-id="ca73b-125">relationshipType</span></span> | <span data-ttu-id="ca73b-126">sträng</span><span class="sxs-lookup"><span data-stu-id="ca73b-126">string</span></span>                                                         | <span data-ttu-id="ca73b-127">Typ av relation.</span><span class="sxs-lookup"><span data-stu-id="ca73b-127">The type of relationship.</span></span>                                                                                                                      |
| <span data-ttu-id="ca73b-128">state</span><span class="sxs-lookup"><span data-stu-id="ca73b-128">state</span></span>            | <span data-ttu-id="ca73b-129">sträng</span><span class="sxs-lookup"><span data-stu-id="ca73b-129">string</span></span>                                                         | <span data-ttu-id="ca73b-130">Status för relationen (till exempel `active` ).</span><span class="sxs-lookup"><span data-stu-id="ca73b-130">The state of the relationship (for example `active`).</span></span>                                                                                                 |
| <span data-ttu-id="ca73b-131">dokumentattribut</span><span class="sxs-lookup"><span data-stu-id="ca73b-131">attributes</span></span>       | [<span data-ttu-id="ca73b-132">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="ca73b-132">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="ca73b-133">Attribut för metadata.</span><span class="sxs-lookup"><span data-stu-id="ca73b-133">The metadata attributes.</span></span>                                                                                                                       |

## <a name="relationshiprequest"></a><span data-ttu-id="ca73b-134">RelationshipRequest</span><span class="sxs-lookup"><span data-stu-id="ca73b-134">RelationshipRequest</span></span>

<span data-ttu-id="ca73b-135">Tillhandahåller URL: en som en kund kan upprätta en relation med en partner till.</span><span class="sxs-lookup"><span data-stu-id="ca73b-135">Provides the URL by which a customer can establish a relationship with a partner.</span></span>

| <span data-ttu-id="ca73b-136">Egenskap</span><span class="sxs-lookup"><span data-stu-id="ca73b-136">Property</span></span>   | <span data-ttu-id="ca73b-137">Typ</span><span class="sxs-lookup"><span data-stu-id="ca73b-137">Type</span></span>                                                           | <span data-ttu-id="ca73b-138">Description</span><span class="sxs-lookup"><span data-stu-id="ca73b-138">Description</span></span>                   |
|------------|----------------------------------------------------------------|-------------------------------|
| <span data-ttu-id="ca73b-139">url</span><span class="sxs-lookup"><span data-stu-id="ca73b-139">url</span></span>        | <span data-ttu-id="ca73b-140">sträng</span><span class="sxs-lookup"><span data-stu-id="ca73b-140">string</span></span>                                                         | <span data-ttu-id="ca73b-141">URL för Relations förfrågan.</span><span class="sxs-lookup"><span data-stu-id="ca73b-141">The relationship request URL.</span></span> |
| <span data-ttu-id="ca73b-142">dokumentattribut</span><span class="sxs-lookup"><span data-stu-id="ca73b-142">attributes</span></span> | [<span data-ttu-id="ca73b-143">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="ca73b-143">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="ca73b-144">Attribut för metadata.</span><span class="sxs-lookup"><span data-stu-id="ca73b-144">The metadata attributes.</span></span>      |
