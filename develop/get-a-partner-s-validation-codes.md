---
title: Hämta en partners offentliga community-moln validerings koder
description: Så här hämtar du en partners offentliga community-moln validerings koder.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: d84a3d3c69d835e42565c4e6f1edb06ab338340a
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769285"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="386aa-103">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="386aa-103">Get a partner's validation codes</span></span>

<span data-ttu-id="386aa-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="386aa-104">**Applies To**</span></span>

- <span data-ttu-id="386aa-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="386aa-105">Partner Center</span></span>

<span data-ttu-id="386aa-106">Så här hämtar du en samling av en partners validerings koder för offentliga community-moln.</span><span class="sxs-lookup"><span data-stu-id="386aa-106">How to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="386aa-107">En validerings kod krävs för att skapa en kund i det offentliga community-molnet.</span><span class="sxs-lookup"><span data-stu-id="386aa-107">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="386aa-108">Om du är intresse rad av att organisationen eller din kund organisation godkänts för Office 365 myndighets GCC för CSP, kan du läsa [Office 365 myndigheter GCC för CSP-partner och kund villkor för godkännande/Partner-Center/CSP-gcc-validate).</span><span class="sxs-lookup"><span data-stu-id="386aa-108">If you are interested in having your organization or your customers organization approved for Office 365 Government GCC for CSP, please see [Office 365 Government GCC for CSP Partner and Customer Eligibility Criteria/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="386aa-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="386aa-109">Prerequisites</span></span>

- <span data-ttu-id="386aa-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="386aa-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="386aa-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="386aa-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="386aa-112">Bekräfta validering efter ifyllning av formulär [här](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span><span class="sxs-lookup"><span data-stu-id="386aa-112">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="386aa-113">En kund utan kvalificering.</span><span class="sxs-lookup"><span data-stu-id="386aa-113">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="386aa-114">C\#</span><span class="sxs-lookup"><span data-stu-id="386aa-114">C\#</span></span>

<span data-ttu-id="386aa-115">Om du vill hämta en lista över alla validerings koder för en partner anropar du **GetValidationCodes**.</span><span class="sxs-lookup"><span data-stu-id="386aa-115">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="386aa-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="386aa-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="386aa-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="386aa-117">Request syntax</span></span>

| <span data-ttu-id="386aa-118">Metod</span><span class="sxs-lookup"><span data-stu-id="386aa-118">Method</span></span>  | <span data-ttu-id="386aa-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="386aa-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="386aa-120">**TA**</span><span class="sxs-lookup"><span data-stu-id="386aa-120">**GET**</span></span> | <span data-ttu-id="386aa-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/all/validations http/1.1</span><span class="sxs-lookup"><span data-stu-id="386aa-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="386aa-122">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="386aa-122">Request headers</span></span>

<span data-ttu-id="386aa-123">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="386aa-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="386aa-124">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="386aa-124">Request body</span></span>

<span data-ttu-id="386aa-125">Inga.</span><span class="sxs-lookup"><span data-stu-id="386aa-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="386aa-126">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="386aa-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="386aa-127">REST-svar</span><span class="sxs-lookup"><span data-stu-id="386aa-127">REST response</span></span>

<span data-ttu-id="386aa-128">Om det lyckas returnerar den här metoden en lista över [**ValidationCode**](utility-resources.md#validationcode) -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="386aa-128">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="386aa-129">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="386aa-129">Response success and error codes</span></span>

<span data-ttu-id="386aa-130">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="386aa-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="386aa-131">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="386aa-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="386aa-132">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="386aa-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="386aa-133">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="386aa-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
