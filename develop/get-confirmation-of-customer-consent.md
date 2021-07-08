---
title: Få bekräftelse på kundgodkännande av Microsoft Cloud-avtal
description: Den här artikeln förklarar hur du får en bekräftelse på kundens godkännande av Microsoft Cloud-avtal.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: 1b1a8cbacb667e579bcd218a29c3f553afce26c2
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549271"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="7da13-103">Få bekräftelse på kundgodkännande av Microsoft Cloud-avtal</span><span class="sxs-lookup"><span data-stu-id="7da13-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="7da13-104">**Gäller för:** Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7da13-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="7da13-105">**Gäller inte för:** Partner Center som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7da13-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7da13-106">**Avtalsresursen** stöds för närvarande endast av Partnercenter i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="7da13-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7da13-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7da13-107">Prerequisites</span></span>

- <span data-ttu-id="7da13-108">Om du använder Partner Center .NET SDK krävs version 1.9 eller senare.</span><span class="sxs-lookup"><span data-stu-id="7da13-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="7da13-109">Om du använder Partner Center Java SDK krävs version 1.8 eller senare.</span><span class="sxs-lookup"><span data-stu-id="7da13-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="7da13-110">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7da13-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="7da13-111">Det här scenariot stöder endast app - och användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="7da13-111">This scenario only supports app + user authentication.</span></span>

- <span data-ttu-id="7da13-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7da13-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7da13-113">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="7da13-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7da13-114">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="7da13-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7da13-115">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="7da13-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7da13-116">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="7da13-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7da13-117">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7da13-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="7da13-118">.NET (version 1.4 eller senare)</span><span class="sxs-lookup"><span data-stu-id="7da13-118">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="7da13-119">Så här hämtar du bekräftelser av kundgodkännande som tidigare har angetts:</span><span class="sxs-lookup"><span data-stu-id="7da13-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="7da13-120">Använd samlingen **IAggregatePartner.Customers och** anropa **ById-metoden** med den angivna kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="7da13-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="7da13-121">Hämta egenskapen **Agreements** och filtrera resultaten för att Microsoft Cloud-avtal **byAgreementType-metoden.**</span><span class="sxs-lookup"><span data-stu-id="7da13-121">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="7da13-122">Anropa **Get-** eller **GetAsync-metoden.**</span><span class="sxs-lookup"><span data-stu-id="7da13-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="7da13-123">Ett komplett exempel finns i klassen [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="7da13-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="7da13-124">.NET (version 1.9–1.13)</span><span class="sxs-lookup"><span data-stu-id="7da13-124">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="7da13-125">Så här hämtar du bekräftelse på kundgodkännande som angavs tidigare:</span><span class="sxs-lookup"><span data-stu-id="7da13-125">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="7da13-126">Använd **samlingen IAggregatePartner.Customers** och anropa **ById-metoden** med den angivna kundens identifierare.</span><span class="sxs-lookup"><span data-stu-id="7da13-126">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="7da13-127">Hämta sedan egenskapen **Avtal följt** av anrop till **get- eller** **GetAsync-metoderna.**</span><span class="sxs-lookup"><span data-stu-id="7da13-127">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="7da13-128">Java</span><span class="sxs-lookup"><span data-stu-id="7da13-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="7da13-129">Så här hämtar du bekräftelse på kundgodkännande som angavs tidigare:</span><span class="sxs-lookup"><span data-stu-id="7da13-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="7da13-130">Använd funktionen **IAggregatePartner.getCustomers** och anropa **byId-funktionen** med den angivna kundens identifierare.</span><span class="sxs-lookup"><span data-stu-id="7da13-130">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="7da13-131">Hämta sedan funktionen **getAgreements** följt av att anropa **get-funktionen.**</span><span class="sxs-lookup"><span data-stu-id="7da13-131">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="7da13-132">Ett komplett exempel finns i klassen [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) från [konsoltestappsprojektet.](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="7da13-132">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="7da13-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7da13-133">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="7da13-134">Så här hämtar du bekräftelse på kundgodkännande som angavs tidigare:</span><span class="sxs-lookup"><span data-stu-id="7da13-134">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="7da13-135">Använd kommandot [**Get-PartnerCustomerAgreement.**](/powershell/module/partnercenter/get-partnercustomeragreement)</span><span class="sxs-lookup"><span data-stu-id="7da13-135">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="7da13-136">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7da13-136">REST request</span></span>

<span data-ttu-id="7da13-137">Information om hur du hämtar bekräftelse på kundgodkännande som angavs tidigare finns i följande anvisningar.</span><span class="sxs-lookup"><span data-stu-id="7da13-137">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="7da13-138">Skapa en ny **avtalsresurs** med relevant certifieringsinformation.</span><span class="sxs-lookup"><span data-stu-id="7da13-138">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7da13-139">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="7da13-139">Request syntax</span></span>

| <span data-ttu-id="7da13-140">Metod</span><span class="sxs-lookup"><span data-stu-id="7da13-140">Method</span></span> | <span data-ttu-id="7da13-141">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7da13-141">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7da13-142">GET</span><span class="sxs-lookup"><span data-stu-id="7da13-142">GET</span></span>    | <span data-ttu-id="7da13-143">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7da13-143">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="7da13-144">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="7da13-144">URI parameter</span></span>

<span data-ttu-id="7da13-145">Använd följande frågeparameter för att ange den kund som du bekräftar.</span><span class="sxs-lookup"><span data-stu-id="7da13-145">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="7da13-146">Namn</span><span class="sxs-lookup"><span data-stu-id="7da13-146">Name</span></span>             | <span data-ttu-id="7da13-147">Typ</span><span class="sxs-lookup"><span data-stu-id="7da13-147">Type</span></span> | <span data-ttu-id="7da13-148">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7da13-148">Required</span></span> | <span data-ttu-id="7da13-149">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7da13-149">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="7da13-150">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="7da13-150">CustomerTenantId</span></span> | <span data-ttu-id="7da13-151">GUID</span><span class="sxs-lookup"><span data-stu-id="7da13-151">GUID</span></span> | <span data-ttu-id="7da13-152">Y</span><span class="sxs-lookup"><span data-stu-id="7da13-152">Y</span></span>        | <span data-ttu-id="7da13-153">Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="7da13-153">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7da13-154">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7da13-154">Request headers</span></span>

<span data-ttu-id="7da13-155">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7da13-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7da13-156">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7da13-156">Request body</span></span>

<span data-ttu-id="7da13-157">Inga.</span><span class="sxs-lookup"><span data-stu-id="7da13-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7da13-158">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7da13-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="7da13-159">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7da13-159">REST response</span></span>

<span data-ttu-id="7da13-160">Om det lyckas returnerar den här metoden en samling **avtalsresurser** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="7da13-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7da13-161">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7da13-161">Response success and error codes</span></span>

<span data-ttu-id="7da13-162">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="7da13-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7da13-163">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7da13-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7da13-164">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7da13-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7da13-165">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7da13-165">Response example</span></span>

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
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
