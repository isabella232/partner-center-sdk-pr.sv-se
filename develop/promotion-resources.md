---
title: Uppflyttningsresurser
description: Beskriver resurserna för kampanjer som tillämpas på transaktioner för nya handelsprenumerationer.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6a0b38576f5756a127fe6ba787f970db9ac59be3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716012"
---
# <a name="promotions-resources"></a>Kampanjresurser

**Gäller för**

- Partnercenter

**Lämpliga roller**

- Global administratör
- Administratörsagent

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av Microsoft 365 och Dynamics 365.

Beskriver resurserna för kampanjer som tillämpas på transaktioner för nya handelsprenumerationer.

## <a name="promotion"></a>Kampanj

Rabatt som tillämpas vid köp av en produkt-SKU om villkoren för berättigande är uppfyllda.

| Egenskap          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| id | sträng                  | Befordrans identifierare. |
| name | sträng                  | Det egna namnet på befordran. |
| beskrivning | sträng                  | En beskrivning av befordran. |
| Startdate | sträng | Startdatumet för när befordran gäller. |
| endDate | sträng  | Slutdatumet för när befordran gäller. |
| requiredProducts | lista över requiredProducts | Produkt-, SKU-information och prissättningsprinciper som befordran gäller för. | 
| properties | lista över egenskaper | Egenskaper för befordran, inklusive om befordran är automatiskt tillämplig. | 

## <a name="requiredproducts"></a>RequiredProducts

Produkt-, SKU-information och prissättningsprinciper som befordran gäller för.

| Egenskap          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| productId| sträng | En identifierare för produkten som befordran är tillgänglig för. |
| skuId | sträng | En identifierare för den SKU som befordran är tillgänglig för. |
| Benämna | Period | En period som omfattar varaktighet och faktureringsperiod som befordran är tillgänglig för. |
| pricingPolicies| Lista över pricingPolicies | En lista över principer som definierar rabatttyperna och värdena för befordran. |

## <a name="term"></a>Period

Representerar en term för vilken befordran kan köpas.

| Egenskap          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| varaktighet          | sträng                  | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (en månad), P1Y (ett år) och P3Y (tre år). 
| billingCycle      | sträng | Beskriver hur ofta befordran kommer att tillämpas på faktureringen. Värdena kan vara Månadsvis, Årlig, OneTime eller Okänd. | 

## <a name="pricingpolicies"></a>PricingPolicies

Beskriv rabatttyper och värden för befordran.

| Egenskap          | Typ               | Description                                                                  |          
|-------------------|--------------------|------------------------------------------------------------------------------|
| typ | sträng | Beskriv om rabatten baseras på procentandelar eller rabatter med fast pris. |
| värde | sträng  | Definierar mängden rabatt som tillämpas. |

## <a name="properties"></a>Egenskaper

Egenskaper för befordran.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| isAutoApplicable  | boolesk  | Anger om befordran tillämpas automatiskt eller om den måste skickas av partnern. |


## <a name="promotioneligibilitiesrequestitem"></a>PromotionEligibilitiesRequestItem

Egenskaper som representerar en transaktion och en befordrans berättigande.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| Identifierare för kampanjeligiitetsobjekt. |
| catalogItemId | sträng | Katalogobjektets identifierare som befordran kommer att tillämpas på. Innehåller produkt-ID, SKU-ID och tillgänglighets-ID. |
| quantity | int | Antalet licenser eller instanser. |
| termDuration | sträng | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (en månad), P1Y (ett år) och P3Y (tre år). |
| billingCycle | sträng | Beskriver hur ofta befordran kommer att tillämpas på faktureringen. Värdena kan vara Månadsvis, Årlig, OneTime eller Okänd. | 
| promotionID | sträng | Befordrans identifierare. |

## <a name="promotioneligibilities"></a>PromotionEligilities

En lista över produkter, SKU:er och deras befordran.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| Identifierare för kampanjeligiitetsobjekt. |
| catalogItemId | sträng | Katalogobjektets identifierare som befordran kommer att tillämpas på. Innehåller produkt-ID, SKU-ID och tillgänglighets-ID. |
| quantity | int | Antalet licenser eller instanser. |
| termDuration | sträng | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (en månad), P1Y (ett år) och P3Y (tre år). |
| billingCycle | sträng | Beskriver hur ofta befordran kommer att tillämpas på faktureringen. Värdena kan vara Månadsvis, Årlig, OneTime eller Okänd. | 
| eligibilities | Lista över PromotionEligibilities | Representerar en lista över berättiganderesultat för befordran. |

## <a name="promotioneligibility"></a>PromotionEligibility

En lista över produkter, SKU:er och deras befordran.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| promotionId | sträng | Befordrans identifierare. |
| isEligible | boolesk | Beskriver om befordran är berättigad till det angivna objektet för berättigandebegäran. |
| fel | Lista över PromotionEligibilityErrors | Fel som beskriver varför ett begärandeobjekt för befordran inte var berättigat. | 

## <a name="promotioneligibilityerror"></a>PromotionEligibilityError

Förklarar varför ett begärandeobjekt för befordran av berättigande inte var berättigat. 

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| typ | sträng | Behörighetsfeltyperna för befordran kan vara InvalidCatalogItemId, InvalidPromotion, PrerequisiteProductOwnership, RedemptionLimit, SeatCount, OfferPurchasedPreviously eller Term. |
| beskrivning | sträng | Beskriver om befordran är berättigad till det angivna objektet för berättigandebegäran. |

## <a name="redemptionlimitpromotioneligibilityerror"></a>RedemptionLimitPromotionEligibilityError

Innehåller information om varför inlösningsgränsen har överskridits.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| maxPromotionRedemptionCount | int | Det maximala antalet gånger som en befordran kan förvärvas. |
| remainingPromotionRedemptionCount| int | Återstående antal gånger som en befordran kan förvärvas. |

## <a name="seatcountpromotioneligibilityerror"></a>SeatCountPromotionEligibilityError

Innehåller information om varför antalet platser har överskridits. Båda värdena kan ha värdet null.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| minimumRequiredSeats | Int? | De lägsta licenserna som en befordran kommer att stödja. |
| maximumRequiredSeats | Int? | Det högsta antalet licenser som en befordran kommer att stödja. |

## <a name="termpromotioneligibilityerror"></a>TermPromotionEligibilityError

Innehåller information om varför befordran inte godkändes.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| eligibleTerms | PromotionTerm | De berättigade villkoren för en befordran kommer att stödja. |

## <a name="promotionterm"></a>PromotionTerm

Innehåller information om varför antalet platser har överskridits.

| Egenskap          | Typ               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| billingCycle | sträng | Beskriver hur ofta befordran kommer att tillämpas på faktureringen. Värdena kan vara Månadsvis, Årlig, OneTime eller Okänd. |
| varaktighet | sträng | Varaktigheten för den period som köps. |




