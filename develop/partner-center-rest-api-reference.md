---
title: Partnercenter – REST API-referens
description: Lär dig hur CSP-partner kan använda Partner Center REST API:er för att integrera sina CRM- och faktureringsprogram med Microsoft-system för att bättre hantera kundkonton.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 18621fdb94f91f066b69a11f7d557410d653787e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548047"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="5c45c-103">PartnerCenter REST API referens till REST-URL:er, REST-huvuden, REST-resurser och REST-händelser</span><span class="sxs-lookup"><span data-stu-id="5c45c-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="5c45c-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5c45c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="5c45c-105">PartnerCenter-REST API</span><span class="sxs-lookup"><span data-stu-id="5c45c-105">Partner Center REST API</span></span>

<span data-ttu-id="5c45c-106">Partnercenter-REST API hjälper Molnlösningsleverantör-partner (CSP) att integrera sin befintliga CRM- eller faktureringsprogramvara med Microsoft-system som hanterar kundkonton, beställer, hanterar prenumerationer och hanterar supportförfrågningar.</span><span class="sxs-lookup"><span data-stu-id="5c45c-106">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="5c45c-107">Mer information om vad API:et kan göra, inklusive exempelkod, finns i [avsnittet Scenarier,](scenarios.md) inklusive bakgrundsöversikten.</span><span class="sxs-lookup"><span data-stu-id="5c45c-107">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="5c45c-108">Innan du börjar koda läser du [avsnittet Kom](get-started.md) igång.</span><span class="sxs-lookup"><span data-stu-id="5c45c-108">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="5c45c-109">Den här artikeln innehåller information om att konfigurera test- och produktionskonton, få autentisering att fungera och hitta exempelkoden.</span><span class="sxs-lookup"><span data-stu-id="5c45c-109">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

<span data-ttu-id="5c45c-110">En referensguide som förklarar varje API finns i [Partnercenter REST API](/rest/api/partner-center-rest/).</span><span class="sxs-lookup"><span data-stu-id="5c45c-110">For a reference guide explaining each API, see [Partner Center REST API](/rest/api/partner-center-rest/).</span></span>

## <a name="topics"></a><span data-ttu-id="5c45c-111">Ämnen</span><span class="sxs-lookup"><span data-stu-id="5c45c-111">Topics</span></span>

| <span data-ttu-id="5c45c-112">Avsnitt</span><span class="sxs-lookup"><span data-stu-id="5c45c-112">Topic</span></span> | <span data-ttu-id="5c45c-113">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5c45c-113">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="5c45c-114">PartnerCenter-REST API</span><span class="sxs-lookup"><span data-stu-id="5c45c-114">Partner Center REST API</span></span>](/rest/api/partner-center-rest/) | <span data-ttu-id="5c45c-115">Referens för varje REST API tillgänglig för Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="5c45c-115">Reference of each REST API available for Partner Center.</span></span> |
| [<span data-ttu-id="5c45c-116">Partnercenter – REST-URL:er</span><span class="sxs-lookup"><span data-stu-id="5c45c-116">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="5c45c-117">Definierar REST API slutpunkter för olika versioner av Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="5c45c-117">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="5c45c-118">Partnercenter – REST-huvuden</span><span class="sxs-lookup"><span data-stu-id="5c45c-118">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="5c45c-119">Definierar de begäran- och svarshuvuden som används av REST API.</span><span class="sxs-lookup"><span data-stu-id="5c45c-119">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="5c45c-120">Partnercenter – REST-resurser</span><span class="sxs-lookup"><span data-stu-id="5c45c-120">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="5c45c-121">Definierar de JSON-konstruktioner som representerar de objekt som behövs för att använda REST API.</span><span class="sxs-lookup"><span data-stu-id="5c45c-121">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="5c45c-122">Partnercenter – REST-händelser</span><span class="sxs-lookup"><span data-stu-id="5c45c-122">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="5c45c-123">Definierar de REST-resursändringshändelser som stöds av PartnerCenter-webhookar.</span><span class="sxs-lookup"><span data-stu-id="5c45c-123">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="5c45c-124">Partnercenter – språk och nationella inställningar som stöds</span><span class="sxs-lookup"><span data-stu-id="5c45c-124">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="5c45c-125">Visar de språk och lands-/regionskoder som stöds i Partner Center-API:erna.</span><span class="sxs-lookup"><span data-stu-id="5c45c-125">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="5c45c-126">Partnercenter – webhooks</span><span class="sxs-lookup"><span data-stu-id="5c45c-126">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="5c45c-127">Så här tar du emot händelser, autentiserar ett återanrop och använder Partner Center-webhook-API:er för att skapa, visa och uppdatera en händelseregistrering.</span><span class="sxs-lookup"><span data-stu-id="5c45c-127">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |
