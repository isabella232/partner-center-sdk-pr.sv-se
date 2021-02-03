---
title: Återkalla en överföring
description: Så här drar du tillbaka en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a9e1e2a33d21fc1338a36b8ac96b528e70b61c86
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768703"
---
# <a name="withdraw-a-transfer"></a>Återkalla en överföring

**Gäller för:**

- Partnercenter

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- En överförings identifierare för en befintlig överföring.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| **TA bort**| [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/transfers/{transfer-ID} http/1.1      |

### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parameter för att identifiera kunden.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-ID** | sträng   | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden.             |
| **överförings-ID** | sträng   | Yes      | Ett GUID-formaterat överförings-ID som identifierar överföringen.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-example"></a>Exempel på begäran

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden inget innehåll (204).

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
