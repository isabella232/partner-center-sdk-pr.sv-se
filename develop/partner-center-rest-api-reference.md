---
title: Partnercenter – REST API-referens
description: 'Lär dig hur CSP-partner kan använda Partner Center REST-API: er för att integrera sina CRM-och fakturerings program med Microsoft-system för att hantera kund konton bättre.'
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 3f83b2b73c3480f76646cae4fcbbcbacd31d4b3f
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769942"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="7a554-103">Partner Center REST API referens till REST-URL: er, REST-rubriker, REST-resurser och REST-händelser</span><span class="sxs-lookup"><span data-stu-id="7a554-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="7a554-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="7a554-104">**Applies to:**</span></span>

- <span data-ttu-id="7a554-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7a554-105">Partner Center</span></span>
- <span data-ttu-id="7a554-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="7a554-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7a554-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="7a554-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7a554-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7a554-108">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="7a554-109">Partner Center-REST API</span><span class="sxs-lookup"><span data-stu-id="7a554-109">Partner Center REST API</span></span>

<span data-ttu-id="7a554-110">Partner Center REST API hjälper leverantörer av moln lösnings leverantörer (CSP) att integrera sin befintliga CRM-eller fakturerings program vara med de Microsoft-system som hanterar kund konton, placerar order, hanterar prenumerationer och hanterar support förfrågningar.</span><span class="sxs-lookup"><span data-stu-id="7a554-110">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="7a554-111">Mer information om vad API: et kan göra, inklusive exempel kod, finns i avsnittet om [scenarier](scenarios.md) , inklusive översikt över bakgrunden.</span><span class="sxs-lookup"><span data-stu-id="7a554-111">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="7a554-112">Innan du börjar koda läser du avsnittet [Kom igång](get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="7a554-112">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="7a554-113">Den här artikeln innehåller information om hur du konfigurerar test-och produktions konton, hur du får autentisering och hur du hittar exempel koden.</span><span class="sxs-lookup"><span data-stu-id="7a554-113">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

## <a name="topics"></a><span data-ttu-id="7a554-114">Ämnen</span><span class="sxs-lookup"><span data-stu-id="7a554-114">Topics</span></span>

| <span data-ttu-id="7a554-115">Avsnitt</span><span class="sxs-lookup"><span data-stu-id="7a554-115">Topic</span></span> | <span data-ttu-id="7a554-116">Description</span><span class="sxs-lookup"><span data-stu-id="7a554-116">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="7a554-117">Partnercenter – REST-URL:er</span><span class="sxs-lookup"><span data-stu-id="7a554-117">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="7a554-118">Definierar REST API-slutpunkter för olika versioner av Partner Center.</span><span class="sxs-lookup"><span data-stu-id="7a554-118">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="7a554-119">Partnercenter – REST-huvuden</span><span class="sxs-lookup"><span data-stu-id="7a554-119">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="7a554-120">Definierar de begärandehuvuden och svarshuvuden som används av REST API.</span><span class="sxs-lookup"><span data-stu-id="7a554-120">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="7a554-121">Partnercenter – REST-resurser</span><span class="sxs-lookup"><span data-stu-id="7a554-121">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="7a554-122">Definierar de JSON-konstruktioner som representerar de objekt som behövs för att använda REST API.</span><span class="sxs-lookup"><span data-stu-id="7a554-122">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="7a554-123">Partnercenter – REST-händelser</span><span class="sxs-lookup"><span data-stu-id="7a554-123">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="7a554-124">Definierar REST-resursens ändrings händelser som stöds av Partner Center-webhookar.</span><span class="sxs-lookup"><span data-stu-id="7a554-124">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="7a554-125">Partnercenter – språk och nationella inställningar som stöds</span><span class="sxs-lookup"><span data-stu-id="7a554-125">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="7a554-126">Visar en lista över nationella inställningar, språk och lands-/regions koder som stöds i API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="7a554-126">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="7a554-127">Partnercenter – webhooks</span><span class="sxs-lookup"><span data-stu-id="7a554-127">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="7a554-128">Hur du tar emot händelser, autentiserar en motringning och använder webhook-API: er för partner Center för att skapa, Visa och uppdatera en händelse registrering.</span><span class="sxs-lookup"><span data-stu-id="7a554-128">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |