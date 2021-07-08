---
title: Hämta en lista över alla partneranvändares begäranden
description: Hämta en lista över alla partneranvändares begäranden med hjälp av partner-REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: cychua
ms.author: cychua
ms.openlocfilehash: 9a367f912669114969f8792a5afcc7020af1112e
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760512"
---
# <a name="get-app-and-user-api-requests"></a>Hämta api-begäranden för appar och användare

**Gäller för:** Partner Center API

Den här artikeln beskriver hur du hämtar en lista över alla partneranvändares begäranden inom en klientorganisation med hjälp av REST-API:er.

 > [!NOTE]
 > Det här API:et returnerar endast de senaste API-begäranden som görs av APP + Användar-autentiseringsuppgifter med en maxgräns på 10 000.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                        |
|---------|--------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/partnerRequests |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/partnerRequests HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling [API-begäranderesurser](mfa-resources.md#api-request-details) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

``` http
HTTP/1.1 200 OK
Content-Length: 2960
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
{
    "totalCount": 2,
    "items": [
        {
            "requestId": "6c583d8d-46cd-420c-ae3d-35b6dfdcdb21",
            "correlationId": "",
            "operationName": "Get /v{version}/nonMfaCompliantPartnerPrincipals",
            "requestDateTime": "2020-05-21T21:02:10.31",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "c69854fe-5fb4-4527-a28f-f24f1acaffd6",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "admin@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": true
        },
        {
            "requestId": "09f8e434-a9ce-43ea-a9ac-270fbb22371a",
            "correlationId": "",
            "operationName": "Get /v{version}/customers/{customer_id}/subscriptions?order_id={order_id_value}&mpn_id={mpn_id_value}",
            "requestDateTime": "2020-05-21T22:18:35.73",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": false
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
