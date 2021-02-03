---
title: Uppdatera användarkonton för en kund
description: Uppdatera information i ett befintligt användar konto för din kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 52a43341bf2c3ba64d8c232af01f3fbae6765d82
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769183"
---
# <a name="update-user-accounts-for-a-customer"></a><span data-ttu-id="3f955-103">Uppdatera användarkonton för en kund</span><span class="sxs-lookup"><span data-stu-id="3f955-103">Update user accounts for a customer</span></span>

<span data-ttu-id="3f955-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="3f955-104">**Applies To**</span></span>

- <span data-ttu-id="3f955-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="3f955-105">Partner Center</span></span>

<span data-ttu-id="3f955-106">Uppdatera information i ett befintligt användar konto för din kund.</span><span class="sxs-lookup"><span data-stu-id="3f955-106">Update details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f955-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3f955-107">Prerequisites</span></span>

- <span data-ttu-id="3f955-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3f955-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3f955-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3f955-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3f955-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3f955-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3f955-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="3f955-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3f955-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="3f955-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3f955-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="3f955-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3f955-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="3f955-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3f955-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3f955-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="3f955-116">C\#</span><span class="sxs-lookup"><span data-stu-id="3f955-116">C\#</span></span>

<span data-ttu-id="3f955-117">Om du vill uppdatera informationen för en angiven kund användare hämtar du först angivet kund-ID och användare för att uppdatera.</span><span class="sxs-lookup"><span data-stu-id="3f955-117">To update the details for a specified customer user, first retrieve the specified customer ID and user to update.</span></span> <span data-ttu-id="3f955-118">Skapa sedan en uppdaterad version av användaren i ett nytt **CustomerUser** -objekt.</span><span class="sxs-lookup"><span data-stu-id="3f955-118">Then, create an updated version of the user in a new **CustomerUser** object.</span></span> <span data-ttu-id="3f955-119">Använd sedan din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="3f955-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="3f955-120">Anropa sedan egenskapen **användare** , metoden **ById ()** , följt av metoden **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="3f955-120">Then call the **Users** property, the **ById()** method, followed by the **Patch()** method.</span></span>

``` csharp
// string selectedCustomerId;
// customerUser specifiedUser;
// IAggregatePartner partnerOperations;

// Updated information
var userToUpdate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "testPw@!122B" },
    DisplayName = "DisplayNameChange",
    FirstName = "FirstNameChange",
    LastName = "LastNameChange",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

// Update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="3f955-121">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3f955-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3f955-122">**Projekt**: PartnerSDK. FeatureSamples- **klass**: CustomerUserUpdate.CS</span><span class="sxs-lookup"><span data-stu-id="3f955-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3f955-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3f955-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3f955-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="3f955-124">Request syntax</span></span>

| <span data-ttu-id="3f955-125">Metod</span><span class="sxs-lookup"><span data-stu-id="3f955-125">Method</span></span>    | <span data-ttu-id="3f955-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3f955-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="3f955-127">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="3f955-127">**PATCH**</span></span> | <span data-ttu-id="3f955-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="3f955-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3f955-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="3f955-129">URI parameter</span></span>

<span data-ttu-id="3f955-130">Använd följande frågeparameter för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="3f955-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="3f955-131">Namn</span><span class="sxs-lookup"><span data-stu-id="3f955-131">Name</span></span>                   | <span data-ttu-id="3f955-132">Typ</span><span class="sxs-lookup"><span data-stu-id="3f955-132">Type</span></span>     | <span data-ttu-id="3f955-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3f955-133">Required</span></span> | <span data-ttu-id="3f955-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3f955-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3f955-135">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="3f955-135">**customer-tenant-id**</span></span> | <span data-ttu-id="3f955-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="3f955-136">**guid**</span></span> | <span data-ttu-id="3f955-137">Y</span><span class="sxs-lookup"><span data-stu-id="3f955-137">Y</span></span>        | <span data-ttu-id="3f955-138">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="3f955-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="3f955-139">**användar-ID**</span><span class="sxs-lookup"><span data-stu-id="3f955-139">**user-id**</span></span>            | <span data-ttu-id="3f955-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="3f955-140">**guid**</span></span> | <span data-ttu-id="3f955-141">Y</span><span class="sxs-lookup"><span data-stu-id="3f955-141">Y</span></span>        | <span data-ttu-id="3f955-142">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.</span><span class="sxs-lookup"><span data-stu-id="3f955-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="3f955-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3f955-143">Request headers</span></span>

<span data-ttu-id="3f955-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3f955-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3f955-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3f955-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="3f955-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3f955-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "new country/region code",

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="3f955-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3f955-147">REST response</span></span>

<span data-ttu-id="3f955-148">Om det lyckas returnerar den här metoden ett användar konto med den uppdaterade informationen.</span><span class="sxs-lookup"><span data-stu-id="3f955-148">If successful, this method returns a user account with the updated information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3f955-149">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3f955-149">Response success and error codes</span></span>

<span data-ttu-id="3f955-150">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="3f955-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3f955-151">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3f955-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3f955-152">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3f955-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3f955-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3f955-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "new country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "emailidchange@abcdefgh1234.ccsctp.net",
  "firstName": "FirstNameChange",
  "lastName": "LastNameChange",
  "displayName": "DisplayNameChange",
  "userDomainType": "none",
  "state": "active",
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/4b10bf41-ab11-40e3-8c53-cd67849b50de",
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
