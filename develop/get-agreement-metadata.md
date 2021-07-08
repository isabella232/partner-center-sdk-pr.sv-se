---
title: Hämta avtalsmetadata för Microsoft Cloud-avtal
description: Den här artikeln förklarar hur du hämtar avtalsmetadata för Microsoft Cloud-avtal.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 2588327e72a13de75eb9e02675edbd535491adc4
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760801"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="9d8fb-103">Hämta avtalsmetadata för Microsoft Cloud-avtal</span><span class="sxs-lookup"><span data-stu-id="9d8fb-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="9d8fb-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9d8fb-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="9d8fb-105">**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9d8fb-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9d8fb-106">**AgreementMetaData-resursen** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d8fb-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9d8fb-107">Prerequisites</span></span>

- <span data-ttu-id="9d8fb-108">Om du använder Partner Center .NET SDK krävs version 1.9 eller senare.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="9d8fb-109">Om du använder Partner Center Java SDK krävs version 1.8 eller senare.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="9d8fb-110">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="9d8fb-111">Det här scenariot stöder app - och användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-111">This scenario supports app + user authentication.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="9d8fb-112">.NET (version 1.14 eller senare)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-112">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="9d8fb-113">Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:</span><span class="sxs-lookup"><span data-stu-id="9d8fb-113">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="9d8fb-114">Hämta först **samlingen IAggregatePartner.AgreementDetails.**</span><span class="sxs-lookup"><span data-stu-id="9d8fb-114">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="9d8fb-115">Anropa **metoden ByAgreementType** för att filtrera samlingen till Microsoft Cloud-avtal.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-115">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="9d8fb-116">Anropa slutligen **metoden Get** eller **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="9d8fb-116">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="9d8fb-117">Ett fullständigt exempel finns i klassen [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-117">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="9d8fb-118">.NET (version 1.9–1.13)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-118">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="9d8fb-119">Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:</span><span class="sxs-lookup"><span data-stu-id="9d8fb-119">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="9d8fb-120">Hämta först **samlingen IAggregatePartner.AgreementDetails** och anropa sedan **metoderna Get** eller **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="9d8fb-120">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="9d8fb-121">Sök sedan efter objektet i samlingen, vilket motsvarar Microsoft Cloud-avtal:</span><span class="sxs-lookup"><span data-stu-id="9d8fb-121">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="9d8fb-122">Java</span><span class="sxs-lookup"><span data-stu-id="9d8fb-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="9d8fb-123">Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:</span><span class="sxs-lookup"><span data-stu-id="9d8fb-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="9d8fb-124">Anropa först **funktionen IAggregatePartner.getAgreementDetails** och anropa sedan **get-funktionen.**</span><span class="sxs-lookup"><span data-stu-id="9d8fb-124">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="9d8fb-125">Sök sedan efter objektet i samlingen, vilket motsvarar Microsoft Cloud-avtal:</span><span class="sxs-lookup"><span data-stu-id="9d8fb-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

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

<span data-ttu-id="9d8fb-126">Ett fullständigt exempel finns i klassen [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) från [konsoltestappsprojektet.](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-126">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="9d8fb-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d8fb-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="9d8fb-128">Så här hämtar du avtalsmetadata för Microsoft Cloud-avtal:</span><span class="sxs-lookup"><span data-stu-id="9d8fb-128">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="9d8fb-129">Använd kommandot [**Get-PartnerAgreementDetail.**](/powershell/module/partnercenter/get-partneragreementdetail)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-129">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="9d8fb-130">Sök sedan efter objektet i samlingen, vilket motsvarar Microsoft Cloud-avtal:</span><span class="sxs-lookup"><span data-stu-id="9d8fb-130">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="9d8fb-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9d8fb-131">REST request</span></span>

<span data-ttu-id="9d8fb-132">Om du vill hämta avtalsmetadata Microsoft Cloud-avtal skapar du först en REST-begäran för att hämta **AgreementMetaData-samlingen.**</span><span class="sxs-lookup"><span data-stu-id="9d8fb-132">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="9d8fb-133">Sök sedan efter det objekt i samlingen som motsvarar Microsoft Cloud-avtal.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-133">Then search for the item in the collection that corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9d8fb-134">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="9d8fb-134">Request syntax</span></span>

| <span data-ttu-id="9d8fb-135">Metod</span><span class="sxs-lookup"><span data-stu-id="9d8fb-135">Method</span></span> | <span data-ttu-id="9d8fb-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9d8fb-136">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="9d8fb-137">GET</span><span class="sxs-lookup"><span data-stu-id="9d8fb-137">GET</span></span>    | <span data-ttu-id="9d8fb-138">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9d8fb-138">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9d8fb-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="9d8fb-139">Request headers</span></span>

<span data-ttu-id="9d8fb-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9d8fb-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9d8fb-141">Request body</span></span>

<span data-ttu-id="9d8fb-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9d8fb-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9d8fb-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="9d8fb-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9d8fb-144">REST response</span></span>

<span data-ttu-id="9d8fb-145">Om det lyckas returnerar den här metoden en samling **AgreementMetaData-resurser** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-145">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9d8fb-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9d8fb-146">Response success and error codes</span></span>

<span data-ttu-id="9d8fb-147">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9d8fb-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9d8fb-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9d8fb-149">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9d8fb-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9d8fb-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9d8fb-150">Response example</span></span>

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

<span data-ttu-id="9d8fb-151">Om du vill identifiera resursen i svaret som motsvarar Microsoft Cloud-avtal letar du efter resursen vars **agreementType-egenskap** har värdet "MicrosoftCloudAgreement".</span><span class="sxs-lookup"><span data-stu-id="9d8fb-151">To identify the resource in the response that corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
