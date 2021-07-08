---
title: Hämta partnerns juridiska företagsprofil
description: Lär dig hur du använder API:er för att hämta din juridiska företagsprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0654e364674bc2db129a0904d411c6fb67cbb9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549067"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="cfbd6-103">Hämta partnerns juridiska företagsprofil</span><span class="sxs-lookup"><span data-stu-id="cfbd6-103">Get the partner legal business profile</span></span>

<span data-ttu-id="cfbd6-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cfbd6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cfbd6-105">Så här hämtar du en partners juridiska affärsprofil.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-105">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfbd6-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cfbd6-106">Prerequisites</span></span>

- <span data-ttu-id="cfbd6-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cfbd6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cfbd6-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="cfbd6-109">C\#</span><span class="sxs-lookup"><span data-stu-id="cfbd6-109">C\#</span></span>

<span data-ttu-id="cfbd6-110">Om du vill hämta partnerns juridiska affärsprofil hämtar du först ett gränssnitt för insamlingen av partnerprofilåtgärder från egenskapen **IAggregatePartner.Profiles.**</span><span class="sxs-lookup"><span data-stu-id="cfbd6-110">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="cfbd6-111">Hämta sedan värdet för egenskapen **LegalBusinessProfile** för att hämta ett gränssnitt för juridiska affärsprofilåtgärder.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-111">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="cfbd6-112">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) för att hämta profilen.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="cfbd6-113">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cfbd6-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cfbd6-114">**Project:** Partnercenter-SDK **Exempelklass:** GetLegalBusinessProfile.cs</span><span class="sxs-lookup"><span data-stu-id="cfbd6-114">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cfbd6-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cfbd6-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cfbd6-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="cfbd6-116">Request syntax</span></span>

| <span data-ttu-id="cfbd6-117">Metod</span><span class="sxs-lookup"><span data-stu-id="cfbd6-117">Method</span></span>  | <span data-ttu-id="cfbd6-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cfbd6-118">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="cfbd6-119">**Få**</span><span class="sxs-lookup"><span data-stu-id="cfbd6-119">**GET**</span></span> | <span data-ttu-id="cfbd6-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cfbd6-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cfbd6-121">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cfbd6-121">Request headers</span></span>

<span data-ttu-id="cfbd6-122">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cfbd6-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cfbd6-123">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cfbd6-123">Request body</span></span>

<span data-ttu-id="cfbd6-124">Inga.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cfbd6-125">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cfbd6-125">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness?vettingVersion=Current HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="cfbd6-126">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cfbd6-126">REST response</span></span>

<span data-ttu-id="cfbd6-127">Om det lyckas returnerar den här metoden **ett LegalBusinessProfile-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-127">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cfbd6-128">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cfbd6-128">Response success and error codes</span></span>

<span data-ttu-id="cfbd6-129">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cfbd6-130">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cfbd6-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cfbd6-131">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="cfbd6-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cfbd6-132">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cfbd6-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1151
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CV: MEgCpJUoGUeXG+4a.0
MS-ServerId: 030011719
Date: Tue, 21 Mar 2017 17:29:52 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550100"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550100"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
