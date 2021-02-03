---
title: Bekräfta kundgodkännande av Microsoft-kundavtal
description: 'Lär dig hur du bekräftar kund godkännande av Microsofts kund avtal med hjälp av API: er för partner Center.'
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 239ca43c70fb8aa7f0d06e564e6c0726b235ffbe
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770074"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="ce599-103">Bekräfta kund godkännande av Microsofts kund avtal med hjälp av API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="ce599-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="ce599-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="ce599-104">**Applies to:**</span></span>

- <span data-ttu-id="ce599-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="ce599-105">Partner Center</span></span>

<span data-ttu-id="ce599-106">Partner Center har för närvarande endast stöd för bekräftelse av kund godkännande av Microsofts kund avtal i *Microsofts offentliga moln*.</span><span class="sxs-lookup"><span data-stu-id="ce599-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="ce599-107">Den här funktionen gäller för närvarande inte för:</span><span class="sxs-lookup"><span data-stu-id="ce599-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="ce599-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="ce599-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ce599-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="ce599-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ce599-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ce599-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ce599-111">I den här artikeln beskrivs hur du bekräftar eller ombekräftar kund godkännande av Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce599-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ce599-112">Prerequisites</span></span>

- <span data-ttu-id="ce599-113">Om du använder Partner Center .NET SDK krävs version 1,14 eller senare.</span><span class="sxs-lookup"><span data-stu-id="ce599-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="ce599-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ce599-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="ce599-115">*Det här scenariot stöder endast app + användarautentisering.*</span><span class="sxs-lookup"><span data-stu-id="ce599-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="ce599-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ce599-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ce599-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="ce599-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ce599-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="ce599-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ce599-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="ce599-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ce599-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="ce599-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ce599-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ce599-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ce599-122">Datumet (**dateAgreed**) när kunden har godkänt Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="ce599-123">Information om användaren från kund organisationen som har godkänt Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="ce599-124">Du måste bland annat:</span><span class="sxs-lookup"><span data-stu-id="ce599-124">This includes:</span></span>
  - <span data-ttu-id="ce599-125">Förnamn</span><span class="sxs-lookup"><span data-stu-id="ce599-125">First name</span></span>
  - <span data-ttu-id="ce599-126">Efternamn</span><span class="sxs-lookup"><span data-stu-id="ce599-126">Last name</span></span>
  - <span data-ttu-id="ce599-127">E-postadress</span><span class="sxs-lookup"><span data-stu-id="ce599-127">Email address</span></span>
  - <span data-ttu-id="ce599-128">Telefonnummer (valfritt)</span><span class="sxs-lookup"><span data-stu-id="ce599-128">Phone number (optional)</span></span>

## <a name="net"></a><span data-ttu-id="ce599-129">.NET</span><span class="sxs-lookup"><span data-stu-id="ce599-129">.NET</span></span>

<span data-ttu-id="ce599-130">För att bekräfta eller bekräfta kund godkännande av Microsofts kund avtal:</span><span class="sxs-lookup"><span data-stu-id="ce599-130">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="ce599-131">Hämta avtals metadata för Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-131">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="ce599-132">Du måste skaffa **templateId** till Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-132">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="ce599-133">Mer information finns i [Hämta avtals-metadata för Microsofts kund avtal](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="ce599-133">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="ce599-134">Skapa ett nytt **avtals** objekt som innehåller information om bekräftelsen.</span><span class="sxs-lookup"><span data-stu-id="ce599-134">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="ce599-135">Använd **IAgreggatePartner. Customers** -samlingen och anropa **ById** -metoden med angivet **kund-ID**.</span><span class="sxs-lookup"><span data-stu-id="ce599-135">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="ce599-136">Använd egenskapen **avtal** , följt av anropa **create** eller **CreateAsync**.</span><span class="sxs-lookup"><span data-stu-id="ce599-136">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

<span data-ttu-id="ce599-137">Ett fullständigt exempel finns i [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.</span><span class="sxs-lookup"><span data-stu-id="ce599-137">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ce599-138">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ce599-138">REST request</span></span>

<span data-ttu-id="ce599-139">För att bekräfta eller bekräfta kund godkännande av Microsofts kund avtal:</span><span class="sxs-lookup"><span data-stu-id="ce599-139">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="ce599-140">Hämta avtals metadata för Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-140">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="ce599-141">Du måste skaffa **templateId** till Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-141">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="ce599-142">Mer information finns i [Hämta avtals-metadata för Microsofts kund avtal](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="ce599-142">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="ce599-143">Skapa en ny [ **avtals** resurs](agreement-resources.md) för att bekräfta att en kund har godkänt Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-143">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="ce599-144">Använd följande [syntax för rest-begäran](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="ce599-144">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ce599-145">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="ce599-145">Request syntax</span></span>

| <span data-ttu-id="ce599-146">Metod</span><span class="sxs-lookup"><span data-stu-id="ce599-146">Method</span></span> | <span data-ttu-id="ce599-147">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ce599-147">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ce599-148">POST</span><span class="sxs-lookup"><span data-stu-id="ce599-148">POST</span></span>   | <span data-ttu-id="ce599-149">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="ce599-149">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="ce599-150">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ce599-150">URI parameter</span></span>

<span data-ttu-id="ce599-151">Använd följande frågeparameter för att ange den kund som du bekräftar.</span><span class="sxs-lookup"><span data-stu-id="ce599-151">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="ce599-152">Namn</span><span class="sxs-lookup"><span data-stu-id="ce599-152">Name</span></span>               | <span data-ttu-id="ce599-153">Typ</span><span class="sxs-lookup"><span data-stu-id="ce599-153">Type</span></span> | <span data-ttu-id="ce599-154">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ce599-154">Required</span></span> | <span data-ttu-id="ce599-155">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ce599-155">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="ce599-156">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="ce599-156">customer-tenant-id</span></span> | <span data-ttu-id="ce599-157">GUID</span><span class="sxs-lookup"><span data-stu-id="ce599-157">GUID</span></span> | <span data-ttu-id="ce599-158">Yes</span><span class="sxs-lookup"><span data-stu-id="ce599-158">Yes</span></span> | <span data-ttu-id="ce599-159">Värdet är ett GUID-formaterat **kund-ID**, som är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="ce599-159">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ce599-160">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ce599-160">Request headers</span></span>

<span data-ttu-id="ce599-161">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ce599-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ce599-162">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ce599-162">Request body</span></span>

<span data-ttu-id="ce599-163">I den här tabellen beskrivs de egenskaper som krävs i innehållet i REST-begäran.</span><span class="sxs-lookup"><span data-stu-id="ce599-163">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="ce599-164">Namn</span><span class="sxs-lookup"><span data-stu-id="ce599-164">Name</span></span>      | <span data-ttu-id="ce599-165">Typ</span><span class="sxs-lookup"><span data-stu-id="ce599-165">Type</span></span>   | <span data-ttu-id="ce599-166">Description</span><span class="sxs-lookup"><span data-stu-id="ce599-166">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="ce599-167">Avtal</span><span class="sxs-lookup"><span data-stu-id="ce599-167">Agreement</span></span> | <span data-ttu-id="ce599-168">objekt</span><span class="sxs-lookup"><span data-stu-id="ce599-168">object</span></span> | <span data-ttu-id="ce599-169">Information som tillhandahålls av partnern för att bekräfta kund godkännande av Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-169">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="ce599-170">Avtal</span><span class="sxs-lookup"><span data-stu-id="ce599-170">Agreement</span></span>

<span data-ttu-id="ce599-171">I den här tabellen beskrivs minimi kraven för de fält som krävs för att skapa en [ **avtals** resurs](agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ce599-171">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="ce599-172">Egenskap</span><span class="sxs-lookup"><span data-stu-id="ce599-172">Property</span></span>       | <span data-ttu-id="ce599-173">Typ</span><span class="sxs-lookup"><span data-stu-id="ce599-173">Type</span></span>   | <span data-ttu-id="ce599-174">Description</span><span class="sxs-lookup"><span data-stu-id="ce599-174">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="ce599-175">primaryContact</span><span class="sxs-lookup"><span data-stu-id="ce599-175">primaryContact</span></span> | [<span data-ttu-id="ce599-176">Kontakt</span><span class="sxs-lookup"><span data-stu-id="ce599-176">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="ce599-177">Information om användaren från kund organisationen som har godkänt Microsofts kund avtal, inklusive:  **FirstName**, **LastName**, **e-post** och **telefonnummer** (valfritt)</span><span class="sxs-lookup"><span data-stu-id="ce599-177">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="ce599-178">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="ce599-178">dateAgreed</span></span>     | <span data-ttu-id="ce599-179">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="ce599-179">string in UTC date time format</span></span> |<span data-ttu-id="ce599-180">Datumet då kunden godkände avtalet.</span><span class="sxs-lookup"><span data-stu-id="ce599-180">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="ce599-181">templateId</span><span class="sxs-lookup"><span data-stu-id="ce599-181">templateId</span></span>     | <span data-ttu-id="ce599-182">sträng</span><span class="sxs-lookup"><span data-stu-id="ce599-182">string</span></span> | <span data-ttu-id="ce599-183">Unik identifierare för den avtals typ som kunden har accepterat.</span><span class="sxs-lookup"><span data-stu-id="ce599-183">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="ce599-184">Du kan hämta **templateId** för Microsofts kund avtal genom att hämta avtals-metadata för Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-184">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="ce599-185">Mer information finns i [Hämta avtals metadata för Microsofts kund avtal](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="ce599-185">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="ce599-186">typ</span><span class="sxs-lookup"><span data-stu-id="ce599-186">type</span></span>           | <span data-ttu-id="ce599-187">sträng</span><span class="sxs-lookup"><span data-stu-id="ce599-187">string</span></span> | <span data-ttu-id="ce599-188">Avtals typ som accepteras av kunden.</span><span class="sxs-lookup"><span data-stu-id="ce599-188">Agreement type accepted by the customer.</span></span> <span data-ttu-id="ce599-189">Använd "MicrosoftCustomerAgreement" om kunden har godkänt Microsofts kund avtal.</span><span class="sxs-lookup"><span data-stu-id="ce599-189">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="ce599-190">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ce599-190">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a><span data-ttu-id="ce599-191">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ce599-191">REST response</span></span>

<span data-ttu-id="ce599-192">Om det lyckas returnerar den här metoden en [ **avtals** resurs](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ce599-192">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ce599-193">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ce599-193">Response success and error codes</span></span>

<span data-ttu-id="ce599-194">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="ce599-194">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="ce599-195">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ce599-195">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ce599-196">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ce599-196">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="ce599-197">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ce599-197">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
