---
title: Få bekräftelse på kundgodkännande av Microsoft-kundavtal
description: Den här artikeln förklarar hur du får bekräftelse på kund godkännande av Microsofts kund avtal.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769438"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="daeee-103">Få bekräftelse på kundgodkännande av Microsoft-kundavtal</span><span class="sxs-lookup"><span data-stu-id="daeee-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="daeee-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="daeee-104">**Applies to:**</span></span>

- <span data-ttu-id="daeee-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="daeee-105">Partner Center</span></span>

<span data-ttu-id="daeee-106">**Avtals** resursen stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*.</span><span class="sxs-lookup"><span data-stu-id="daeee-106">The **Agreement** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="daeee-107">Den här resursen gäller inte för:</span><span class="sxs-lookup"><span data-stu-id="daeee-107">This resource doesn't apply to:</span></span>

- <span data-ttu-id="daeee-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="daeee-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="daeee-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="daeee-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="daeee-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="daeee-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="daeee-111">I den här artikeln förklaras hur du kan hämta bekräftelse (er) av kundens godkännande av Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="daeee-111">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daeee-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="daeee-112">Prerequisites</span></span>

- <span data-ttu-id="daeee-113">Om du använder Partner Center .NET SDK krävs version 1,14 eller senare.</span><span class="sxs-lookup"><span data-stu-id="daeee-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="daeee-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="daeee-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="daeee-115">Det här scenariot stöder endast app + användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="daeee-115">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="daeee-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="daeee-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="daeee-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="daeee-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="daeee-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="daeee-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="daeee-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="daeee-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="daeee-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="daeee-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="daeee-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="daeee-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="daeee-122">.NET</span><span class="sxs-lookup"><span data-stu-id="daeee-122">.NET</span></span>

<span data-ttu-id="daeee-123">För att hämta bekräftelser för kundgodkännande som tidigare har tillhandahållits:</span><span class="sxs-lookup"><span data-stu-id="daeee-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="daeee-124">Använd **IAggregatePartner. Customers** -samlingen och anropa **ById** -metoden med det angivna kund-ID: n.</span><span class="sxs-lookup"><span data-stu-id="daeee-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="daeee-125">Hämta **avtals** egenskapen och filtrera resultaten till Microsofts kund avtal genom att anropa **ByAgreementType** -metoden.</span><span class="sxs-lookup"><span data-stu-id="daeee-125">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="daeee-126">Anropa **Get** -eller **GetAsync** -metoden.</span><span class="sxs-lookup"><span data-stu-id="daeee-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="daeee-127">Ett fullständigt exempel finns i [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.</span><span class="sxs-lookup"><span data-stu-id="daeee-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="daeee-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="daeee-128">REST request</span></span>

<span data-ttu-id="daeee-129">Så här hämtar du bekräftelse på kundgodkännande som tidigare har tillhandahållits:</span><span class="sxs-lookup"><span data-stu-id="daeee-129">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="daeee-130">Skapa en REST-begäran för att hämta [avtals](./agreement-resources.md) samlingen för kunden.</span><span class="sxs-lookup"><span data-stu-id="daeee-130">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="daeee-131">Använd Frågeparametern **agreementType** för att begränsa resultatet till enbart Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="daeee-131">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="daeee-132">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="daeee-132">Request syntax</span></span>

<span data-ttu-id="daeee-133">Använd följande syntax för begäran:</span><span class="sxs-lookup"><span data-stu-id="daeee-133">Use the following request syntax:</span></span>

| <span data-ttu-id="daeee-134">Metod</span><span class="sxs-lookup"><span data-stu-id="daeee-134">Method</span></span> | <span data-ttu-id="daeee-135">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="daeee-135">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="daeee-136">GET</span><span class="sxs-lookup"><span data-stu-id="daeee-136">GET</span></span>    | <span data-ttu-id="daeee-137">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements? agreementType = {Agreement-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="daeee-137">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="daeee-138">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="daeee-138">URI parameters</span></span>

<span data-ttu-id="daeee-139">Du kan använda följande URI-parametrar med din begäran:</span><span class="sxs-lookup"><span data-stu-id="daeee-139">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="daeee-140">Namn</span><span class="sxs-lookup"><span data-stu-id="daeee-140">Name</span></span>             | <span data-ttu-id="daeee-141">Typ</span><span class="sxs-lookup"><span data-stu-id="daeee-141">Type</span></span> | <span data-ttu-id="daeee-142">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="daeee-142">Required</span></span> | <span data-ttu-id="daeee-143">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="daeee-143">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="daeee-144">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="daeee-144">customer-tenant-id</span></span> | <span data-ttu-id="daeee-145">GUID</span><span class="sxs-lookup"><span data-stu-id="daeee-145">GUID</span></span> | <span data-ttu-id="daeee-146">Yes</span><span class="sxs-lookup"><span data-stu-id="daeee-146">Yes</span></span> | <span data-ttu-id="daeee-147">Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="daeee-147">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="daeee-148">avtals typ</span><span class="sxs-lookup"><span data-stu-id="daeee-148">agreement-type</span></span> | <span data-ttu-id="daeee-149">sträng</span><span class="sxs-lookup"><span data-stu-id="daeee-149">string</span></span> | <span data-ttu-id="daeee-150">No</span><span class="sxs-lookup"><span data-stu-id="daeee-150">No</span></span> | <span data-ttu-id="daeee-151">Den här parametern returnerar alla avtals-metadata.</span><span class="sxs-lookup"><span data-stu-id="daeee-151">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="daeee-152">Använd den här parametern om du vill begränsa fråge svaret till en speciell avtals typ.</span><span class="sxs-lookup"><span data-stu-id="daeee-152">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="daeee-153">De värden som stöds är:</span><span class="sxs-lookup"><span data-stu-id="daeee-153">The supported values are:</span></span> <br/><br/> <span data-ttu-id="daeee-154">**MicrosoftCloudAgreement** som endast omfattar avtals-metadata av typen *MicrosoftCloudAgreement*.</span><span class="sxs-lookup"><span data-stu-id="daeee-154">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="daeee-155">**MicrosoftCustomerAgreement** som endast omfattar avtals-metadata av typen *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="daeee-155">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="daeee-156">**\*** som returnerar alla avtals-metadata.</span><span class="sxs-lookup"><span data-stu-id="daeee-156">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="daeee-157">(Använd inte **\*** om din kod har den nödvändiga logiken för att hantera oväntade avtals typer.)</span><span class="sxs-lookup"><span data-stu-id="daeee-157">(Don't use **\*** unless your code has the necessary logic to handle unexpected agreement types.)</span></span><br/><br/> <span data-ttu-id="daeee-158">**Obs:** Om URI-parametern inte anges använder frågan standardvärdet för **MicrosoftCloudAgreement** för bakåtkompatibilitet.</span><span class="sxs-lookup"><span data-stu-id="daeee-158">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="daeee-159">Microsoft kan införa avtals-metadata med nya avtals typer när som helst.</span><span class="sxs-lookup"><span data-stu-id="daeee-159">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="daeee-160">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="daeee-160">Request headers</span></span>

<span data-ttu-id="daeee-161">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="daeee-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="daeee-162">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="daeee-162">Request body</span></span>

<span data-ttu-id="daeee-163">Inga.</span><span class="sxs-lookup"><span data-stu-id="daeee-163">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="daeee-164">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="daeee-164">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="daeee-165">REST-svar</span><span class="sxs-lookup"><span data-stu-id="daeee-165">REST response</span></span>

<span data-ttu-id="daeee-166">Om det lyckas returnerar den här metoden en samling **avtals** resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="daeee-166">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="daeee-167">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="daeee-167">Response success and error codes</span></span>

<span data-ttu-id="daeee-168">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="daeee-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="daeee-169">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="daeee-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="daeee-170">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="daeee-170">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="daeee-171">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="daeee-171">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
