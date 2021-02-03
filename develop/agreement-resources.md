---
title: Avtals resurser
description: Avtals resursen representerar ett Microsoft Cloud kund avtal med information om certifieringen som tillhandahålls av partnern.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770020"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="a468b-103">Avtals resurser som representerar ett Microsofts moln kund avtal</span><span class="sxs-lookup"><span data-stu-id="a468b-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="a468b-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="a468b-104">**Applies to:**</span></span>

- <span data-ttu-id="a468b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a468b-105">Partner Center</span></span>

<span data-ttu-id="a468b-106">**Avtals** resursen stöds för närvarande av Partner Center i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="a468b-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="a468b-107">Den gäller inte för:</span><span class="sxs-lookup"><span data-stu-id="a468b-107">It isn't applicable to:</span></span>

- <span data-ttu-id="a468b-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a468b-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a468b-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="a468b-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a468b-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a468b-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a468b-111">**Avtals** resursen representerar ett Microsofts moln kund avtal.</span><span class="sxs-lookup"><span data-stu-id="a468b-111">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="a468b-112">Avtal</span><span class="sxs-lookup"><span data-stu-id="a468b-112">Agreement</span></span>

<span data-ttu-id="a468b-113">**Avtals** resursen representerar information om certifieringen som tillhandahålls av partnern.</span><span class="sxs-lookup"><span data-stu-id="a468b-113">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="a468b-114">Egenskap</span><span class="sxs-lookup"><span data-stu-id="a468b-114">Property</span></span>       | <span data-ttu-id="a468b-115">Typ</span><span class="sxs-lookup"><span data-stu-id="a468b-115">Type</span></span>   | <span data-ttu-id="a468b-116">Description</span><span class="sxs-lookup"><span data-stu-id="a468b-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a468b-117">userId</span><span class="sxs-lookup"><span data-stu-id="a468b-117">userId</span></span>         | <span data-ttu-id="a468b-118">sträng</span><span class="sxs-lookup"><span data-stu-id="a468b-118">string</span></span>                         | <span data-ttu-id="a468b-119">Objekt identifierare för den inloggade användaren i partner innehavaren som tillhandahåller bekräftelse på uppdrag av partner organisationen.</span><span class="sxs-lookup"><span data-stu-id="a468b-119">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="a468b-120">När du använder app + användarautentisering för att skapa en avtals resurs härleder Partner Center automatiskt in **userId** -attributvärdet från App + User token.</span><span class="sxs-lookup"><span data-stu-id="a468b-120">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="a468b-121">primaryContact</span><span class="sxs-lookup"><span data-stu-id="a468b-121">primaryContact</span></span> | [<span data-ttu-id="a468b-122">Kontakt</span><span class="sxs-lookup"><span data-stu-id="a468b-122">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="a468b-123">Information om användaren från kund organisationen som har godkänt avtalet, inklusive:  **FirstName**, **LastName**, **email** och **telefonnummer** (valfritt).</span><span class="sxs-lookup"><span data-stu-id="a468b-123">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="a468b-124">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="a468b-124">dateAgreed</span></span>     | <span data-ttu-id="a468b-125">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="a468b-125">string in UTC date time format</span></span> | <span data-ttu-id="a468b-126">Datumet då kunden godkände avtalet.</span><span class="sxs-lookup"><span data-stu-id="a468b-126">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="a468b-127">templateId</span><span class="sxs-lookup"><span data-stu-id="a468b-127">templateId</span></span>     |<span data-ttu-id="a468b-128">sträng</span><span class="sxs-lookup"><span data-stu-id="a468b-128">string</span></span>                          | <span data-ttu-id="a468b-129">Unik identifierare för det avtal som kunden har accepterat.</span><span class="sxs-lookup"><span data-stu-id="a468b-129">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="a468b-130">typ</span><span class="sxs-lookup"><span data-stu-id="a468b-130">type</span></span>           |<span data-ttu-id="a468b-131">sträng</span><span class="sxs-lookup"><span data-stu-id="a468b-131">string</span></span>                          | <span data-ttu-id="a468b-132">Avtals typ.</span><span class="sxs-lookup"><span data-stu-id="a468b-132">Agreement type.</span></span> <span data-ttu-id="a468b-133">De värden som stöds för närvarande är **MicrosoftCloudAgreement** och **MicrosoftCustomerAgreement**.</span><span class="sxs-lookup"><span data-stu-id="a468b-133">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="a468b-134">agreementLink</span><span class="sxs-lookup"><span data-stu-id="a468b-134">agreementLink</span></span>  | <span data-ttu-id="a468b-135">sträng</span><span class="sxs-lookup"><span data-stu-id="a468b-135">string</span></span>                         | <span data-ttu-id="a468b-136">URL till avtals mal len.</span><span class="sxs-lookup"><span data-stu-id="a468b-136">URL for the agreement template.</span></span>                                                    |
