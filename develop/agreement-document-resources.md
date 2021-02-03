---
title: Avtals dokument resurser
description: AgreementDocument-resursen är ett Microsoft Agreement-dokument för för hands version och nedladdning. Den stöds av Partner Center i det offentliga Microsoft-molnet.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770029"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="298d9-104">Avtals dokument resurser som stöds av Partner Center i det offentliga Microsoft-molnet</span><span class="sxs-lookup"><span data-stu-id="298d9-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="298d9-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="298d9-105">**Applies to:**</span></span>

- <span data-ttu-id="298d9-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="298d9-106">Partner Center</span></span>

<span data-ttu-id="298d9-107">**AgreementDocument** -resursen stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*.</span><span class="sxs-lookup"><span data-stu-id="298d9-107">The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="298d9-108">Den här resursen är inte tillämplig för:</span><span class="sxs-lookup"><span data-stu-id="298d9-108">This resource not applicable to:</span></span>

- <span data-ttu-id="298d9-109">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="298d9-109">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="298d9-110">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="298d9-110">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="298d9-111">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="298d9-111">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="298d9-112">**AgreementDocument** -resursen representerar ett Microsoft Agreement-dokument som är tillgängligt för för hands version och nedladdning.</span><span class="sxs-lookup"><span data-stu-id="298d9-112">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="298d9-113">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="298d9-113">AgreementDocument</span></span>

<span data-ttu-id="298d9-114">En **AgreementDocument** -resurs innehåller följande egenskaper:</span><span class="sxs-lookup"><span data-stu-id="298d9-114">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="298d9-115">Egenskap</span><span class="sxs-lookup"><span data-stu-id="298d9-115">Property</span></span>       | <span data-ttu-id="298d9-116">Typ</span><span class="sxs-lookup"><span data-stu-id="298d9-116">Type</span></span>   | <span data-ttu-id="298d9-117">Description</span><span class="sxs-lookup"><span data-stu-id="298d9-117">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="298d9-118">land</span><span class="sxs-lookup"><span data-stu-id="298d9-118">country</span></span> | <span data-ttu-id="298d9-119">sträng</span><span class="sxs-lookup"><span data-stu-id="298d9-119">string</span></span> | <span data-ttu-id="298d9-120">Landet eller marknaden som detta dokument gäller.</span><span class="sxs-lookup"><span data-stu-id="298d9-120">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="298d9-121">language</span><span class="sxs-lookup"><span data-stu-id="298d9-121">language</span></span> | <span data-ttu-id="298d9-122">sträng</span><span class="sxs-lookup"><span data-stu-id="298d9-122">string</span></span> | <span data-ttu-id="298d9-123">Språket som det här dokumentet är lokaliserat till.</span><span class="sxs-lookup"><span data-stu-id="298d9-123">The language in which this document is localized.</span></span> |
| <span data-ttu-id="298d9-124">displayUri</span><span class="sxs-lookup"><span data-stu-id="298d9-124">displayUri</span></span> | <span data-ttu-id="298d9-125">sträng</span><span class="sxs-lookup"><span data-stu-id="298d9-125">string</span></span> | <span data-ttu-id="298d9-126">En länk för att förhandsgranska avtals dokumentet i en webbläsare.</span><span class="sxs-lookup"><span data-stu-id="298d9-126">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="298d9-127">downloadUri</span><span class="sxs-lookup"><span data-stu-id="298d9-127">downloadUri</span></span> |<span data-ttu-id="298d9-128">sträng</span><span class="sxs-lookup"><span data-stu-id="298d9-128">string</span></span> | <span data-ttu-id="298d9-129">En länk för att ladda ned avtals dokumentet (i Microsoft Word-format).</span><span class="sxs-lookup"><span data-stu-id="298d9-129">A link to download the agreement document (in Microsoft Word format).</span></span> |
