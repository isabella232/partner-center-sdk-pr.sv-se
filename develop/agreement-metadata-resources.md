---
title: Avtals resurser för metadata
description: Resurs samlingen AgreementMetadata beskriver avtals typer som partner kan använda för att bekräfta kund godkännande.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768838"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="5a0b0-103">Avtals resurser för metadata</span><span class="sxs-lookup"><span data-stu-id="5a0b0-103">Agreement metadata resources</span></span>

<span data-ttu-id="5a0b0-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="5a0b0-104">**Applies to:**</span></span>

- <span data-ttu-id="5a0b0-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="5a0b0-105">Partner Center</span></span>

<span data-ttu-id="5a0b0-106">**AgreementMetaData** -resursen stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*.</span><span class="sxs-lookup"><span data-stu-id="5a0b0-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="5a0b0-107">Den här resursen gäller inte:</span><span class="sxs-lookup"><span data-stu-id="5a0b0-107">This resource isn't applicable to:</span></span>

- <span data-ttu-id="5a0b0-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="5a0b0-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5a0b0-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="5a0b0-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5a0b0-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5a0b0-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5a0b0-111">**AgreementMetaData** -samlingen innehåller metadata om alla avtals typer.</span><span class="sxs-lookup"><span data-stu-id="5a0b0-111">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="5a0b0-112">Partner kan använda den här samlingen för att tillhandahålla bekräftelse av kund godkännande av avtal.</span><span class="sxs-lookup"><span data-stu-id="5a0b0-112">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="5a0b0-113">**AgreementMetaData** -samlingen Returnerar metadata för båda avtals typerna (**Microsoft Cloud avtal** och **Microsofts kund avtal**).</span><span class="sxs-lookup"><span data-stu-id="5a0b0-113">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="5a0b0-114">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="5a0b0-114">AgreementMetaData</span></span>

<span data-ttu-id="5a0b0-115">Avtalade metadata som returneras innehåller följande egenskaper:</span><span class="sxs-lookup"><span data-stu-id="5a0b0-115">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="5a0b0-116">Egenskap</span><span class="sxs-lookup"><span data-stu-id="5a0b0-116">Property</span></span>      | <span data-ttu-id="5a0b0-117">Typ</span><span class="sxs-lookup"><span data-stu-id="5a0b0-117">Type</span></span>               | <span data-ttu-id="5a0b0-118">Description</span><span class="sxs-lookup"><span data-stu-id="5a0b0-118">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="5a0b0-119">templateId</span><span class="sxs-lookup"><span data-stu-id="5a0b0-119">templateId</span></span>    | <span data-ttu-id="5a0b0-120">sträng</span><span class="sxs-lookup"><span data-stu-id="5a0b0-120">string</span></span>             | <span data-ttu-id="5a0b0-121">Unikt ID för en avtals mal len.</span><span class="sxs-lookup"><span data-stu-id="5a0b0-121">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="5a0b0-122">typ</span><span class="sxs-lookup"><span data-stu-id="5a0b0-122">type</span></span>          | <span data-ttu-id="5a0b0-123">sträng</span><span class="sxs-lookup"><span data-stu-id="5a0b0-123">string</span></span>             | <span data-ttu-id="5a0b0-124">Avtals typ.</span><span class="sxs-lookup"><span data-stu-id="5a0b0-124">Agreement type.</span></span> <span data-ttu-id="5a0b0-125">De värden som stöds för närvarande är **MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement** (för hands version).</span><span class="sxs-lookup"><span data-stu-id="5a0b0-125">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="5a0b0-126">agreementLink</span><span class="sxs-lookup"><span data-stu-id="5a0b0-126">agreementLink</span></span> | <span data-ttu-id="5a0b0-127">sträng</span><span class="sxs-lookup"><span data-stu-id="5a0b0-127">string</span></span>             | <span data-ttu-id="5a0b0-128">URL till avtals mal len.</span><span class="sxs-lookup"><span data-stu-id="5a0b0-128">URL for the agreement template.</span></span>                                                    |
