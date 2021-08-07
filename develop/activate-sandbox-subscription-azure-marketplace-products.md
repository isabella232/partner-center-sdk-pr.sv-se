---
title: Aktivera en sandbox-prenumeration för produkter på den kommersiella marknadsplatsen
description: Lär dig hur du använder REST-API:er för C/# och Partner Center för att aktivera en sandbox-prenumeration för produkter på den kommersiella marknadsplatsen.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ea581695e4328f02d08486c91b7b90a78e75a50985279d78cc54ef8b35fa715
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990502"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Aktivera en sandbox-prenumeration för SaaS-produkter på den kommersiella marknadsplatsen för att aktivera fakturering

Så här aktiverar du en prenumeration för SaaS-produkter (Programvara som en tjänst) på den kommersiella marknadsplatsen från sandbox-konton för integrering för att aktivera fakturering.

> [!NOTE]
> Det går bara att aktivera en prenumeration för SaaS-produkter på den kommersiella marknadsplatsen från integrations-sandbox-konton. Om du har en produktionsprenumeration måste du besöka utgivarens webbplats för att slutföra installationen. Prenumerationsfakturering börjar först när installationen är klar.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett partnerkonto för sandbox-integrering med en kund som har en aktiv prenumeration på SaaS-produkter på den kommersiella marknadsplatsen.

- För partner som använder Partner Center .NET SDK måste du använda SDK version 1.14.0 eller senare för att få åtkomst till den här funktionen.

## <a name="c"></a>C\#

Använd följande steg för att aktivera en prenumeration för SaaS-produkter på den kommersiella marknadsplatsen:

1. Gör ett gränssnitt för prenumerationsåtgärder tillgängligt. Du måste identifiera kunden och ange prenumerations-ID för utvärderingsprenumerationen.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktivera prenumerationen med hjälp av **åtgärden** Aktivera.

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod     | URI för förfrågan                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-klient-id** | **guid** | Y | Värdet är ett GUID-formaterat kundklientorganisations-ID (**customer-tenant-id**), som gör att du kan ange en kund. |
| **prenumerations-id** | **guid** | Y | Värdet är en GUID-formaterad prenumerationsidentifierare (**subscription-id**) som gör att du kan ange en prenumeration. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Den här metoden returnerar **egenskaperna subscription-id** **och status.**

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
