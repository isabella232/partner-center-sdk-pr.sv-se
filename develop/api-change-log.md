---
title: Partnercenter – REST API-ändringslogg
description: På den här sidan visas ändringar i Partner Center REST API:er
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572003"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="e9d18-103">December 2020 -ändringar i Partner Center REST API:er</span><span class="sxs-lookup"><span data-stu-id="e9d18-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="e9d18-104">Kontrollera här om det finns ändringar i Partner Center REST API:er.</span><span class="sxs-lookup"><span data-stu-id="e9d18-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="e9d18-105">Förbättringar av API:er för berättigande till utbildningspriser</span><span class="sxs-lookup"><span data-stu-id="e9d18-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="e9d18-106">Vad har ändrats?</span><span class="sxs-lookup"><span data-stu-id="e9d18-106">What has changed?</span></span>

<span data-ttu-id="e9d18-107">Partner Center-API:et har för närvarande GET- och PUT-kvalificeringar för att verifiera berättigandet för Education-kunder.</span><span class="sxs-lookup"><span data-stu-id="e9d18-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="e9d18-108">Det kommer inte att ske några ändringar i GET-kvalificerings-API:et.</span><span class="sxs-lookup"><span data-stu-id="e9d18-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="e9d18-109">Vi har dock lagt till ett returfall i PUT-kvalificerings-API:et.</span><span class="sxs-lookup"><span data-stu-id="e9d18-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="e9d18-110">GET – ändras inte.</span><span class="sxs-lookup"><span data-stu-id="e9d18-110">GET - doesn't change.</span></span>
- <span data-ttu-id="e9d18-111">PUT – returfall läggs till.</span><span class="sxs-lookup"><span data-stu-id="e9d18-111">PUT - return case will be added.</span></span>

<span data-ttu-id="e9d18-112">Dessa API:er dras tillbaka i slutet av februari 2021 för att ersättas med nya API:er enligt beskrivningen nedan.</span><span class="sxs-lookup"><span data-stu-id="e9d18-112">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="e9d18-113">Scenarier som påverkas:</span><span class="sxs-lookup"><span data-stu-id="e9d18-113">Scenarios impacted:</span></span>

<span data-ttu-id="e9d18-114">Kundberättigande till utbildningsprissättning för utvalda SKU:er</span><span class="sxs-lookup"><span data-stu-id="e9d18-114">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="e9d18-115">Informationsbeskrivningar</span><span class="sxs-lookup"><span data-stu-id="e9d18-115">Detail descriptions</span></span>

<span data-ttu-id="e9d18-116">Två nya GET- och POST-kvalificerings-API:er kommer att introduceras.</span><span class="sxs-lookup"><span data-stu-id="e9d18-116">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="e9d18-117">De nya API:erna kommer att använda **kvalificering**, inte **kvalificering.**</span><span class="sxs-lookup"><span data-stu-id="e9d18-117">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="e9d18-118">API:erna kommer att vara tillgängliga för testning under FY21 Q2.</span><span class="sxs-lookup"><span data-stu-id="e9d18-118">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="e9d18-119">GET-kvalificeringar</span><span class="sxs-lookup"><span data-stu-id="e9d18-119">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="e9d18-120">Svarsexempel:</span><span class="sxs-lookup"><span data-stu-id="e9d18-120">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="e9d18-121">Svarsfält:</span><span class="sxs-lookup"><span data-stu-id="e9d18-121">Response fields:</span></span> 

- <span data-ttu-id="e9d18-122">VettingStatus-värden: Godkänd, Nekad, InReview osv.</span><span class="sxs-lookup"><span data-stu-id="e9d18-122">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="e9d18-123">VettingReason-värden:</span><span class="sxs-lookup"><span data-stu-id="e9d18-123">VettingReason values:</span></span>
   - <span data-ttu-id="e9d18-124">Inte utbildningskund</span><span class="sxs-lookup"><span data-stu-id="e9d18-124">Not an Education Customer</span></span>
   - <span data-ttu-id="e9d18-125">Inte längre utbildningskund</span><span class="sxs-lookup"><span data-stu-id="e9d18-125">No longer an Education Customer</span></span>
   - <span data-ttu-id="e9d18-126">Inte utbildningskund – efter granskning</span><span class="sxs-lookup"><span data-stu-id="e9d18-126">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="e9d18-127">Begränsad att vara utbildningskund</span><span class="sxs-lookup"><span data-stu-id="e9d18-127">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="e9d18-128">Inte en academic-domän</span><span class="sxs-lookup"><span data-stu-id="e9d18-128">Not an Academic Domain</span></span>
   - <span data-ttu-id="e9d18-129">Inte ett kvalificerande bibliotek</span><span class="sxs-lookup"><span data-stu-id="e9d18-129">Not an eligible Library</span></span>
   - <span data-ttu-id="e9d18-130">Inte berättigad Till detta</span><span class="sxs-lookup"><span data-stu-id="e9d18-130">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="e9d18-131">POST-kvalificeringar</span><span class="sxs-lookup"><span data-stu-id="e9d18-131">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="e9d18-132">Svarsexempel:</span><span class="sxs-lookup"><span data-stu-id="e9d18-132">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="e9d18-133">Nästa steg</span><span class="sxs-lookup"><span data-stu-id="e9d18-133">Next steps</span></span>

[<span data-ttu-id="e9d18-134">Partnercenter – REST API-referens</span><span class="sxs-lookup"><span data-stu-id="e9d18-134">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
