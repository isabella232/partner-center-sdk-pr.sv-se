---
title: Hämta adressformateringsregler efter marknad
description: Hämta det förväntade adress formatet baserat på ISO-koden för marknaden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c755a38c11ed9803edb7777a0f661c1fbc5a6107
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769006"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="a85c2-103">Hämta adressformateringsregler efter marknad</span><span class="sxs-lookup"><span data-stu-id="a85c2-103">Get address formatting rules by market</span></span>

<span data-ttu-id="a85c2-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="a85c2-104">**Applies To**</span></span>

- <span data-ttu-id="a85c2-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a85c2-105">Partner Center</span></span>
- <span data-ttu-id="a85c2-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a85c2-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a85c2-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="a85c2-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a85c2-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a85c2-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a85c2-109">Hämta det förväntade adress formatet baserat på ISO-koden för marknaden.</span><span class="sxs-lookup"><span data-stu-id="a85c2-109">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a85c2-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a85c2-110">Prerequisites</span></span>

- <span data-ttu-id="a85c2-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a85c2-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a85c2-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a85c2-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a85c2-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a85c2-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a85c2-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="a85c2-114">Request syntax</span></span>

| <span data-ttu-id="a85c2-115">Metod</span><span class="sxs-lookup"><span data-stu-id="a85c2-115">Method</span></span>  | <span data-ttu-id="a85c2-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a85c2-116">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="a85c2-117">**TA**</span><span class="sxs-lookup"><span data-stu-id="a85c2-117">**GET**</span></span> | <span data-ttu-id="a85c2-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a85c2-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a85c2-119">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="a85c2-119">URI parameter</span></span>

| <span data-ttu-id="a85c2-120">Namn</span><span class="sxs-lookup"><span data-stu-id="a85c2-120">Name</span></span>           | <span data-ttu-id="a85c2-121">Typ</span><span class="sxs-lookup"><span data-stu-id="a85c2-121">Type</span></span>       | <span data-ttu-id="a85c2-122">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a85c2-122">Required</span></span> | <span data-ttu-id="a85c2-123">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a85c2-123">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="a85c2-124">**isocode-ID**</span><span class="sxs-lookup"><span data-stu-id="a85c2-124">**isocode-id**</span></span> | <span data-ttu-id="a85c2-125">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="a85c2-125">**string**</span></span> | <span data-ttu-id="a85c2-126">Y</span><span class="sxs-lookup"><span data-stu-id="a85c2-126">Y</span></span>        | <span data-ttu-id="a85c2-127">ISO-landkoden med två tecken.</span><span class="sxs-lookup"><span data-stu-id="a85c2-127">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a85c2-128">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a85c2-128">Request headers</span></span>

<span data-ttu-id="a85c2-129">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a85c2-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a85c2-130">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a85c2-130">Request body</span></span>

<span data-ttu-id="a85c2-131">Inga.</span><span class="sxs-lookup"><span data-stu-id="a85c2-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a85c2-132">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a85c2-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="a85c2-133">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a85c2-133">REST response</span></span>

<span data-ttu-id="a85c2-134">Om det lyckas returnerar den här metoden ett **CountryInformation** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="a85c2-134">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a85c2-135">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a85c2-135">Response success and error codes</span></span>

<span data-ttu-id="a85c2-136">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="a85c2-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a85c2-137">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a85c2-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a85c2-138">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a85c2-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a85c2-139">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a85c2-139">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1856
Content-Type: application/json
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
Date: Wed, 25 Nov 2015 06:36:47 GMT

{
    "iso2Code": "US",
    "defaultCulture": "en-US",
    "isStateRequired": true,
    "states": {
        "value": ["AK","AL","AR", "AZ","CA","CO","CT","DC","DE","FL","GA","HI","IA","ID","IL","IN",
        "KS","KY","LA","MA","MD","ME","MI","MN","MO","MS","MT","NC","ND","NE","NH","NJ","NM","NV",
        "NY","OH","OK","OR","PA","RI","SC","SD","TN","TX","UT","VA","VT","WA","WI","WV","WY"]
    },
    "supportedLanguages": {
        "value": ["en",
        "es"]
    },
    "supportedCultures": {
        "value": ["en-US",
        "es-US"]
    },
    "isPostalCodeRequired": true,
    "postalCodeRegex": "^\\d{
        5
    }(-\\d{
        4
    })?$",
    "isCityRequired": true,
    "isVatIdSupported": false,
    "taxIdFormat": "US######",
    "taxIdSample": "US999965",
    "phoneNumberRegex": "^(1[\\-\\/\\.]?)?(\((\\d{3})\)|(\\d{3}))[\\-\\/\\.]?(\\d{3})[\\-\\/\\.]?(\\d{4})$",
    "isRegistrationNumberSupported": false,
    "isTaxIdSupported": true,
    "resellerAgreementRegion": "AOC",
    "geographicRegion": "NorthAndLatinAmerica",
    "countryCallingCodes": {
        "value": ["1"]
    },
    "attributes": {
        "objectType": "CountryInformation"
    }
}
```
