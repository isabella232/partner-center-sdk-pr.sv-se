---
title: Hämta en samling berättiganden
description: Så här hämtar du en samling rättigheter.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2cc485429941dd2080bd285553333a01fc0ffd1
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769291"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="25cff-103">Hämta en samling berättiganden</span><span class="sxs-lookup"><span data-stu-id="25cff-103">Get a collection of entitlements</span></span>

<span data-ttu-id="25cff-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="25cff-104">**Applies To**</span></span>

- <span data-ttu-id="25cff-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="25cff-105">Partner Center</span></span>

<span data-ttu-id="25cff-106">Så här hämtar du en samling rättigheter.</span><span class="sxs-lookup"><span data-stu-id="25cff-106">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25cff-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="25cff-107">Prerequisites</span></span>

- <span data-ttu-id="25cff-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="25cff-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="25cff-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="25cff-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="25cff-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25cff-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="25cff-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="25cff-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="25cff-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="25cff-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="25cff-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="25cff-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="25cff-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="25cff-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="25cff-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25cff-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="25cff-116">C\#</span><span class="sxs-lookup"><span data-stu-id="25cff-116">C\#</span></span>

<span data-ttu-id="25cff-117">Om du vill hämta en berättigad samling för en kund kan du skaffa ett gränssnitt till [**rättighets**](entitlement-resources.md#entitlement) åtgärder genom att anropa metoden  [**IAggregatePartner. Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="25cff-117">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="25cff-118">Hämta sedan gränssnittet från egenskapen **berättiganden** och anropa metoden **Get ()** eller **GetAsync ()** för att hämta samlingen av rättigheter.</span><span class="sxs-lookup"><span data-stu-id="25cff-118">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="25cff-119">Om du vill fylla i förfallo datum för de rättigheter som ska hämtas anropar du samma metoder ovan och anger den valfria booleska parametern **showExpiry** till True **Get (true)** eller **GetAsync (true)**.</span><span class="sxs-lookup"><span data-stu-id="25cff-119">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="25cff-120">Detta anger att förfallo datum för rättigheten krävs (om tillämpligt).</span><span class="sxs-lookup"><span data-stu-id="25cff-120">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25cff-121">Lokala rättighets typer har inte förfallo datum.</span><span class="sxs-lookup"><span data-stu-id="25cff-121">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="25cff-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="25cff-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25cff-123">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="25cff-123">Request syntax</span></span>

| <span data-ttu-id="25cff-124">Metod</span><span class="sxs-lookup"><span data-stu-id="25cff-124">Method</span></span> | <span data-ttu-id="25cff-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="25cff-125">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="25cff-126">**TA**</span><span class="sxs-lookup"><span data-stu-id="25cff-126">**GET**</span></span> | <span data-ttu-id="25cff-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Entitlements http/1.1</span><span class="sxs-lookup"><span data-stu-id="25cff-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="25cff-128">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="25cff-128">URI parameters</span></span>

<span data-ttu-id="25cff-129">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="25cff-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="25cff-130">Namn</span><span class="sxs-lookup"><span data-stu-id="25cff-130">Name</span></span> | <span data-ttu-id="25cff-131">Typ</span><span class="sxs-lookup"><span data-stu-id="25cff-131">Type</span></span> | <span data-ttu-id="25cff-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="25cff-132">Required</span></span> | <span data-ttu-id="25cff-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="25cff-133">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="25cff-134">customerId</span><span class="sxs-lookup"><span data-stu-id="25cff-134">customerId</span></span> | <span data-ttu-id="25cff-135">sträng</span><span class="sxs-lookup"><span data-stu-id="25cff-135">string</span></span> | <span data-ttu-id="25cff-136">Yes</span><span class="sxs-lookup"><span data-stu-id="25cff-136">Yes</span></span> | <span data-ttu-id="25cff-137">Ett GUID-formaterat Kundnr som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="25cff-137">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="25cff-138">entitlementType</span><span class="sxs-lookup"><span data-stu-id="25cff-138">entitlementType</span></span> | <span data-ttu-id="25cff-139">sträng</span><span class="sxs-lookup"><span data-stu-id="25cff-139">string</span></span> | <span data-ttu-id="25cff-140">No</span><span class="sxs-lookup"><span data-stu-id="25cff-140">No</span></span> | <span data-ttu-id="25cff-141">Kan användas för att ange vilken typ av rättigheter som ska hämtas (**program vara** eller **reservedInstance** ).</span><span class="sxs-lookup"><span data-stu-id="25cff-141">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="25cff-142">Om inget anges hämtas alla typer</span><span class="sxs-lookup"><span data-stu-id="25cff-142">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="25cff-143">showExpiry</span><span class="sxs-lookup"><span data-stu-id="25cff-143">showExpiry</span></span> | <span data-ttu-id="25cff-144">boolean</span><span class="sxs-lookup"><span data-stu-id="25cff-144">boolean</span></span> | <span data-ttu-id="25cff-145">No</span><span class="sxs-lookup"><span data-stu-id="25cff-145">No</span></span> | <span data-ttu-id="25cff-146">Valfri flagga som anger om förfallo datum för rättigheter måste anges.</span><span class="sxs-lookup"><span data-stu-id="25cff-146">Optional flag which indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="25cff-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="25cff-147">Request headers</span></span>

<span data-ttu-id="25cff-148">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="25cff-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="25cff-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="25cff-149">Request body</span></span>

<span data-ttu-id="25cff-150">Inga.</span><span class="sxs-lookup"><span data-stu-id="25cff-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="25cff-151">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="25cff-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="25cff-152">REST-svar</span><span class="sxs-lookup"><span data-stu-id="25cff-152">REST response</span></span>

<span data-ttu-id="25cff-153">Om det lyckas innehåller svars texten en samling [rättighets](entitlement-resources.md#entitlement) resurser.</span><span class="sxs-lookup"><span data-stu-id="25cff-153">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25cff-154">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="25cff-154">Response success and error codes</span></span>

<span data-ttu-id="25cff-155">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="25cff-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="25cff-156">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="25cff-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="25cff-157">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="25cff-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="25cff-158">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="25cff-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
    },
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <a name="additional-examples"></a><span data-ttu-id="25cff-159">Ytterligare exempel</span><span class="sxs-lookup"><span data-stu-id="25cff-159">Additional Examples</span></span>

<span data-ttu-id="25cff-160">I följande exempel visas hur du hämtar en speciell typ av rättigheter tillsammans med utgångs datum (om tillämpligt)</span><span class="sxs-lookup"><span data-stu-id="25cff-160">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="25cff-161">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="25cff-161">C\# example</span></span>

<span data-ttu-id="25cff-162">Om du vill hämta en bestämd typ av rättigheter hämtar du **ByEntitlementType** -gränssnittet från **rättighets** gränssnittet och använder metoderna **Get ()** eller **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="25cff-162">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="25cff-163">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="25cff-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="25cff-164">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="25cff-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="25cff-165">I följande exempel visas hur du hämtar information om produkter och reservationer från en rättighet.</span><span class="sxs-lookup"><span data-stu-id="25cff-165">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="25cff-166">Hämta reservations information för virtuell dator från en rättighet med hjälp av SDK V 1.8</span><span class="sxs-lookup"><span data-stu-id="25cff-166">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="25cff-167">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="25cff-167">C\# example</span></span>

<span data-ttu-id="25cff-168">Om du vill hämta mer information om de virtuella dator reservationerna från en rättighet, anropar du URI: n som exponeras under entitledArtifacts. Link with artifactType = virtual_machine_reserved_instance.</span><span class="sxs-lookup"><span data-stu-id="25cff-168">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance .</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="25cff-169">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="25cff-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="25cff-170">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="25cff-170">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="25cff-171">Hämta reservations information från en rättighet med hjälp av SDK V 1.9</span><span class="sxs-lookup"><span data-stu-id="25cff-171">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="25cff-172">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="25cff-172">C\# example</span></span>

<span data-ttu-id="25cff-173">Om du vill hämta mer information som rör reservationer från en reserverad instans kan du anropa den URI som exponeras under ```entitledArtifacts.link``` med ```artifactType = reservedinstance``` .</span><span class="sxs-lookup"><span data-stu-id="25cff-173">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="25cff-174">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="25cff-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="25cff-175">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="25cff-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "reservedinstance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="api-consumers"></a><span data-ttu-id="25cff-176">API-konsumenter</span><span class="sxs-lookup"><span data-stu-id="25cff-176">API Consumers</span></span>

<span data-ttu-id="25cff-177">Partner som använder API: et för att fråga om reserverade instanser av virtuella datorer – uppdatera begärd URI från **/Customers/{customerId}/Entitlements till/Customers/{customerId}/Entitlements? entitlementType = virtualmachinereservedinstance** för att upprätthålla bakåtkompatibilitet.</span><span class="sxs-lookup"><span data-stu-id="25cff-177">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="25cff-178">För att kunna använda den virtuella datorn eller Azure SQL med förbättrat kontrakt uppdaterar du URI för begäran till **/Customers/{customerId}/Entitlements? entitlementType = reservedinstance**.</span><span class="sxs-lookup"><span data-stu-id="25cff-178">In order to consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
