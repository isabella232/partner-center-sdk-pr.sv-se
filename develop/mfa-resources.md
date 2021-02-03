---
title: Resurser för säkerhets krav för partner
description: Förstå implementerings information för Multi-Factor Authentication (MFA) för att uppfylla partner säkerhets kraven.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 5eb77c3c10e95c9dc835cfe05e014b9256531b51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768853"
---
# <a name="partner-security-requirements-resources"></a>Resurser för säkerhets krav för partner

**Gäller för:**

- Partnercenter

Den här artikeln hjälper dig att förstå hur du använder MFA-information (Multi-Factor Authentication) för att hjälpa din organisation att uppfylla status för partner säkerhets krav. 

## <a name="portal-request-without-mfa"></a>Portal förfrågan utan MFA

Ange en användare som har åtkomst till Partner Center-portalen utan MFA-autentisering.

| Egenskap                            | Typ            | Beskrivning                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | sträng          | Användar objekt-ID                        |
| TenantId                            | sträng          | CSP-klient-ID                         |
| UPN                                 | sträng          | Användarens huvud namn                   |
| LastNonMfaCompliantLoginDateTime    | datetime        | Senaste gången användaren loggar in utan MFA |


## <a name="api-request-summarized-by-application"></a>API-begäran sammanfattas efter program

En sammanfattning av API-begäran som gjorts av APP + User Credential, som sammanställs efter datum för begäran och program-ID.

| Egenskap                            | Typ            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | Datum för API-begäran          |
| MfaCompliantRequestCount            | long            | Antal begär Anden med MFA    |
| TotalRequestCount                   | long            | Totalt antal begär Anden       |
| ApplicationId                       | sträng          | Program-ID        |
| ApplicationName                     | sträng          | Program namnet      |


## <a name="api-request-details"></a>Information om API-begäran

API-begäran gjorda av APP + användarens autentiseringsuppgifter. 

| Egenskap                            | Typ            | Description                              |
|-------------------------------------|-----------------|------------------------------------------|
| RequestId                           | sträng          | MS-RequestId                             |
| CorrelationId                       | sträng          | MS-CorrelationId                         |
| OperationName                       | sträng          | API-sökväg med metoden Request         |
| RequestDateTime                     | DateTime        | Tid för API-begäran                     |
| Adresser                           | sträng          | Källans IP-adress                        |
| ObjectId                            | sträng          | Användar objekt-ID                           |
| TenantId                            | sträng          | CSP-klient-ID                            |
| UPN                                 | sträng          | Användarens huvud namn                      |
| ApplicationId                       | sträng          | Ditt program                         |
| MfaCompliant                        | boolesk            | Ange begäran med eller utan MFA |
