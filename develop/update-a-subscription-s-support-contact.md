---
title: Uppdatera en prenumerations supportkontakt
description: Så här uppdaterar du en prenumerations support kontakt till en av partnerns mervärdes åter försäljare.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8c6b658cfe6e14c75b0c06b177920ce3eb1b4ed
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769588"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="30323-103">Uppdatera en prenumerations supportkontakt</span><span class="sxs-lookup"><span data-stu-id="30323-103">Update a subscription's support contact</span></span>

<span data-ttu-id="30323-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="30323-104">**Applies To**</span></span>

- <span data-ttu-id="30323-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="30323-105">Partner Center</span></span>
- <span data-ttu-id="30323-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="30323-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="30323-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="30323-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="30323-108">Så här uppdaterar du en prenumerations support kontakt till en av partnerns mervärdes åter försäljare.</span><span class="sxs-lookup"><span data-stu-id="30323-108">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30323-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="30323-109">Prerequisites</span></span>

- <span data-ttu-id="30323-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="30323-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="30323-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="30323-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="30323-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30323-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="30323-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="30323-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="30323-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="30323-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="30323-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="30323-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="30323-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="30323-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="30323-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30323-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="30323-118">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="30323-118">A subscription identifier.</span></span>

- <span data-ttu-id="30323-119">Information om den nya support kontakten: klient-ID, Microsoft Partner Network identifierare och namn.</span><span class="sxs-lookup"><span data-stu-id="30323-119">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="30323-120">Support kontakten måste vara en av partnerns mervärdes åter försäljare.</span><span class="sxs-lookup"><span data-stu-id="30323-120">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="30323-121">C\#</span><span class="sxs-lookup"><span data-stu-id="30323-121">C\#</span></span>

<span data-ttu-id="30323-122">Om du vill uppdatera support kontakten för en prenumeration måste du först instansiera och fylla i ett [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) -objekt med de nya värdena.</span><span class="sxs-lookup"><span data-stu-id="30323-122">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="30323-123">Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="30323-123">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="30323-124">Hämta sedan ett gränssnitt till prenumerations åtgärder genom att anropa metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID: t.</span><span class="sxs-lookup"><span data-stu-id="30323-124">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="30323-125">Använd sedan egenskapen [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) för att hämta ett gränssnitt som stöder kontakt åtgärder.</span><span class="sxs-lookup"><span data-stu-id="30323-125">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="30323-126">Slutligen kan du anropa [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) -eller [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) -metoden med det ifyllda SupportContact-objektet för att uppdatera support kontakten.</span><span class="sxs-lookup"><span data-stu-id="30323-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

<span data-ttu-id="30323-127">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="30323-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="30323-128">**Projekt**: Partner Center SDK-exempel **klass**: UpdateSubscriptionSupportContact.CS</span><span class="sxs-lookup"><span data-stu-id="30323-128">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="30323-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="30323-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="30323-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="30323-130">Request syntax</span></span>

| <span data-ttu-id="30323-131">Metod</span><span class="sxs-lookup"><span data-stu-id="30323-131">Method</span></span>  | <span data-ttu-id="30323-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="30323-132">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="30323-133">**PUT**</span><span class="sxs-lookup"><span data-stu-id="30323-133">**PUT**</span></span> | <span data-ttu-id="30323-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="30323-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="30323-135">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="30323-135">URI parameter</span></span>

<span data-ttu-id="30323-136">Använd följande Sök vägs parametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="30323-136">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="30323-137">Namn</span><span class="sxs-lookup"><span data-stu-id="30323-137">Name</span></span>            | <span data-ttu-id="30323-138">Typ</span><span class="sxs-lookup"><span data-stu-id="30323-138">Type</span></span>   | <span data-ttu-id="30323-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="30323-139">Required</span></span> | <span data-ttu-id="30323-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="30323-140">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="30323-141">kund-ID</span><span class="sxs-lookup"><span data-stu-id="30323-141">customer-id</span></span>     | <span data-ttu-id="30323-142">sträng</span><span class="sxs-lookup"><span data-stu-id="30323-142">string</span></span> | <span data-ttu-id="30323-143">Yes</span><span class="sxs-lookup"><span data-stu-id="30323-143">Yes</span></span>      | <span data-ttu-id="30323-144">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="30323-144">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="30323-145">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="30323-145">subscription-id</span></span> | <span data-ttu-id="30323-146">sträng</span><span class="sxs-lookup"><span data-stu-id="30323-146">string</span></span> | <span data-ttu-id="30323-147">Yes</span><span class="sxs-lookup"><span data-stu-id="30323-147">Yes</span></span>      | <span data-ttu-id="30323-148">En GUID-formaterad sträng som identifierar utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="30323-148">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="30323-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="30323-149">Request headers</span></span>

<span data-ttu-id="30323-150">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="30323-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="30323-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="30323-151">Request body</span></span>

<span data-ttu-id="30323-152">Du måste inkludera en fylld [SupportContact](subscription-resources.md#supportcontact) -resurs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="30323-152">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="30323-153">Support kontakten måste vara en befintlig åter försäljare med en relation till partnern.</span><span class="sxs-lookup"><span data-stu-id="30323-153">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="30323-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="30323-154">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="30323-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="30323-155">REST response</span></span>

<span data-ttu-id="30323-156">Om det lyckas innehåller svars texten [SupportContact](subscription-resources.md#supportcontact) -resursen.</span><span class="sxs-lookup"><span data-stu-id="30323-156">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="30323-157">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="30323-157">Response success and error codes</span></span>

<span data-ttu-id="30323-158">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="30323-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="30323-159">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="30323-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="30323-160">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="30323-160">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="30323-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="30323-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
