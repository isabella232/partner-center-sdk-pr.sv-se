---
title: Avvisa en överföring
description: Så här avvisar du en överföring av prenumerationer för en kund.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e4a182ff92a21cf72ca1c2da9de7e211b433725f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768979"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="43cfc-103">Avvisa en överföring</span><span class="sxs-lookup"><span data-stu-id="43cfc-103">Reject a transfer</span></span>

<span data-ttu-id="43cfc-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="43cfc-104">**Applies to:**</span></span>

- <span data-ttu-id="43cfc-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="43cfc-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43cfc-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="43cfc-106">Prerequisites</span></span>

- <span data-ttu-id="43cfc-107">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="43cfc-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="43cfc-108">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="43cfc-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="43cfc-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="43cfc-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="43cfc-110">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="43cfc-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="43cfc-111">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="43cfc-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="43cfc-112">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="43cfc-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="43cfc-113">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="43cfc-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="43cfc-114">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="43cfc-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="43cfc-115">En överförings identifierare för en befintlig överföring.</span><span class="sxs-lookup"><span data-stu-id="43cfc-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="43cfc-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="43cfc-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="43cfc-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="43cfc-117">Request syntax</span></span>

| <span data-ttu-id="43cfc-118">Metod</span><span class="sxs-lookup"><span data-stu-id="43cfc-118">Method</span></span>   | <span data-ttu-id="43cfc-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="43cfc-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="43cfc-120">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="43cfc-120">**PATCH**</span></span> | <span data-ttu-id="43cfc-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="43cfc-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="43cfc-122">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="43cfc-122">URI parameter</span></span>

<span data-ttu-id="43cfc-123">Använd följande Sök vägs parameter för att identifiera kunden och ange den överföring som ska godkännas.</span><span class="sxs-lookup"><span data-stu-id="43cfc-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="43cfc-124">Namn</span><span class="sxs-lookup"><span data-stu-id="43cfc-124">Name</span></span>            | <span data-ttu-id="43cfc-125">Typ</span><span class="sxs-lookup"><span data-stu-id="43cfc-125">Type</span></span>     | <span data-ttu-id="43cfc-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="43cfc-126">Required</span></span> | <span data-ttu-id="43cfc-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="43cfc-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="43cfc-128">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="43cfc-128">**customer-id**</span></span> | <span data-ttu-id="43cfc-129">sträng</span><span class="sxs-lookup"><span data-stu-id="43cfc-129">string</span></span>   | <span data-ttu-id="43cfc-130">Yes</span><span class="sxs-lookup"><span data-stu-id="43cfc-130">Yes</span></span>      | <span data-ttu-id="43cfc-131">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="43cfc-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="43cfc-132">**överförings-ID**</span><span class="sxs-lookup"><span data-stu-id="43cfc-132">**transfer-id**</span></span> | <span data-ttu-id="43cfc-133">sträng</span><span class="sxs-lookup"><span data-stu-id="43cfc-133">string</span></span>   | <span data-ttu-id="43cfc-134">Yes</span><span class="sxs-lookup"><span data-stu-id="43cfc-134">Yes</span></span>      | <span data-ttu-id="43cfc-135">Ett GUID-formaterat överförings-ID som identifierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="43cfc-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="43cfc-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="43cfc-136">Request headers</span></span>

<span data-ttu-id="43cfc-137">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="43cfc-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="43cfc-138">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="43cfc-138">Request body</span></span>

<span data-ttu-id="43cfc-139">I den här tabellen beskrivs egenskaperna för [TransferEntity](transfer-entity-resources.md) i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="43cfc-139">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="43cfc-140">Egenskap</span><span class="sxs-lookup"><span data-stu-id="43cfc-140">Property</span></span>              | <span data-ttu-id="43cfc-141">Typ</span><span class="sxs-lookup"><span data-stu-id="43cfc-141">Type</span></span>          | <span data-ttu-id="43cfc-142">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="43cfc-142">Required</span></span>  | <span data-ttu-id="43cfc-143">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="43cfc-143">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="43cfc-144">id</span><span class="sxs-lookup"><span data-stu-id="43cfc-144">id</span></span>                    | <span data-ttu-id="43cfc-145">sträng</span><span class="sxs-lookup"><span data-stu-id="43cfc-145">string</span></span>        | <span data-ttu-id="43cfc-146">No</span><span class="sxs-lookup"><span data-stu-id="43cfc-146">No</span></span>    | <span data-ttu-id="43cfc-147">En transferEntity-identifierare som anges när transferEntity har skapats.</span><span class="sxs-lookup"><span data-stu-id="43cfc-147">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="43cfc-148">status</span><span class="sxs-lookup"><span data-stu-id="43cfc-148">status</span></span>                | <span data-ttu-id="43cfc-149">sträng</span><span class="sxs-lookup"><span data-stu-id="43cfc-149">string</span></span>        | <span data-ttu-id="43cfc-150">No</span><span class="sxs-lookup"><span data-stu-id="43cfc-150">No</span></span>    | <span data-ttu-id="43cfc-151">Status för transferEntity.</span><span class="sxs-lookup"><span data-stu-id="43cfc-151">The status of the transferEntity.</span></span> <span data-ttu-id="43cfc-152">Om du vill avvisa en överföring ska värdet anges som "avvisa"</span><span class="sxs-lookup"><span data-stu-id="43cfc-152">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="43cfc-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="43cfc-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="43cfc-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="43cfc-154">REST response</span></span>

<span data-ttu-id="43cfc-155">Om det lyckas returnerar den här metoden den ifyllda [TransferEntity](transfer-entity-resources.md) -resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="43cfc-155">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="43cfc-156">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="43cfc-156">Response success and error codes</span></span>

<span data-ttu-id="43cfc-157">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="43cfc-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="43cfc-158">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="43cfc-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="43cfc-159">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="43cfc-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="43cfc-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="43cfc-160">Response example</span></span>

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
