---
title: Ta bort indirekt återförsäljare i sandbox-miljö
description: Innehåller information om hur du tar bort indirekta Sandbox-återförsäljare och aktiverar testning från slutet till slut med hjälp av API:er.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba1fd002ac62aba4e414d263b33ecc8153054602
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973017"
---
# <a name="delete-indirect-reseller-in-sandbox"></a>Ta bort indirekt återförsäljare i sandbox-miljö

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Tyskland

Det här dokumentet visar hur du tar bort indirekta sandbox-leverantörer och aktiverar testning från slutet till slut med hjälp av API:er.

> [!Important]
> Det här dokumentet beskriver funktioner som endast tillåts i sandbox-miljön för indirekta modellupplevelser.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a>Indirekt Sandbox-provider – Ta bort indirekt Sandbox-återförsäljare 

Den här funktionen är bara tillgänglig i sandbox-miljön och ger indirekta sandbox-leverantörer möjlighet att skapa indirekta Sandbox-återförsäljare.

1. Krav för att ta bort en indirekt Sandbox-återförsäljare
    1. Pausa prenumerationerna för varje kund av den indirekta Sandbox-återförsäljaren
    2. Ta bort alla indirekt återförsäljares kunder
2. Gräns på fem indirekta Sandbox-återförsäljare per indirekt Sandbox-leverantör. När den indirekta sandbox-återförsäljaren har tagits bort återställs kvoten.

## <a name="delete-sandbox-indirect-reseller-through-api"></a>Ta bort indirekt Sandbox-återförsäljare via API

### <a name="rest-request"></a>REST-begäran

#### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan                                                                             |
|------------|-------------------------------------------------------------------------------------|
| **Ta bort** | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId} |

#### <a name="request-headers"></a>Begärandehuvuden

- Det här API:et är idempotent (det ger inte ett annat resultat om du anropar det flera gånger)
- Ett begärande-ID och korrelations-ID krävs
- Mer information finns i [Partner Center REST-huvuden](headers.md)

### <a name="request-example"></a>Exempel på begäran

Ta bort https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad och annan felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

Den här metoden returnerar följande status för lyckade och felkoder:

| HTTP-statuskod                     | Felkod     | Beskrivning                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| 401                                  | 6002           | Obehörig token eller Inte ett konto för tipsprovider |
| 403                                  | 6003           | Det är inte tillåtet att ta bort sandbox-miljö-IR                 |
| 403                                  | 6004           | Det går inte att skapa sandbox-miljöns IR-åtgärd          |
| 409                                  | 1003           | Konflikt när klientorganisationen skapas                   |
