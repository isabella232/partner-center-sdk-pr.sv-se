---
title: Webhook-händelser i Partnercenter
description: Lär dig hur du testar och använder Webhook-händelser för att observera när prenumerationer och andra händelser ändras i Partnercenter.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: e5e363a2f928dd38304887547bdc0e5d652728d6
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547748"
---
# <a name="partner-center-webhook-events"></a>Webhook-händelser i Partnercenter

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Partnercenter-webhookhändelser är resursändringshändelser som levereras i form av HTTP-POST:er till en registrerad URL. Om du vill ta emot en händelse från Partnercenter är du värd för ett återanrop där Partnercenter kan PUBLICERA händelsen. Händelsen har signerats digitalt så att du kan verifiera att den har skickats från Partnercenter.

Information om hur du tar emot händelser, autentiserar ett återanrop och använder Partner Center-webhook-API:er för att skapa, visa och uppdatera en händelseregistrering finns [i Webhooks för Partnercenter.](partner-center-webhooks.md)

## <a name="supported-events"></a>Händelser som stöds

Följande webhook-händelser stöds av Partnercenter.

### <a name="test-event"></a>Testhändelse

Med den här händelsen kan du registrera dig själv och testa registreringen genom att begära en testhändelse och sedan spåra förloppet. Du kommer att kunna se felmeddelanden som tas emot från Microsoft när du försöker leverera händelsen. Detta gäller endast för "testskapade" händelser och data som är äldre än sju dagar tas bort.

>[!NOTE]
>Det finns en begränsning på 2 begäranden per minut när du publicerar en testskapad händelse.

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Beskrivning                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Namnet på händelsen. I formuläret {resource}-{action}. För den här händelsen är värdet "test-created".                                          |
| ResourceUri               | URI                                | URI:en för att hämta resursen. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | sträng                             | Namnet på den resurs som utlöser händelsen. För den här händelsen är värdet "test".                                  |
| AuditUri                  | URI                                | (Valfritt) URI:en för att hämta granskningsposten, om den finns. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resursändringen inträffade.                                                         |

#### <a name="example"></a>Exempel

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>Händelse med uppdaterad prenumeration

Den här händelsen utlöses när den angivna prenumerationen ändras. En händelse som uppdateras av prenumerationen genereras när det sker en intern ändring utöver när ändringar görs via Partner Center-API:et.  Den här händelsen genereras bara när det finns ändringar på handelsnivå, till exempel när antalet licenser ändras och när prenumerationens tillstånd ändras. Den genereras inte när resurser skapas i prenumerationen.

>[!NOTE]
>Det finns en fördröjning på upp till 48 timmar mellan den tidpunkt då en prenumeration ändras och när den uppdaterade prenumerationshändelsen utlöses.

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Beskrivning                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Namnet på händelsen. I formuläret {resource}-{action}. För den här händelsen är värdet "subscription-updated".                                  |
| ResourceUri               | URI                                | URI:en för att hämta resursen. Använder syntaxen:[*"{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | sträng                             | Namnet på den resurs som utlöser händelsen. För den här händelsen är värdet "prenumeration".                          |
| AuditUri                  | URI                                | (Valfritt) URI:en för att hämta granskningsposten, om den finns. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resursändringen inträffade.                                                         |

#### <a name="example"></a>Exempel

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>Överskriden händelse för tröskelvärde

Den här händelsen utlöses när mängden Microsoft Azure för en kund överskrider sin utgiftsbudget för användning (deras tröskelvärde). Mer information finns i [Ange en Azure-utgiftsbudget för dina kunder/partnercenter/set-an-azure-spending-budget-for-your-customers).

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Beskrivning                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Namnet på händelsen. I formuläret {resource}-{action}. För den här händelsen är värdet "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | URI:en för att hämta resursen. Använder syntaxen:[*"{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | sträng                             | Namnet på den resurs som utlöser händelsen. För den här händelsen är värdet "usagerecords".                          |
| AuditUri                  | URI                                | (Valfritt) URI:en för att hämta granskningsposten, om den finns. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resursändringen inträffade.                                                         |

#### <a name="example"></a>Exempel

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>Skapad referenshändelse

Den här händelsen utlöses när hänvisningen skapas.

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Beskrivning                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Namnet på händelsen. I formuläret {resource}-{action}. För den här händelsen är värdet "referral-created".                                  |
| ResourceUri               | URI                                | URI:en för att hämta resursen. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | sträng                             | Namnet på den resurs som utlöser händelsen. För den här händelsen är värdet "hänvisning".                          |
| AuditUri                  | URI                                | (Valfritt) URI:en för att hämta granskningsposten, om den finns. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resursändringen inträffade.                                                         |

#### <a name="example"></a>Exempel

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>Referens för uppdaterad händelse

Den här händelsen utlöses när hänvisningen uppdateras.

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Beskrivning                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Namnet på händelsen. I formuläret {resource}-{action}. För den här händelsen är värdet "referral-updated".                                  |
| ResourceUri               | URI                                | URI:en för att hämta resursen. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | sträng                             | Namnet på den resurs som utlöser händelsen. För den här händelsen är värdet "hänvisning".                          |
| AuditUri                  | URI                                | (Valfritt) URI:en för att hämta granskningsposten, om den finns. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resursändringen inträffade.                                                         |

#### <a name="example"></a>Exempel

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>Fakturaklar händelse

Den här händelsen utlöses när den nya fakturan är klar.

| Egenskap                  | Typ                               | Beskrivning                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | sträng | Namnet på händelsen. I formuläret {resource}-{action}. För den här händelsen är värdet "fakturaklart". |
| ResourceUri | URI | URI:en för att hämta resursen. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName | sträng | Namnet på den resurs som utlöser händelsen. För den här händelsen är värdet "faktura". |
| AuditUri |  URI | (Valfritt) URI:en för att hämta granskningsposten, om den finns. Använder syntaxen: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}") |
| ResourceChangeUtcDate | sträng i UTC-datum/tid-format | Datum och tid då resursändringen inträffade. |

#### <a name="example"></a>Exempel

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
