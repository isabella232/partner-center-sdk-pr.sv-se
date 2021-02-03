---
title: Skapa användarkonton för en kund
description: Skapa ett nytt användar konto för din kund.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9131a1c4c37d07b1994b67379ec8361fda13a371
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768808"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="554b2-103">Skapa användarkonton för en kund</span><span class="sxs-lookup"><span data-stu-id="554b2-103">Create user accounts for a customer</span></span>

<span data-ttu-id="554b2-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="554b2-104">**Applies to:**</span></span>

- <span data-ttu-id="554b2-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="554b2-105">Partner Center</span></span>

<span data-ttu-id="554b2-106">Skapa ett nytt användar konto för din kund.</span><span class="sxs-lookup"><span data-stu-id="554b2-106">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="554b2-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="554b2-107">Prerequisites</span></span>

- <span data-ttu-id="554b2-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="554b2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="554b2-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="554b2-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="554b2-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="554b2-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="554b2-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="554b2-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="554b2-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="554b2-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="554b2-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="554b2-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="554b2-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="554b2-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="554b2-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="554b2-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="554b2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="554b2-116">C\#</span></span>

<span data-ttu-id="554b2-117">Så här hämtar du ett nytt användar konto för en kund:</span><span class="sxs-lookup"><span data-stu-id="554b2-117">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="554b2-118">Skapa ett nytt **CustomerUser** -objekt med relevant användar information.</span><span class="sxs-lookup"><span data-stu-id="554b2-118">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="554b2-119">Använd din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="554b2-119">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="554b2-120">Anropa egenskapen **Users** följt av **create** -metoden.</span><span class="sxs-lookup"><span data-stu-id="554b2-120">Call the **Users** property, followed by the **Create** method.</span></span>

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

<span data-ttu-id="554b2-121">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="554b2-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="554b2-122">**Projekt**: PartnerSDK. FeatureSamples- **klass**: CustomerUserCreate.CS</span><span class="sxs-lookup"><span data-stu-id="554b2-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="554b2-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="554b2-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="554b2-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="554b2-124">Request syntax</span></span>

| <span data-ttu-id="554b2-125">Metod</span><span class="sxs-lookup"><span data-stu-id="554b2-125">Method</span></span>   | <span data-ttu-id="554b2-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="554b2-126">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="554b2-127">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="554b2-127">**POST**</span></span> | <span data-ttu-id="554b2-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="554b2-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="554b2-129">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="554b2-129">URI parameters</span></span>

<span data-ttu-id="554b2-130">Använd följande frågeparametrar för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="554b2-130">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="554b2-131">Namn</span><span class="sxs-lookup"><span data-stu-id="554b2-131">Name</span></span> | <span data-ttu-id="554b2-132">Typ</span><span class="sxs-lookup"><span data-stu-id="554b2-132">Type</span></span> | <span data-ttu-id="554b2-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="554b2-133">Required</span></span> | <span data-ttu-id="554b2-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="554b2-134">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="554b2-135">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="554b2-135">**customer-tenant-id**</span></span> | <span data-ttu-id="554b2-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="554b2-136">**guid**</span></span> | <span data-ttu-id="554b2-137">Y</span><span class="sxs-lookup"><span data-stu-id="554b2-137">Y</span></span> | <span data-ttu-id="554b2-138">Värdet är ett GUID-formaterat **kund-Tenant-ID**. Den gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="554b2-138">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="554b2-139">**användar-ID**</span><span class="sxs-lookup"><span data-stu-id="554b2-139">**user-id**</span></span> | <span data-ttu-id="554b2-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="554b2-140">**guid**</span></span> | <span data-ttu-id="554b2-141">N</span><span class="sxs-lookup"><span data-stu-id="554b2-141">N</span></span> | <span data-ttu-id="554b2-142">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.</span><span class="sxs-lookup"><span data-stu-id="554b2-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="554b2-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="554b2-143">Request headers</span></span>

<span data-ttu-id="554b2-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="554b2-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="554b2-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="554b2-145">Request body</span></span>

<span data-ttu-id="554b2-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="554b2-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="554b2-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="554b2-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="554b2-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="554b2-148">REST response</span></span>

<span data-ttu-id="554b2-149">Om det lyckas returnerar den här metoden ett användar konto, inklusive GUID.</span><span class="sxs-lookup"><span data-stu-id="554b2-149">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="554b2-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="554b2-150">Response success and error codes</span></span>

<span data-ttu-id="554b2-151">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="554b2-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="554b2-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="554b2-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="554b2-153">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="554b2-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="554b2-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="554b2-154">Response example</span></span>

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