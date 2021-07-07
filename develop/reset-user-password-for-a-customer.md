---
title: Återställ användarlösenord för en kund
description: Att återställa ett lösenord liknar att uppdatera annan information i ett befintligt användarkonto för din kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: f3661a588f566485cbd58035c63ae9f8e5d383af
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445688"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="147c1-103">Återställ användarlösenord för en kund</span><span class="sxs-lookup"><span data-stu-id="147c1-103">Reset user password for a customer</span></span>

<span data-ttu-id="147c1-104">Att återställa ett lösenord liknar att uppdatera annan information i ett befintligt användarkonto för din kund.</span><span class="sxs-lookup"><span data-stu-id="147c1-104">Resetting a password is similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="147c1-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="147c1-105">Prerequisites</span></span>

- <span data-ttu-id="147c1-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="147c1-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="147c1-107">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="147c1-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="147c1-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="147c1-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="147c1-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="147c1-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="147c1-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="147c1-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="147c1-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="147c1-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="147c1-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="147c1-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="147c1-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="147c1-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="147c1-114">C\#</span><span class="sxs-lookup"><span data-stu-id="147c1-114">C\#</span></span>

<span data-ttu-id="147c1-115">Om du vill återställa ett lösenord för en angiven kundanvändare hämtar du först det angivna kund-ID:t och målanvändaren.</span><span class="sxs-lookup"><span data-stu-id="147c1-115">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="147c1-116">Skapa sedan ett nytt **CustomerUser-objekt** som innehåller informationen för den befintliga kunden, men med ett nytt **PasswordProfile-objekt.**</span><span class="sxs-lookup"><span data-stu-id="147c1-116">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="147c1-117">Använd sedan din **IAggregatePartner.Customers-samling** och anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="147c1-117">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="147c1-118">Anropa sedan **egenskapen** Användare, **metoden ById()** och sedan **metoden Patch.**</span><span class="sxs-lookup"><span data-stu-id="147c1-118">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

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

<span data-ttu-id="147c1-119">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="147c1-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="147c1-120">**Project:** PartnerSDK.FeatureSamples-klass: CustomerUserUpdate.cs </span><span class="sxs-lookup"><span data-stu-id="147c1-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="147c1-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="147c1-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="147c1-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="147c1-122">Request syntax</span></span>

| <span data-ttu-id="147c1-123">Metod</span><span class="sxs-lookup"><span data-stu-id="147c1-123">Method</span></span>    | <span data-ttu-id="147c1-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="147c1-124">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="147c1-125">**Patch**</span><span class="sxs-lookup"><span data-stu-id="147c1-125">**PATCH**</span></span> | <span data-ttu-id="147c1-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="147c1-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="147c1-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="147c1-127">URI parameter</span></span>

<span data-ttu-id="147c1-128">Använd följande frågeparameter för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="147c1-128">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="147c1-129">Namn</span><span class="sxs-lookup"><span data-stu-id="147c1-129">Name</span></span>                   | <span data-ttu-id="147c1-130">Typ</span><span class="sxs-lookup"><span data-stu-id="147c1-130">Type</span></span>     | <span data-ttu-id="147c1-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="147c1-131">Required</span></span> | <span data-ttu-id="147c1-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="147c1-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="147c1-133">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="147c1-133">**customer-tenant-id**</span></span> | <span data-ttu-id="147c1-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="147c1-134">**guid**</span></span> | <span data-ttu-id="147c1-135">Y</span><span class="sxs-lookup"><span data-stu-id="147c1-135">Y</span></span>        | <span data-ttu-id="147c1-136">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="147c1-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="147c1-137">**användar-id**</span><span class="sxs-lookup"><span data-stu-id="147c1-137">**user-id**</span></span>            | <span data-ttu-id="147c1-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="147c1-138">**guid**</span></span> | <span data-ttu-id="147c1-139">Y</span><span class="sxs-lookup"><span data-stu-id="147c1-139">Y</span></span>        | <span data-ttu-id="147c1-140">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.</span><span class="sxs-lookup"><span data-stu-id="147c1-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="147c1-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="147c1-141">Request headers</span></span>

<span data-ttu-id="147c1-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="147c1-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="147c1-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="147c1-143">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="147c1-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="147c1-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="147c1-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="147c1-145">REST response</span></span>

<span data-ttu-id="147c1-146">Om det lyckas returnerar den här metoden användarinformationen tillsammans med den uppdaterade lösenordsinformationen.</span><span class="sxs-lookup"><span data-stu-id="147c1-146">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="147c1-147">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="147c1-147">Response success and error codes</span></span>

<span data-ttu-id="147c1-148">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="147c1-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="147c1-149">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="147c1-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="147c1-150">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="147c1-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="147c1-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="147c1-151">Response example</span></span>

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
