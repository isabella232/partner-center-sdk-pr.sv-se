---
title: Hämta partnerns juridiska företagsprofil
description: 'Lär dig hur du använder API: er för att få din juridiska företags profil.'
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1d488c8deb9f01110e92327035ce0c3c023fcb46
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500030"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="db849-103">Hämta partnerns juridiska företagsprofil</span><span class="sxs-lookup"><span data-stu-id="db849-103">Get the partner legal business profile</span></span>

<span data-ttu-id="db849-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="db849-104">**Applies To**</span></span>

- <span data-ttu-id="db849-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="db849-105">Partner Center</span></span>
- <span data-ttu-id="db849-106">Partnercenter drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="db849-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="db849-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="db849-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="db849-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="db849-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="db849-109">Så här hämtar du en partners juridiska företags profil.</span><span class="sxs-lookup"><span data-stu-id="db849-109">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db849-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="db849-110">Prerequisites</span></span>

- <span data-ttu-id="db849-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="db849-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="db849-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="db849-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="db849-113">C\#</span><span class="sxs-lookup"><span data-stu-id="db849-113">C\#</span></span>

<span data-ttu-id="db849-114">Om du vill hämta partnerns juridiska företags profil måste du först hämta ett gränssnitt till samlingen av partner profil åtgärder från egenskapen **IAggregatePartner. profiles** .</span><span class="sxs-lookup"><span data-stu-id="db849-114">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="db849-115">Hämta sedan värdet för egenskapen **LegalBusinessProfile** för att hämta ett gränssnitt till juridiska affärs profil åtgärder.</span><span class="sxs-lookup"><span data-stu-id="db849-115">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="db849-116">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) för att hämta profilen.</span><span class="sxs-lookup"><span data-stu-id="db849-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="db849-117">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="db849-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="db849-118">**Projekt**: Partner Center SDK-exempel **klass**: GetLegalBusinessProfile. CS</span><span class="sxs-lookup"><span data-stu-id="db849-118">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="db849-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="db849-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="db849-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="db849-120">Request syntax</span></span>

| <span data-ttu-id="db849-121">Metod</span><span class="sxs-lookup"><span data-stu-id="db849-121">Method</span></span>  | <span data-ttu-id="db849-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="db849-122">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="db849-123">**TA**</span><span class="sxs-lookup"><span data-stu-id="db849-123">**GET**</span></span> | <span data-ttu-id="db849-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="db849-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="db849-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="db849-125">Request headers</span></span>

<span data-ttu-id="db849-126">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="db849-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="db849-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="db849-127">Request body</span></span>

<span data-ttu-id="db849-128">Inga.</span><span class="sxs-lookup"><span data-stu-id="db849-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="db849-129">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="db849-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="db849-130">REST-svar</span><span class="sxs-lookup"><span data-stu-id="db849-130">REST response</span></span>

<span data-ttu-id="db849-131">Om det lyckas returnerar den här metoden ett **LegalBusinessProfile** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="db849-131">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="db849-132">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="db849-132">Response success and error codes</span></span>

<span data-ttu-id="db849-133">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="db849-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="db849-134">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="db849-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="db849-135">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="db849-135">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="db849-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="db849-136">Response example</span></span>

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
