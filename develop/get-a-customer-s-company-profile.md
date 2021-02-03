---
title: Hämta en kunds företagsprofil
description: Hämtar företags profilen för en kund.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c26a86ecb96e5e7942ba179f8a3cc704abab7df5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769372"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="cb339-103">Hämta en kunds företagsprofil</span><span class="sxs-lookup"><span data-stu-id="cb339-103">Get a customer's company profile</span></span>

<span data-ttu-id="cb339-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="cb339-104">**Applies To**</span></span>

- <span data-ttu-id="cb339-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="cb339-105">Partner Center</span></span>
- <span data-ttu-id="cb339-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cb339-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cb339-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="cb339-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cb339-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cb339-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cb339-109">Hämtar företags profilen för en kund.</span><span class="sxs-lookup"><span data-stu-id="cb339-109">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb339-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cb339-110">Prerequisites</span></span>

- <span data-ttu-id="cb339-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cb339-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cb339-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cb339-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cb339-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb339-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cb339-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="cb339-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cb339-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="cb339-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cb339-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="cb339-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cb339-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="cb339-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cb339-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb339-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="cb339-119">C\#</span><span class="sxs-lookup"><span data-stu-id="cb339-119">C\#</span></span>

<span data-ttu-id="cb339-120">Om du vill hämta företags profilen för en kund anropar du metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="cb339-120">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="cb339-121">Hämta sedan kundens [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) -gränssnitt från [**profil**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) egenskapen för att få åtkomst till företagets egenskap.</span><span class="sxs-lookup"><span data-stu-id="cb339-121">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="cb339-122">Sedan hämtar du [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) -gränssnittet från egenskapen [**ICustomerProfileCollection. Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) och anropar metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .</span><span class="sxs-lookup"><span data-stu-id="cb339-122">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="cb339-123">**Exempel**: [Ladda ned SDK för partner Center](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span><span class="sxs-lookup"><span data-stu-id="cb339-123">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="cb339-124">**Projekt**: PartnerSdk. FeatureSamples- **klass**: GetCustomerCompanyProfile.CS</span><span class="sxs-lookup"><span data-stu-id="cb339-124">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="cb339-125">Java</span><span class="sxs-lookup"><span data-stu-id="cb339-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="cb339-126">Om du vill hämta företags profilen för en kund anropar du funktionen **IAggregatePartner. getCustomers (). byId** med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="cb339-126">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="cb339-127">Hämta sedan kundens **ICustomerProfileCollection** -gränssnitt från [**getProfiles**]-funktionen för att få åtkomst till företagets egenskap.</span><span class="sxs-lookup"><span data-stu-id="cb339-127">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="cb339-128">Hämta sedan **ICustomerReadonlyProfile** -gränssnittet från funktionen **ICustomerProfileCollection. getCompany** och anropa funktionen **Get** .</span><span class="sxs-lookup"><span data-stu-id="cb339-128">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="cb339-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cb339-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cb339-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="cb339-130">Request syntax</span></span>

| <span data-ttu-id="cb339-131">Metod</span><span class="sxs-lookup"><span data-stu-id="cb339-131">Method</span></span>  | <span data-ttu-id="cb339-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cb339-132">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="cb339-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="cb339-133">**GET**</span></span> | <span data-ttu-id="cb339-134">*{baseURL}*/v1/Customers/{Customer-Tenant-ID}/Profiles/Company http/1.1</span><span class="sxs-lookup"><span data-stu-id="cb339-134">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cb339-135">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="cb339-135">URI parameter</span></span>

<span data-ttu-id="cb339-136">Använd följande frågeparameter för att hämta företags profilen.</span><span class="sxs-lookup"><span data-stu-id="cb339-136">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="cb339-137">Namn</span><span class="sxs-lookup"><span data-stu-id="cb339-137">Name</span></span>                   | <span data-ttu-id="cb339-138">Typ</span><span class="sxs-lookup"><span data-stu-id="cb339-138">Type</span></span>     | <span data-ttu-id="cb339-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cb339-139">Required</span></span> | <span data-ttu-id="cb339-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cb339-140">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb339-141">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="cb339-141">**customer-tenant-id**</span></span> | <span data-ttu-id="cb339-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="cb339-142">**guid**</span></span> | <span data-ttu-id="cb339-143">Y</span><span class="sxs-lookup"><span data-stu-id="cb339-143">Y</span></span>        | <span data-ttu-id="cb339-144">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="cb339-144">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cb339-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cb339-145">Request headers</span></span>

<span data-ttu-id="cb339-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cb339-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cb339-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cb339-147">Request body</span></span>

<span data-ttu-id="cb339-148">Inget</span><span class="sxs-lookup"><span data-stu-id="cb339-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="cb339-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cb339-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cb339-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cb339-150">REST response</span></span>

<span data-ttu-id="cb339-151">Om det lyckas returnerar den här metoden information i svars texten.</span><span class="sxs-lookup"><span data-stu-id="cb339-151">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cb339-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cb339-152">Response success and error codes</span></span>

<span data-ttu-id="cb339-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="cb339-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cb339-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cb339-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cb339-155">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cb339-155">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cb339-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cb339-156">Response example</span></span>

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
