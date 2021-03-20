---
title: Partnercenter – REST API-ändringslogg
description: 'Den här sidan visar ändringar i REST-API: er för partner Center'
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: b2c2cac36a8bd1bec7aa5bf6e5d1aa73b4779535
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711856"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="cd16e-103">Ändringar i 2020 i samarbets-API: er i Partner Center</span><span class="sxs-lookup"><span data-stu-id="cd16e-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="cd16e-104">Sök efter ändringar i REST-API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="cd16e-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="cd16e-105">Förbättringar av API: er för utbildnings prissättning</span><span class="sxs-lookup"><span data-stu-id="cd16e-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="cd16e-106">Vad har ändrats?</span><span class="sxs-lookup"><span data-stu-id="cd16e-106">What has changed?</span></span>

<span data-ttu-id="cd16e-107">Partner Center-API: et har för närvarande GET-och-kvalifikationer för att verifiera utbildningens kunders berättigande.</span><span class="sxs-lookup"><span data-stu-id="cd16e-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="cd16e-108">Inga ändringar görs i GET kvalificerings-API: et.</span><span class="sxs-lookup"><span data-stu-id="cd16e-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="cd16e-109">Vi har dock lagt till ett retur ärende i API för att skicka kvalificering.</span><span class="sxs-lookup"><span data-stu-id="cd16e-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="cd16e-110">GET – ändras inte.</span><span class="sxs-lookup"><span data-stu-id="cd16e-110">GET - doesn't change.</span></span> [<span data-ttu-id="cd16e-111">Aktuell API-artikel</span><span class="sxs-lookup"><span data-stu-id="cd16e-111">Current API article</span></span>](./get-customer-qualification-synchronous.md)
- <span data-ttu-id="cd16e-112">Ärendet för att skicka returer läggs till.</span><span class="sxs-lookup"><span data-stu-id="cd16e-112">PUT - return case will be added.</span></span> [<span data-ttu-id="cd16e-113">Aktuell API-artikel</span><span class="sxs-lookup"><span data-stu-id="cd16e-113">Current API article</span></span>](./update-customer-qualification-synchronous.md)

<span data-ttu-id="cd16e-114">Dessa API: er kommer att dras tillbaka i slutet av februari 2021 och ersätts av nya API: er enligt beskrivningen nedan.</span><span class="sxs-lookup"><span data-stu-id="cd16e-114">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="cd16e-115">Scenarier som påverkas:</span><span class="sxs-lookup"><span data-stu-id="cd16e-115">Scenarios impacted:</span></span>

<span data-ttu-id="cd16e-116">Kund berättigande för utbildnings pris för utvalda SKU: er</span><span class="sxs-lookup"><span data-stu-id="cd16e-116">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="cd16e-117">Detalj beskrivningar</span><span class="sxs-lookup"><span data-stu-id="cd16e-117">Detail descriptions</span></span>

<span data-ttu-id="cd16e-118">Två nya API: er för GET-och POST-kvalifikationer kommer att införas.</span><span class="sxs-lookup"><span data-stu-id="cd16e-118">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="cd16e-119">De nya API: erna kommer att använda **kvalifikationer**, inte **kvalificering**.</span><span class="sxs-lookup"><span data-stu-id="cd16e-119">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="cd16e-120">API: er är tillgängliga för testning i FY21 Q2.</span><span class="sxs-lookup"><span data-stu-id="cd16e-120">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="cd16e-121">Hämta kvalifikationer</span><span class="sxs-lookup"><span data-stu-id="cd16e-121">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="cd16e-122">Svarsexempel:</span><span class="sxs-lookup"><span data-stu-id="cd16e-122">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="cd16e-123">Svars fält:</span><span class="sxs-lookup"><span data-stu-id="cd16e-123">Response fields:</span></span> 

- <span data-ttu-id="cd16e-124">VettingStatus-värden: godkänd, nekad, ingranskning osv.</span><span class="sxs-lookup"><span data-stu-id="cd16e-124">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="cd16e-125">VettingReason-värden:</span><span class="sxs-lookup"><span data-stu-id="cd16e-125">VettingReason values:</span></span>
   - <span data-ttu-id="cd16e-126">Inte en utbildnings kund</span><span class="sxs-lookup"><span data-stu-id="cd16e-126">Not an Education Customer</span></span>
   - <span data-ttu-id="cd16e-127">Inte längre en utbildnings kund</span><span class="sxs-lookup"><span data-stu-id="cd16e-127">No longer an Education Customer</span></span>
   - <span data-ttu-id="cd16e-128">Inte en utbildnings kund – efter granskning</span><span class="sxs-lookup"><span data-stu-id="cd16e-128">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="cd16e-129">Begränsad som en utbildnings kund</span><span class="sxs-lookup"><span data-stu-id="cd16e-129">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="cd16e-130">Inte en akademisk domän</span><span class="sxs-lookup"><span data-stu-id="cd16e-130">Not an Academic Domain</span></span>
   - <span data-ttu-id="cd16e-131">Inte ett giltigt bibliotek</span><span class="sxs-lookup"><span data-stu-id="cd16e-131">Not an eligible Library</span></span>
   - <span data-ttu-id="cd16e-132">Inte en giltig Museum</span><span class="sxs-lookup"><span data-stu-id="cd16e-132">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="cd16e-133">PUBLICERA kvalifikationer</span><span class="sxs-lookup"><span data-stu-id="cd16e-133">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="cd16e-134">Svarsexempel:</span><span class="sxs-lookup"><span data-stu-id="cd16e-134">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="cd16e-135">Nästa steg</span><span class="sxs-lookup"><span data-stu-id="cd16e-135">Next steps</span></span>

[<span data-ttu-id="cd16e-136">Partnercenter – REST API-referens</span><span class="sxs-lookup"><span data-stu-id="cd16e-136">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)