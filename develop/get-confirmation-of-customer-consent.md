---
title: Få bekräftelse på kundgodkännande av Microsoft Cloud-avtal
description: I den här artikeln förklaras hur du får bekräftelse på kund godkännande av Microsoft Cloud avtalet.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769858"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Få bekräftelse på kundgodkännande av Microsoft Cloud-avtal

**Gäller för**

- Partnercenter

> [!NOTE]
> **Avtals** resursen stöds för närvarande av Partner Center i det offentliga Microsoft-molnet. Den gäller inte för:
>
> - Partner Center som drivs av 21Vianet
> - Partnercenter för Microsoft Cloud Tyskland
> - Välkommen till Partnercenter för Microsoft Cloud for US Government

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1,9 eller senare.

- Om du använder Partner Center Java SDK krävs version 1,8 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md). Det här scenariot stöder endast app + användarautentisering.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="net-version-14-or-newer"></a>.NET (version 1,4 eller senare)

För att hämta bekräftelser för kundgodkännande som tidigare har tillhandahållits:

- Använd **IAggregatePartner. Customers** -samlingen och anropa **ById** -metoden med det angivna kund-ID: n.

- Hämta **avtals** egenskapen och filtrera resultaten till Microsoft Cloud avtalet genom att anropa **ByAgreementType** -metoden.

- Anropa **Get** -eller **GetAsync** -metoden.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Ett fullständigt exempel finns i [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.

## <a name="net-version-19---113"></a>.NET (version 1,9-1,13)

Så här hämtar du bekräftelse av kundgodkännande som har tillhandahållits tidigare:

Använd **IAggregatePartner. Customers** -samlingen och anropa **ById** -metoden med den angivna kundens ID. Hämta sedan **avtals** egenskapen följt av metoderna **Get** eller **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Så här hämtar du bekräftelse av kundgodkännande som har tillhandahållits tidigare:

Använd funktionen **IAggregatePartner. getCustomers** och anropa funktionen **byId** med den angivna kundens identifierare. Hämta sedan funktionen **getAgreements** , följt av anropa funktionen **Get** .

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

Ett fullständigt exempel finns i [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) -klassen från projektets [test app](https://github.com/Microsoft/Partner-Center-Java-Samples) -projekt.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Så här hämtar du bekräftelse av kundgodkännande som har tillhandahållits tidigare:

Använd kommandot [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) .

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>REST-begäran

Information om hur du hämtar bekräftelse på kundgodkännanden tidigare finns i följande instruktioner.

Skapa en ny **avtals** resurs med relevant certifierings information.

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ange kunden som du bekräftar.

| Namn             | Typ | Obligatorisk | Beskrivning                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling **avtals** resurser i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
