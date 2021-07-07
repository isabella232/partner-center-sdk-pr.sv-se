---
title: Aktivera en sandbox-prenumeration för produkter på den kommersiella marknadsplatsen
description: Lär dig hur du använder REST-API:er för C/# och Partner Center för att aktivera en sandbox-prenumeration för produkter på den kommersiella marknadsplatsen.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b32c3e87462f58218771fc5da7da56ed177489cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025708"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="ac7f4-103">Aktivera en sandbox-prenumeration för SaaS-produkter på den kommersiella marknadsplatsen för att aktivera fakturering</span><span class="sxs-lookup"><span data-stu-id="ac7f4-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="ac7f4-104">Så här aktiverar du en prenumeration på den kommersiella marknadsplatsen SaaS-produkter (Programvara som en tjänst) från sandbox-konton för integrering för att aktivera fakturering.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-104">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="ac7f4-105">Det går bara att aktivera en prenumeration för SaaS-produkter på den kommersiella marknadsplatsen från sandbox-konton för integrering.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-105">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="ac7f4-106">Om du har en produktionsprenumeration måste du besöka utgivarens webbplats för att slutföra installationen.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-106">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="ac7f4-107">Prenumerationsfakturering börjar först när installationen är klar.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-107">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac7f4-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ac7f4-108">Prerequisites</span></span>

- <span data-ttu-id="ac7f4-109">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f4-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ac7f4-110">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ac7f4-111">Ett partnerkonto för sandbox-integrering med en kund som har en aktiv prenumeration på SaaS-produkter på den kommersiella marknadsplatsen.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-111">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="ac7f4-112">För partner som använder Partner Center .NET SDK måste du använda SDK version 1.14.0 eller senare för att få åtkomst till den här funktionen.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-112">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="ac7f4-113">C\#</span><span class="sxs-lookup"><span data-stu-id="ac7f4-113">C\#</span></span>

<span data-ttu-id="ac7f4-114">Använd följande steg för att aktivera en prenumeration för SaaS-produkter på den kommersiella marknadsplatsen:</span><span class="sxs-lookup"><span data-stu-id="ac7f4-114">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="ac7f4-115">Gör ett gränssnitt för prenumerationsåtgärder tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-115">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="ac7f4-116">Du måste identifiera kunden och ange prenumerations-ID för utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-116">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="ac7f4-117">Aktivera prenumerationen med hjälp av **åtgärden** Aktivera.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-117">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="ac7f4-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ac7f4-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ac7f4-119">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ac7f4-119">Request syntax</span></span>

| <span data-ttu-id="ac7f4-120">Metod</span><span class="sxs-lookup"><span data-stu-id="ac7f4-120">Method</span></span>     | <span data-ttu-id="ac7f4-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ac7f4-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="ac7f4-122">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="ac7f4-122">**POST**</span></span> | <span data-ttu-id="ac7f4-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ac7f4-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ac7f4-124">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ac7f4-124">URI parameter</span></span>

| <span data-ttu-id="ac7f4-125">Namn</span><span class="sxs-lookup"><span data-stu-id="ac7f4-125">Name</span></span>                   | <span data-ttu-id="ac7f4-126">Typ</span><span class="sxs-lookup"><span data-stu-id="ac7f4-126">Type</span></span>     | <span data-ttu-id="ac7f4-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ac7f4-127">Required</span></span> | <span data-ttu-id="ac7f4-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ac7f4-128">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ac7f4-129">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="ac7f4-129">**customer-tenant-id**</span></span> | <span data-ttu-id="ac7f4-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="ac7f4-130">**guid**</span></span> | <span data-ttu-id="ac7f4-131">Y</span><span class="sxs-lookup"><span data-stu-id="ac7f4-131">Y</span></span> | <span data-ttu-id="ac7f4-132">Värdet är ett GUID-formaterat kundklient-ID (**customer-tenant-id**), som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-132">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="ac7f4-133">**prenumerations-id**</span><span class="sxs-lookup"><span data-stu-id="ac7f4-133">**subscription-id**</span></span> | <span data-ttu-id="ac7f4-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="ac7f4-134">**guid**</span></span> | <span data-ttu-id="ac7f4-135">Y</span><span class="sxs-lookup"><span data-stu-id="ac7f4-135">Y</span></span> | <span data-ttu-id="ac7f4-136">Värdet är en GUID-formaterad prenumerationsidentifierare (**subscription-id**) som gör att du kan ange en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-136">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ac7f4-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ac7f4-137">Request headers</span></span>

<span data-ttu-id="ac7f4-138">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f4-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ac7f4-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ac7f4-139">Request body</span></span>

<span data-ttu-id="ac7f4-140">Inga.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ac7f4-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ac7f4-141">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="ac7f4-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ac7f4-142">REST response</span></span>

<span data-ttu-id="ac7f4-143">Den här metoden returnerar **egenskaperna subscription-id** **och status.**</span><span class="sxs-lookup"><span data-stu-id="ac7f4-143">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ac7f4-144">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ac7f4-144">Response success and error codes</span></span>

<span data-ttu-id="ac7f4-145">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ac7f4-146">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ac7f4-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ac7f4-147">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f4-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ac7f4-148">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ac7f4-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
