---
title: Aktivera en Sandbox-prenumeration för kommersiella Marketplace-produkter
description: 'Lär dig hur du använder REST-API: er för C/# och partner Center för att aktivera en Sandbox-prenumeration för kommersiella Marketplace-produkter.'
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769951"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="b650b-103">Aktivera en Sandbox-prenumeration för kommersiella Marketplace SaaS-produkter för att möjliggöra fakturering</span><span class="sxs-lookup"><span data-stu-id="b650b-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="b650b-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="b650b-104">**Applies to:**</span></span>

- <span data-ttu-id="b650b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b650b-105">Partner Center</span></span>

<span data-ttu-id="b650b-106">Så här aktiverar du en prenumeration för SaaS-produkter (Software as a Service) från integration för integration i sandbox-konton.</span><span class="sxs-lookup"><span data-stu-id="b650b-106">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="b650b-107">Det går bara att aktivera en prenumeration för SaaS-produkter från affärs platser från integration sandbox-konton.</span><span class="sxs-lookup"><span data-stu-id="b650b-107">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="b650b-108">Om du har en produktions prenumeration måste du gå till utgivarens webbplats för att slutföra installations processen.</span><span class="sxs-lookup"><span data-stu-id="b650b-108">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="b650b-109">Prenumerations faktureringen påbörjas bara efter att installationen har slutförts.</span><span class="sxs-lookup"><span data-stu-id="b650b-109">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b650b-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b650b-110">Prerequisites</span></span>

- <span data-ttu-id="b650b-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b650b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b650b-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b650b-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b650b-113">Ett partner konto för integration i begränsat läge med en kund som har en aktiv prenumeration på kommersiella Marketplace SaaS-produkter.</span><span class="sxs-lookup"><span data-stu-id="b650b-113">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="b650b-114">För partner som använder Partner Center .NET SDK måste du använda SDK-version 1.14.0 eller högre för att få åtkomst till den här funktionen.</span><span class="sxs-lookup"><span data-stu-id="b650b-114">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="b650b-115">C\#</span><span class="sxs-lookup"><span data-stu-id="b650b-115">C\#</span></span>

<span data-ttu-id="b650b-116">Använd följande steg för att aktivera en prenumeration för SaaS-produkter från kommersiella platser:</span><span class="sxs-lookup"><span data-stu-id="b650b-116">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="b650b-117">Gör ett gränssnitt till tillgängliga prenumerations åtgärder.</span><span class="sxs-lookup"><span data-stu-id="b650b-117">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="b650b-118">Du måste identifiera kunden och ange prenumerations-ID för utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="b650b-118">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="b650b-119">Aktivera prenumerationen med hjälp av åtgärden **Aktivera** .</span><span class="sxs-lookup"><span data-stu-id="b650b-119">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="b650b-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b650b-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b650b-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b650b-121">Request syntax</span></span>

| <span data-ttu-id="b650b-122">Metod</span><span class="sxs-lookup"><span data-stu-id="b650b-122">Method</span></span>     | <span data-ttu-id="b650b-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b650b-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b650b-124">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="b650b-124">**POST**</span></span> | <span data-ttu-id="b650b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/Activate http/1.1</span><span class="sxs-lookup"><span data-stu-id="b650b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b650b-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="b650b-126">URI parameter</span></span>

| <span data-ttu-id="b650b-127">Namn</span><span class="sxs-lookup"><span data-stu-id="b650b-127">Name</span></span>                   | <span data-ttu-id="b650b-128">Typ</span><span class="sxs-lookup"><span data-stu-id="b650b-128">Type</span></span>     | <span data-ttu-id="b650b-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b650b-129">Required</span></span> | <span data-ttu-id="b650b-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b650b-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b650b-131">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="b650b-131">**customer-tenant-id**</span></span> | <span data-ttu-id="b650b-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="b650b-132">**guid**</span></span> | <span data-ttu-id="b650b-133">Y</span><span class="sxs-lookup"><span data-stu-id="b650b-133">Y</span></span> | <span data-ttu-id="b650b-134">Värdet är ett GUID-formaterat kund klient-ID (**kund-Tenant-ID**), vilket gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="b650b-134">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="b650b-135">**prenumerations-ID**</span><span class="sxs-lookup"><span data-stu-id="b650b-135">**subscription-id**</span></span> | <span data-ttu-id="b650b-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="b650b-136">**guid**</span></span> | <span data-ttu-id="b650b-137">Y</span><span class="sxs-lookup"><span data-stu-id="b650b-137">Y</span></span> | <span data-ttu-id="b650b-138">Värdet är ett GUID-formaterat prenumerations-**ID (prenumerations-ID**), vilket gör att du kan ange en prenumeration.</span><span class="sxs-lookup"><span data-stu-id="b650b-138">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b650b-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b650b-139">Request headers</span></span>

<span data-ttu-id="b650b-140">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b650b-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b650b-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b650b-141">Request body</span></span>

<span data-ttu-id="b650b-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="b650b-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b650b-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b650b-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="b650b-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b650b-144">REST response</span></span>

<span data-ttu-id="b650b-145">Den här metoden returnerar egenskaperna för **prenumerations-ID** och **status** .</span><span class="sxs-lookup"><span data-stu-id="b650b-145">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b650b-146">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b650b-146">Response success and error codes</span></span>

<span data-ttu-id="b650b-147">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b650b-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b650b-148">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b650b-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b650b-149">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b650b-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b650b-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b650b-150">Response example</span></span>

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
