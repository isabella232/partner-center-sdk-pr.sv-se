---
title: Få bekräftelse på kundgodkännande av Microsoft-kundavtal
description: Den här artikeln förklarar hur du får en bekräftelse på kundens godkännande av Microsoft-kundavtal.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3668a5e510effb533cade311f52513b9a81d40af
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760546"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="1acf3-103">Få bekräftelse på kundgodkännande av Microsoft-kundavtal</span><span class="sxs-lookup"><span data-stu-id="1acf3-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="1acf3-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="1acf3-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="1acf3-105">**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1acf3-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1acf3-106">**Avtalsresursen** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="1acf3-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="1acf3-107">Den här artikeln förklarar hur du kan hämta bekräftelser av en kunds godkännande av Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="1acf3-107">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1acf3-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1acf3-108">Prerequisites</span></span>

- <span data-ttu-id="1acf3-109">Om du använder Partner Center .NET SDK krävs version 1.14 eller senare.</span><span class="sxs-lookup"><span data-stu-id="1acf3-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="1acf3-110">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1acf3-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="1acf3-111">Det här scenariot stöder endast app- och användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="1acf3-111">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="1acf3-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1acf3-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1acf3-113">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1acf3-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1acf3-114">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="1acf3-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1acf3-115">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="1acf3-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1acf3-116">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="1acf3-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1acf3-117">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1acf3-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="1acf3-118">.NET</span><span class="sxs-lookup"><span data-stu-id="1acf3-118">.NET</span></span>

<span data-ttu-id="1acf3-119">Så här hämtar du bekräftelser av kundgodkännande som angavs tidigare:</span><span class="sxs-lookup"><span data-stu-id="1acf3-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="1acf3-120">Använd **samlingen IAggregatePartner.Customers och** anropa **ById-metoden** med den angivna kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="1acf3-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="1acf3-121">Hämta egenskapen **Agreements** och filtrera resultaten för att Microsoft-kundavtal by calling **ByAgreementType method (ByAgreementType-metod).**</span><span class="sxs-lookup"><span data-stu-id="1acf3-121">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="1acf3-122">Anropa **Get-** eller **GetAsync-metoden.**</span><span class="sxs-lookup"><span data-stu-id="1acf3-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="1acf3-123">Ett fullständigt exempel finns i klassen [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) från [konsoltestappprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="1acf3-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="1acf3-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1acf3-124">REST request</span></span>

<span data-ttu-id="1acf3-125">Så här hämtar du en bekräftelse på kundgodkännande som angavs tidigare:</span><span class="sxs-lookup"><span data-stu-id="1acf3-125">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="1acf3-126">Skapa en REST-begäran för att [hämta avtalssamlingen](./agreement-resources.md) för kunden.</span><span class="sxs-lookup"><span data-stu-id="1acf3-126">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="1acf3-127">Använd **frågeparametern agreementType** för att begränsa resultatet till endast Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="1acf3-127">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1acf3-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="1acf3-128">Request syntax</span></span>

<span data-ttu-id="1acf3-129">Använd följande syntax för begäran:</span><span class="sxs-lookup"><span data-stu-id="1acf3-129">Use the following request syntax:</span></span>

| <span data-ttu-id="1acf3-130">Metod</span><span class="sxs-lookup"><span data-stu-id="1acf3-130">Method</span></span> | <span data-ttu-id="1acf3-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1acf3-131">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1acf3-132">GET</span><span class="sxs-lookup"><span data-stu-id="1acf3-132">GET</span></span>    | <span data-ttu-id="1acf3-133">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1acf3-133">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1acf3-134">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="1acf3-134">URI parameters</span></span>

<span data-ttu-id="1acf3-135">Du kan använda följande URI-parametrar med din begäran:</span><span class="sxs-lookup"><span data-stu-id="1acf3-135">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="1acf3-136">Namn</span><span class="sxs-lookup"><span data-stu-id="1acf3-136">Name</span></span>             | <span data-ttu-id="1acf3-137">Typ</span><span class="sxs-lookup"><span data-stu-id="1acf3-137">Type</span></span> | <span data-ttu-id="1acf3-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1acf3-138">Required</span></span> | <span data-ttu-id="1acf3-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1acf3-139">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="1acf3-140">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="1acf3-140">customer-tenant-id</span></span> | <span data-ttu-id="1acf3-141">GUID</span><span class="sxs-lookup"><span data-stu-id="1acf3-141">GUID</span></span> | <span data-ttu-id="1acf3-142">Ja</span><span class="sxs-lookup"><span data-stu-id="1acf3-142">Yes</span></span> | <span data-ttu-id="1acf3-143">Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="1acf3-143">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="1acf3-144">avtalstyp</span><span class="sxs-lookup"><span data-stu-id="1acf3-144">agreement-type</span></span> | <span data-ttu-id="1acf3-145">sträng</span><span class="sxs-lookup"><span data-stu-id="1acf3-145">string</span></span> | <span data-ttu-id="1acf3-146">No</span><span class="sxs-lookup"><span data-stu-id="1acf3-146">No</span></span> | <span data-ttu-id="1acf3-147">Den här parametern returnerar alla avtalsmetadata.</span><span class="sxs-lookup"><span data-stu-id="1acf3-147">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="1acf3-148">Använd den här parametern för att begränsa frågesvaret till specifik avtalstyp.</span><span class="sxs-lookup"><span data-stu-id="1acf3-148">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="1acf3-149">Värdena som stöds är:</span><span class="sxs-lookup"><span data-stu-id="1acf3-149">The supported values are:</span></span> <br/><br/> <span data-ttu-id="1acf3-150">**MicrosoftCloudAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCloudAgreement*.</span><span class="sxs-lookup"><span data-stu-id="1acf3-150">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="1acf3-151">**MicrosoftCustomerAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="1acf3-151">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="1acf3-152">**\**_ som returnerar alla avtalsmetadata. (Använd inte _\* \* \*_ såvida inte koden har den logik som krävs för att hantera oväntade avtalstyper.) <br/> <br/> _\* Obs!*\* Om URI-parametern inte anges används **MicrosoftCloudAgreement** som standard för bakåtkompatibilitet.</span><span class="sxs-lookup"><span data-stu-id="1acf3-152">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary logic to handle unexpected agreement types.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="1acf3-153">Microsoft kan när som helst införa avtalsmetadata med nya avtalstyper.</span><span class="sxs-lookup"><span data-stu-id="1acf3-153">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="1acf3-154">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1acf3-154">Request headers</span></span>

<span data-ttu-id="1acf3-155">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1acf3-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1acf3-156">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1acf3-156">Request body</span></span>

<span data-ttu-id="1acf3-157">Inga.</span><span class="sxs-lookup"><span data-stu-id="1acf3-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1acf3-158">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1acf3-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="1acf3-159">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1acf3-159">REST response</span></span>

<span data-ttu-id="1acf3-160">Om det lyckas returnerar den här metoden en samling **avtalsresurser** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="1acf3-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1acf3-161">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1acf3-161">Response success and error codes</span></span>

<span data-ttu-id="1acf3-162">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="1acf3-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="1acf3-163">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1acf3-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1acf3-164">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1acf3-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1acf3-165">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1acf3-165">Response example</span></span>

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
