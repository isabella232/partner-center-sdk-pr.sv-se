---
title: Hämta en kund efter ID
description: Hämtar en kund resurs som motsvarar ett kund-ID.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: dd4301dbb6f749b675fe624daf7f63751806f856
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769378"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="f8489-103">Hämta en kund efter ID</span><span class="sxs-lookup"><span data-stu-id="f8489-103">Get a customer by ID</span></span>

<span data-ttu-id="f8489-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="f8489-104">**Applies To**</span></span>

- <span data-ttu-id="f8489-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="f8489-105">Partner Center</span></span>
- <span data-ttu-id="f8489-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="f8489-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f8489-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="f8489-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f8489-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f8489-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f8489-109">Hämtar en **kund** resurs som motsvarar ett kund-ID.</span><span class="sxs-lookup"><span data-stu-id="f8489-109">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8489-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f8489-110">Prerequisites</span></span>

- <span data-ttu-id="f8489-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f8489-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f8489-112">Det här scenariot stöder app + användarautentiseringsuppgifter eller endast app-autentisering.</span><span class="sxs-lookup"><span data-stu-id="f8489-112">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="f8489-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f8489-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f8489-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="f8489-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f8489-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="f8489-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f8489-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="f8489-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f8489-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="f8489-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f8489-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f8489-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f8489-119">C\#</span><span class="sxs-lookup"><span data-stu-id="f8489-119">C\#</span></span>

<span data-ttu-id="f8489-120">För att få en kund utifrån ID använder du din [**IAggregatePartner.**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling, anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) och anropar metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) .</span><span class="sxs-lookup"><span data-stu-id="f8489-120">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="f8489-121">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f8489-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f8489-122">**Projekt**: PartnerSDK. FeatureSamples- **klass**: CustomerInformation.CS</span><span class="sxs-lookup"><span data-stu-id="f8489-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="f8489-123">Java</span><span class="sxs-lookup"><span data-stu-id="f8489-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f8489-124">Om du vill hämta en kund med ID använder du din **IAggregatePartner. getCustomers** -funktion, anropar funktionen **byId ()** och anropar funktionen **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="f8489-124">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="f8489-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8489-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f8489-126">Om du vill hämta en kund efter ID kör du kommandot [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) och anger parametern **CustomerId** .</span><span class="sxs-lookup"><span data-stu-id="f8489-126">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="f8489-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f8489-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f8489-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="f8489-128">Request syntax</span></span>

| <span data-ttu-id="f8489-129">Metod</span><span class="sxs-lookup"><span data-stu-id="f8489-129">Method</span></span>  | <span data-ttu-id="f8489-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f8489-130">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="f8489-131">**TA**</span><span class="sxs-lookup"><span data-stu-id="f8489-131">**GET**</span></span> | <span data-ttu-id="f8489-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f8489-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f8489-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="f8489-133">URI parameter</span></span>

<span data-ttu-id="f8489-134">Använd följande frågeparameter för en specifik kund.</span><span class="sxs-lookup"><span data-stu-id="f8489-134">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="f8489-135">Namn</span><span class="sxs-lookup"><span data-stu-id="f8489-135">Name</span></span>                   | <span data-ttu-id="f8489-136">Typ</span><span class="sxs-lookup"><span data-stu-id="f8489-136">Type</span></span>     | <span data-ttu-id="f8489-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="f8489-137">Required</span></span> | <span data-ttu-id="f8489-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="f8489-138">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f8489-139">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="f8489-139">**customer-tenant-id**</span></span> | <span data-ttu-id="f8489-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="f8489-140">**guid**</span></span> | <span data-ttu-id="f8489-141">Y</span><span class="sxs-lookup"><span data-stu-id="f8489-141">Y</span></span>        | <span data-ttu-id="f8489-142">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="f8489-142">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f8489-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f8489-143">Request headers</span></span>

<span data-ttu-id="f8489-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f8489-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f8489-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f8489-145">Request body</span></span>

<span data-ttu-id="f8489-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="f8489-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f8489-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f8489-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="f8489-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f8489-148">REST response</span></span>

<span data-ttu-id="f8489-149">Om det lyckas returnerar den här metoden en [kund](customer-resources.md#customer) resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="f8489-149">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f8489-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f8489-150">Response success and error codes</span></span>

<span data-ttu-id="f8489-151">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="f8489-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f8489-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f8489-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f8489-153">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f8489-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f8489-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f8489-154">Response example</span></span>

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
