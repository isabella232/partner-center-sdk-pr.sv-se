---
title: Skapa användarkonton för en kund
description: Skapa ett nytt användarkonto för kunden.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d086d7ba72c9d9e42dc88684ddeafc9a597bfd7c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973391"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="b615b-103">Skapa användarkonton för en kund</span><span class="sxs-lookup"><span data-stu-id="b615b-103">Create user accounts for a customer</span></span>

<span data-ttu-id="b615b-104">Skapa ett nytt användarkonto för kunden.</span><span class="sxs-lookup"><span data-stu-id="b615b-104">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b615b-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b615b-105">Prerequisites</span></span>

- <span data-ttu-id="b615b-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b615b-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b615b-107">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b615b-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b615b-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b615b-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b615b-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b615b-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b615b-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="b615b-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b615b-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="b615b-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b615b-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="b615b-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b615b-113">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b615b-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b615b-114">C\#</span><span class="sxs-lookup"><span data-stu-id="b615b-114">C\#</span></span>

<span data-ttu-id="b615b-115">Så här skaffar du ett nytt användarkonto för en kund:</span><span class="sxs-lookup"><span data-stu-id="b615b-115">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="b615b-116">Skapa ett nytt **CustomerUser-objekt** med relevant användarinformation.</span><span class="sxs-lookup"><span data-stu-id="b615b-116">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="b615b-117">Använd din **IAggregatePartner.Customers-samling** och anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="b615b-117">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="b615b-118">Anropa egenskapen **Användare** följt av **metoden** Skapa.</span><span class="sxs-lookup"><span data-stu-id="b615b-118">Call the **Users** property, followed by the **Create** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// var SelectedCustomer;

var userToCreate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "Password!1" },
    DisplayName = "TestDisplayName",
    FirstName = "TestFirstName",
    LastName = "TestLastName",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

User createdUser = partnerOperations.Customers.ById(selectedCustomerId).Users.Create(userToCreate);
```

<span data-ttu-id="b615b-119">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b615b-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b615b-120">**Project:** PartnerSDK.FeatureSamples-klass: CustomerUserCreate.cs </span><span class="sxs-lookup"><span data-stu-id="b615b-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b615b-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b615b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b615b-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b615b-122">Request syntax</span></span>

| <span data-ttu-id="b615b-123">Metod</span><span class="sxs-lookup"><span data-stu-id="b615b-123">Method</span></span>   | <span data-ttu-id="b615b-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b615b-124">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="b615b-125">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="b615b-125">**POST**</span></span> | <span data-ttu-id="b615b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b615b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b615b-127">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b615b-127">URI parameters</span></span>

<span data-ttu-id="b615b-128">Använd följande frågeparametrar för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="b615b-128">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="b615b-129">Namn</span><span class="sxs-lookup"><span data-stu-id="b615b-129">Name</span></span> | <span data-ttu-id="b615b-130">Typ</span><span class="sxs-lookup"><span data-stu-id="b615b-130">Type</span></span> | <span data-ttu-id="b615b-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b615b-131">Required</span></span> | <span data-ttu-id="b615b-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b615b-132">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="b615b-133">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="b615b-133">**customer-tenant-id**</span></span> | <span data-ttu-id="b615b-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="b615b-134">**guid**</span></span> | <span data-ttu-id="b615b-135">Y</span><span class="sxs-lookup"><span data-stu-id="b615b-135">Y</span></span> | <span data-ttu-id="b615b-136">Värdet är ett GUID-formaterat **kundklient-id.** Det gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="b615b-136">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b615b-137">**användar-id**</span><span class="sxs-lookup"><span data-stu-id="b615b-137">**user-id**</span></span> | <span data-ttu-id="b615b-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="b615b-138">**guid**</span></span> | <span data-ttu-id="b615b-139">N</span><span class="sxs-lookup"><span data-stu-id="b615b-139">N</span></span> | <span data-ttu-id="b615b-140">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.</span><span class="sxs-lookup"><span data-stu-id="b615b-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b615b-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b615b-141">Request headers</span></span>

<span data-ttu-id="b615b-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b615b-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b615b-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b615b-143">Request body</span></span>

<span data-ttu-id="b615b-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="b615b-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b615b-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b615b-145">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "country/region code",
      "userPrincipalName": "userid@domain.onmicrosoft.com",
      "firstName": "First",
      "lastName": "Last",
      "displayName": "User name",
      "immutableId": "Some unique ID",
      "passwordProfile":{
                 password: "abCD123*",
                 forceChangePassword: true
      },
      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="b615b-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b615b-146">REST response</span></span>

<span data-ttu-id="b615b-147">Om det lyckas returnerar den här metoden ett användarkonto, inklusive GUID.</span><span class="sxs-lookup"><span data-stu-id="b615b-147">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b615b-148">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b615b-148">Response success and error codes</span></span>

<span data-ttu-id="b615b-149">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b615b-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b615b-150">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b615b-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b615b-151">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b615b-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b615b-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b615b-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
  "usageLocation": "country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "userid@domain.onmicrosoft.com",
  "firstName": "First",
  "lastName": "Last",
  "displayName": "User name",
  "immutableId": "Some unique ID",
  "passwordProfile": {
    "forceChangePassword": true,
    "password": "abCD123*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```