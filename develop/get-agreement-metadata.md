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
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="e0948-103">Hämta avtalsmetadata för Microsoft Cloud-avtal</span><span class="sxs-lookup"><span data-stu-id="e0948-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="e0948-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="e0948-104">**Applies To**</span></span>

- <span data-ttu-id="e0948-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e0948-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="e0948-106">**AgreementMetaData** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="e0948-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="e0948-107">Den gäller inte för:</span><span class="sxs-lookup"><span data-stu-id="e0948-107">It isn't applicable to:</span></span>
> - <span data-ttu-id="e0948-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e0948-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="e0948-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="e0948-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="e0948-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e0948-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0948-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e0948-111">Prerequisites</span></span>

- <span data-ttu-id="e0948-112">Om du använder Partner Center .NET SDK krävs version 1,9 eller senare.</span><span class="sxs-lookup"><span data-stu-id="e0948-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="e0948-113">Om du använder Partner Center Java SDK krävs version 1,8 eller senare.</span><span class="sxs-lookup"><span data-stu-id="e0948-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="e0948-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e0948-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="e0948-115">Det här scenariot stöder app + användarautentisering..</span><span class="sxs-lookup"><span data-stu-id="e0948-115">This scenario supports app + user authentication..</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="e0948-116">.NET (version 1,14 eller senare)</span><span class="sxs-lookup"><span data-stu-id="e0948-116">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="e0948-117">Så här hämtar du avtals metadata för Microsoft Cloud avtal:</span><span class="sxs-lookup"><span data-stu-id="e0948-117">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="e0948-118">Börja med att hämta samlingen **IAggregatePartner. AgreementDetails** .</span><span class="sxs-lookup"><span data-stu-id="e0948-118">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="e0948-119">Anropa **ByAgreementType** -metoden för att filtrera samlingen till Microsoft Cloud avtal.</span><span class="sxs-lookup"><span data-stu-id="e0948-119">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="e0948-120">Anropa slutligen **Get** -eller **GetAsync** -metoden.</span><span class="sxs-lookup"><span data-stu-id="e0948-120">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="e0948-121">Ett fullständigt exempel finns i [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.</span><span class="sxs-lookup"><span data-stu-id="e0948-121">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="e0948-122">.NET (version 1,9-1,13)</span><span class="sxs-lookup"><span data-stu-id="e0948-122">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="e0948-123">Så här hämtar du avtals metadata för Microsoft Cloud avtalet:</span><span class="sxs-lookup"><span data-stu-id="e0948-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="e0948-124">Hämta först **IAggregatePartner. AgreementDetails** -samlingen och anropa sedan metoderna **Get** eller **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="e0948-124">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="e0948-125">Sök sedan efter objektet i samlingen, som motsvarar Microsoft Cloud avtalet:</span><span class="sxs-lookup"><span data-stu-id="e0948-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="e0948-126">Java</span><span class="sxs-lookup"><span data-stu-id="e0948-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e0948-127">Så här hämtar du avtals metadata för Microsoft Cloud avtalet:</span><span class="sxs-lookup"><span data-stu-id="e0948-127">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="e0948-128">Anropa först funktionen **IAggregatePartner. getAgreementDetails** och anropa sedan **Get** -funktionen.</span><span class="sxs-lookup"><span data-stu-id="e0948-128">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="e0948-129">Sök sedan efter objektet i samlingen, som motsvarar Microsoft Cloud avtalet:</span><span class="sxs-lookup"><span data-stu-id="e0948-129">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

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

<span data-ttu-id="e0948-130">Ett fullständigt exempel finns i [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) -klassen från projektets [test app](https://github.com/Microsoft/Partner-Center-Java-Samples) -projekt.</span><span class="sxs-lookup"><span data-stu-id="e0948-130">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="e0948-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0948-131">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e0948-132">Så här hämtar du avtals metadata för Microsoft Cloud avtalet:</span><span class="sxs-lookup"><span data-stu-id="e0948-132">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="e0948-133">Använd kommandot [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) .</span><span class="sxs-lookup"><span data-stu-id="e0948-133">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="e0948-134">Sök sedan efter objektet i samlingen, som motsvarar Microsoft Cloud avtalet:</span><span class="sxs-lookup"><span data-stu-id="e0948-134">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="e0948-135">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e0948-135">REST request</span></span>

<span data-ttu-id="e0948-136">Om du vill hämta avtals metadata för Microsoft Cloud avtal måste du först skapa en REST-begäran för att hämta **AgreementMetaData** -samlingen.</span><span class="sxs-lookup"><span data-stu-id="e0948-136">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="e0948-137">Sök sedan efter objektet i samlingen som motsvarar Microsoft Cloud avtalet.</span><span class="sxs-lookup"><span data-stu-id="e0948-137">Then search for the item in the collection which corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e0948-138">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e0948-138">Request syntax</span></span>

| <span data-ttu-id="e0948-139">Metod</span><span class="sxs-lookup"><span data-stu-id="e0948-139">Method</span></span> | <span data-ttu-id="e0948-140">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e0948-140">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="e0948-141">GET</span><span class="sxs-lookup"><span data-stu-id="e0948-141">GET</span></span>    | <span data-ttu-id="e0948-142">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="e0948-142">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e0948-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e0948-143">Request headers</span></span>

<span data-ttu-id="e0948-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e0948-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e0948-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e0948-145">Request body</span></span>

<span data-ttu-id="e0948-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="e0948-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e0948-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e0948-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="e0948-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e0948-148">REST response</span></span>

<span data-ttu-id="e0948-149">Om det lyckas returnerar den här metoden en samling **AgreementMetaData** -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="e0948-149">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e0948-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e0948-150">Response success and error codes</span></span>

<span data-ttu-id="e0948-151">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e0948-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e0948-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e0948-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e0948-153">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e0948-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e0948-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e0948-154">Response example</span></span>

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

<span data-ttu-id="e0948-155">Identifiera resursen i svaret som motsvarar Microsoft Cloud avtalet genom att leta efter resursen vars **agreementType** -egenskap har värdet "MicrosoftCloudAgreement".</span><span class="sxs-lookup"><span data-stu-id="e0948-155">To identify the resource in the response which corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
