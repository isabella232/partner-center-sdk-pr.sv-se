---
title: Få en kunds kompetens
description: Lär dig hur du använder asynkron verifiering för att få en kund kvalificering via API för partner Center. Partner kan använda detta för att validera utbildnings kunder.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 130ee276461e3390ac78ac7abd8baeefe6a70d7c
ms.sourcegitcommit: 97f93caa57df6c64fe19868e6b2a0f7937226b51
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/21/2021
ms.locfileid: "98636391"
---
# <a name="get-a-customers-qualification-asynchronously"></a>Få en kund kvalificering asynkront

**Gäller för**

- Partnercenter

Så här får du en kunds kvalifikationer asynkront.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta all kvalificering.

| Namn               | Typ   | Obligatorisk | Beskrivning                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| **kund-ID för klient organisation** | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling kvalifikationer i svars texten.  Nedan visas exempel på **Get** -anrop på en kund med **utbildnings** kompetensen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-examples"></a>Svars exempel

#### <a name="approved"></a>Godkända

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Approved",
        }
    ]
}

```

#### <a name="in-review"></a>Under granskning

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "InReview",
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

#### <a name="denied"></a>Nekad

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Denied",
            "vettingReason": "Not an Education Customer", // example Vetting Reason
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

## <a name="related-articles"></a>Relaterade artiklar

- [Uppdatera en kunds kompetens](update-a-customer-s-qualifications.md)