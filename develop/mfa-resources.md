---
title: Resurser för partnersäkerhetskrav
description: Förstå implementeringsinformation för multifaktorautentisering (MFA) för att uppfylla säkerhetskraven för partner.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: b41a0e46fa6e0643e82a5a2dbfb7141f54a0f824
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445552"
---
# <a name="partner-security-requirements-resources"></a>Resurser för partnersäkerhetskrav

Den här artikeln hjälper dig att förstå implementeringsinformationen för multifaktorautentisering (MFA) för att hjälpa din organisation att uppfylla partnersäkerhetskravsstatus. 

## <a name="portal-request-without-mfa"></a>Portalbegäran utan MFA

Ange en användare som kommer åt Partner Center-portalen utan MFA-autentisering.

| Egenskap                            | Typ            | Beskrivning                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | sträng          | Användarobjekt-ID                        |
| TenantId                            | sträng          | CSP-klientorganisations-ID                         |
| Upn                                 | sträng          | Användarens huvudnamn                   |
| LastNonMfaCompliantLoginDateTime    | datetime        | Senaste användarinloggning utan MFA |


## <a name="api-request-summarized-by-application"></a>API-begäran sammanfattad efter program

En sammanfattning av API-begäran som görs av APP + användar-autentiseringsuppgifter, aggregerad efter begärandedatum och program-ID.

| Egenskap                            | Typ            | Beskrivning               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | Datum för API-begäran          |
| MfaCompliantRequestCount            | long            | Antal förfrågningar med MFA    |
| TotalRequestCount                   | long            | Totalt antal förfrågningar       |
| ApplicationId                       | sträng          | Program-ID        |
| ApplicationName                     | sträng          | Programnamnet      |


## <a name="api-request-details"></a>Information om API-begäran

API-begäran som görs av AUTENTISERINGSUPPGIFTER FÖR APP + användare. 

| Egenskap                            | Typ            | Beskrivning                              |
|-------------------------------------|-----------------|------------------------------------------|
| Id                           | sträng          | MS-RequestId                             |
| CorrelationId                       | sträng          | MS-CorrelationId                         |
| OperationName                       | sträng          | API-sökvägen med begärandemetod         |
| RequestDateTime                     | DateTime        | Tid för API-begäran                     |
| Ip                           | sträng          | Källans IP-adress                        |
| ObjectId                            | sträng          | Användarobjekt-ID                           |
| TenantId                            | sträng          | CSP-klientorganisations-ID                            |
| Upn                                 | sträng          | Användarens huvudnamn                      |
| ApplicationId                       | sträng          | Ditt program                         |
| MfaCompliant                        | boolesk            | Ange begäran med eller utan MFA |
