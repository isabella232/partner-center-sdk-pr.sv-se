---
title: Acceptera en överföring av prenumerationer
description: Lär dig hur du använder Partnercenter REST API för att acceptera en överföring av prenumerationer för en kund. Innehåller syntax för REST-begäran, rubriker och REST-svar.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 762f2106d6173e352bec11936c96bc3a9c9f89cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025759"
---
# <a name="accept-a-transfer-of-subscriptions-for-a-customer-using-partner-center-rest-apis"></a><span data-ttu-id="37909-104">Acceptera en överföring av prenumerationer för en kund med hjälp av Partner Center REST API:er</span><span class="sxs-lookup"><span data-stu-id="37909-104">Accept a transfer of subscriptions for a customer using Partner Center REST APIs</span></span>

<span data-ttu-id="37909-105">Den här artikeln beskriver hur du använder REST API i Partnercenter för att acceptera överföringen av prenumerationer för en kund.</span><span class="sxs-lookup"><span data-stu-id="37909-105">This article covers how to use the REST API in Partner Center to accept the transfer of subscriptions for a customer.</span></span> <span data-ttu-id="37909-106">Exemplet innehåller REST-syntax, rubriker och REST-svar.</span><span class="sxs-lookup"><span data-stu-id="37909-106">The example includes REST syntax, headers, and REST responses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37909-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="37909-107">Prerequisites</span></span>

- <span data-ttu-id="37909-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="37909-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="37909-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="37909-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="37909-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="37909-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="37909-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="37909-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="37909-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="37909-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="37909-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="37909-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="37909-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="37909-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="37909-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="37909-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="37909-116">En överföringsidentifierare för en befintlig överföring.</span><span class="sxs-lookup"><span data-stu-id="37909-116">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="37909-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="37909-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="37909-118">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="37909-118">Request syntax</span></span>

| <span data-ttu-id="37909-119">Metod</span><span class="sxs-lookup"><span data-stu-id="37909-119">Method</span></span>   | <span data-ttu-id="37909-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="37909-120">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="37909-121">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="37909-121">**POST**</span></span> | <span data-ttu-id="37909-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id}/accept HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="37909-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id}/accept HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="37909-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="37909-123">URI parameter</span></span>

<span data-ttu-id="37909-124">Använd följande sökvägsparameter för att identifiera kunden och ange vilken överföring som ska godkännas.</span><span class="sxs-lookup"><span data-stu-id="37909-124">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="37909-125">Namn</span><span class="sxs-lookup"><span data-stu-id="37909-125">Name</span></span>            | <span data-ttu-id="37909-126">Typ</span><span class="sxs-lookup"><span data-stu-id="37909-126">Type</span></span>     | <span data-ttu-id="37909-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="37909-127">Required</span></span> | <span data-ttu-id="37909-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="37909-128">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="37909-129">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="37909-129">**customer-id**</span></span> | <span data-ttu-id="37909-130">sträng</span><span class="sxs-lookup"><span data-stu-id="37909-130">string</span></span>   | <span data-ttu-id="37909-131">Ja</span><span class="sxs-lookup"><span data-stu-id="37909-131">Yes</span></span>      | <span data-ttu-id="37909-132">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="37909-132">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="37909-133">**transfer-id**</span><span class="sxs-lookup"><span data-stu-id="37909-133">**transfer-id**</span></span> | <span data-ttu-id="37909-134">sträng</span><span class="sxs-lookup"><span data-stu-id="37909-134">string</span></span>   | <span data-ttu-id="37909-135">Ja</span><span class="sxs-lookup"><span data-stu-id="37909-135">Yes</span></span>      | <span data-ttu-id="37909-136">Ett GUID-formaterat överförings-ID som identifierar överföringen.</span><span class="sxs-lookup"><span data-stu-id="37909-136">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="37909-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="37909-137">Request headers</span></span>

<span data-ttu-id="37909-138">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="37909-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="37909-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="37909-139">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/aa2bddb6-9cc8-4949-80fe-a37d5e0a13ba/accept HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0

```

## <a name="rest-response"></a><span data-ttu-id="37909-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="37909-140">REST response</span></span>

<span data-ttu-id="37909-141">Om det lyckas returnerar den här metoden den [ifyllda TransferSubmitResult-resursen](transfer-entity-resources.md#transfersubmitresult) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="37909-141">If successful, this method returns the populated [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="37909-142">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="37909-142">Response success and error codes</span></span>

<span data-ttu-id="37909-143">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="37909-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="37909-144">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="37909-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="37909-145">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="37909-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="37909-146">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="37909-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3389
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Date: Wed, 25 Mar 2020 19:13:06 GMT

{
  "orders": [
    {
      "id": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "alternateId": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "5344C201-3099-44E5-B333-C3EB0401EDE0",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Customer Engagement Plan (36 mo)",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:23.183+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6IjIxYjkyMzkzLWZmY2UtNGJjNy04N2M1LTYyY2ZhODk3ZDhmOSIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    },
    {
      "id": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "alternateId": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "1A90EE13-2CB4-4785-BB0F-542813F00A37",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Business Central Essential",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:34.59+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6Ijc0MTRiOGVhLWMxNjctNGNjNC1iYzhlLWI0M2VmYzE3N2E0NiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    }
  ],
  "transferErrors": [
    {
      "transferGroupId": "1",
      "lineItems": [
        {
          "id": 1,
          "subscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "entitlementId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "offerId": "A4179D30-CC09-49F0-977E-DC2CB70B874F",
          "friendlyName": "Project Online Essentials",
          "quantity": 1,
          "transferGroupId": "1",
          "addonItems": [ ],
          "partnerIdOnRecord": "5139005",
          "billingCycle": "annual",
          "sourceSubscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A"
        }
      ],
      "code": 900103,
      "description": "Subscription SyncState must be SyncComplete for the Subscription to be a source in a Subscription Ownership Transfer. Subscription: 637ff8f6-d842-4573-8da8-89765356cd1a, current state: None",
      "attributes": {
        "objectType": "TransferError"
      }
    }
  ],
  "attributes": {
    "objectType": "TransferSubmitResult"
  }
}
```
