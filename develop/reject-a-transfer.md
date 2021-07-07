---
title: Avvisa en överföring
description: Så här avvisar du en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d09905979a89c9b2092462512c485524cd681d5f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445382"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="997ad-103">Avvisa en överföring</span><span class="sxs-lookup"><span data-stu-id="997ad-103">Reject a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="997ad-104">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="997ad-104">Prerequisites</span></span>

- <span data-ttu-id="997ad-105">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="997ad-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="997ad-106">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="997ad-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="997ad-107">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="997ad-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="997ad-108">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="997ad-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="997ad-109">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="997ad-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="997ad-110">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="997ad-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="997ad-111">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="997ad-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="997ad-112">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="997ad-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="997ad-113">En överföringsidentifierare för en befintlig överföring.</span><span class="sxs-lookup"><span data-stu-id="997ad-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="997ad-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="997ad-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="997ad-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="997ad-115">Request syntax</span></span>

| <span data-ttu-id="997ad-116">Metod</span><span class="sxs-lookup"><span data-stu-id="997ad-116">Method</span></span>   | <span data-ttu-id="997ad-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="997ad-117">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="997ad-118">**Patch**</span><span class="sxs-lookup"><span data-stu-id="997ad-118">**PATCH**</span></span> | <span data-ttu-id="997ad-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="997ad-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="997ad-120">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="997ad-120">URI parameter</span></span>

<span data-ttu-id="997ad-121">Använd följande sökvägsparameter för att identifiera kunden och ange vilken överföring som ska godkännas.</span><span class="sxs-lookup"><span data-stu-id="997ad-121">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="997ad-122">Namn</span><span class="sxs-lookup"><span data-stu-id="997ad-122">Name</span></span>            | <span data-ttu-id="997ad-123">Typ</span><span class="sxs-lookup"><span data-stu-id="997ad-123">Type</span></span>     | <span data-ttu-id="997ad-124">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="997ad-124">Required</span></span> | <span data-ttu-id="997ad-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="997ad-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="997ad-126">**kund-id**</span><span class="sxs-lookup"><span data-stu-id="997ad-126">**customer-id**</span></span> | <span data-ttu-id="997ad-127">sträng</span><span class="sxs-lookup"><span data-stu-id="997ad-127">string</span></span>   | <span data-ttu-id="997ad-128">Ja</span><span class="sxs-lookup"><span data-stu-id="997ad-128">Yes</span></span>      | <span data-ttu-id="997ad-129">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="997ad-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="997ad-130">**transfer-id**</span><span class="sxs-lookup"><span data-stu-id="997ad-130">**transfer-id**</span></span> | <span data-ttu-id="997ad-131">sträng</span><span class="sxs-lookup"><span data-stu-id="997ad-131">string</span></span>   | <span data-ttu-id="997ad-132">Ja</span><span class="sxs-lookup"><span data-stu-id="997ad-132">Yes</span></span>      | <span data-ttu-id="997ad-133">Ett GUID-formaterat överförings-ID som identifierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="997ad-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="997ad-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="997ad-134">Request headers</span></span>

<span data-ttu-id="997ad-135">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="997ad-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="997ad-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="997ad-136">Request body</span></span>

<span data-ttu-id="997ad-137">I den här tabellen beskrivs [TransferEntity-egenskaperna](transfer-entity-resources.md) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="997ad-137">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="997ad-138">Egenskap</span><span class="sxs-lookup"><span data-stu-id="997ad-138">Property</span></span>              | <span data-ttu-id="997ad-139">Typ</span><span class="sxs-lookup"><span data-stu-id="997ad-139">Type</span></span>          | <span data-ttu-id="997ad-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="997ad-140">Required</span></span>  | <span data-ttu-id="997ad-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="997ad-141">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="997ad-142">id</span><span class="sxs-lookup"><span data-stu-id="997ad-142">id</span></span>                    | <span data-ttu-id="997ad-143">sträng</span><span class="sxs-lookup"><span data-stu-id="997ad-143">string</span></span>        | <span data-ttu-id="997ad-144">No</span><span class="sxs-lookup"><span data-stu-id="997ad-144">No</span></span>    | <span data-ttu-id="997ad-145">En transferEntity-identifierare som anges när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="997ad-145">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="997ad-146">status</span><span class="sxs-lookup"><span data-stu-id="997ad-146">status</span></span>                | <span data-ttu-id="997ad-147">sträng</span><span class="sxs-lookup"><span data-stu-id="997ad-147">string</span></span>        | <span data-ttu-id="997ad-148">No</span><span class="sxs-lookup"><span data-stu-id="997ad-148">No</span></span>    | <span data-ttu-id="997ad-149">Status för transferEntity.</span><span class="sxs-lookup"><span data-stu-id="997ad-149">The status of the transferEntity.</span></span> <span data-ttu-id="997ad-150">Om du vill avvisa en överföring ska värdet anges som "avvisa"</span><span class="sxs-lookup"><span data-stu-id="997ad-150">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="997ad-151">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="997ad-151">Request example</span></span>

```http
PATCH /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
Connection: keep-alive
Content-Length: 63

{"id":"ac4a9d22-ba07-444e-890f-cfe084eed498","status":"reject"}

```

## <a name="rest-response"></a><span data-ttu-id="997ad-152">REST-svar</span><span class="sxs-lookup"><span data-stu-id="997ad-152">REST response</span></span>

<span data-ttu-id="997ad-153">Om det lyckas returnerar den här metoden den [ifyllda TransferEntity-resursen](transfer-entity-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="997ad-153">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="997ad-154">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="997ad-154">Response success and error codes</span></span>

<span data-ttu-id="997ad-155">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="997ad-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="997ad-156">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="997ad-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="997ad-157">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="997ad-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="997ad-158">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="997ad-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1069
Content-Type: application/json; charset=utf-8
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
X-Locale: en-US
Date: Fri, 27 Mar 2020 17:50:33 GMT

{
  "id": "ac4a9d22-ba07-444e-890f-cfe084eed498",
  "status": "Reject",
  "createdTime": "2020-03-25T22:05:25.1057725Z",
  "lastModifiedTime": "2020-03-27T17:50:32Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
      "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
      "billingCycle": "monthly",
      "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
      "quantity": 20,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498",
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
