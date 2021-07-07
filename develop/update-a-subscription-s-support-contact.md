---
title: Uppdatera en prenumerations supportkontakt
description: Så här uppdaterar du en prenumerations supportkontakt till en av partnerns mervärdesåterförsäljare.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c89f91fc9e89384a7be1237c08d7a9a1cfe3164
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530369"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="4c583-103">Uppdatera en prenumerations supportkontakt</span><span class="sxs-lookup"><span data-stu-id="4c583-103">Update a subscription's support contact</span></span>

<span data-ttu-id="4c583-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4c583-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4c583-105">Så här uppdaterar du en prenumerations supportkontakt till en av partnerns mervärdesåterförsäljare.</span><span class="sxs-lookup"><span data-stu-id="4c583-105">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c583-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="4c583-106">Prerequisites</span></span>

- <span data-ttu-id="4c583-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4c583-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4c583-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="4c583-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4c583-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4c583-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4c583-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4c583-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4c583-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="4c583-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4c583-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="4c583-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4c583-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="4c583-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4c583-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4c583-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4c583-115">En prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="4c583-115">A subscription identifier.</span></span>

- <span data-ttu-id="4c583-116">Information om den nya supportkontakten: klientorganisations-ID, Microsoft Partner Network-ID och namn.</span><span class="sxs-lookup"><span data-stu-id="4c583-116">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="4c583-117">Supportkontakten måste vara en av partnerns mervärdesåterförsäljare.</span><span class="sxs-lookup"><span data-stu-id="4c583-117">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="4c583-118">C\#</span><span class="sxs-lookup"><span data-stu-id="4c583-118">C\#</span></span>

<span data-ttu-id="4c583-119">Uppdatera supportkontakten för en prenumeration genom att först instansiera och fylla i ett [**SupportContact-objekt**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) med de nya värdena.</span><span class="sxs-lookup"><span data-stu-id="4c583-119">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="4c583-120">Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="4c583-120">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="4c583-121">Hämta sedan ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID:t.</span><span class="sxs-lookup"><span data-stu-id="4c583-121">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="4c583-122">Använd sedan egenskapen [**SupportContact för**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) att hämta ett gränssnitt som stöder kontaktåtgärder.</span><span class="sxs-lookup"><span data-stu-id="4c583-122">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="4c583-123">Anropa slutligen metoden [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) eller [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) med det ifyllda SupportContact-objektet för att uppdatera supportkontakten.</span><span class="sxs-lookup"><span data-stu-id="4c583-123">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

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

<span data-ttu-id="4c583-124">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4c583-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4c583-125">**Project:** Partnercenter-SDK **exempelklass:** UpdateSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="4c583-125">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4c583-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="4c583-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4c583-127">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="4c583-127">Request syntax</span></span>

| <span data-ttu-id="4c583-128">Metod</span><span class="sxs-lookup"><span data-stu-id="4c583-128">Method</span></span>  | <span data-ttu-id="4c583-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="4c583-129">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4c583-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="4c583-130">**PUT**</span></span> | <span data-ttu-id="4c583-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4c583-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4c583-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="4c583-132">URI parameter</span></span>

<span data-ttu-id="4c583-133">Använd följande sökvägsparametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="4c583-133">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="4c583-134">Namn</span><span class="sxs-lookup"><span data-stu-id="4c583-134">Name</span></span>            | <span data-ttu-id="4c583-135">Typ</span><span class="sxs-lookup"><span data-stu-id="4c583-135">Type</span></span>   | <span data-ttu-id="4c583-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4c583-136">Required</span></span> | <span data-ttu-id="4c583-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4c583-137">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="4c583-138">kund-ID</span><span class="sxs-lookup"><span data-stu-id="4c583-138">customer-id</span></span>     | <span data-ttu-id="4c583-139">sträng</span><span class="sxs-lookup"><span data-stu-id="4c583-139">string</span></span> | <span data-ttu-id="4c583-140">Ja</span><span class="sxs-lookup"><span data-stu-id="4c583-140">Yes</span></span>      | <span data-ttu-id="4c583-141">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="4c583-141">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="4c583-142">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="4c583-142">subscription-id</span></span> | <span data-ttu-id="4c583-143">sträng</span><span class="sxs-lookup"><span data-stu-id="4c583-143">string</span></span> | <span data-ttu-id="4c583-144">Ja</span><span class="sxs-lookup"><span data-stu-id="4c583-144">Yes</span></span>      | <span data-ttu-id="4c583-145">En GUID-formaterad sträng som identifierar utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="4c583-145">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4c583-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="4c583-146">Request headers</span></span>

<span data-ttu-id="4c583-147">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4c583-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4c583-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="4c583-148">Request body</span></span>

<span data-ttu-id="4c583-149">Du måste inkludera en ifylld [SupportContact-resurs](subscription-resources.md#supportcontact) i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="4c583-149">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="4c583-150">Supportkontakten måste vara en befintlig återförsäljare med en relation till partnern.</span><span class="sxs-lookup"><span data-stu-id="4c583-150">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="4c583-151">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="4c583-151">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4c583-152">REST-svar</span><span class="sxs-lookup"><span data-stu-id="4c583-152">REST response</span></span>

<span data-ttu-id="4c583-153">Om det lyckas innehåller svarstexten [SupportContact-resursen.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="4c583-153">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4c583-154">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="4c583-154">Response success and error codes</span></span>

<span data-ttu-id="4c583-155">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="4c583-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4c583-156">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="4c583-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4c583-157">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4c583-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4c583-158">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="4c583-158">Response example</span></span>

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
