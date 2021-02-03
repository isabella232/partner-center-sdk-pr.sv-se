---
title: Uppdatera en lista över enheter med en princip
description: Så här uppdaterar du en lista med enheter med en konfigurations princip för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04c2ef33116335db40bd2934dc7e33d57f015097
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769753"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="056dd-103">Uppdatera en lista över enheter med en princip</span><span class="sxs-lookup"><span data-stu-id="056dd-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="056dd-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="056dd-104">**Applies To**</span></span>

- <span data-ttu-id="056dd-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="056dd-105">Partner Center</span></span>
- <span data-ttu-id="056dd-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="056dd-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="056dd-107">Så här uppdaterar du en lista med enheter med en konfigurations princip för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="056dd-107">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="056dd-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="056dd-108">Prerequisites</span></span>

- <span data-ttu-id="056dd-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="056dd-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="056dd-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="056dd-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="056dd-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="056dd-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="056dd-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="056dd-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="056dd-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="056dd-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="056dd-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="056dd-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="056dd-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="056dd-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="056dd-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="056dd-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="056dd-117">Princip identifieraren.</span><span class="sxs-lookup"><span data-stu-id="056dd-117">The policy identifier.</span></span>

- <span data-ttu-id="056dd-118">Enhets identifierare för de enheter som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="056dd-118">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="056dd-119">C\#</span><span class="sxs-lookup"><span data-stu-id="056dd-119">C\#</span></span>

<span data-ttu-id="056dd-120">Om du vill uppdatera en lista över enheter med den angivna konfigurations principen först instansierar du en [List/dotNet/API/system. Collections. Generic. list -1) av typen [KeyValuePair/dotNet/API/system. Collections. Generic. KeyValuePair -2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) och lägger till principen som ska tillämpas, enligt följande kod exempel.</span><span class="sxs-lookup"><span data-stu-id="056dd-120">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="056dd-121">Du behöver princip identifieraren för principen.</span><span class="sxs-lookup"><span data-stu-id="056dd-121">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="056dd-122">Skapa sedan en lista över [**enhets**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objekt som ska uppdateras med principen, ange enhets-ID och den lista som innehåller principen som ska tillämpas för varje enhet.</span><span class="sxs-lookup"><span data-stu-id="056dd-122">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="056dd-123">Sedan instansierar du ett [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) -objekt och anger egenskapen [**enheter**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) till listan över enhets objekt.</span><span class="sxs-lookup"><span data-stu-id="056dd-123">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="056dd-124">Om du vill bearbeta begäran om uppdatering av enhets princip anropar du metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: n för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="056dd-124">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="056dd-125">Hämta sedan egenskapen [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) för att hämta ett gränssnitt till kund enhets samlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="056dd-125">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="056dd-126">Slutligen kan du anropa [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) -metoden med DevicePolicyUpdateRequest-objektet för att uppdatera enheterna med principen.</span><span class="sxs-lookup"><span data-stu-id="056dd-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

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

<span data-ttu-id="056dd-127">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="056dd-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="056dd-128">**Projekt**: Partner Center SDK-exempel **klass**: UpdateDevicesPolicy.CS</span><span class="sxs-lookup"><span data-stu-id="056dd-128">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="056dd-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="056dd-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="056dd-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="056dd-130">Request syntax</span></span>

| <span data-ttu-id="056dd-131">Metod</span><span class="sxs-lookup"><span data-stu-id="056dd-131">Method</span></span>    | <span data-ttu-id="056dd-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="056dd-132">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="056dd-133">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="056dd-133">**PATCH**</span></span> | <span data-ttu-id="056dd-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/DevicePolicyUpdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="056dd-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="056dd-135">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="056dd-135">URI parameter</span></span>

<span data-ttu-id="056dd-136">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="056dd-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="056dd-137">Namn</span><span class="sxs-lookup"><span data-stu-id="056dd-137">Name</span></span>        | <span data-ttu-id="056dd-138">Typ</span><span class="sxs-lookup"><span data-stu-id="056dd-138">Type</span></span>   | <span data-ttu-id="056dd-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="056dd-139">Required</span></span> | <span data-ttu-id="056dd-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="056dd-140">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="056dd-141">kund-ID</span><span class="sxs-lookup"><span data-stu-id="056dd-141">customer-id</span></span> | <span data-ttu-id="056dd-142">sträng</span><span class="sxs-lookup"><span data-stu-id="056dd-142">string</span></span> | <span data-ttu-id="056dd-143">Yes</span><span class="sxs-lookup"><span data-stu-id="056dd-143">Yes</span></span>      | <span data-ttu-id="056dd-144">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="056dd-144">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="056dd-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="056dd-145">Request headers</span></span>

<span data-ttu-id="056dd-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="056dd-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="056dd-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="056dd-147">Request body</span></span>

<span data-ttu-id="056dd-148">Begär ande texten måste innehålla en [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) -resurs.</span><span class="sxs-lookup"><span data-stu-id="056dd-148">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="056dd-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="056dd-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="056dd-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="056dd-150">REST response</span></span>

<span data-ttu-id="056dd-151">Om det lyckas innehåller svaret ett **plats** huvud som har en URI som kan användas för att hämta status för den här batch-processen.</span><span class="sxs-lookup"><span data-stu-id="056dd-151">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="056dd-152">Spara denna URI för användning med andra relaterade REST API: er.</span><span class="sxs-lookup"><span data-stu-id="056dd-152">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="056dd-153">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="056dd-153">Response success and error codes</span></span>

<span data-ttu-id="056dd-154">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="056dd-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="056dd-155">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="056dd-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="056dd-156">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="056dd-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="056dd-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="056dd-157">Response example</span></span>

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
