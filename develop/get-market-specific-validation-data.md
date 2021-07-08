---
title: Hämta adressformateringsregler efter marknad
description: Hämta det förväntade adressformatet baserat på iso-koden för marknaden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5233d059ea6e71c28df36b2242659c28c5dd857
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549050"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="b04be-103">Hämta adressformateringsregler efter marknad</span><span class="sxs-lookup"><span data-stu-id="b04be-103">Get address formatting rules by market</span></span>

<span data-ttu-id="b04be-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b04be-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>


<span data-ttu-id="b04be-105">Hämta det förväntade adressformatet baserat på iso-koden för marknaden.</span><span class="sxs-lookup"><span data-stu-id="b04be-105">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b04be-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b04be-106">Prerequisites</span></span>

- <span data-ttu-id="b04be-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b04be-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b04be-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b04be-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b04be-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b04be-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b04be-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b04be-110">Request syntax</span></span>

| <span data-ttu-id="b04be-111">Metod</span><span class="sxs-lookup"><span data-stu-id="b04be-111">Method</span></span>  | <span data-ttu-id="b04be-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b04be-112">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="b04be-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="b04be-113">**GET**</span></span> | <span data-ttu-id="b04be-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b04be-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b04be-115">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="b04be-115">URI parameter</span></span>

| <span data-ttu-id="b04be-116">Namn</span><span class="sxs-lookup"><span data-stu-id="b04be-116">Name</span></span>           | <span data-ttu-id="b04be-117">Typ</span><span class="sxs-lookup"><span data-stu-id="b04be-117">Type</span></span>       | <span data-ttu-id="b04be-118">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b04be-118">Required</span></span> | <span data-ttu-id="b04be-119">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b04be-119">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="b04be-120">**isocode-id**</span><span class="sxs-lookup"><span data-stu-id="b04be-120">**isocode-id**</span></span> | <span data-ttu-id="b04be-121">**sträng**</span><span class="sxs-lookup"><span data-stu-id="b04be-121">**string**</span></span> | <span data-ttu-id="b04be-122">Y</span><span class="sxs-lookup"><span data-stu-id="b04be-122">Y</span></span>        | <span data-ttu-id="b04be-123">ISO-landskoden med två tecken.</span><span class="sxs-lookup"><span data-stu-id="b04be-123">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b04be-124">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b04be-124">Request headers</span></span>

<span data-ttu-id="b04be-125">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b04be-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b04be-126">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b04be-126">Request body</span></span>

<span data-ttu-id="b04be-127">Inga.</span><span class="sxs-lookup"><span data-stu-id="b04be-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b04be-128">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b04be-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="b04be-129">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b04be-129">REST response</span></span>

<span data-ttu-id="b04be-130">Om det lyckas returnerar den här metoden **ett CountryInformation-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="b04be-130">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b04be-131">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b04be-131">Response success and error codes</span></span>

<span data-ttu-id="b04be-132">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b04be-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b04be-133">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b04be-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b04be-134">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b04be-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b04be-135">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b04be-135">Response example</span></span>

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
