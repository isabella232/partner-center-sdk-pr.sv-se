---
title: Hämta avtalsmetadata för Microsoft-kundavtalet
description: Den här artikeln förklarar hur du hämtar avtalsmetadata för Microsoft-kundavtal.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025732"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="daa7d-103">Hämta avtalsmetadata för Microsoft-kundavtalet</span><span class="sxs-lookup"><span data-stu-id="daa7d-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="daa7d-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="daa7d-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="daa7d-105">**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="daa7d-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="daa7d-106">Avtalsmetadata för Microsoft-kundavtal stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="daa7d-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="daa7d-107">Du måste hämta avtalets metadata för Microsoft-kundavtal innan du kan:</span><span class="sxs-lookup"><span data-stu-id="daa7d-107">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="daa7d-108">Bekräfta en kunds godkännande av Microsoft-kundavtal</span><span class="sxs-lookup"><span data-stu-id="daa7d-108">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="daa7d-109">Hämta en nedladdningslänk för Microsoft-kundavtal mallen</span><span class="sxs-lookup"><span data-stu-id="daa7d-109">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="daa7d-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="daa7d-110">Prerequisites</span></span>

- <span data-ttu-id="daa7d-111">Om du använder Partner Center .NET SDK krävs version 1.14 eller senare.</span><span class="sxs-lookup"><span data-stu-id="daa7d-111">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="daa7d-112">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="daa7d-112">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="daa7d-113">Det här scenariot stöder endast app- och användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="daa7d-113">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="daa7d-114">.NET (version 1.14 eller senare)</span><span class="sxs-lookup"><span data-stu-id="daa7d-114">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="daa7d-115">Så här hämtar du avtalsmetadata för Microsoft-kundavtal:</span><span class="sxs-lookup"><span data-stu-id="daa7d-115">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="daa7d-116">Hämta först **samlingen IAggregatePartner.AgreementDetails.**</span><span class="sxs-lookup"><span data-stu-id="daa7d-116">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="daa7d-117">Anropa **metoden ByAgreementType** för att filtrera samlingen till Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="daa7d-117">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="daa7d-118">Anropa slutligen **metoden Get** eller **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="daa7d-118">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="daa7d-119">Ett fullständigt exempel finns i klassen [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="daa7d-119">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="daa7d-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="daa7d-120">REST request</span></span>

<span data-ttu-id="daa7d-121">Så här hämtar du avtalsmetadata för Microsoft-kundavtal:</span><span class="sxs-lookup"><span data-stu-id="daa7d-121">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="daa7d-122">Skapa en REST-begäran för att hämta [AgreementMetaData-samlingen.](./agreement-metadata-resources.md)</span><span class="sxs-lookup"><span data-stu-id="daa7d-122">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="daa7d-123">Använd **frågeparametern agreementType** för att begränsa resultatet till endast Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="daa7d-123">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="daa7d-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="daa7d-124">Request syntax</span></span>

| <span data-ttu-id="daa7d-125">Metod</span><span class="sxs-lookup"><span data-stu-id="daa7d-125">Method</span></span> | <span data-ttu-id="daa7d-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="daa7d-126">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="daa7d-127">GET</span><span class="sxs-lookup"><span data-stu-id="daa7d-127">GET</span></span>    | <span data-ttu-id="daa7d-128">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="daa7d-128">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="daa7d-129">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="daa7d-129">URI parameters</span></span>

| <span data-ttu-id="daa7d-130">Namn</span><span class="sxs-lookup"><span data-stu-id="daa7d-130">Name</span></span>                   | <span data-ttu-id="daa7d-131">Typ</span><span class="sxs-lookup"><span data-stu-id="daa7d-131">Type</span></span>     | <span data-ttu-id="daa7d-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="daa7d-132">Required</span></span> | <span data-ttu-id="daa7d-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="daa7d-133">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="daa7d-134">avtalstyp</span><span class="sxs-lookup"><span data-stu-id="daa7d-134">agreement-type</span></span> | <span data-ttu-id="daa7d-135">sträng</span><span class="sxs-lookup"><span data-stu-id="daa7d-135">string</span></span> | <span data-ttu-id="daa7d-136">No</span><span class="sxs-lookup"><span data-stu-id="daa7d-136">No</span></span> | <span data-ttu-id="daa7d-137">Använd den här parametern för att begränsa frågesvaret till specifik avtalstyp.</span><span class="sxs-lookup"><span data-stu-id="daa7d-137">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="daa7d-138">Värdena som stöds är:</span><span class="sxs-lookup"><span data-stu-id="daa7d-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="daa7d-139">**MicrosoftCloudAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCloudAgreement*</span><span class="sxs-lookup"><span data-stu-id="daa7d-139">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="daa7d-140">**MicrosoftCustomerAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="daa7d-140">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="daa7d-141">**\**_ som returnerar alla avtalsmetadata. (Använd inte _\* \* _ såvida inte din kod har den nödvändiga körningslogiken för att hantera okända avtalstyper eftersom Microsoft kan införa avtalsmetadata med nya avtalstyper när *som helst.) <br/> <br/> _* Obs!*\* Om URI-parametern inte anges används **MicrosoftCloudAgreement** som standard för bakåtkompatibilitet.</span><span class="sxs-lookup"><span data-stu-id="daa7d-141">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="daa7d-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="daa7d-142">Request headers</span></span>

<span data-ttu-id="daa7d-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="daa7d-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="daa7d-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="daa7d-144">Request body</span></span>

<span data-ttu-id="daa7d-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="daa7d-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="daa7d-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="daa7d-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="daa7d-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="daa7d-147">REST response</span></span>

<span data-ttu-id="daa7d-148">Om det lyckas returnerar den här metoden en samling [ **AgreementMetaData-resurser**](./agreement-metadata-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="daa7d-148">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="daa7d-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="daa7d-149">Response success and error codes</span></span>

<span data-ttu-id="daa7d-150">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="daa7d-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="daa7d-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="daa7d-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="daa7d-152">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="daa7d-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="daa7d-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="daa7d-153">Response example</span></span>

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
