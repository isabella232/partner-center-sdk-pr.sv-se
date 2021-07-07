---
title: Resurser för avtalsmetadata
description: AgreementMetadata-resurssamlingen beskriver avtalstyper som partner kan använda för att bekräfta kundens godkännande.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025639"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="555e1-103">Resurser för avtalsmetadata</span><span class="sxs-lookup"><span data-stu-id="555e1-103">Agreement metadata resources</span></span>

<span data-ttu-id="555e1-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="555e1-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="555e1-105">**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="555e1-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="555e1-106">**AgreementMetaData-resursen** stöds för närvarande endast av Partnercenter i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="555e1-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span> 

<span data-ttu-id="555e1-107">**AgreementMetaData-samlingen** innehåller metadata om alla avtalstyper.</span><span class="sxs-lookup"><span data-stu-id="555e1-107">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="555e1-108">Partner kan använda den här samlingen för att bekräfta kundens godkännande av avtal.</span><span class="sxs-lookup"><span data-stu-id="555e1-108">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="555e1-109">**AgreementMetaData-samlingen** returnerar metadata för båda avtalstyperna (**Microsoft Cloud-avtal** **och Microsoft-kundavtal**).</span><span class="sxs-lookup"><span data-stu-id="555e1-109">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="555e1-110">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="555e1-110">AgreementMetaData</span></span>

<span data-ttu-id="555e1-111">Returnerade avtalsmetadata innehåller följande egenskaper:</span><span class="sxs-lookup"><span data-stu-id="555e1-111">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="555e1-112">Egenskap</span><span class="sxs-lookup"><span data-stu-id="555e1-112">Property</span></span>      | <span data-ttu-id="555e1-113">Typ</span><span class="sxs-lookup"><span data-stu-id="555e1-113">Type</span></span>               | <span data-ttu-id="555e1-114">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="555e1-114">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="555e1-115">templateId</span><span class="sxs-lookup"><span data-stu-id="555e1-115">templateId</span></span>    | <span data-ttu-id="555e1-116">sträng</span><span class="sxs-lookup"><span data-stu-id="555e1-116">string</span></span>             | <span data-ttu-id="555e1-117">Unik identifierare för en avtalsmall.</span><span class="sxs-lookup"><span data-stu-id="555e1-117">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="555e1-118">typ</span><span class="sxs-lookup"><span data-stu-id="555e1-118">type</span></span>          | <span data-ttu-id="555e1-119">sträng</span><span class="sxs-lookup"><span data-stu-id="555e1-119">string</span></span>             | <span data-ttu-id="555e1-120">Avtalstyp.</span><span class="sxs-lookup"><span data-stu-id="555e1-120">Agreement type.</span></span> <span data-ttu-id="555e1-121">Värden som stöds är för **närvarande MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement** (förhandsversion).</span><span class="sxs-lookup"><span data-stu-id="555e1-121">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="555e1-122">agreementLink</span><span class="sxs-lookup"><span data-stu-id="555e1-122">agreementLink</span></span> | <span data-ttu-id="555e1-123">sträng</span><span class="sxs-lookup"><span data-stu-id="555e1-123">string</span></span>             | <span data-ttu-id="555e1-124">URL för avtalsmallen.</span><span class="sxs-lookup"><span data-stu-id="555e1-124">URL for the agreement template.</span></span>                                                    |
