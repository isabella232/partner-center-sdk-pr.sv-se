---
title: Hämta en prenumerations supportkontakt
description: Så här hämtar du en prenumerations support kontakt.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df3bce48902d95dc541c4a45e4e633569fc4406e
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769273"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="297d5-103">Hämta en prenumerations supportkontakt</span><span class="sxs-lookup"><span data-stu-id="297d5-103">Get a subscription's support contact</span></span>

<span data-ttu-id="297d5-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="297d5-104">**Applies To**</span></span>

- <span data-ttu-id="297d5-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="297d5-105">Partner Center</span></span>
- <span data-ttu-id="297d5-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="297d5-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="297d5-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="297d5-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="297d5-108">Så här hämtar du en prenumerations support kontakt.</span><span class="sxs-lookup"><span data-stu-id="297d5-108">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="297d5-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="297d5-109">Prerequisites</span></span>

- <span data-ttu-id="297d5-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="297d5-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="297d5-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="297d5-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="297d5-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="297d5-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="297d5-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="297d5-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="297d5-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="297d5-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="297d5-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="297d5-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="297d5-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="297d5-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="297d5-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="297d5-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="297d5-118">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="297d5-118">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="297d5-119">C\#</span><span class="sxs-lookup"><span data-stu-id="297d5-119">C\#</span></span>

<span data-ttu-id="297d5-120">Börja med att använda metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att identifiera kunden för att få en prenumerations support kontakt.</span><span class="sxs-lookup"><span data-stu-id="297d5-120">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="297d5-121">Hämta sedan ett gränssnitt till prenumerations åtgärder genom att anropa metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID: t.</span><span class="sxs-lookup"><span data-stu-id="297d5-121">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="297d5-122">Använd sedan egenskapen [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) för att hämta ett gränssnitt som stöder kontakt åtgärder och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) -objektet.</span><span class="sxs-lookup"><span data-stu-id="297d5-122">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="297d5-123">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="297d5-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="297d5-124">**Projekt**: Partner Center SDK-exempel **klass**: GetSubscriptionSupportContact.CS</span><span class="sxs-lookup"><span data-stu-id="297d5-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="297d5-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="297d5-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="297d5-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="297d5-126">Request syntax</span></span>

| <span data-ttu-id="297d5-127">Metod</span><span class="sxs-lookup"><span data-stu-id="297d5-127">Method</span></span>  | <span data-ttu-id="297d5-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="297d5-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="297d5-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="297d5-129">**GET**</span></span> | <span data-ttu-id="297d5-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="297d5-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="297d5-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="297d5-131">URI parameter</span></span>

<span data-ttu-id="297d5-132">Använd följande Sök vägs parametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="297d5-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="297d5-133">Namn</span><span class="sxs-lookup"><span data-stu-id="297d5-133">Name</span></span>            | <span data-ttu-id="297d5-134">Typ</span><span class="sxs-lookup"><span data-stu-id="297d5-134">Type</span></span>   | <span data-ttu-id="297d5-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="297d5-135">Required</span></span> | <span data-ttu-id="297d5-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="297d5-136">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="297d5-137">kund-ID</span><span class="sxs-lookup"><span data-stu-id="297d5-137">customer-id</span></span>     | <span data-ttu-id="297d5-138">sträng</span><span class="sxs-lookup"><span data-stu-id="297d5-138">string</span></span> | <span data-ttu-id="297d5-139">Yes</span><span class="sxs-lookup"><span data-stu-id="297d5-139">Yes</span></span>      | <span data-ttu-id="297d5-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="297d5-140">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="297d5-141">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="297d5-141">subscription-id</span></span> | <span data-ttu-id="297d5-142">sträng</span><span class="sxs-lookup"><span data-stu-id="297d5-142">string</span></span> | <span data-ttu-id="297d5-143">Yes</span><span class="sxs-lookup"><span data-stu-id="297d5-143">Yes</span></span>      | <span data-ttu-id="297d5-144">En GUID-formaterad sträng som identifierar utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="297d5-144">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="297d5-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="297d5-145">Request headers</span></span>

<span data-ttu-id="297d5-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="297d5-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="297d5-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="297d5-147">Request body</span></span>

<span data-ttu-id="297d5-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="297d5-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="297d5-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="297d5-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="297d5-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="297d5-150">REST response</span></span>

<span data-ttu-id="297d5-151">Om det lyckas innehåller svars texten [SupportContact](subscription-resources.md#supportcontact) -resursen.</span><span class="sxs-lookup"><span data-stu-id="297d5-151">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="297d5-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="297d5-152">Response success and error codes</span></span>

<span data-ttu-id="297d5-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="297d5-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="297d5-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="297d5-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="297d5-155">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="297d5-155">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="297d5-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="297d5-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

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
