---
title: Hämta en kund efter ID
description: Hämtar en kundresurs som motsvarar ett kund-ID.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 196d653c789c4b4e1327f0c6e5d2531a18681a71
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111875000"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="fac31-103">Hämta en kund efter ID</span><span class="sxs-lookup"><span data-stu-id="fac31-103">Get a customer by ID</span></span>

<span data-ttu-id="fac31-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fac31-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fac31-105">Hämtar en **kundresurs** som motsvarar ett kund-ID.</span><span class="sxs-lookup"><span data-stu-id="fac31-105">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fac31-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="fac31-106">Prerequisites</span></span>

- <span data-ttu-id="fac31-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fac31-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fac31-108">Det här scenariot stöder autentiseringsuppgifter för app+användare eller appbaserad autentisering.</span><span class="sxs-lookup"><span data-stu-id="fac31-108">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="fac31-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fac31-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fac31-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fac31-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fac31-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="fac31-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fac31-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="fac31-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fac31-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="fac31-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fac31-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fac31-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="fac31-115">C\#</span><span class="sxs-lookup"><span data-stu-id="fac31-115">C\#</span></span>

<span data-ttu-id="fac31-116">Om du vill hämta en kund via ID använder du [**samlingen IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) anropar [**metoden ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) och anropar sedan [**metoderna Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) [**eller GetAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync)</span><span class="sxs-lookup"><span data-stu-id="fac31-116">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="fac31-117">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fac31-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fac31-118">**Project:** PartnerSDK.FeatureSamples-klass: CustomerInformation.cs </span><span class="sxs-lookup"><span data-stu-id="fac31-118">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="fac31-119">Java</span><span class="sxs-lookup"><span data-stu-id="fac31-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="fac31-120">Om du vill hämta en kund via ID använder du funktionen **IAggregatePartner.getCustomers,** anropar **funktionen byId()** och anropar **sedan funktionen get().**</span><span class="sxs-lookup"><span data-stu-id="fac31-120">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="fac31-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fac31-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="fac31-122">Om du vill hämta en kund efter ID kör du [**kommandot Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) och anger **parametern CustomerId.**</span><span class="sxs-lookup"><span data-stu-id="fac31-122">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="fac31-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="fac31-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fac31-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="fac31-124">Request syntax</span></span>

| <span data-ttu-id="fac31-125">Metod</span><span class="sxs-lookup"><span data-stu-id="fac31-125">Method</span></span>  | <span data-ttu-id="fac31-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="fac31-126">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="fac31-127">**Få**</span><span class="sxs-lookup"><span data-stu-id="fac31-127">**GET**</span></span> | <span data-ttu-id="fac31-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fac31-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fac31-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="fac31-129">URI parameter</span></span>

<span data-ttu-id="fac31-130">Använd följande frågeparameter för en specifik kund.</span><span class="sxs-lookup"><span data-stu-id="fac31-130">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="fac31-131">Namn</span><span class="sxs-lookup"><span data-stu-id="fac31-131">Name</span></span>                   | <span data-ttu-id="fac31-132">Typ</span><span class="sxs-lookup"><span data-stu-id="fac31-132">Type</span></span>     | <span data-ttu-id="fac31-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="fac31-133">Required</span></span> | <span data-ttu-id="fac31-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="fac31-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fac31-135">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="fac31-135">**customer-tenant-id**</span></span> | <span data-ttu-id="fac31-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="fac31-136">**guid**</span></span> | <span data-ttu-id="fac31-137">Y</span><span class="sxs-lookup"><span data-stu-id="fac31-137">Y</span></span>        | <span data-ttu-id="fac31-138">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="fac31-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fac31-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="fac31-139">Request headers</span></span>

<span data-ttu-id="fac31-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fac31-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fac31-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="fac31-141">Request body</span></span>

<span data-ttu-id="fac31-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="fac31-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fac31-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="fac31-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="fac31-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="fac31-144">REST response</span></span>

<span data-ttu-id="fac31-145">Om det lyckas returnerar den här metoden [en kundresurs](customer-resources.md#customer) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="fac31-145">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fac31-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="fac31-146">Response success and error codes</span></span>

<span data-ttu-id="fac31-147">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="fac31-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fac31-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="fac31-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fac31-149">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fac31-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fac31-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="fac31-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1530
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b

{
  "id": "eebd1b55-5360-4438-a11d-5c06918c3014",
  "commerceId": "99e6a635-48e7-424d-9059-c9db944e3c54",
  "companyProfile": {
    "tenantId": "eebd1b55-5360-4438-a11d-5c06918c3014",
    "domain": "abcdefgh1234.ccsctp.net",
    "companyName": "1kl as kjk",
    "address": {
      "country": "US",
      "region": "wa",
      "city": "redmond",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "phoneNumber": "1234567890"
    },
    "email": "a@a.com",
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/company",
        "method": "GET",
        "headers": []
      }
    },
    "attributes": {
      "objectType": "CustomerCompanyProfile"
    }
  },
  "billingProfile": {
    "id": "eeada110-69d6-4cc9-b093-75feb7ca9d3f",
    "firstName": "d0d89d776d03471c819bf772191ed728",
    "lastName": "kjkAJJAAAAAAAAAAAAAAAAAAAA",
    "email": "a@a.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "1kl as kjkAAAAAAAAAAAAAAAJJJJJJJJJJJAAAAAJJJJJJJJJJJAAJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJAJJJJJAJJAAAAJAJJAAAAAAAAAAAAAAAAAAAA",
    "defaultAddress": {
      "country": "US",
      "city": "redmond",
      "state": "WA",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "firstName": "1kl as",
      "lastName": "kjk",
      "phoneNumber": "1234567890"
    },
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/billing",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "etag": "-4242348048554929329",
      "objectType": "CustomerBillingProfile"
    }
  },
  "relationshipToPartner": "reseller",
  "allowDelegatedAccess": true,
  "customDomains": [
    "abcdefgh1234.ccsctp.net"
  ],
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Customer"
  }
}
```
