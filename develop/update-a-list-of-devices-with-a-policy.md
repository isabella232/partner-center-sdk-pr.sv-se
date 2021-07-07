---
title: Uppdatera en lista över enheter med en princip
description: Uppdatera en lista över enheter med en konfigurationsprincip för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b35873eb253b0929bfc01662b0beb9b31d0c6b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530080"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="449d8-103">Uppdatera en lista över enheter med en princip</span><span class="sxs-lookup"><span data-stu-id="449d8-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="449d8-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="449d8-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="449d8-105">Uppdatera en lista över enheter med en konfigurationsprincip för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="449d8-105">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="449d8-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="449d8-106">Prerequisites</span></span>

- <span data-ttu-id="449d8-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="449d8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="449d8-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="449d8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="449d8-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="449d8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="449d8-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="449d8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="449d8-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="449d8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="449d8-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="449d8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="449d8-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="449d8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="449d8-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="449d8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="449d8-115">Principidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="449d8-115">The policy identifier.</span></span>

- <span data-ttu-id="449d8-116">Enhetsidentifierarna för de enheter som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="449d8-116">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="449d8-117">C\#</span><span class="sxs-lookup"><span data-stu-id="449d8-117">C\#</span></span>

<span data-ttu-id="449d8-118">Om du vill uppdatera en lista över enheter med den angivna konfigurationsprincipen instansierar du först en [List/dotnet/api/system.collections.generic.list-1) av typen [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)sträng) och lägger till principen som ska tillämpas, enligt följande kodexempel.</span><span class="sxs-lookup"><span data-stu-id="449d8-118">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="449d8-119">Du behöver principidentifieraren för principen.</span><span class="sxs-lookup"><span data-stu-id="449d8-119">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="449d8-120">Skapa sedan en lista över [**enhetsobjekt**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) som ska uppdateras med principen och ange enhets-ID och listan som innehåller principen som ska tillämpas för varje enhet.</span><span class="sxs-lookup"><span data-stu-id="449d8-120">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="449d8-121">Skapa sedan en instans av [**ett DevicePolicyUpdateRequest-objekt**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) och ange [**enhetsegenskapen**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) till listan över enhetsobjekt.</span><span class="sxs-lookup"><span data-stu-id="449d8-121">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="449d8-122">Om du vill bearbeta begäran om uppdatering av enhetsprincipen anropar du metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren för att hämta ett gränssnitt för åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="449d8-122">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="449d8-123">Hämta sedan [**devicePolicy-egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) för att hämta ett gränssnitt till kundens enhetsinsamlingsåtgärder.</span><span class="sxs-lookup"><span data-stu-id="449d8-123">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="449d8-124">Anropa slutligen metoden [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) med devicePolicyUpdateRequest-objektet för att uppdatera enheterna med principen.</span><span class="sxs-lookup"><span data-stu-id="449d8-124">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

<span data-ttu-id="449d8-125">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="449d8-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="449d8-126">**Project:** Partnercenter-SDK **exempelklass:** UpdateDevicesPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="449d8-126">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="449d8-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="449d8-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="449d8-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="449d8-128">Request syntax</span></span>

| <span data-ttu-id="449d8-129">Metod</span><span class="sxs-lookup"><span data-stu-id="449d8-129">Method</span></span>    | <span data-ttu-id="449d8-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="449d8-130">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="449d8-131">**Patch**</span><span class="sxs-lookup"><span data-stu-id="449d8-131">**PATCH**</span></span> | <span data-ttu-id="449d8-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="449d8-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="449d8-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="449d8-133">URI parameter</span></span>

<span data-ttu-id="449d8-134">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="449d8-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="449d8-135">Namn</span><span class="sxs-lookup"><span data-stu-id="449d8-135">Name</span></span>        | <span data-ttu-id="449d8-136">Typ</span><span class="sxs-lookup"><span data-stu-id="449d8-136">Type</span></span>   | <span data-ttu-id="449d8-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="449d8-137">Required</span></span> | <span data-ttu-id="449d8-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="449d8-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="449d8-139">kund-ID</span><span class="sxs-lookup"><span data-stu-id="449d8-139">customer-id</span></span> | <span data-ttu-id="449d8-140">sträng</span><span class="sxs-lookup"><span data-stu-id="449d8-140">string</span></span> | <span data-ttu-id="449d8-141">Ja</span><span class="sxs-lookup"><span data-stu-id="449d8-141">Yes</span></span>      | <span data-ttu-id="449d8-142">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="449d8-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="449d8-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="449d8-143">Request headers</span></span>

<span data-ttu-id="449d8-144">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="449d8-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="449d8-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="449d8-145">Request body</span></span>

<span data-ttu-id="449d8-146">Begärandetexten måste innehålla en [DevicePolicyUpdateRequest-resurs.](device-deployment-resources.md#devicepolicyupdaterequest)</span><span class="sxs-lookup"><span data-stu-id="449d8-146">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="449d8-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="449d8-147">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="449d8-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="449d8-148">REST response</span></span>

<span data-ttu-id="449d8-149">Om det lyckas innehåller svaret ett **Location-huvud** som har en URI som kan användas för att hämta status för den här batchprocessen.</span><span class="sxs-lookup"><span data-stu-id="449d8-149">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="449d8-150">Spara den här URI:en för användning med andra relaterade REST API:er.</span><span class="sxs-lookup"><span data-stu-id="449d8-150">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="449d8-151">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="449d8-151">Response success and error codes</span></span>

<span data-ttu-id="449d8-152">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="449d8-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="449d8-153">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="449d8-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="449d8-154">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="449d8-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="449d8-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="449d8-155">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
