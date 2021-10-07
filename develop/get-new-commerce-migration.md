---
title: Skaffa en ny migrering av en handelsprenumeration
description: Så här får du en ny migrering av en handelsprenumeration
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fc793e6a3ab43a50a07c955b69ba77c9deedf879
ms.sourcegitcommit: 53980dc43fb2277878bf61a15a86013b8b1c2574
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/06/2021
ms.locfileid: "129609970"
---
#  <a name="get-a-new-commerce-subscription-migration"></a>Skaffa en ny migrering av en handelsprenumeration

**Gäller för:** Partner Center | Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här hämtar du en migrering av en prenumeration till New Commerce Experience för att kontrollera migreringsstatus

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Ett aktuellt prenumerations-ID

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                                           |
|---------|---------------------------------------------------------------------------------------------------------------------------------------|
| **FÅ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/migrations/newcommerce/{migration-id} HTTP/1.1           |

### <a name="uri-parameter"></a>URI-parameter

I den här tabellen visas de frågeparametrar som krävs för att skapa en ny handelsmigrering.

| Namn               | Typ   | Obligatorisk | Beskrivning                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| kund-klient-id | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden. |
| migration-id       | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling [prenumerationsresurser](subscription-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-examples"></a>Svarsexempel

```http
{
    "id": "d3a0ef43-a208-4c32-8b10-f15e99d4e782",
    "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
    "status": "Processing",
    "customerTenantId": "a836f6d8-1b17-44af-aaf1-1e5511c5d4e1",
    "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV",
    "subscriptionEndDate": "2022-09-06T00:00:00Z",
    "quantity": 1,
    "termDuration": "P1Y",
    "billingCycle": "Monthly"
}
```
