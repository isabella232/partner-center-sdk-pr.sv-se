---
title: Avtalsdokumentresurser
description: AgreementDocument-resursen är ett Microsoft-avtalsdokument för förhandsgranskning och nedladdning. Det stöds av Partner Center i Microsofts offentliga moln.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 1a81da4f75594f241669db831125bd437872561c
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025674"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="90ed7-104">Avtalsdokumentresurser som stöds av PartnerCenter i Microsofts offentliga moln</span><span class="sxs-lookup"><span data-stu-id="90ed7-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="90ed7-105">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="90ed7-105">**Applies to**: Partner Center</span></span>

<span data-ttu-id="90ed7-106">**Gäller inte för:** Partner Center som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="90ed7-106">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="90ed7-107">**AgreementDocument-resursen** stöds för närvarande endast av PartnerCenter i Det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="90ed7-107">The **AgreementDocument** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="90ed7-108">**AgreementDocument-resursen** representerar ett Microsoft-avtalsdokument som är tillgängligt för förhandsgranskning och nedladdning.</span><span class="sxs-lookup"><span data-stu-id="90ed7-108">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="90ed7-109">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="90ed7-109">AgreementDocument</span></span>

<span data-ttu-id="90ed7-110">En **AgreementDocument-resurs** innehåller följande egenskaper:</span><span class="sxs-lookup"><span data-stu-id="90ed7-110">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="90ed7-111">Egenskap</span><span class="sxs-lookup"><span data-stu-id="90ed7-111">Property</span></span>       | <span data-ttu-id="90ed7-112">Typ</span><span class="sxs-lookup"><span data-stu-id="90ed7-112">Type</span></span>   | <span data-ttu-id="90ed7-113">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="90ed7-113">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="90ed7-114">land</span><span class="sxs-lookup"><span data-stu-id="90ed7-114">country</span></span> | <span data-ttu-id="90ed7-115">sträng</span><span class="sxs-lookup"><span data-stu-id="90ed7-115">string</span></span> | <span data-ttu-id="90ed7-116">Land eller marknad som det här dokumentet gäller för.</span><span class="sxs-lookup"><span data-stu-id="90ed7-116">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="90ed7-117">language</span><span class="sxs-lookup"><span data-stu-id="90ed7-117">language</span></span> | <span data-ttu-id="90ed7-118">sträng</span><span class="sxs-lookup"><span data-stu-id="90ed7-118">string</span></span> | <span data-ttu-id="90ed7-119">Det språk som det här dokumentet är lokaliserat på.</span><span class="sxs-lookup"><span data-stu-id="90ed7-119">The language in which this document is localized.</span></span> |
| <span data-ttu-id="90ed7-120">displayUri</span><span class="sxs-lookup"><span data-stu-id="90ed7-120">displayUri</span></span> | <span data-ttu-id="90ed7-121">sträng</span><span class="sxs-lookup"><span data-stu-id="90ed7-121">string</span></span> | <span data-ttu-id="90ed7-122">En länk för att förhandsgranska avtalsdokumentet i en webbläsare.</span><span class="sxs-lookup"><span data-stu-id="90ed7-122">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="90ed7-123">downloadUri</span><span class="sxs-lookup"><span data-stu-id="90ed7-123">downloadUri</span></span> |<span data-ttu-id="90ed7-124">sträng</span><span class="sxs-lookup"><span data-stu-id="90ed7-124">string</span></span> | <span data-ttu-id="90ed7-125">En länk för att ladda ned avtalsdokumentet (i Microsoft Word format).</span><span class="sxs-lookup"><span data-stu-id="90ed7-125">A link to download the agreement document (in Microsoft Word format).</span></span> |
