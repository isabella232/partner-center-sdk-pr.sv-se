---
title: Hämta en kunds företagsprofil
description: Hämtar företagsprofilen för en kund.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: a1c0c8401207f4b0bb33755a8eabc66de0ad9ff9
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874983"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="9522b-103">Hämta en kunds företagsprofil</span><span class="sxs-lookup"><span data-stu-id="9522b-103">Get a customer's company profile</span></span>

<span data-ttu-id="9522b-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9522b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9522b-105">Hämtar företagsprofilen för en kund.</span><span class="sxs-lookup"><span data-stu-id="9522b-105">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9522b-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9522b-106">Prerequisites</span></span>

- <span data-ttu-id="9522b-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9522b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9522b-108">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="9522b-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9522b-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9522b-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9522b-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="9522b-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9522b-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="9522b-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9522b-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="9522b-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9522b-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="9522b-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9522b-114">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9522b-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9522b-115">C\#</span><span class="sxs-lookup"><span data-stu-id="9522b-115">C\#</span></span>

<span data-ttu-id="9522b-116">Om du vill hämta företagsprofilen för en kund anropar du [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="9522b-116">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="9522b-117">Hämta sedan kundens [**ICustomerProfileCollection-gränssnitt**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) från egenskapen [**Profiler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) för att få åtkomst till dess företagsegenskap.</span><span class="sxs-lookup"><span data-stu-id="9522b-117">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="9522b-118">Hämta sedan [**gränssnittet ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) från egenskapen [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) och anropa dess [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) eller [**GetAsync()-metoder.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)</span><span class="sxs-lookup"><span data-stu-id="9522b-118">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="9522b-119">**Exempel:** [Ladda ned Partnercenter-SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span><span class="sxs-lookup"><span data-stu-id="9522b-119">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="9522b-120">**Project:** PartnerSdk.FeatureSamples-klass: GetCustomerCompanyProfile.cs </span><span class="sxs-lookup"><span data-stu-id="9522b-120">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="9522b-121">Java</span><span class="sxs-lookup"><span data-stu-id="9522b-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="9522b-122">Om du vill hämta företagsprofilen för en kund anropar du funktionen **IAggregatePartner.getCustomers().byId** med kundidentifieraren för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="9522b-122">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="9522b-123">Hämta sedan kundens **ICustomerProfileCollection-gränssnitt** från funktionen [**getProfiles**] för att få åtkomst till dess företagsegenskap.</span><span class="sxs-lookup"><span data-stu-id="9522b-123">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="9522b-124">Hämta sedan **gränssnittet ICustomerReadonlyProfile** från funktionen **ICustomerProfileCollection.getCompany** och anropa **get-funktionen.**</span><span class="sxs-lookup"><span data-stu-id="9522b-124">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="9522b-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9522b-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9522b-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="9522b-126">Request syntax</span></span>

| <span data-ttu-id="9522b-127">Metod</span><span class="sxs-lookup"><span data-stu-id="9522b-127">Method</span></span>  | <span data-ttu-id="9522b-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9522b-128">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="9522b-129">**Få**</span><span class="sxs-lookup"><span data-stu-id="9522b-129">**GET**</span></span> | <span data-ttu-id="9522b-130">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9522b-130">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9522b-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="9522b-131">URI parameter</span></span>

<span data-ttu-id="9522b-132">Använd följande frågeparameter för att hämta företagsprofilen.</span><span class="sxs-lookup"><span data-stu-id="9522b-132">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="9522b-133">Namn</span><span class="sxs-lookup"><span data-stu-id="9522b-133">Name</span></span>                   | <span data-ttu-id="9522b-134">Typ</span><span class="sxs-lookup"><span data-stu-id="9522b-134">Type</span></span>     | <span data-ttu-id="9522b-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="9522b-135">Required</span></span> | <span data-ttu-id="9522b-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="9522b-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9522b-137">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="9522b-137">**customer-tenant-id**</span></span> | <span data-ttu-id="9522b-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="9522b-138">**guid**</span></span> | <span data-ttu-id="9522b-139">Y</span><span class="sxs-lookup"><span data-stu-id="9522b-139">Y</span></span>        | <span data-ttu-id="9522b-140">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="9522b-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9522b-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="9522b-141">Request headers</span></span>

<span data-ttu-id="9522b-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9522b-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9522b-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9522b-143">Request body</span></span>

<span data-ttu-id="9522b-144">Ingen</span><span class="sxs-lookup"><span data-stu-id="9522b-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="9522b-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9522b-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9522b-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9522b-146">REST response</span></span>

<span data-ttu-id="9522b-147">Om det lyckas returnerar den här metoden information i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="9522b-147">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9522b-148">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9522b-148">Response success and error codes</span></span>

<span data-ttu-id="9522b-149">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="9522b-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9522b-150">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9522b-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9522b-151">En fullständig lista finns i [Felkoder för Partner Center REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9522b-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9522b-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9522b-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```
