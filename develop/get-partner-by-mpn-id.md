---
title: Verifiera ett partner-MPN-ID
description: Lär dig hur du verifierar en partners Microsoft Partner Network-ID (MPN-ID) genom att begära partnerns MPN-profil via C eller \# partnercenter-REST API.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 223f0da94f5a1c12b4f6de32184296b88ab5f443a69feac89152acc1aa9ccbd6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995925"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Verifiera ett PARTNER-MPN-ID via C \# eller partnercenter-REST API

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här verifierar du en partners Microsoft Partner Network (MPN-ID).

Tekniken som visas här verifierar partnerns Microsoft Partner Network identifierare genom att begära partnerns MPN-profil från Partnercenter. Identifieraren anses vara giltig om begäran lyckas.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

- Partnerns MPN-ID som ska verifieras. Om du utelämnar det här värdet hämtar begäran MPN-profilen för den inloggade partnern.

## <a name="c"></a>C\#

Om du vill verifiera en partners MPN-ID hämtar du först ett gränssnitt för insamlingsåtgärder för partnerprofiler [**från egenskapen IAggregatePartner.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) Hämta sedan ett gränssnitt för MPN-profilåtgärder från [**egenskapen MpnProfile.**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) Anropa slutligen metoderna [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) eller [**GetAsync med**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) MPN-ID:t för att hämta MPN-profilen. Om du utelämnar MPN-ID från anropet Get eller GetAsync försöker begäran hämta MPN-profilen för den inloggade partnern.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **exempelklass:** VerifyPartnerMpnId.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Ange följande frågeparameter för att identifiera partnern. Om du utelämnar den här frågeparametern returnerar begäran MPN-profilen för den inloggade partnern.

| Namn   | Typ | Obligatorisk | Beskrivning                                                 |
|--------|------|----------|-------------------------------------------------------------|
| mpn-id | int  | No       | Ett Microsoft Partner Network-ID som identifierar partnern. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten [MpnProfile-resursen](profile-resources.md#mpnprofile) för partnern.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example-success"></a>Svarsexempel (lyckades)

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a>Svarsexempel (fel)

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
