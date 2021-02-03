---
title: Hämta avtalsmetadata för Microsoft Cloud-avtal
description: Den här artikeln beskriver hur du får avtals-metadata i Microsoft Cloud avtal.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6a404eb38c4c31d3e69bb598872b932d8985529
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769261"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Hämta avtalsmetadata för Microsoft Cloud-avtal

**Gäller för**

- Partnercenter

> [!NOTE]
> **AgreementMetaData** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet. Den gäller inte för:
> - Partner Center som drivs av 21Vianet
> - Partnercenter för Microsoft Cloud Tyskland
> - Välkommen till Partnercenter för Microsoft Cloud for US Government

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1,9 eller senare.

- Om du använder Partner Center Java SDK krävs version 1,8 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md). Det här scenariot stöder app + användarautentisering..

## <a name="net-version-114-or-newer"></a>.NET (version 1,14 eller senare)

Så här hämtar du avtals metadata för Microsoft Cloud avtal:

1. Börja med att hämta samlingen **IAggregatePartner. AgreementDetails** .

2. Anropa **ByAgreementType** -metoden för att filtrera samlingen till Microsoft Cloud avtal.

3. Anropa slutligen **Get** -eller **GetAsync** -metoden.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Ett fullständigt exempel finns i [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.

## <a name="net-version-19---113"></a>.NET (version 1,9-1,13)

Så här hämtar du avtals metadata för Microsoft Cloud avtalet:

Hämta först **IAggregatePartner. AgreementDetails** -samlingen och anropa sedan metoderna **Get** eller **GetAsync** . Sök sedan efter objektet i samlingen, som motsvarar Microsoft Cloud avtalet:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Så här hämtar du avtals metadata för Microsoft Cloud avtalet:

Anropa först funktionen **IAggregatePartner. getAgreementDetails** och anropa sedan **Get** -funktionen. Sök sedan efter objektet i samlingen, som motsvarar Microsoft Cloud avtalet:

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

Ett fullständigt exempel finns i [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) -klassen från projektets [test app](https://github.com/Microsoft/Partner-Center-Java-Samples) -projekt.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Så här hämtar du avtals metadata för Microsoft Cloud avtalet:

Använd kommandot [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) . Sök sedan efter objektet i samlingen, som motsvarar Microsoft Cloud avtalet:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>REST-begäran

Om du vill hämta avtals metadata för Microsoft Cloud avtal måste du först skapa en REST-begäran för att hämta **AgreementMetaData** -samlingen. Sök sedan efter objektet i samlingen som motsvarar Microsoft Cloud avtalet.

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Agreements http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas returnerar den här metoden en samling **AgreementMetaData** -resurser i svars texten.

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

Identifiera resursen i svaret som motsvarar Microsoft Cloud avtalet genom att leta efter resursen vars **agreementType** -egenskap har värdet "MicrosoftCloudAgreement".
