---
title: Aktivera en Sandbox-prenumeration för kommersiella Marketplace-produkter
description: 'Lär dig hur du använder REST-API: er för C/# och partner Center för att aktivera en Sandbox-prenumeration för kommersiella Marketplace-produkter.'
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769951"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Aktivera en Sandbox-prenumeration för kommersiella Marketplace SaaS-produkter för att möjliggöra fakturering

**Gäller för:**

- Partnercenter

Så här aktiverar du en prenumeration för SaaS-produkter (Software as a Service) från integration för integration i sandbox-konton.

> [!NOTE]
> Det går bara att aktivera en prenumeration för SaaS-produkter från affärs platser från integration sandbox-konton. Om du har en produktions prenumeration måste du gå till utgivarens webbplats för att slutföra installations processen. Prenumerations faktureringen påbörjas bara efter att installationen har slutförts.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett partner konto för integration i begränsat läge med en kund som har en aktiv prenumeration på kommersiella Marketplace SaaS-produkter.

- För partner som använder Partner Center .NET SDK måste du använda SDK-version 1.14.0 eller högre för att få åtkomst till den här funktionen.

## <a name="c"></a>C\#

Använd följande steg för att aktivera en prenumeration för SaaS-produkter från kommersiella platser:

1. Gör ett gränssnitt till tillgängliga prenumerations åtgärder. Du måste identifiera kunden och ange prenumerations-ID för utvärderings prenumerationen.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktivera prenumerationen med hjälp av åtgärden **Aktivera** .

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod     | URI för förfrågan                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/Activate http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y | Värdet är ett GUID-formaterat kund klient-ID (**kund-Tenant-ID**), vilket gör att du kan ange en kund. |
| **prenumerations-ID** | **guid** | Y | Värdet är ett GUID-formaterat prenumerations-**ID (prenumerations-ID**), vilket gör att du kan ange en prenumeration. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>REST-svar

Den här metoden returnerar egenskaperna för **prenumerations-ID** och **status** .

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
