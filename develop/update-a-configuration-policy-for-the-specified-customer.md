---
title: Uppdatera en konfigurationsprincip för den angivna kunden
description: Så här uppdaterar du den angivna konfigurations principen för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bf3b6f4db7516779c157b647725368ff0e4a570
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769792"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>Uppdatera en konfigurationsprincip för den angivna kunden

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland

Så här uppdaterar du den angivna konfigurations principen för den angivna kunden.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Princip identifieraren.

## <a name="c"></a>C\#

Om du vill uppdatera en befintlig konfigurations princip för den angivna kunden instansierar du ett nytt [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) -objekt som visas i följande kodfragment. Värdena i det nya objektet ersätter motsvarande värden i det befintliga objektet. Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att hämta ett gränssnitt till åtgärder på den angivna kunden. Anropa sedan metoden [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) med princip-ID: t för att hämta ett gränssnitt till konfigurations princip åtgärder för den angivna principen. Slutligen kan du anropa [**korrigerings filen**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) eller [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) -metoden för att uppdatera konfigurations principen.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: UpdateConfigurationPolicy.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parametrar när du skapar begäran.

| Namn        | Typ   | Obligatorisk | Beskrivning                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| kund-ID | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden.         |
| princip-ID   | sträng | Yes      | En GUID-formaterad sträng som identifierar den princip som ska uppdateras. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Begär ande texten måste innehålla ett objekt som innehåller princip informationen.

| Namn            | Typ             | Obligatorisk | Uppdateras | Description                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | sträng           | Ja      | Nej        | Den GUID-formaterade sträng som identifierar principen.                                                                                                    |
| name            | sträng           | Ja      | Ja       | Det egna namnet på principen.                                                                                                                         |
| category        | sträng           | Ja      | Nej        | Princip kategorin.                                                                                                                                     |
| beskrivning     | sträng           | No       | Ja       | Princip beskrivningen.                                                                                                                                  |
| devicesAssigned | antal           | Nej       | Nej        | Antalet enheter.                                                                                                                                   |
| policySettings  | matris med strängar | Ja      | Ja       | Princip inställningarna: "ingen", "ta bort \_ OEM \_ -förinstallationer", "OOBE \_ User \_ not \_ Local \_ admin", "hoppa över \_ Express \_ Inställningar", "hoppa över \_ OEM \_ -registrering", hoppa över \_ EULA ". |

### <a name="request-example"></a>Exempel på begäran

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -resursen för den nya principen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
