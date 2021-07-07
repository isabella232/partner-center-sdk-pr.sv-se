---
title: Avtalsresurser
description: Avtalsresursen representerar ett Microsoft-molnkundavtal med information om certifiering som tillhandahålls av partnern.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025633"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="03ab0-103">Avtalsresurser som representerar ett Microsoft Cloud-kundavtal</span><span class="sxs-lookup"><span data-stu-id="03ab0-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="03ab0-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="03ab0-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="03ab0-105">**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="03ab0-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="03ab0-106">**Avtalsresursen** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="03ab0-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="03ab0-107">**Avtalsresursen** representerar ett Microsoft Cloud-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="03ab0-107">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="03ab0-108">Avtal</span><span class="sxs-lookup"><span data-stu-id="03ab0-108">Agreement</span></span>

<span data-ttu-id="03ab0-109">**Avtalsresursen** representerar information om certifiering som tillhandahålls av partnern.</span><span class="sxs-lookup"><span data-stu-id="03ab0-109">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="03ab0-110">Egenskap</span><span class="sxs-lookup"><span data-stu-id="03ab0-110">Property</span></span>       | <span data-ttu-id="03ab0-111">Typ</span><span class="sxs-lookup"><span data-stu-id="03ab0-111">Type</span></span>   | <span data-ttu-id="03ab0-112">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="03ab0-112">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="03ab0-113">userId</span><span class="sxs-lookup"><span data-stu-id="03ab0-113">userId</span></span>         | <span data-ttu-id="03ab0-114">sträng</span><span class="sxs-lookup"><span data-stu-id="03ab0-114">string</span></span>                         | <span data-ttu-id="03ab0-115">Objektidentifierare för den inloggade användaren i partnerklientorganisationen som bekräftar för partnerorganisationens räkning.</span><span class="sxs-lookup"><span data-stu-id="03ab0-115">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="03ab0-116">När du använder app- och användarautentisering för att skapa en avtalsresurs, härleder Partnercenter automatiskt **userId-attributvärdet** från app- och användartoken.</span><span class="sxs-lookup"><span data-stu-id="03ab0-116">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="03ab0-117">primaryContact</span><span class="sxs-lookup"><span data-stu-id="03ab0-117">primaryContact</span></span> | [<span data-ttu-id="03ab0-118">Kontakt</span><span class="sxs-lookup"><span data-stu-id="03ab0-118">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="03ab0-119">Information om användaren från kundorganisationen som godkände avtalet, inklusive:  **firstName,** **lastName,** **email** och **phoneNumber** (valfritt).</span><span class="sxs-lookup"><span data-stu-id="03ab0-119">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="03ab0-120">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="03ab0-120">dateAgreed</span></span>     | <span data-ttu-id="03ab0-121">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="03ab0-121">string in UTC date time format</span></span> | <span data-ttu-id="03ab0-122">Det datum då kunden godkände avtalet.</span><span class="sxs-lookup"><span data-stu-id="03ab0-122">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="03ab0-123">templateId</span><span class="sxs-lookup"><span data-stu-id="03ab0-123">templateId</span></span>     |<span data-ttu-id="03ab0-124">sträng</span><span class="sxs-lookup"><span data-stu-id="03ab0-124">string</span></span>                          | <span data-ttu-id="03ab0-125">Unik identifierare för det avtal som kunden har accepterat.</span><span class="sxs-lookup"><span data-stu-id="03ab0-125">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="03ab0-126">typ</span><span class="sxs-lookup"><span data-stu-id="03ab0-126">type</span></span>           |<span data-ttu-id="03ab0-127">sträng</span><span class="sxs-lookup"><span data-stu-id="03ab0-127">string</span></span>                          | <span data-ttu-id="03ab0-128">Avtalstyp.</span><span class="sxs-lookup"><span data-stu-id="03ab0-128">Agreement type.</span></span> <span data-ttu-id="03ab0-129">Värden som stöds är för **närvarande MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement.**</span><span class="sxs-lookup"><span data-stu-id="03ab0-129">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="03ab0-130">agreementLink</span><span class="sxs-lookup"><span data-stu-id="03ab0-130">agreementLink</span></span>  | <span data-ttu-id="03ab0-131">sträng</span><span class="sxs-lookup"><span data-stu-id="03ab0-131">string</span></span>                         | <span data-ttu-id="03ab0-132">URL för avtalsmallen.</span><span class="sxs-lookup"><span data-stu-id="03ab0-132">URL for the agreement template.</span></span>                                                    |
