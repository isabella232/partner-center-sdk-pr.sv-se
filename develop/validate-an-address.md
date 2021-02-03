---
title: Validera en adress
description: Verifiera en adress med hjälp av API för adress validering.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 22d5faec2fdab4907067bb01cb74e110032dea9a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768931"
---
# <a name="validate-an-address"></a><span data-ttu-id="22463-103">Validera en adress</span><span class="sxs-lookup"><span data-stu-id="22463-103">Validate an address</span></span>

<span data-ttu-id="22463-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="22463-104">**Applies To**</span></span>

- <span data-ttu-id="22463-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="22463-105">Partner Center</span></span>
- <span data-ttu-id="22463-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="22463-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="22463-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="22463-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="22463-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="22463-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="22463-109">Verifiera en adress med hjälp av API för adress validering.</span><span class="sxs-lookup"><span data-stu-id="22463-109">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="22463-110">Adress verifierings-API: t bör endast användas för för validering av kund profil uppdateringar.</span><span class="sxs-lookup"><span data-stu-id="22463-110">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="22463-111">Använd det för att förstå att om landet är USA, Kanada, Kina eller Mexiko, verifieras fältet Delstat mot en lista över giltiga tillstånd för respektive land.</span><span class="sxs-lookup"><span data-stu-id="22463-111">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="22463-112">I alla andra länder sker inte det här testet, och API: et kontrollerar att tillstånd är en giltig sträng.</span><span class="sxs-lookup"><span data-stu-id="22463-112">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22463-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="22463-113">Prerequisites</span></span>

<span data-ttu-id="22463-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="22463-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="22463-115">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="22463-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="22463-116">C\#</span><span class="sxs-lookup"><span data-stu-id="22463-116">C\#</span></span>

<span data-ttu-id="22463-117">Om du vill verifiera en adress måste du först instansiera ett nytt **adress** objekt och fylla det med den adress som ska verifieras.</span><span class="sxs-lookup"><span data-stu-id="22463-117">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="22463-118">Hämta sedan ett gränssnitt till **validerings** åtgärder från egenskapen **IAggregatePartner.** Recalls och anropa **IsAddressValid** -metoden med objektet address.</span><span class="sxs-lookup"><span data-stu-id="22463-118">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="java"></a><span data-ttu-id="22463-119">Java</span><span class="sxs-lookup"><span data-stu-id="22463-119">Java</span></span>

<span data-ttu-id="22463-120">Om du vill verifiera en adress måste du först instansiera ett nytt **adress** objekt och fylla det med den adress som ska verifieras.</span><span class="sxs-lookup"><span data-stu-id="22463-120">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="22463-121">Hämta sedan ett gränssnitt till **validerings** åtgärder från funktionen **IAggregatePartner. GetValidations** och anropa **isAddressValid** -metoden med objektet address.</span><span class="sxs-lookup"><span data-stu-id="22463-121">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="22463-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22463-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="22463-123">Verifiera en adress genom att köra [**testet-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) med adress parametrarna ifyllda.</span><span class="sxs-lookup"><span data-stu-id="22463-123">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="22463-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="22463-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="22463-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="22463-125">Request syntax</span></span>

| <span data-ttu-id="22463-126">Metod</span><span class="sxs-lookup"><span data-stu-id="22463-126">Method</span></span>   | <span data-ttu-id="22463-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="22463-127">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="22463-128">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="22463-128">**POST**</span></span> | <span data-ttu-id="22463-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/Address http/1.1</span><span class="sxs-lookup"><span data-stu-id="22463-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="22463-130">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="22463-130">Request headers</span></span>

<span data-ttu-id="22463-131">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="22463-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="22463-132">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="22463-132">Request body</span></span>

<span data-ttu-id="22463-133">I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="22463-133">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="22463-134">Namn</span><span class="sxs-lookup"><span data-stu-id="22463-134">Name</span></span>         | <span data-ttu-id="22463-135">Typ</span><span class="sxs-lookup"><span data-stu-id="22463-135">Type</span></span>   | <span data-ttu-id="22463-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="22463-136">Required</span></span> | <span data-ttu-id="22463-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="22463-137">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="22463-138">addressline1</span><span class="sxs-lookup"><span data-stu-id="22463-138">addressline1</span></span> | <span data-ttu-id="22463-139">sträng</span><span class="sxs-lookup"><span data-stu-id="22463-139">string</span></span> | <span data-ttu-id="22463-140">Y</span><span class="sxs-lookup"><span data-stu-id="22463-140">Y</span></span>        | <span data-ttu-id="22463-141">Den första raden i adressen.</span><span class="sxs-lookup"><span data-stu-id="22463-141">The first line of the address.</span></span>                             |
| <span data-ttu-id="22463-142">addressline2</span><span class="sxs-lookup"><span data-stu-id="22463-142">addressline2</span></span> | <span data-ttu-id="22463-143">sträng</span><span class="sxs-lookup"><span data-stu-id="22463-143">string</span></span> | <span data-ttu-id="22463-144">N</span><span class="sxs-lookup"><span data-stu-id="22463-144">N</span></span>        | <span data-ttu-id="22463-145">Den andra raden i adressen.</span><span class="sxs-lookup"><span data-stu-id="22463-145">The second line of the address.</span></span> <span data-ttu-id="22463-146">Den här egenskapen är valfri.</span><span class="sxs-lookup"><span data-stu-id="22463-146">This property is optional.</span></span> |
| <span data-ttu-id="22463-147">city</span><span class="sxs-lookup"><span data-stu-id="22463-147">city</span></span>         | <span data-ttu-id="22463-148">sträng</span><span class="sxs-lookup"><span data-stu-id="22463-148">string</span></span> | <span data-ttu-id="22463-149">Y</span><span class="sxs-lookup"><span data-stu-id="22463-149">Y</span></span>        | <span data-ttu-id="22463-150">Staden.</span><span class="sxs-lookup"><span data-stu-id="22463-150">The city.</span></span>                                                  |
| <span data-ttu-id="22463-151">state</span><span class="sxs-lookup"><span data-stu-id="22463-151">state</span></span>        | <span data-ttu-id="22463-152">sträng</span><span class="sxs-lookup"><span data-stu-id="22463-152">string</span></span> | <span data-ttu-id="22463-153">Y</span><span class="sxs-lookup"><span data-stu-id="22463-153">Y</span></span>        | <span data-ttu-id="22463-154">Status.</span><span class="sxs-lookup"><span data-stu-id="22463-154">The state.</span></span>                                                 |
| <span data-ttu-id="22463-155">post nummer</span><span class="sxs-lookup"><span data-stu-id="22463-155">postalcode</span></span>   | <span data-ttu-id="22463-156">sträng</span><span class="sxs-lookup"><span data-stu-id="22463-156">string</span></span> | <span data-ttu-id="22463-157">Y</span><span class="sxs-lookup"><span data-stu-id="22463-157">Y</span></span>        | <span data-ttu-id="22463-158">Post numret.</span><span class="sxs-lookup"><span data-stu-id="22463-158">The postal code.</span></span>                                           |
| <span data-ttu-id="22463-159">land</span><span class="sxs-lookup"><span data-stu-id="22463-159">country</span></span>      | <span data-ttu-id="22463-160">sträng</span><span class="sxs-lookup"><span data-stu-id="22463-160">string</span></span> | <span data-ttu-id="22463-161">Y</span><span class="sxs-lookup"><span data-stu-id="22463-161">Y</span></span>        | <span data-ttu-id="22463-162">ISO alpha-2-lands koden med två tecken.</span><span class="sxs-lookup"><span data-stu-id="22463-162">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="22463-163">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="22463-163">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="22463-164">REST-svar</span><span class="sxs-lookup"><span data-stu-id="22463-164">REST response</span></span>

<span data-ttu-id="22463-165">Om det lyckas returnerar metoden en status kod 200 som visas i exemplet svars valideringen lyckades nedan.</span><span class="sxs-lookup"><span data-stu-id="22463-165">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="22463-166">Om begäran Miss lyckas returnerar metoden en status kod 400 som visas i exemplet på svars valideringen som visas nedan.</span><span class="sxs-lookup"><span data-stu-id="22463-166">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="22463-167">Svars texten innehåller en JSON-nyttolast med ytterligare information om felet.</span><span class="sxs-lookup"><span data-stu-id="22463-167">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="22463-168">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="22463-168">Response success and error codes</span></span>

<span data-ttu-id="22463-169">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="22463-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="22463-170">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="22463-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="22463-171">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="22463-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="22463-172">Svars validering lyckades, exempel</span><span class="sxs-lookup"><span data-stu-id="22463-172">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="22463-173">Svar – validering misslyckades, exempel</span><span class="sxs-lookup"><span data-stu-id="22463-173">Response - validation failed example</span></span>

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
