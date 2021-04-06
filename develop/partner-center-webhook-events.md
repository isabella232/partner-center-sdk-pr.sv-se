---
title: Partner Center-webhook-händelser
description: Lär dig att testa och använda webhook-händelser för att notera när prenumerationer och andra händelser ändras i Partner Center.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 03ee1d4e74408b8cf69e2971054bf9060650cb77
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500047"
---
# <a name="partner-center-webhook-events"></a>Partner Center-webhook-händelser

**Gäller för**

- Partnercenter
- Partnercenter drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Partner Center-webhook-händelser är resurs ändrings händelser som levereras i form av HTTP-inlägg till en registrerad URL. Om du vill ta emot en händelse från Partner Center är du värd för ett återanrop där Partner Center kan publicera händelsen. Händelsen har signerats digitalt så att du kan verifiera att den har skickats från Partner Center.

Information om hur du tar emot händelser, autentiserar en motringning och använder webhook-API: er för partner Center för att skapa, Visa och uppdatera en händelse registrering finns i [partner Center Webhooks](partner-center-webhooks.md).

## <a name="supported-events"></a>Händelser som stöds

Följande webhook-händelser stöds av Partner Center.

### <a name="test-event"></a>Test händelse

Med den här händelsen kan du själv publicera och testa registreringen genom att begära ett test händelser och sedan följa förloppet. Du kommer att kunna se de fel meddelanden som tas emot från Microsoft när du försöker leverera evenemanget. Detta gäller endast för "test-skapade"-händelser och data som är äldre än 7 dagar rensas.

>[!NOTE]
>Det finns en begränsning på 2 begär Anden per minut när en test-skapad-händelse publiceras.

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Händelsens namn. I formatet {Resource}-{action}. I den här händelsen är värdet "test-created".                                          |
| ResourceUri               | URI                                | URI: n för att hämta resursen. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/Webhooks/v1/Registration/validationEvents/{{correlationId}} |
| ResourceName              | sträng                             | Namnet på den resurs som ska utlösa händelsen. I den här händelsen är värdet "test".                                  |
| AuditUri                  | URI                                | Valfritt URI: n för att hämta gransknings posten, om den finns. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resurs ändringen utfördes.                                                         |

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

### <a name="subscription-updated-event"></a>Händelsen uppdatering av prenumeration

Den här händelsen inträffar när den angivna prenumerationen ändras. En uppdaterad händelse för prenumeration skapas när det finns en intern ändring utöver när ändringar görs via partner Center-API: et.  Den här händelsen kommer bara att genereras när det finns ändringar på handels nivå, till exempel när antalet licenser ändras och när prenumerationens tillstånd ändras. Det kommer inte att genereras när resurser skapas i prenumerationen.

>[!NOTE]
>Det finns en fördröjning på upp till 48 timmar mellan den tidpunkt då en prenumeration ändras och när händelsen uppdatering av prenumeration utlöses.

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Händelsens namn. I formatet {Resource}-{action}. I den här händelsen är värdet "prenumeration-uppdaterat".                                  |
| ResourceUri               | URI                                | URI: n för att hämta resursen. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/Webhooks/v1/Customers/{{CustomerId}}/Subscriptions/{{SubscriptionId}} |
| ResourceName              | sträng                             | Namnet på den resurs som ska utlösa händelsen. I den här händelsen är värdet "Subscription".                          |
| AuditUri                  | URI                                | Valfritt URI: n för att hämta gransknings posten, om den finns. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resurs ändringen utfördes.                                                         |

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

### <a name="threshold-exceeded-event"></a>Händelsen tröskel överskreds

Den här händelsen inträffar när mängden Microsoft Azure användning för en kund överskrider deras användnings utgifts budget (tröskel). Mer information finns i [ställa in en Azure utgifts budget för dina kunder/Partner Center/set-a-Azure-utgifter-budget – för-kunder).

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Händelsens namn. I formatet {Resource}-{action}. I den här händelsen är värdet "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | URI: n för att hämta resursen. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/Webhooks/v1/Customers/usagerecords |
| ResourceName              | sträng                             | Namnet på den resurs som ska utlösa händelsen. I den här händelsen är värdet "usagerecords".                          |
| AuditUri                  | URI                                | Valfritt URI: n för att hämta gransknings posten, om den finns. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resurs ändringen utfördes.                                                         |

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

### <a name="referral-created-event"></a>Händelse för skapande av hänvisning

Den här händelsen inträffar när referensen skapas.

#### <a name="properties"></a>Egenskaper

| Egenskap                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Händelsens namn. I formatet {Resource}-{action}. I den här händelsen är värdet "referral-created".                                  |
| ResourceUri               | URI                                | URI: n för att hämta resursen. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/Engagements/v1/Referrals/{{ReferralID}} |
| ResourceName              | sträng                             | Namnet på den resurs som ska utlösa händelsen. I den här händelsen är värdet "referral".                          |
| AuditUri                  | URI                                | Valfritt URI: n för att hämta gransknings posten, om den finns. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resurs ändringen utfördes.                                                         |

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

| Egenskap                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sträng                             | Händelsens namn. I formatet {Resource}-{action}. I den här händelsen är värdet "referral-updated".                                  |
| ResourceUri               | URI                                | URI: n för att hämta resursen. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/Engagements/v1/Referrals/{{ReferralID}} |
| ResourceName              | sträng                             | Namnet på den resurs som ska utlösa händelsen. I den här händelsen är värdet "referral".                          |
| AuditUri                  | URI                                | Valfritt URI: n för att hämta gransknings posten, om den finns. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} |
| ResourceChangeUtcDate     | sträng i UTC-datum/tid-format | Datum och tid då resurs ändringen utfördes.                                                         |

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

### <a name="invoice-ready-event"></a>Händelse för faktura klar

Den här händelsen inträffar när den nya fakturan är klar.

| Egenskap                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | sträng | Händelsens namn. I formatet {Resource}-{action}. I den här händelsen är värdet "faktureras Ready". |
| ResourceUri | URI | URI: n för att hämta resursen. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{{InvoiceId}} |
| ResourceName | sträng | Namnet på den resurs som ska utlösa händelsen. I den här händelsen är värdet "faktura". |
| AuditUri |  URI | Valfritt URI: n för att hämta gransknings posten, om den finns. Använder syntaxen:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}}) |
| ResourceChangeUtcDate | sträng i UTC-datum/tid-format | Datum och tid då resurs ändringen utfördes. |

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
