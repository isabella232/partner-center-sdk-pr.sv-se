---
title: Validera en adress
description: Så här verifierar du en adress med hjälp av API:et för adressverifiering.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2eeca91b0e5a507dac6df4ecf61a56aed2d2d921
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572088"
---
# <a name="validate-an-address"></a><span data-ttu-id="faae1-103">Validera en adress</span><span class="sxs-lookup"><span data-stu-id="faae1-103">Validate an address</span></span>

<span data-ttu-id="faae1-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="faae1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="faae1-105">Så här verifierar du en adress med hjälp av API:et för adressverifiering.</span><span class="sxs-lookup"><span data-stu-id="faae1-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="faae1-106">API:et för adressvalidering bör endast användas för förvalidering av kundprofiluppdateringar.</span><span class="sxs-lookup"><span data-stu-id="faae1-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="faae1-107">Använd det med förståelsen att om landet är USA, Kanada, Kina eller Mexiko verifieras fältet Delstat mot en lista över giltiga delstater för respektive land.</span><span class="sxs-lookup"><span data-stu-id="faae1-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="faae1-108">I alla andra länder utförs inte det här testet och API:et kontrollerar endast att tillståndet är en giltig sträng.</span><span class="sxs-lookup"><span data-stu-id="faae1-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faae1-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="faae1-109">Prerequisites</span></span>

<span data-ttu-id="faae1-110">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="faae1-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="faae1-111">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="faae1-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="faae1-112">C\#</span><span class="sxs-lookup"><span data-stu-id="faae1-112">C\#</span></span>

<span data-ttu-id="faae1-113">Verifiera en adress genom att först skapa en instans av ett **nytt address-objekt** och fylla i den med adressen som ska verifieras.</span><span class="sxs-lookup"><span data-stu-id="faae1-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="faae1-114">Hämta sedan ett gränssnitt till **valideringsåtgärder** från **egenskapen IAggregatePartner.Validations** och anropa **metoden IsAddressValid** med adressobjektet.</span><span class="sxs-lookup"><span data-stu-id="faae1-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",
    Country = "US"
};

// Validate the address.
AddressValidationResponse result = partnerOperations.Validations.IsAddressValid(address);

// If the request completes successfully, you can inspect the response object.

// See the status of the validation.
Console.WriteLine($"Status: {addressValidationResult.Status}");

// See the validation message returned.
Console.WriteLine($"Validation Message Returned: {addressValidationResult.ValidationMessage ?? "No message returned."}");

// See the original address submitted for validation.
Console.WriteLine($"Original Address:\n{this.DisplayAddress(addressValidationResult.OriginalAddress)}");

// See the suggested addresses returned by the API, if any exist.
Console.WriteLine($"Suggested Addresses Returned: {addressValidationResult.SuggestedAddresses?.Count ?? "None."}");

if (addressValidationResult.SuggestedAddresses != null && addressValidationResult.SuggestedAddresses.Any())
{
    addressValidationResult.SuggestedAddresses.ForEach(a => Console.WriteLine(this.DisplayAddress(a)));
}

// Helper method to pretty-print an Address object.
private string DisplayAddress(Address address)
{
    StringBuilder sb = new StringBuilder();

    foreach (var property in address.GetType().GetProperties())
    {
        sb.AppendLine($"{property.Name}: {property.GetValue(address) ?? "None to Display."}");
    }

    return sb.ToString();
}
```

## <a name="rest-request"></a><span data-ttu-id="faae1-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="faae1-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="faae1-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="faae1-116">Request syntax</span></span>

| <span data-ttu-id="faae1-117">Metod</span><span class="sxs-lookup"><span data-stu-id="faae1-117">Method</span></span>   | <span data-ttu-id="faae1-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="faae1-118">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="faae1-119">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="faae1-119">**POST**</span></span> | <span data-ttu-id="faae1-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="faae1-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="faae1-121">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="faae1-121">Request headers</span></span>

<span data-ttu-id="faae1-122">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="faae1-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="faae1-123">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="faae1-123">Request body</span></span>

<span data-ttu-id="faae1-124">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="faae1-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="faae1-125">Namn</span><span class="sxs-lookup"><span data-stu-id="faae1-125">Name</span></span>         | <span data-ttu-id="faae1-126">Typ</span><span class="sxs-lookup"><span data-stu-id="faae1-126">Type</span></span>   | <span data-ttu-id="faae1-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="faae1-127">Required</span></span> | <span data-ttu-id="faae1-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="faae1-128">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="faae1-129">addressline1</span><span class="sxs-lookup"><span data-stu-id="faae1-129">addressline1</span></span> | <span data-ttu-id="faae1-130">sträng</span><span class="sxs-lookup"><span data-stu-id="faae1-130">string</span></span> | <span data-ttu-id="faae1-131">Y</span><span class="sxs-lookup"><span data-stu-id="faae1-131">Y</span></span>        | <span data-ttu-id="faae1-132">Den första raden i adressen.</span><span class="sxs-lookup"><span data-stu-id="faae1-132">The first line of the address.</span></span>                             |
| <span data-ttu-id="faae1-133">addressline2</span><span class="sxs-lookup"><span data-stu-id="faae1-133">addressline2</span></span> | <span data-ttu-id="faae1-134">sträng</span><span class="sxs-lookup"><span data-stu-id="faae1-134">string</span></span> | <span data-ttu-id="faae1-135">N</span><span class="sxs-lookup"><span data-stu-id="faae1-135">N</span></span>        | <span data-ttu-id="faae1-136">Den andra raden i adressen.</span><span class="sxs-lookup"><span data-stu-id="faae1-136">The second line of the address.</span></span> <span data-ttu-id="faae1-137">Den här egenskapen är valfri.</span><span class="sxs-lookup"><span data-stu-id="faae1-137">This property is optional.</span></span> |
| <span data-ttu-id="faae1-138">city</span><span class="sxs-lookup"><span data-stu-id="faae1-138">city</span></span>         | <span data-ttu-id="faae1-139">sträng</span><span class="sxs-lookup"><span data-stu-id="faae1-139">string</span></span> | <span data-ttu-id="faae1-140">Y</span><span class="sxs-lookup"><span data-stu-id="faae1-140">Y</span></span>        | <span data-ttu-id="faae1-141">Staden.</span><span class="sxs-lookup"><span data-stu-id="faae1-141">The city.</span></span>                                                  |
| <span data-ttu-id="faae1-142">state</span><span class="sxs-lookup"><span data-stu-id="faae1-142">state</span></span>        | <span data-ttu-id="faae1-143">sträng</span><span class="sxs-lookup"><span data-stu-id="faae1-143">string</span></span> | <span data-ttu-id="faae1-144">Y</span><span class="sxs-lookup"><span data-stu-id="faae1-144">Y</span></span>        | <span data-ttu-id="faae1-145">Tillståndet.</span><span class="sxs-lookup"><span data-stu-id="faae1-145">The state.</span></span>                                                 |
| <span data-ttu-id="faae1-146">Postnummer</span><span class="sxs-lookup"><span data-stu-id="faae1-146">postalcode</span></span>   | <span data-ttu-id="faae1-147">sträng</span><span class="sxs-lookup"><span data-stu-id="faae1-147">string</span></span> | <span data-ttu-id="faae1-148">Y</span><span class="sxs-lookup"><span data-stu-id="faae1-148">Y</span></span>        | <span data-ttu-id="faae1-149">Postnumret.</span><span class="sxs-lookup"><span data-stu-id="faae1-149">The postal code.</span></span>                                           |
| <span data-ttu-id="faae1-150">land</span><span class="sxs-lookup"><span data-stu-id="faae1-150">country</span></span>      | <span data-ttu-id="faae1-151">sträng</span><span class="sxs-lookup"><span data-stu-id="faae1-151">string</span></span> | <span data-ttu-id="faae1-152">Y</span><span class="sxs-lookup"><span data-stu-id="faae1-152">Y</span></span>        | <span data-ttu-id="faae1-153">Landskoden ISO alpha-2 med två tecken.</span><span class="sxs-lookup"><span data-stu-id="faae1-153">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="response-details"></a><span data-ttu-id="faae1-154">Svarsinformation</span><span class="sxs-lookup"><span data-stu-id="faae1-154">Response details</span></span>

<span data-ttu-id="faae1-155">Svaret returnerar något av följande statusmeddelanden:</span><span class="sxs-lookup"><span data-stu-id="faae1-155">The response will return one of the following status messages:</span></span>

| <span data-ttu-id="faae1-156">Status</span><span class="sxs-lookup"><span data-stu-id="faae1-156">Status</span></span>     | <span data-ttu-id="faae1-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="faae1-157">Description</span></span> |    <span data-ttu-id="faae1-158">Antal föreslagna adresser som returneras</span><span class="sxs-lookup"><span data-stu-id="faae1-158">Number of suggested addresses returned</span></span> |
|-------|---------------|-------------------|
|<span data-ttu-id="faae1-159">Verifierad leverans</span><span class="sxs-lookup"><span data-stu-id="faae1-159">Verified shippable</span></span> | <span data-ttu-id="faae1-160">Adressen är verifierad och kan skickas till.</span><span class="sxs-lookup"><span data-stu-id="faae1-160">Address is verified and can be shipped to.</span></span> | <span data-ttu-id="faae1-161">Enkel</span><span class="sxs-lookup"><span data-stu-id="faae1-161">Single</span></span> |
|<span data-ttu-id="faae1-162">Verifierat</span><span class="sxs-lookup"><span data-stu-id="faae1-162">Verified</span></span> | <span data-ttu-id="faae1-163">Adressen är verifierad.</span><span class="sxs-lookup"><span data-stu-id="faae1-163">Address is verified.</span></span> | <span data-ttu-id="faae1-164">Enkel</span><span class="sxs-lookup"><span data-stu-id="faae1-164">Single</span></span> |
|<span data-ttu-id="faae1-165">Interaktion krävs</span><span class="sxs-lookup"><span data-stu-id="faae1-165">Interaction required</span></span> | <span data-ttu-id="faae1-166">Den föreslagna adressen har ändrats avsevärt och kräver användarbekräftelse.</span><span class="sxs-lookup"><span data-stu-id="faae1-166">Suggested address has been changed significantly and needs user confirmation.</span></span> | <span data-ttu-id="faae1-167">Enkel</span><span class="sxs-lookup"><span data-stu-id="faae1-167">Single</span></span> |
|<span data-ttu-id="faae1-168">Partiell gatuadress</span><span class="sxs-lookup"><span data-stu-id="faae1-168">Street partial</span></span> | <span data-ttu-id="faae1-169">Den angivna gatuadressen är delvis och behöver mer information.</span><span class="sxs-lookup"><span data-stu-id="faae1-169">The given street in the address is partial and needs more info.</span></span> | <span data-ttu-id="faae1-170">Flera – högst tre</span><span class="sxs-lookup"><span data-stu-id="faae1-170">Multiple—maximum of three</span></span> |
|<span data-ttu-id="faae1-171">Delvis lokal</span><span class="sxs-lookup"><span data-stu-id="faae1-171">Premises partial</span></span> | <span data-ttu-id="faae1-172">De angivna lokalerna (byggnadsnummer, svitnummer och andra) är ofullständiga och behöver mer information.</span><span class="sxs-lookup"><span data-stu-id="faae1-172">The given premises (building number, suite number, and others) are partial and need more info.</span></span> | <span data-ttu-id="faae1-173">Flera – högst tre</span><span class="sxs-lookup"><span data-stu-id="faae1-173">Multiple—maximum of three</span></span> |
|<span data-ttu-id="faae1-174">Flera</span><span class="sxs-lookup"><span data-stu-id="faae1-174">Multiple</span></span> | <span data-ttu-id="faae1-175">Det finns flera fält som är partiella i adressen (inklusive delvis gatuadress och delvis lokal).</span><span class="sxs-lookup"><span data-stu-id="faae1-175">There are multiple fields that are partial in the address (potentially also including street partial and premises partial).</span></span> | <span data-ttu-id="faae1-176">Flera – högst tre</span><span class="sxs-lookup"><span data-stu-id="faae1-176">Multiple—maximum of three</span></span> |
|<span data-ttu-id="faae1-177">Ingen</span><span class="sxs-lookup"><span data-stu-id="faae1-177">None</span></span> | <span data-ttu-id="faae1-178">Adressen är felaktig.</span><span class="sxs-lookup"><span data-stu-id="faae1-178">Address is incorrect.</span></span> | <span data-ttu-id="faae1-179">Ingen</span><span class="sxs-lookup"><span data-stu-id="faae1-179">None</span></span> |
|<span data-ttu-id="faae1-180">Inte validerat</span><span class="sxs-lookup"><span data-stu-id="faae1-180">Not validated</span></span> | <span data-ttu-id="faae1-181">Adressen kunde inte skickas via verifieringsprocessen.</span><span class="sxs-lookup"><span data-stu-id="faae1-181">Address was not able to be sent through the validation process.</span></span> | <span data-ttu-id="faae1-182">Ingen</span><span class="sxs-lookup"><span data-stu-id="faae1-182">None</span></span> |

### <a name="request-example"></a><span data-ttu-id="faae1-183">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="faae1-183">Request example</span></span>

```http
# "VerifiedShippable" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
Host: api.partnercenter.microsoft.com
Content-Length: 137
X-Locale: en-US

{
    "AddressLine1": "1 Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}

# "StreetPartial" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
Host: api.partnercenter.microsoft.com
Content-Length: 135
X-Locale: en-US

{
    "AddressLine1": "Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="faae1-184">REST-svar</span><span class="sxs-lookup"><span data-stu-id="faae1-184">REST response</span></span>

<span data-ttu-id="faae1-185">Om det lyckas returnerar metoden ett **AddressValidationResponse-objekt** i svarstexten med en **HTTP 200-statuskod.**</span><span class="sxs-lookup"><span data-stu-id="faae1-185">If successful, the method returns an **AddressValidationResponse** object in the response body, with a **HTTP 200** status code.</span></span> <span data-ttu-id="faae1-186">Ett exempel på detta visas nedan.</span><span class="sxs-lookup"><span data-stu-id="faae1-186">An example is shown below.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="faae1-187">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="faae1-187">Response success and error codes</span></span>

<span data-ttu-id="faae1-188">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="faae1-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="faae1-189">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="faae1-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="faae1-190">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="faae1-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="faae1-191">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="faae1-191">Response example</span></span>

```http
# "VerifiedShippable" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:19:19 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-8300"
        }
    ],
    "status": "VerifiedShippable"
}

# "StreetPartial" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:34:08 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-6399"
        }
    ],
    "status": "StreetPartial",
    "validationMessage": "Address field invalid for property: 'Region', 'PostalCode', 'City'"
}
```
