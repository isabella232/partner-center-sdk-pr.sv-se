---
title: Återställ användarlösenord för en kund
description: Att återställa ett lösen ord är mycket likt att uppdatera annan information i ett befintligt användar konto för din kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e0df93c2db55ec0fe49fc0e3089b7e11928f32bb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768874"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="2e86b-103">Återställ användarlösenord för en kund</span><span class="sxs-lookup"><span data-stu-id="2e86b-103">Reset user password for a customer</span></span>

<span data-ttu-id="2e86b-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="2e86b-104">**Applies To**</span></span>

- <span data-ttu-id="2e86b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2e86b-105">Partner Center</span></span>

<span data-ttu-id="2e86b-106">Att återställa ett lösen ord är mycket likt att uppdatera annan information i ett befintligt användar konto för din kund.</span><span class="sxs-lookup"><span data-stu-id="2e86b-106">Resetting a password is very similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e86b-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2e86b-107">Prerequisites</span></span>

- <span data-ttu-id="2e86b-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2e86b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e86b-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2e86b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2e86b-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e86b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2e86b-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2e86b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2e86b-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2e86b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2e86b-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2e86b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2e86b-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2e86b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2e86b-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e86b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2e86b-116">C\#</span><span class="sxs-lookup"><span data-stu-id="2e86b-116">C\#</span></span>

<span data-ttu-id="2e86b-117">Om du vill återställa ett lösen ord för en angiven kund användare hämtar du först det angivna kund-ID: t och mål användaren.</span><span class="sxs-lookup"><span data-stu-id="2e86b-117">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="2e86b-118">Skapa sedan ett nytt **CustomerUser** -objekt som innehåller informationen för den befintliga kunden, men med ett nytt **PasswordProfile** -objekt.</span><span class="sxs-lookup"><span data-stu-id="2e86b-118">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="2e86b-119">Använd sedan din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="2e86b-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="2e86b-120">Anropa sedan egenskapen **användare** , metoden **ById ()** och sedan **korrigerings** metoden.</span><span class="sxs-lookup"><span data-stu-id="2e86b-120">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// CustomerUser specifiedUser;

var selectedCustomer = partnerOperations.Customers.ById(selectedCustomerId).Get();
var userToUpdate = new CustomerUser()
   {
      PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "newPassword" },
      DisplayName = "Roger Federer",
      FirstName = "Roger",
      LastName = "Federer",
      UsageLocation = "US",
      UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
   };

// update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="2e86b-121">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2e86b-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2e86b-122">**Projekt**: PartnerSDK. FeatureSamples- **klass**: CustomerUserUpdate.CS</span><span class="sxs-lookup"><span data-stu-id="2e86b-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2e86b-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2e86b-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e86b-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2e86b-124">Request syntax</span></span>

| <span data-ttu-id="2e86b-125">Metod</span><span class="sxs-lookup"><span data-stu-id="2e86b-125">Method</span></span>    | <span data-ttu-id="2e86b-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2e86b-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e86b-127">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="2e86b-127">**PATCH**</span></span> | <span data-ttu-id="2e86b-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="2e86b-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2e86b-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2e86b-129">URI parameter</span></span>

<span data-ttu-id="2e86b-130">Använd följande frågeparameter för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="2e86b-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="2e86b-131">Namn</span><span class="sxs-lookup"><span data-stu-id="2e86b-131">Name</span></span>                   | <span data-ttu-id="2e86b-132">Typ</span><span class="sxs-lookup"><span data-stu-id="2e86b-132">Type</span></span>     | <span data-ttu-id="2e86b-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2e86b-133">Required</span></span> | <span data-ttu-id="2e86b-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2e86b-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e86b-135">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="2e86b-135">**customer-tenant-id**</span></span> | <span data-ttu-id="2e86b-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="2e86b-136">**guid**</span></span> | <span data-ttu-id="2e86b-137">Y</span><span class="sxs-lookup"><span data-stu-id="2e86b-137">Y</span></span>        | <span data-ttu-id="2e86b-138">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="2e86b-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="2e86b-139">**användar-ID**</span><span class="sxs-lookup"><span data-stu-id="2e86b-139">**user-id**</span></span>            | <span data-ttu-id="2e86b-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="2e86b-140">**guid**</span></span> | <span data-ttu-id="2e86b-141">Y</span><span class="sxs-lookup"><span data-stu-id="2e86b-141">Y</span></span>        | <span data-ttu-id="2e86b-142">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.</span><span class="sxs-lookup"><span data-stu-id="2e86b-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="2e86b-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2e86b-143">Request headers</span></span>

<span data-ttu-id="2e86b-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2e86b-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2e86b-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2e86b-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="2e86b-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2e86b-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
     "passwordProfile":{
        password: "Renew456*",
        forceChangePassword: true
      },

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="2e86b-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2e86b-147">REST response</span></span>

<span data-ttu-id="2e86b-148">Om det lyckas returnerar den här metoden användar informationen, tillsammans med den uppdaterade lösen ords informationen.</span><span class="sxs-lookup"><span data-stu-id="2e86b-148">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e86b-149">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2e86b-149">Response success and error codes</span></span>

<span data-ttu-id="2e86b-150">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2e86b-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2e86b-151">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2e86b-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e86b-152">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2e86b-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2e86b-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2e86b-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "AX",
  "id": "95794928-9abe-4548-8b43-50ffc20b9404",
  "userPrincipalName": "aaaa4@abcdefgh1234.ccsctp.net",
  "firstName": "aaaa4",
  "lastName": "aaaa4",
  "displayName": "aaaa4",
  "passwordProfile": {
    "forceChangePassword": false,
    "password": "Renew456*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/95794928-9abe-4548-8b43-50ffc20b9404",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
