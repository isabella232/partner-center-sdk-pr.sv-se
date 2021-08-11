---
title: Hämta avtalsmetadata för Microsoft Cloud-avtal
description: Den här artikeln förklarar hur du hämtar avtalsmetadata för Microsoft Cloud-avtal.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 55a09752844f74caaf878f1e2dcfe3d8a70a283c5e0e9daefba89c558405690a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994123"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Hämta avtalsmetadata för Microsoft Cloud-avtal

**Gäller för:** Partnercenter

**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**AgreementMetaData-resursen** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1.9 eller senare.

- Om du använder Partner Center Java SDK krävs version 1.8 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](./partner-center-authentication.md) Det här scenariot stöder app - och användarautentisering.

## <a name="net-version-114-or-newer"></a>.NET (version 1.14 eller senare)

Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:

1. Hämta först **samlingen IAggregatePartner.AgreementDetails.**

2. Anropa **metoden ByAgreementType** för att filtrera samlingen till Microsoft Cloud-avtal.

3. Anropa slutligen **metoden Get** eller **GetAsync.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Ett fullständigt exempel finns i klassen [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="net-version-19---113"></a>.NET (version 1.9–1.13)

Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:

Hämta först **samlingen IAggregatePartner.AgreementDetails** och anropa sedan **metoderna Get** eller **GetAsync.** Sök sedan efter objektet i samlingen, vilket motsvarar Microsoft Cloud-avtal:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:

Anropa först **funktionen IAggregatePartner.getAgreementDetails** och anropa sedan **get-funktionen.** Sök sedan efter objektet i samlingen, vilket motsvarar Microsoft Cloud-avtal:

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

Ett fullständigt exempel finns i klassen [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) från [konsoltestappsprojektet.](https://github.com/Microsoft/Partner-Center-Java-Samples)

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:

Använd kommandot [**Get-PartnerAgreementDetail.**](/powershell/module/partnercenter/get-partneragreementdetail) Sök sedan efter objektet i samlingen, vilket motsvarar Microsoft Cloud-avtal:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>REST-begäran

Om du vill hämta avtalsmetadata Microsoft Cloud-avtal skapar du först en REST-begäran för att hämta **AgreementMetaData-samlingen.** Sök sedan efter det objekt i samlingen som motsvarar Microsoft Cloud-avtal.

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling **AgreementMetaData-resurser** i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

Om du vill identifiera resursen i svaret som motsvarar Microsoft Cloud-avtal letar du efter resursen vars **agreementType-egenskap** har värdet "MicrosoftCloudAgreement".
