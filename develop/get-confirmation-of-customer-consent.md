---
title: Få bekräftelse på kundgodkännande av Microsoft Cloud-avtal
description: I den här artikeln förklaras hur du får bekräftelse på kund godkännande av Microsoft Cloud avtalet.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769858"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="c56ac-103">Få bekräftelse på kundgodkännande av Microsoft Cloud-avtal</span><span class="sxs-lookup"><span data-stu-id="c56ac-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="c56ac-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="c56ac-104">**Applies To**</span></span>

- <span data-ttu-id="c56ac-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="c56ac-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="c56ac-106">**Avtals** resursen stöds för närvarande av Partner Center i det offentliga Microsoft-molnet.</span><span class="sxs-lookup"><span data-stu-id="c56ac-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="c56ac-107">Den gäller inte för:</span><span class="sxs-lookup"><span data-stu-id="c56ac-107">It isn't applicable to:</span></span>
>
> - <span data-ttu-id="c56ac-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c56ac-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="c56ac-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="c56ac-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="c56ac-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c56ac-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c56ac-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c56ac-111">Prerequisites</span></span>

- <span data-ttu-id="c56ac-112">Om du använder Partner Center .NET SDK krävs version 1,9 eller senare.</span><span class="sxs-lookup"><span data-stu-id="c56ac-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="c56ac-113">Om du använder Partner Center Java SDK krävs version 1,8 eller senare.</span><span class="sxs-lookup"><span data-stu-id="c56ac-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="c56ac-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c56ac-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="c56ac-115">Det här scenariot stöder endast app + användarautentisering.</span><span class="sxs-lookup"><span data-stu-id="c56ac-115">This scenario supports only supports app + user authentication.</span></span>

- <span data-ttu-id="c56ac-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c56ac-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c56ac-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="c56ac-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c56ac-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="c56ac-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c56ac-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="c56ac-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c56ac-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="c56ac-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c56ac-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c56ac-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="c56ac-122">.NET (version 1,4 eller senare)</span><span class="sxs-lookup"><span data-stu-id="c56ac-122">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="c56ac-123">För att hämta bekräftelser för kundgodkännande som tidigare har tillhandahållits:</span><span class="sxs-lookup"><span data-stu-id="c56ac-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="c56ac-124">Använd **IAggregatePartner. Customers** -samlingen och anropa **ById** -metoden med det angivna kund-ID: n.</span><span class="sxs-lookup"><span data-stu-id="c56ac-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="c56ac-125">Hämta **avtals** egenskapen och filtrera resultaten till Microsoft Cloud avtalet genom att anropa **ByAgreementType** -metoden.</span><span class="sxs-lookup"><span data-stu-id="c56ac-125">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="c56ac-126">Anropa **Get** -eller **GetAsync** -metoden.</span><span class="sxs-lookup"><span data-stu-id="c56ac-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="c56ac-127">Ett fullständigt exempel finns i [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.</span><span class="sxs-lookup"><span data-stu-id="c56ac-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="c56ac-128">.NET (version 1,9-1,13)</span><span class="sxs-lookup"><span data-stu-id="c56ac-128">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="c56ac-129">Så här hämtar du bekräftelse av kundgodkännande som har tillhandahållits tidigare:</span><span class="sxs-lookup"><span data-stu-id="c56ac-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="c56ac-130">Använd **IAggregatePartner. Customers** -samlingen och anropa **ById** -metoden med den angivna kundens ID.</span><span class="sxs-lookup"><span data-stu-id="c56ac-130">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="c56ac-131">Hämta sedan **avtals** egenskapen följt av metoderna **Get** eller **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="c56ac-131">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="c56ac-132">Java</span><span class="sxs-lookup"><span data-stu-id="c56ac-132">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="c56ac-133">Så här hämtar du bekräftelse av kundgodkännande som har tillhandahållits tidigare:</span><span class="sxs-lookup"><span data-stu-id="c56ac-133">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="c56ac-134">Använd funktionen **IAggregatePartner. getCustomers** och anropa funktionen **byId** med den angivna kundens identifierare.</span><span class="sxs-lookup"><span data-stu-id="c56ac-134">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="c56ac-135">Hämta sedan funktionen **getAgreements** , följt av anropa funktionen **Get** .</span><span class="sxs-lookup"><span data-stu-id="c56ac-135">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="c56ac-136">Ett fullständigt exempel finns i [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) -klassen från projektets [test app](https://github.com/Microsoft/Partner-Center-Java-Samples) -projekt.</span><span class="sxs-lookup"><span data-stu-id="c56ac-136">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="c56ac-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c56ac-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="c56ac-138">Så här hämtar du bekräftelse av kundgodkännande som har tillhandahållits tidigare:</span><span class="sxs-lookup"><span data-stu-id="c56ac-138">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="c56ac-139">Använd kommandot [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) .</span><span class="sxs-lookup"><span data-stu-id="c56ac-139">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="c56ac-140">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c56ac-140">REST request</span></span>

<span data-ttu-id="c56ac-141">Information om hur du hämtar bekräftelse på kundgodkännanden tidigare finns i följande instruktioner.</span><span class="sxs-lookup"><span data-stu-id="c56ac-141">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="c56ac-142">Skapa en ny **avtals** resurs med relevant certifierings information.</span><span class="sxs-lookup"><span data-stu-id="c56ac-142">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c56ac-143">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="c56ac-143">Request syntax</span></span>

| <span data-ttu-id="c56ac-144">Metod</span><span class="sxs-lookup"><span data-stu-id="c56ac-144">Method</span></span> | <span data-ttu-id="c56ac-145">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c56ac-145">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c56ac-146">GET</span><span class="sxs-lookup"><span data-stu-id="c56ac-146">GET</span></span>    | <span data-ttu-id="c56ac-147">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="c56ac-147">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="c56ac-148">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="c56ac-148">URI parameter</span></span>

<span data-ttu-id="c56ac-149">Använd följande frågeparameter för att ange kunden som du bekräftar.</span><span class="sxs-lookup"><span data-stu-id="c56ac-149">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="c56ac-150">Namn</span><span class="sxs-lookup"><span data-stu-id="c56ac-150">Name</span></span>             | <span data-ttu-id="c56ac-151">Typ</span><span class="sxs-lookup"><span data-stu-id="c56ac-151">Type</span></span> | <span data-ttu-id="c56ac-152">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c56ac-152">Required</span></span> | <span data-ttu-id="c56ac-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c56ac-153">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="c56ac-154">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="c56ac-154">CustomerTenantId</span></span> | <span data-ttu-id="c56ac-155">GUID</span><span class="sxs-lookup"><span data-stu-id="c56ac-155">GUID</span></span> | <span data-ttu-id="c56ac-156">Y</span><span class="sxs-lookup"><span data-stu-id="c56ac-156">Y</span></span>        | <span data-ttu-id="c56ac-157">Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund.</span><span class="sxs-lookup"><span data-stu-id="c56ac-157">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c56ac-158">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c56ac-158">Request headers</span></span>

<span data-ttu-id="c56ac-159">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c56ac-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c56ac-160">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="c56ac-160">Request body</span></span>

<span data-ttu-id="c56ac-161">Inga.</span><span class="sxs-lookup"><span data-stu-id="c56ac-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c56ac-162">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="c56ac-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="c56ac-163">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c56ac-163">REST response</span></span>

<span data-ttu-id="c56ac-164">Om det lyckas returnerar den här metoden en samling **avtals** resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="c56ac-164">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c56ac-165">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c56ac-165">Response success and error codes</span></span>

<span data-ttu-id="c56ac-166">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="c56ac-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c56ac-167">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c56ac-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c56ac-168">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c56ac-168">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c56ac-169">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="c56ac-169">Response example</span></span>

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
