---
title: Validera en adress
description: Så här verifierar du en adress med hjälp av API:et för adressverifiering.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14d45977f3af6e8bba1b7cb7f969aa7c5bb671da
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529893"
---
# <a name="validate-an-address"></a><span data-ttu-id="d9011-103">Validera en adress</span><span class="sxs-lookup"><span data-stu-id="d9011-103">Validate an address</span></span>

<span data-ttu-id="d9011-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d9011-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d9011-105">Så här verifierar du en adress med hjälp av API:et för adressverifiering.</span><span class="sxs-lookup"><span data-stu-id="d9011-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="d9011-106">API:et för adressvalidering bör endast användas för förvalidering av kundprofiluppdateringar.</span><span class="sxs-lookup"><span data-stu-id="d9011-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="d9011-107">Använd det med förståelsen att om landet är USA, Kanada, Kina eller Mexiko verifieras fältet Delstat mot en lista över giltiga delstater för respektive land.</span><span class="sxs-lookup"><span data-stu-id="d9011-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="d9011-108">I alla andra länder utförs inte det här testet och API:et kontrollerar endast att tillståndet är en giltig sträng.</span><span class="sxs-lookup"><span data-stu-id="d9011-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9011-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d9011-109">Prerequisites</span></span>

<span data-ttu-id="d9011-110">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d9011-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d9011-111">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d9011-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d9011-112">C\#</span><span class="sxs-lookup"><span data-stu-id="d9011-112">C\#</span></span>

<span data-ttu-id="d9011-113">Verifiera en adress genom att först skapa en instans av ett **nytt address-objekt** och fylla i den med adressen som ska verifieras.</span><span class="sxs-lookup"><span data-stu-id="d9011-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="d9011-114">Hämta sedan ett gränssnitt till **valideringsåtgärder** från **egenskapen IAggregatePartner.Validations** och anropa **metoden IsAddressValid** med adressobjektet.</span><span class="sxs-lookup"><span data-stu-id="d9011-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

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
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";

    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);

    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

## <a name="java"></a><span data-ttu-id="d9011-115">Java</span><span class="sxs-lookup"><span data-stu-id="d9011-115">Java</span></span>

<span data-ttu-id="d9011-116">Verifiera en adress genom att först skapa en instans av ett **nytt address-objekt** och fylla i den med adressen som ska verifieras.</span><span class="sxs-lookup"><span data-stu-id="d9011-116">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="d9011-117">Hämta sedan ett gränssnitt till **valideringsåtgärder** från **funktionen IAggregatePartner.getValidations** och anropa **metoden isAddressValid** med adressobjektet.</span><span class="sxs-lookup"><span data-stu-id="d9011-117">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");

    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

## <a name="powershell"></a><span data-ttu-id="d9011-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9011-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="d9011-119">Verifiera en adress genom att köra [**Test-PartnerAddress med**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) adressparametrarna ifyllda.</span><span class="sxs-lookup"><span data-stu-id="d9011-119">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="d9011-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d9011-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d9011-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="d9011-121">Request syntax</span></span>

| <span data-ttu-id="d9011-122">Metod</span><span class="sxs-lookup"><span data-stu-id="d9011-122">Method</span></span>   | <span data-ttu-id="d9011-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d9011-123">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="d9011-124">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="d9011-124">**POST**</span></span> | <span data-ttu-id="d9011-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d9011-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d9011-126">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d9011-126">Request headers</span></span>

<span data-ttu-id="d9011-127">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d9011-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d9011-128">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d9011-128">Request body</span></span>

<span data-ttu-id="d9011-129">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="d9011-129">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="d9011-130">Namn</span><span class="sxs-lookup"><span data-stu-id="d9011-130">Name</span></span>         | <span data-ttu-id="d9011-131">Typ</span><span class="sxs-lookup"><span data-stu-id="d9011-131">Type</span></span>   | <span data-ttu-id="d9011-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d9011-132">Required</span></span> | <span data-ttu-id="d9011-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d9011-133">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="d9011-134">addressline1</span><span class="sxs-lookup"><span data-stu-id="d9011-134">addressline1</span></span> | <span data-ttu-id="d9011-135">sträng</span><span class="sxs-lookup"><span data-stu-id="d9011-135">string</span></span> | <span data-ttu-id="d9011-136">Y</span><span class="sxs-lookup"><span data-stu-id="d9011-136">Y</span></span>        | <span data-ttu-id="d9011-137">Den första raden i adressen.</span><span class="sxs-lookup"><span data-stu-id="d9011-137">The first line of the address.</span></span>                             |
| <span data-ttu-id="d9011-138">addressline2</span><span class="sxs-lookup"><span data-stu-id="d9011-138">addressline2</span></span> | <span data-ttu-id="d9011-139">sträng</span><span class="sxs-lookup"><span data-stu-id="d9011-139">string</span></span> | <span data-ttu-id="d9011-140">N</span><span class="sxs-lookup"><span data-stu-id="d9011-140">N</span></span>        | <span data-ttu-id="d9011-141">Den andra raden i adressen.</span><span class="sxs-lookup"><span data-stu-id="d9011-141">The second line of the address.</span></span> <span data-ttu-id="d9011-142">Den här egenskapen är valfri.</span><span class="sxs-lookup"><span data-stu-id="d9011-142">This property is optional.</span></span> |
| <span data-ttu-id="d9011-143">city</span><span class="sxs-lookup"><span data-stu-id="d9011-143">city</span></span>         | <span data-ttu-id="d9011-144">sträng</span><span class="sxs-lookup"><span data-stu-id="d9011-144">string</span></span> | <span data-ttu-id="d9011-145">Y</span><span class="sxs-lookup"><span data-stu-id="d9011-145">Y</span></span>        | <span data-ttu-id="d9011-146">Staden.</span><span class="sxs-lookup"><span data-stu-id="d9011-146">The city.</span></span>                                                  |
| <span data-ttu-id="d9011-147">state</span><span class="sxs-lookup"><span data-stu-id="d9011-147">state</span></span>        | <span data-ttu-id="d9011-148">sträng</span><span class="sxs-lookup"><span data-stu-id="d9011-148">string</span></span> | <span data-ttu-id="d9011-149">Y</span><span class="sxs-lookup"><span data-stu-id="d9011-149">Y</span></span>        | <span data-ttu-id="d9011-150">Tillståndet.</span><span class="sxs-lookup"><span data-stu-id="d9011-150">The state.</span></span>                                                 |
| <span data-ttu-id="d9011-151">Postnummer</span><span class="sxs-lookup"><span data-stu-id="d9011-151">postalcode</span></span>   | <span data-ttu-id="d9011-152">sträng</span><span class="sxs-lookup"><span data-stu-id="d9011-152">string</span></span> | <span data-ttu-id="d9011-153">Y</span><span class="sxs-lookup"><span data-stu-id="d9011-153">Y</span></span>        | <span data-ttu-id="d9011-154">Postnumret.</span><span class="sxs-lookup"><span data-stu-id="d9011-154">The postal code.</span></span>                                           |
| <span data-ttu-id="d9011-155">land</span><span class="sxs-lookup"><span data-stu-id="d9011-155">country</span></span>      | <span data-ttu-id="d9011-156">sträng</span><span class="sxs-lookup"><span data-stu-id="d9011-156">string</span></span> | <span data-ttu-id="d9011-157">Y</span><span class="sxs-lookup"><span data-stu-id="d9011-157">Y</span></span>        | <span data-ttu-id="d9011-158">Landskoden ISO alpha-2 med två tecken.</span><span class="sxs-lookup"><span data-stu-id="d9011-158">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="d9011-159">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d9011-159">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    "AddressLine1": "One Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="d9011-160">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d9011-160">REST response</span></span>

<span data-ttu-id="d9011-161">Om det lyckas returnerar metoden statuskoden 200 enligt exemplet Svar – valideringen lyckades som visas nedan.</span><span class="sxs-lookup"><span data-stu-id="d9011-161">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="d9011-162">Om begäran misslyckas returnerar metoden statuskoden 400 enligt exemplet Svar – verifieringen misslyckades som visas nedan.</span><span class="sxs-lookup"><span data-stu-id="d9011-162">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="d9011-163">Svarstexten innehåller en JSON-nyttolast med ytterligare information om felet.</span><span class="sxs-lookup"><span data-stu-id="d9011-163">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d9011-164">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d9011-164">Response success and error codes</span></span>

<span data-ttu-id="d9011-165">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="d9011-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d9011-166">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d9011-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d9011-167">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d9011-167">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="d9011-168">Svar – exempel på att valideringen lyckades</span><span class="sxs-lookup"><span data-stu-id="d9011-168">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="d9011-169">Svar – exempel på misslyckad validering</span><span class="sxs-lookup"><span data-stu-id="d9011-169">Response - validation failed example</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```
