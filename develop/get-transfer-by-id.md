---
title: Hämta överförings information per ID
description: Så här hämtar du information om en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c39e9483f1e51469981b0d6fa2541a6372ff2dac
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768910"
---
# <a name="get-transfer-details-by-id"></a><span data-ttu-id="d8a13-103">Hämta överförings information per ID</span><span class="sxs-lookup"><span data-stu-id="d8a13-103">Get transfer details by id</span></span>

<span data-ttu-id="d8a13-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="d8a13-104">**Applies to:**</span></span>

- <span data-ttu-id="d8a13-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d8a13-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8a13-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d8a13-106">Prerequisites</span></span>

- <span data-ttu-id="d8a13-107">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d8a13-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d8a13-108">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d8a13-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d8a13-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d8a13-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d8a13-110">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="d8a13-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d8a13-111">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="d8a13-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d8a13-112">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="d8a13-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d8a13-113">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="d8a13-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d8a13-114">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d8a13-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d8a13-115">En överförings identifierare för en befintlig överföring.</span><span class="sxs-lookup"><span data-stu-id="d8a13-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d8a13-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d8a13-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d8a13-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d8a13-117">Request syntax</span></span>

| <span data-ttu-id="d8a13-118">Metod</span><span class="sxs-lookup"><span data-stu-id="d8a13-118">Method</span></span>   | <span data-ttu-id="d8a13-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d8a13-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8a13-120">**TA**</span><span class="sxs-lookup"><span data-stu-id="d8a13-120">**GET**</span></span> | <span data-ttu-id="d8a13-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d8a13-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="d8a13-122">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d8a13-122">URI parameter</span></span>

<span data-ttu-id="d8a13-123">Använd följande Sök vägs parameter för att identifiera kunden och ange den överföring som ska godkännas.</span><span class="sxs-lookup"><span data-stu-id="d8a13-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="d8a13-124">Namn</span><span class="sxs-lookup"><span data-stu-id="d8a13-124">Name</span></span>            | <span data-ttu-id="d8a13-125">Typ</span><span class="sxs-lookup"><span data-stu-id="d8a13-125">Type</span></span>     | <span data-ttu-id="d8a13-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d8a13-126">Required</span></span> | <span data-ttu-id="d8a13-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d8a13-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="d8a13-128">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="d8a13-128">**customer-id**</span></span> | <span data-ttu-id="d8a13-129">sträng</span><span class="sxs-lookup"><span data-stu-id="d8a13-129">string</span></span>   | <span data-ttu-id="d8a13-130">Yes</span><span class="sxs-lookup"><span data-stu-id="d8a13-130">Yes</span></span>      | <span data-ttu-id="d8a13-131">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="d8a13-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="d8a13-132">**överförings-ID**</span><span class="sxs-lookup"><span data-stu-id="d8a13-132">**transfer-id**</span></span> | <span data-ttu-id="d8a13-133">sträng</span><span class="sxs-lookup"><span data-stu-id="d8a13-133">string</span></span>   | <span data-ttu-id="d8a13-134">Yes</span><span class="sxs-lookup"><span data-stu-id="d8a13-134">Yes</span></span>      | <span data-ttu-id="d8a13-135">Ett GUID-formaterat överförings-ID som identifierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="d8a13-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="d8a13-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d8a13-136">Request headers</span></span>

<span data-ttu-id="d8a13-137">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d8a13-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="d8a13-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d8a13-138">Request example</span></span>

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556 HTTP/1.1
Authorization: Bearer <token>
Connection: keep-alive
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
Accept: application/json
```

## <a name="rest-response"></a><span data-ttu-id="d8a13-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d8a13-139">REST response</span></span>

<span data-ttu-id="d8a13-140">Om det lyckas returnerar den här metoden den ifyllda [TransferEntity](transfer-entity-resources.md) -resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="d8a13-140">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d8a13-141">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d8a13-141">Response success and error codes</span></span>

<span data-ttu-id="d8a13-142">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d8a13-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d8a13-143">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d8a13-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d8a13-144">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d8a13-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d8a13-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d8a13-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1501
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
X-Locale: en-US
Date: Fri, 27 Mar 2020 18:25:25 GMT

{
  "id": "46e8ed67-8adf-4f65-b3d8-d31318080556",
  "status": "Active",
  "createdTime": "2020-03-27T18:22:33.2875302Z",
  "lastModifiedTime": "2020-03-27T18:22:33Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "75B71186-73C3-45B4-A403-281C0D7EB032",
      "offerId": "F72752C8-3E37-4C9B-A1A0-69E8442068DC",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central Team Member",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 1,
      "subscriptionId": "1FB4CB0A-EB79-4300-9E87-7D486054888A",
      "offerId": "88F9EB8A-0636-45E8-A601-553E0A48AA9E",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central External Accountant",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 2,
      "subscriptionId": "08AB3010-B647-402E-8955-B6C0FB364D8F",
      "offerId": "4D8F3B90-29B3-4E7B-B37C-4A435DDEF1D9",
      "billingCycle": "annual",
      "friendlyName": "Common Area Phone",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "TransferEntity"
  }
}

```
