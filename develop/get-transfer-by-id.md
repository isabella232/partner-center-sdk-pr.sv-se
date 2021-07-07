---
title: Hämta överföringsinformation efter ID
description: Så här hämtar du information om en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1347f95debec458b8c70c5e803cef6203ad34818
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445943"
---
# <a name="get-transfer-details-by-id"></a><span data-ttu-id="51d27-103">Hämta överföringsinformation efter ID</span><span class="sxs-lookup"><span data-stu-id="51d27-103">Get transfer details by ID</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51d27-104">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="51d27-104">Prerequisites</span></span>

- <span data-ttu-id="51d27-105">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="51d27-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="51d27-106">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="51d27-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="51d27-107">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="51d27-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="51d27-108">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="51d27-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="51d27-109">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="51d27-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="51d27-110">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="51d27-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="51d27-111">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="51d27-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="51d27-112">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="51d27-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="51d27-113">En överföringsidentifierare för en befintlig överföring.</span><span class="sxs-lookup"><span data-stu-id="51d27-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="51d27-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="51d27-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="51d27-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="51d27-115">Request syntax</span></span>

| <span data-ttu-id="51d27-116">Metod</span><span class="sxs-lookup"><span data-stu-id="51d27-116">Method</span></span>   | <span data-ttu-id="51d27-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="51d27-117">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="51d27-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="51d27-118">**GET**</span></span> | <span data-ttu-id="51d27-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="51d27-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="51d27-120">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="51d27-120">URI parameter</span></span>

<span data-ttu-id="51d27-121">Använd följande sökvägsparameter för att identifiera kunden och ange vilken överföring som ska godkännas.</span><span class="sxs-lookup"><span data-stu-id="51d27-121">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="51d27-122">Namn</span><span class="sxs-lookup"><span data-stu-id="51d27-122">Name</span></span>            | <span data-ttu-id="51d27-123">Typ</span><span class="sxs-lookup"><span data-stu-id="51d27-123">Type</span></span>     | <span data-ttu-id="51d27-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="51d27-124">Required</span></span> | <span data-ttu-id="51d27-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="51d27-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="51d27-126">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="51d27-126">**customer-id**</span></span> | <span data-ttu-id="51d27-127">sträng</span><span class="sxs-lookup"><span data-stu-id="51d27-127">string</span></span>   | <span data-ttu-id="51d27-128">Ja</span><span class="sxs-lookup"><span data-stu-id="51d27-128">Yes</span></span>      | <span data-ttu-id="51d27-129">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="51d27-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="51d27-130">**transfer-id**</span><span class="sxs-lookup"><span data-stu-id="51d27-130">**transfer-id**</span></span> | <span data-ttu-id="51d27-131">sträng</span><span class="sxs-lookup"><span data-stu-id="51d27-131">string</span></span>   | <span data-ttu-id="51d27-132">Ja</span><span class="sxs-lookup"><span data-stu-id="51d27-132">Yes</span></span>      | <span data-ttu-id="51d27-133">Ett GUID-formaterat överförings-ID som identifierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="51d27-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="51d27-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="51d27-134">Request headers</span></span>

<span data-ttu-id="51d27-135">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="51d27-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="51d27-136">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="51d27-136">Request example</span></span>

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556 HTTP/1.1
Authorization: Bearer <token>
Connection: keep-alive
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
Accept: application/json
```

## <a name="rest-response"></a><span data-ttu-id="51d27-137">REST-svar</span><span class="sxs-lookup"><span data-stu-id="51d27-137">REST response</span></span>

<span data-ttu-id="51d27-138">Om det lyckas returnerar den här metoden den [ifyllda TransferEntity-resursen](transfer-entity-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="51d27-138">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="51d27-139">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="51d27-139">Response success and error codes</span></span>

<span data-ttu-id="51d27-140">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="51d27-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="51d27-141">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="51d27-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="51d27-142">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="51d27-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="51d27-143">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="51d27-143">Response example</span></span>

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
