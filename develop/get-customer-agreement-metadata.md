---
title: Hämta avtalsmetadata för Microsoft-kundavtalet
description: Den här artikeln förklarar hur du får avtals-metadata för Microsofts kund avtal.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769432"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="b5d8a-103">Hämta avtalsmetadata för Microsoft-kundavtalet</span><span class="sxs-lookup"><span data-stu-id="b5d8a-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="b5d8a-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="b5d8a-104">**Applies to:**</span></span>

- <span data-ttu-id="b5d8a-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b5d8a-105">Partner Center</span></span>

<span data-ttu-id="b5d8a-106">Avtals-metadata för Microsofts kund avtal stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="b5d8a-107">Den gäller inte för:</span><span class="sxs-lookup"><span data-stu-id="b5d8a-107">It doesn't apply to:</span></span>

- <span data-ttu-id="b5d8a-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b5d8a-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b5d8a-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="b5d8a-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b5d8a-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b5d8a-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b5d8a-111">Du måste hämta avtals metadata för Microsofts kund avtal innan du kan:</span><span class="sxs-lookup"><span data-stu-id="b5d8a-111">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="b5d8a-112">Bekräfta en kunds godkännande av Microsofts kund avtal</span><span class="sxs-lookup"><span data-stu-id="b5d8a-112">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="b5d8a-113">Hämta en nedladdnings länk för Microsofts kund avtals mall</span><span class="sxs-lookup"><span data-stu-id="b5d8a-113">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="b5d8a-114">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b5d8a-114">Prerequisites</span></span>

- <span data-ttu-id="b5d8a-115">Om du använder Partner Center .NET SDK krävs version 1,14 eller senare.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-115">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="b5d8a-116">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b5d8a-116">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="b5d8a-117">Det här scenariot stöder endast app + User Authentication.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-117">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="b5d8a-118">.NET (version 1,14 eller senare)</span><span class="sxs-lookup"><span data-stu-id="b5d8a-118">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="b5d8a-119">Så här hämtar du avtals metadata för Microsofts kund avtal:</span><span class="sxs-lookup"><span data-stu-id="b5d8a-119">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="b5d8a-120">Börja med att hämta samlingen **IAggregatePartner. AgreementDetails** .</span><span class="sxs-lookup"><span data-stu-id="b5d8a-120">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="b5d8a-121">Anropa **ByAgreementType** -metoden för att filtrera samlingen till Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-121">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="b5d8a-122">Anropa slutligen **Get** -eller **GetAsync** -metoden.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-122">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="b5d8a-123">Ett fullständigt exempel finns i [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-123">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b5d8a-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b5d8a-124">REST request</span></span>

<span data-ttu-id="b5d8a-125">Så här hämtar du avtals metadata för Microsofts kund avtal:</span><span class="sxs-lookup"><span data-stu-id="b5d8a-125">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="b5d8a-126">Skapa en REST-begäran för att hämta [AgreementMetaData](./agreement-metadata-resources.md) -samlingen.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-126">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="b5d8a-127">Använd Frågeparametern **agreementType** för att begränsa resultatet till enbart Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-127">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b5d8a-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b5d8a-128">Request syntax</span></span>

| <span data-ttu-id="b5d8a-129">Metod</span><span class="sxs-lookup"><span data-stu-id="b5d8a-129">Method</span></span> | <span data-ttu-id="b5d8a-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b5d8a-130">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="b5d8a-131">GET</span><span class="sxs-lookup"><span data-stu-id="b5d8a-131">GET</span></span>    | <span data-ttu-id="b5d8a-132">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Agreements? agreementType = {Agreement-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b5d8a-132">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b5d8a-133">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b5d8a-133">URI parameters</span></span>

| <span data-ttu-id="b5d8a-134">Namn</span><span class="sxs-lookup"><span data-stu-id="b5d8a-134">Name</span></span>                   | <span data-ttu-id="b5d8a-135">Typ</span><span class="sxs-lookup"><span data-stu-id="b5d8a-135">Type</span></span>     | <span data-ttu-id="b5d8a-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b5d8a-136">Required</span></span> | <span data-ttu-id="b5d8a-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b5d8a-137">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="b5d8a-138">avtals typ</span><span class="sxs-lookup"><span data-stu-id="b5d8a-138">agreement-type</span></span> | <span data-ttu-id="b5d8a-139">sträng</span><span class="sxs-lookup"><span data-stu-id="b5d8a-139">string</span></span> | <span data-ttu-id="b5d8a-140">No</span><span class="sxs-lookup"><span data-stu-id="b5d8a-140">No</span></span> | <span data-ttu-id="b5d8a-141">Använd den här parametern om du vill begränsa fråge svaret till en speciell avtals typ.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-141">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="b5d8a-142">De värden som stöds är:</span><span class="sxs-lookup"><span data-stu-id="b5d8a-142">The supported values are:</span></span> <br/><br/><span data-ttu-id="b5d8a-143">**MicrosoftCloudAgreement** som endast inkluderar avtals-metadata av typen *MicrosoftCloudAgreement*</span><span class="sxs-lookup"><span data-stu-id="b5d8a-143">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="b5d8a-144">**MicrosoftCustomerAgreement** som endast inkluderar avtals-metadata av typen *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-144">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="b5d8a-145">**\*** som returnerar alla avtals-metadata.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-145">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="b5d8a-146">(Använd inte **\*** om din kod har den nödvändiga körnings logiken för att hantera okända avtals typer eftersom Microsoft kan presentera avtals metadata med nya avtals typer när som helst.)</span><span class="sxs-lookup"><span data-stu-id="b5d8a-146">(Don't use **\*** unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)</span></span><br/><br/> <span data-ttu-id="b5d8a-147">**Obs:** Om URI-parametern inte anges använder frågan standardvärdet för **MicrosoftCloudAgreement** för bakåtkompatibilitet.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-147">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="b5d8a-148">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b5d8a-148">Request headers</span></span>

<span data-ttu-id="b5d8a-149">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b5d8a-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b5d8a-150">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b5d8a-150">Request body</span></span>

<span data-ttu-id="b5d8a-151">Inga.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b5d8a-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b5d8a-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="b5d8a-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b5d8a-153">REST response</span></span>

<span data-ttu-id="b5d8a-154">Om det lyckas returnerar den här metoden en samling [ **AgreementMetaData** -resurser](./agreement-metadata-resources.md) i svars texten.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-154">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b5d8a-155">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b5d8a-155">Response success and error codes</span></span>

<span data-ttu-id="b5d8a-156">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="b5d8a-157">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b5d8a-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b5d8a-158">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b5d8a-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b5d8a-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b5d8a-159">Response example</span></span>

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
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
