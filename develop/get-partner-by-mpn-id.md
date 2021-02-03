---
title: Verifiera ett partner-MPN-ID
description: Lär dig hur du verifierar en partners Microsoft Partner Network identifierare (MPN-ID) genom att begära partnerns MPN-profil via C \# eller REST API för partner Center.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769939"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Verifiera ett partner MPN-ID via C \# eller partner Center REST API

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här verifierar du en partners Microsoft Partner Network identifierare (MPN-ID).

Den teknik som visas här verifierar partnerns Microsoft Partner Network identifierare genom att begära partnerns MPN-profil från Partner Center. Identifieraren anses vara giltig om begäran lyckas.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Partnerns MPN-ID som ska verifieras. Om du utelämnar det här värdet hämtar förfrågan MPN-profilen för den inloggade partnern.

## <a name="c"></a>C\#

För att verifiera en partners MPN-ID måste du först hämta ett gränssnitt till partner profil insamlings åtgärder från egenskapen [**IAggregatePartner. profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) . Hämta sedan ett gränssnitt för att MPN profil åtgärder från egenskapen [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) . Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) med MPN-ID: t för att hämta MPN-profilen. Om du utelämnar MPN-ID: t från get-eller GetAsync-anropet försöker begäran att hämta MPN-profilen för den inloggade partnern.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: VerifyPartnerMpnId.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN? mpnId = {MPN-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Ange följande frågeparameter för att identifiera partnern. Om du utelämnar den här Frågeparametern returnerar begäran MPN-profilen för den inloggade partnern.

| Namn   | Typ | Obligatorisk | Beskrivning                                                 |
|--------|------|----------|-------------------------------------------------------------|
| MPN-ID | int  | No       | Ett Microsoft Partner Network-ID som identifierar partnern. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas innehåller svars texten [MpnProfile](profile-resources.md#mpnprofile) -resursen för partnern.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example-success"></a>Svars exempel (lyckades)

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

### <a name="response-example-failure"></a>Svars exempel (haveri)

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
