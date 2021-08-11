---
title: Resurser för partnersäkerhetskrav
description: Förstå implementeringsinformation för multifaktorautentisering (MFA) för att uppfylla säkerhetskraven för partner.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 6377dbde574edd1b8d8058f7b8e88ae6497d615b9237bbda91e9c4617486b569
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997897"
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

| Egenskap                            | Typ            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | Datum för API-begäran          |
| MfaCompliantRequestCount            | long            | Antal förfrågningar med MFA    |
| TotalRequestCount                   | long            | Totalt antal förfrågningar       |
| ApplicationId                       | sträng          | Program-ID        |
| ApplicationName                     | sträng          | Programnamnet      |


## <a name="api-request-details"></a>Information om API-begäran

API-begäran som görs av AUTENTISERINGSUPPGIFTER FÖR APP + användare. 

| Egenskap                            | Typ            | Description                              |
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
