---
title: Partnercenter – REST API-ändringslogg
description: 'Den här sidan visar ändringar i REST-API: er för partner Center'
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: 79359414276a1259117a8f506bbfae4441cdcbed
ms.sourcegitcommit: f8ca3a14a763013fefafd3262d0a740881d1d7b1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/17/2020
ms.locfileid: "97770281"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="1b820-103">Ändringar i 2020 i samarbets-API: er i Partner Center</span><span class="sxs-lookup"><span data-stu-id="1b820-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="1b820-104">Sök efter ändringar i REST-API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="1b820-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="1b820-105">Förbättringar av API: er för utbildnings prissättning</span><span class="sxs-lookup"><span data-stu-id="1b820-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="1b820-106">Vad har ändrats?</span><span class="sxs-lookup"><span data-stu-id="1b820-106">What has changed?</span></span>

<span data-ttu-id="1b820-107">Partner Center-API: et har för närvarande GET-och-kvalifikationer för att verifiera utbildningens kunders berättigande.</span><span class="sxs-lookup"><span data-stu-id="1b820-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="1b820-108">Inga ändringar görs i GET kvalificerings-API: et.</span><span class="sxs-lookup"><span data-stu-id="1b820-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="1b820-109">Vi har dock lagt till ett retur ärende i API för att skicka kvalificering.</span><span class="sxs-lookup"><span data-stu-id="1b820-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="1b820-110">GET – ändras inte.</span><span class="sxs-lookup"><span data-stu-id="1b820-110">GET - doesn't change.</span></span> [<span data-ttu-id="1b820-111">Aktuell API-artikel</span><span class="sxs-lookup"><span data-stu-id="1b820-111">Current API article</span></span>](get-a-customer-s-qualification.md)
- <span data-ttu-id="1b820-112">Ärendet för att skicka returer läggs till.</span><span class="sxs-lookup"><span data-stu-id="1b820-112">PUT - return case will be added.</span></span> [<span data-ttu-id="1b820-113">Aktuell API-artikel</span><span class="sxs-lookup"><span data-stu-id="1b820-113">Current API article</span></span>](update-a-customer-s-qualification.md)

<span data-ttu-id="1b820-114">Dessa API: er kommer att dras tillbaka i slutet av februari 2021 och ersätts av nya API: er enligt beskrivningen nedan.</span><span class="sxs-lookup"><span data-stu-id="1b820-114">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="1b820-115">Scenarier som påverkas:</span><span class="sxs-lookup"><span data-stu-id="1b820-115">Scenarios impacted:</span></span>

<span data-ttu-id="1b820-116">Kund berättigande för utbildnings pris för utvalda SKU: er</span><span class="sxs-lookup"><span data-stu-id="1b820-116">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="1b820-117">Detalj beskrivningar</span><span class="sxs-lookup"><span data-stu-id="1b820-117">Detail descriptions</span></span>

<span data-ttu-id="1b820-118">Två nya API: er för GET-och POST-kvalifikationer kommer att införas.</span><span class="sxs-lookup"><span data-stu-id="1b820-118">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="1b820-119">De nya API: erna kommer att använda **kvalifikationer**, inte **kvalificering**.</span><span class="sxs-lookup"><span data-stu-id="1b820-119">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="1b820-120">API: er är tillgängliga för testning i FY21 Q2.</span><span class="sxs-lookup"><span data-stu-id="1b820-120">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="1b820-121">Hämta kvalifikationer</span><span class="sxs-lookup"><span data-stu-id="1b820-121">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="1b820-122">Svarsexempel:</span><span class="sxs-lookup"><span data-stu-id="1b820-122">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="1b820-123">Svars fält:</span><span class="sxs-lookup"><span data-stu-id="1b820-123">Response fields:</span></span> 

- <span data-ttu-id="1b820-124">VettingStatus-värden: godkänd, nekad, ingranskning osv.</span><span class="sxs-lookup"><span data-stu-id="1b820-124">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="1b820-125">VettingReason-värden:</span><span class="sxs-lookup"><span data-stu-id="1b820-125">VettingReason values:</span></span>
   - <span data-ttu-id="1b820-126">Inte en utbildnings kund</span><span class="sxs-lookup"><span data-stu-id="1b820-126">Not an Education Customer</span></span>
   - <span data-ttu-id="1b820-127">Inte längre en utbildnings kund</span><span class="sxs-lookup"><span data-stu-id="1b820-127">No longer an Education Customer</span></span>
   - <span data-ttu-id="1b820-128">Inte en utbildnings kund – efter granskning</span><span class="sxs-lookup"><span data-stu-id="1b820-128">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="1b820-129">Begränsad som en utbildnings kund</span><span class="sxs-lookup"><span data-stu-id="1b820-129">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="1b820-130">Inte en akademisk domän</span><span class="sxs-lookup"><span data-stu-id="1b820-130">Not an Academic Domain</span></span>
   - <span data-ttu-id="1b820-131">Inte ett giltigt bibliotek</span><span class="sxs-lookup"><span data-stu-id="1b820-131">Not an eligible Library</span></span>
   - <span data-ttu-id="1b820-132">Inte en giltig Museum</span><span class="sxs-lookup"><span data-stu-id="1b820-132">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="1b820-133">PUBLICERA kvalifikationer</span><span class="sxs-lookup"><span data-stu-id="1b820-133">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="1b820-134">Svarsexempel:</span><span class="sxs-lookup"><span data-stu-id="1b820-134">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="1b820-135">Nästa steg</span><span class="sxs-lookup"><span data-stu-id="1b820-135">Next steps</span></span>

[<span data-ttu-id="1b820-136">Partnercenter – REST API-referens</span><span class="sxs-lookup"><span data-stu-id="1b820-136">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
