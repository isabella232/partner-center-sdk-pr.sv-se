---
title: Hämta en prenumerations supportkontakt
description: Så här hämtar du en prenumerations supportkontakt.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b6c98e5ed96f2ca4787e93504c9e094bd46ae783
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760767"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="748e1-103">Hämta en prenumerations supportkontakt</span><span class="sxs-lookup"><span data-stu-id="748e1-103">Get a subscription's support contact</span></span>

<span data-ttu-id="748e1-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="748e1-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="748e1-105">Så här hämtar du en prenumerations supportkontakt.</span><span class="sxs-lookup"><span data-stu-id="748e1-105">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="748e1-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="748e1-106">Prerequisites</span></span>

- <span data-ttu-id="748e1-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="748e1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="748e1-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="748e1-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="748e1-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="748e1-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="748e1-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="748e1-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="748e1-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="748e1-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="748e1-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="748e1-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="748e1-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="748e1-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="748e1-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="748e1-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="748e1-115">En prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="748e1-115">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="748e1-116">C\#</span><span class="sxs-lookup"><span data-stu-id="748e1-116">C\#</span></span>

<span data-ttu-id="748e1-117">Om du vill hämta supportkontakten för en prenumeration börjar du med att använda metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="748e1-117">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="748e1-118">Hämta sedan ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID:t.</span><span class="sxs-lookup"><span data-stu-id="748e1-118">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="748e1-119">Använd sedan egenskapen [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) för att hämta ett gränssnitt som stöder kontaktåtgärder och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta [**SupportContact-objektet.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact)</span><span class="sxs-lookup"><span data-stu-id="748e1-119">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="748e1-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="748e1-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="748e1-121">**Project:** Partnercenter-SDK **Exempelklass:** GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="748e1-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="748e1-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="748e1-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="748e1-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="748e1-123">Request syntax</span></span>

| <span data-ttu-id="748e1-124">Metod</span><span class="sxs-lookup"><span data-stu-id="748e1-124">Method</span></span>  | <span data-ttu-id="748e1-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="748e1-125">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="748e1-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="748e1-126">**GET**</span></span> | <span data-ttu-id="748e1-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="748e1-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="748e1-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="748e1-128">URI parameter</span></span>

<span data-ttu-id="748e1-129">Använd följande sökvägsparametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="748e1-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="748e1-130">Namn</span><span class="sxs-lookup"><span data-stu-id="748e1-130">Name</span></span>            | <span data-ttu-id="748e1-131">Typ</span><span class="sxs-lookup"><span data-stu-id="748e1-131">Type</span></span>   | <span data-ttu-id="748e1-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="748e1-132">Required</span></span> | <span data-ttu-id="748e1-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="748e1-133">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="748e1-134">kund-id</span><span class="sxs-lookup"><span data-stu-id="748e1-134">customer-id</span></span>     | <span data-ttu-id="748e1-135">sträng</span><span class="sxs-lookup"><span data-stu-id="748e1-135">string</span></span> | <span data-ttu-id="748e1-136">Ja</span><span class="sxs-lookup"><span data-stu-id="748e1-136">Yes</span></span>      | <span data-ttu-id="748e1-137">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="748e1-137">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="748e1-138">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="748e1-138">subscription-id</span></span> | <span data-ttu-id="748e1-139">sträng</span><span class="sxs-lookup"><span data-stu-id="748e1-139">string</span></span> | <span data-ttu-id="748e1-140">Ja</span><span class="sxs-lookup"><span data-stu-id="748e1-140">Yes</span></span>      | <span data-ttu-id="748e1-141">En GUID-formaterad sträng som identifierar utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="748e1-141">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="748e1-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="748e1-142">Request headers</span></span>

<span data-ttu-id="748e1-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="748e1-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="748e1-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="748e1-144">Request body</span></span>

<span data-ttu-id="748e1-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="748e1-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="748e1-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="748e1-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="748e1-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="748e1-147">REST response</span></span>

<span data-ttu-id="748e1-148">Om det lyckas innehåller svarstexten [SupportContact-resursen.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="748e1-148">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="748e1-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="748e1-149">Response success and error codes</span></span>

<span data-ttu-id="748e1-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="748e1-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="748e1-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="748e1-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="748e1-152">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="748e1-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="748e1-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="748e1-153">Response example</span></span>

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
