---
title: Uppdatera en kunds kompetens
description: Lär dig hur du uppdaterar en kunds kvalifikationer via asynkron gallring eller först konsumentsajter, inklusive adressen som är kopplad till profilen.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: e0390e8a9c2a277dcb9e18b026f12625400ae176
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770201"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Uppdatera en kunds kvalifikationer asynkront

**Gäller för**

- Partnercenter

Lär dig hur du uppdaterar en kunds kvalifikationer asynkront via API: er för partner Center. Information om hur du gör detta synkront finns i [Uppdatera en kunds kvalificering via synkron verifiering](update-customer-qualification-synchronous.md).

En partner kan uppdatera en kunds kvalifikationer asynkront så att de blir "utbildning" eller "GovernmentCommunityCloud". Andra värden, "ingen" och "icke-vinst" kan inte anges.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? Code = {VALIDATIONCODE} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att uppdatera kvalificeringen.

| Namn                   | Typ | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | GUID | Yes      | Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren. |
| **validationCode**     | int  | No       | Krävs endast för Community-molnet för myndigheter.                                                                                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Heltal svärdet från [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) -uppräkningen.

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden ett kvalificerings objekt i svars texten. Nedan visas ett exempel på **post** anropet på en kund (med ett tidigare kvalificerings **ingen**) med **utbildnings** kompetensen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a>Relaterade artiklar

- [Få en kunds kompetens](get-a-customer-s-qualifications.md)
- [Hämta en partners valideringskoder](get-a-partner-s-validation-codes.md)