---
title: Bekräfta kundgodkännande av Microsoft-kundavtal
description: Lär dig hur du bekräftar kundens godkännande av Microsoft-kundavtal partnercenter-API:er.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974020"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="18833-103">Bekräfta kundens godkännande av Microsoft-kundavtal partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="18833-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="18833-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="18833-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="18833-105">**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="18833-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="18833-106">Partnercenter stöder för närvarande bekräftelse av kundgodkännande av Microsoft-kundavtal endast i Microsofts offentliga moln.</span><span class="sxs-lookup"><span data-stu-id="18833-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the Microsoft public cloud.</span></span>

<span data-ttu-id="18833-107">Den här artikeln beskriver hur du bekräftar eller bekräftar kundens godkännande av Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-107">This article describes how to confirm or reconfirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18833-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="18833-108">Prerequisites</span></span>

- <span data-ttu-id="18833-109">Om du använder Partner Center .NET SDK krävs version 1.14 eller senare.</span><span class="sxs-lookup"><span data-stu-id="18833-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="18833-110">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="18833-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="18833-111">*Det här scenariot stöder endast app- och användarautentisering.*</span><span class="sxs-lookup"><span data-stu-id="18833-111">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="18833-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="18833-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="18833-113">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="18833-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="18833-114">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="18833-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="18833-115">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="18833-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="18833-116">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="18833-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="18833-117">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="18833-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="18833-118">Datumet (**dateAgreed**) när kunden godkände Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-118">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="18833-119">Information om användaren från kundorganisationen som godkände Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-119">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="18833-120">Du måste bland annat:</span><span class="sxs-lookup"><span data-stu-id="18833-120">This includes:</span></span>
  - <span data-ttu-id="18833-121">Förnamn</span><span class="sxs-lookup"><span data-stu-id="18833-121">First name</span></span>
  - <span data-ttu-id="18833-122">Efternamn</span><span class="sxs-lookup"><span data-stu-id="18833-122">Last name</span></span>
  - <span data-ttu-id="18833-123">E-postadress</span><span class="sxs-lookup"><span data-stu-id="18833-123">Email address</span></span>
  - <span data-ttu-id="18833-124">Telefon (valfritt)</span><span class="sxs-lookup"><span data-stu-id="18833-124">Phone number (optional)</span></span>
- <span data-ttu-id="18833-125">Om följande värden ändras för en kund tillåter Partnercenter att ett annat avtal skapas för kunden: Förnamn e-postadress Telefon-nummer Annars får partner följande felkod på grund av att en duplicerad kund skapas</span><span class="sxs-lookup"><span data-stu-id="18833-125">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a><span data-ttu-id="18833-126">.NET</span><span class="sxs-lookup"><span data-stu-id="18833-126">.NET</span></span>

<span data-ttu-id="18833-127">Bekräfta eller bekräfta kundens godkännande av Microsoft-kundavtal:</span><span class="sxs-lookup"><span data-stu-id="18833-127">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="18833-128">Hämta avtalsmetadata för Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-128">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="18833-129">Du måste hämta **templateId för** Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-129">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="18833-130">Mer information finns i Hämta [avtalsmetadata för Microsoft-kundavtal](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="18833-130">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="18833-131">Skapa ett nytt **avtalsobjekt** som innehåller information om bekräftelsen.</span><span class="sxs-lookup"><span data-stu-id="18833-131">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="18833-132">Använd **samlingen IAgreggatePartner.Customers** och anropa **ById-metoden** med det **angivna kund-klient-ID:t**.</span><span class="sxs-lookup"><span data-stu-id="18833-132">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="18833-133">Använd egenskapen **Avtal** följt av anropet **Create** eller **CreateAsync**.</span><span class="sxs-lookup"><span data-stu-id="18833-133">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="18833-134">Ett fullständigt exempel finns i klassen [CreateCustomerAgreement från](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) [konsoltestappprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="18833-134">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="18833-135">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="18833-135">REST request</span></span>

<span data-ttu-id="18833-136">Bekräfta eller bekräfta kundens godkännande av Microsoft-kundavtal:</span><span class="sxs-lookup"><span data-stu-id="18833-136">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="18833-137">Hämta avtalsmetadata för Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-137">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="18833-138">Du måste hämta **templateId för** Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-138">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="18833-139">Mer information finns i Hämta [avtalsmetadata för Microsoft-kundavtal](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="18833-139">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="18833-140">Skapa en ny [ **avtalsresurs**](agreement-resources.md) för att bekräfta att en kund har accepterat Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-140">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="18833-141">Använd följande [REST-begärandesyntax](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="18833-141">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="18833-142">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="18833-142">Request syntax</span></span>

| <span data-ttu-id="18833-143">Metod</span><span class="sxs-lookup"><span data-stu-id="18833-143">Method</span></span> | <span data-ttu-id="18833-144">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="18833-144">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="18833-145">POST</span><span class="sxs-lookup"><span data-stu-id="18833-145">POST</span></span>   | <span data-ttu-id="18833-146">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="18833-146">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="18833-147">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="18833-147">URI parameter</span></span>

<span data-ttu-id="18833-148">Använd följande frågeparameter för att ange den kund som du bekräftar.</span><span class="sxs-lookup"><span data-stu-id="18833-148">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="18833-149">Namn</span><span class="sxs-lookup"><span data-stu-id="18833-149">Name</span></span>               | <span data-ttu-id="18833-150">Typ</span><span class="sxs-lookup"><span data-stu-id="18833-150">Type</span></span> | <span data-ttu-id="18833-151">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="18833-151">Required</span></span> | <span data-ttu-id="18833-152">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="18833-152">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="18833-153">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="18833-153">customer-tenant-id</span></span> | <span data-ttu-id="18833-154">GUID</span><span class="sxs-lookup"><span data-stu-id="18833-154">GUID</span></span> | <span data-ttu-id="18833-155">Ja</span><span class="sxs-lookup"><span data-stu-id="18833-155">Yes</span></span> | <span data-ttu-id="18833-156">Värdet är ett GUID-formaterat **kundklient-id,** vilket är en identifierare som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="18833-156">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="18833-157">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="18833-157">Request headers</span></span>

<span data-ttu-id="18833-158">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="18833-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="18833-159">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="18833-159">Request body</span></span>

<span data-ttu-id="18833-160">I den här tabellen beskrivs de obligatoriska egenskaperna i REST-begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="18833-160">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="18833-161">Namn</span><span class="sxs-lookup"><span data-stu-id="18833-161">Name</span></span>      | <span data-ttu-id="18833-162">Typ</span><span class="sxs-lookup"><span data-stu-id="18833-162">Type</span></span>   | <span data-ttu-id="18833-163">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="18833-163">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="18833-164">Avtal</span><span class="sxs-lookup"><span data-stu-id="18833-164">Agreement</span></span> | <span data-ttu-id="18833-165">objekt</span><span class="sxs-lookup"><span data-stu-id="18833-165">object</span></span> | <span data-ttu-id="18833-166">Information som tillhandahålls av partnern för att bekräfta kundens godkännande av Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-166">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="18833-167">Avtal</span><span class="sxs-lookup"><span data-stu-id="18833-167">Agreement</span></span>

<span data-ttu-id="18833-168">I den här tabellen beskrivs de minsta obligatoriska fälten för att skapa en [ **avtalsresurs**](agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="18833-168">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="18833-169">Egenskap</span><span class="sxs-lookup"><span data-stu-id="18833-169">Property</span></span>       | <span data-ttu-id="18833-170">Typ</span><span class="sxs-lookup"><span data-stu-id="18833-170">Type</span></span>   | <span data-ttu-id="18833-171">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="18833-171">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="18833-172">primaryContact</span><span class="sxs-lookup"><span data-stu-id="18833-172">primaryContact</span></span> | [<span data-ttu-id="18833-173">Kontakt</span><span class="sxs-lookup"><span data-stu-id="18833-173">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="18833-174">Information om användaren från kundorganisationen som godkände Microsoft-kundavtal, inklusive:  **firstName**, **lastName,** **email** och **phoneNumber** (valfritt)</span><span class="sxs-lookup"><span data-stu-id="18833-174">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="18833-175">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="18833-175">dateAgreed</span></span>     | <span data-ttu-id="18833-176">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="18833-176">string in UTC date time format</span></span> |<span data-ttu-id="18833-177">Det datum då kunden godkände avtalet.</span><span class="sxs-lookup"><span data-stu-id="18833-177">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="18833-178">templateId</span><span class="sxs-lookup"><span data-stu-id="18833-178">templateId</span></span>     | <span data-ttu-id="18833-179">sträng</span><span class="sxs-lookup"><span data-stu-id="18833-179">string</span></span> | <span data-ttu-id="18833-180">Unik identifierare för den avtalstyp som accepteras av kunden.</span><span class="sxs-lookup"><span data-stu-id="18833-180">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="18833-181">Du kan hämta **templateId för** Microsoft-kundavtal genom att hämta avtalets metadata för Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-181">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="18833-182">Mer [information finns i Hämta avtalsmetadata Microsoft-kundavtal](./get-customer-agreement-metadata.md) information.</span><span class="sxs-lookup"><span data-stu-id="18833-182">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="18833-183">typ</span><span class="sxs-lookup"><span data-stu-id="18833-183">type</span></span>           | <span data-ttu-id="18833-184">sträng</span><span class="sxs-lookup"><span data-stu-id="18833-184">string</span></span> | <span data-ttu-id="18833-185">Avtalstyp som accepteras av kunden.</span><span class="sxs-lookup"><span data-stu-id="18833-185">Agreement type accepted by the customer.</span></span> <span data-ttu-id="18833-186">Använd "MicrosoftCustomerAgreement" om kunden har accepterat Microsoft-kundavtal.</span><span class="sxs-lookup"><span data-stu-id="18833-186">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="18833-187">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="18833-187">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="18833-188">REST-svar</span><span class="sxs-lookup"><span data-stu-id="18833-188">REST response</span></span>

<span data-ttu-id="18833-189">Om det lyckas returnerar den här metoden en [ **avtalsresurs**](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="18833-189">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="18833-190">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="18833-190">Response success and error codes</span></span>

<span data-ttu-id="18833-191">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="18833-191">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="18833-192">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="18833-192">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="18833-193">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="18833-193">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="18833-194">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="18833-194">Response example</span></span>

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
