---
title: Hämta en samling berättiganden
description: Så här hämtar du en samling rättigheter.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7bb8d3aefb11fae0af4bce790b41598d935de57c
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906416"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="43ec1-103">Hämta en samling berättiganden</span><span class="sxs-lookup"><span data-stu-id="43ec1-103">Get a collection of entitlements</span></span>

<span data-ttu-id="43ec1-104">Så här hämtar du en samling rättigheter.</span><span class="sxs-lookup"><span data-stu-id="43ec1-104">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43ec1-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="43ec1-105">Prerequisites</span></span>

- <span data-ttu-id="43ec1-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="43ec1-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="43ec1-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="43ec1-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="43ec1-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="43ec1-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="43ec1-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="43ec1-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="43ec1-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="43ec1-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="43ec1-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="43ec1-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="43ec1-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="43ec1-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="43ec1-113">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="43ec1-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="43ec1-114">C\#</span><span class="sxs-lookup"><span data-stu-id="43ec1-114">C\#</span></span>

<span data-ttu-id="43ec1-115">Om du vill hämta en berättigandesamling [](entitlement-resources.md#entitlement) för en kund hämtar du ett gränssnitt för berättigandeåtgärder genom att anropa [**metoden IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="43ec1-115">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="43ec1-116">Hämta sedan gränssnittet från egenskapen **Entitlements** och anropa metoden **Get()** eller **GetAsync()** för att hämta samlingen med rättigheter.</span><span class="sxs-lookup"><span data-stu-id="43ec1-116">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="43ec1-117">Om du vill fylla i förfallodatum för de rättigheter som ska hämtas anropar du samma metoder ovan och anger den valfria booleska parametern **showExpiry** till true **Get(true)** eller **GetAsync(true).**</span><span class="sxs-lookup"><span data-stu-id="43ec1-117">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="43ec1-118">Detta anger att förfallodatum för rättigheter krävs (i förekommande fall).</span><span class="sxs-lookup"><span data-stu-id="43ec1-118">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43ec1-119">Lokala berättigandetyper har inga förfallodatum.</span><span class="sxs-lookup"><span data-stu-id="43ec1-119">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="43ec1-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="43ec1-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="43ec1-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="43ec1-121">Request syntax</span></span>

| <span data-ttu-id="43ec1-122">Metod</span><span class="sxs-lookup"><span data-stu-id="43ec1-122">Method</span></span> | <span data-ttu-id="43ec1-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="43ec1-123">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="43ec1-124">**Få**</span><span class="sxs-lookup"><span data-stu-id="43ec1-124">**GET**</span></span> | <span data-ttu-id="43ec1-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/rättigheter HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="43ec1-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="43ec1-126">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="43ec1-126">URI parameters</span></span>

<span data-ttu-id="43ec1-127">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="43ec1-127">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="43ec1-128">Namn</span><span class="sxs-lookup"><span data-stu-id="43ec1-128">Name</span></span> | <span data-ttu-id="43ec1-129">Typ</span><span class="sxs-lookup"><span data-stu-id="43ec1-129">Type</span></span> | <span data-ttu-id="43ec1-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="43ec1-130">Required</span></span> | <span data-ttu-id="43ec1-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="43ec1-131">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="43ec1-132">customerId</span><span class="sxs-lookup"><span data-stu-id="43ec1-132">customerId</span></span> | <span data-ttu-id="43ec1-133">sträng</span><span class="sxs-lookup"><span data-stu-id="43ec1-133">string</span></span> | <span data-ttu-id="43ec1-134">Ja</span><span class="sxs-lookup"><span data-stu-id="43ec1-134">Yes</span></span> | <span data-ttu-id="43ec1-135">Ett GUID-formaterat customerId som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="43ec1-135">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="43ec1-136">entitlementType</span><span class="sxs-lookup"><span data-stu-id="43ec1-136">entitlementType</span></span> | <span data-ttu-id="43ec1-137">sträng</span><span class="sxs-lookup"><span data-stu-id="43ec1-137">string</span></span> | <span data-ttu-id="43ec1-138">No</span><span class="sxs-lookup"><span data-stu-id="43ec1-138">No</span></span> | <span data-ttu-id="43ec1-139">Kan användas för att ange vilken typ av rättigheter som ska hämtas (**programvara** eller **reservedInstance** ).</span><span class="sxs-lookup"><span data-stu-id="43ec1-139">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="43ec1-140">Om detta inte anges hämtas alla typer</span><span class="sxs-lookup"><span data-stu-id="43ec1-140">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="43ec1-141">showExpiry</span><span class="sxs-lookup"><span data-stu-id="43ec1-141">showExpiry</span></span> | <span data-ttu-id="43ec1-142">boolean</span><span class="sxs-lookup"><span data-stu-id="43ec1-142">boolean</span></span> | <span data-ttu-id="43ec1-143">Inga</span><span class="sxs-lookup"><span data-stu-id="43ec1-143">No</span></span> | <span data-ttu-id="43ec1-144">Valfri flagga som anger om förfallodatum för rättigheter krävs.</span><span class="sxs-lookup"><span data-stu-id="43ec1-144">Optional flag that indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="43ec1-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="43ec1-145">Request headers</span></span>

<span data-ttu-id="43ec1-146">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="43ec1-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="43ec1-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="43ec1-147">Request body</span></span>

<span data-ttu-id="43ec1-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="43ec1-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="43ec1-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="43ec1-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="43ec1-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="43ec1-150">REST response</span></span>

<span data-ttu-id="43ec1-151">Om det lyckas innehåller svarstexten en samling [berättiganderesurser.](entitlement-resources.md#entitlement)</span><span class="sxs-lookup"><span data-stu-id="43ec1-151">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="43ec1-152">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="43ec1-152">Response success and error codes</span></span>

<span data-ttu-id="43ec1-153">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="43ec1-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="43ec1-154">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="43ec1-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="43ec1-155">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="43ec1-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="43ec1-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="43ec1-156">Response example</span></span>

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

## <a name="additional-examples"></a><span data-ttu-id="43ec1-157">Ytterligare exempel</span><span class="sxs-lookup"><span data-stu-id="43ec1-157">Additional Examples</span></span>

<span data-ttu-id="43ec1-158">I följande exempel visas hur du hämtar en specifik typ av rättigheter tillsammans med förfallodatum (om tillämpligt)</span><span class="sxs-lookup"><span data-stu-id="43ec1-158">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="43ec1-159">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="43ec1-159">C\# example</span></span>

<span data-ttu-id="43ec1-160">Om du vill hämta en specifik typ av rättigheter hämtar du **gränssnittet ByEntitlementType** från gränssnittet **Entitlements** och använder **metoderna Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="43ec1-160">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="43ec1-161">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="43ec1-161">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="43ec1-162">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="43ec1-162">Response example</span></span>

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

<span data-ttu-id="43ec1-163">I följande exempel visas hur du hämtar information om produkter och reservationer från en berättigande.</span><span class="sxs-lookup"><span data-stu-id="43ec1-163">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="43ec1-164">Hämta information om virtuell datorreservation från ett berättigande med hjälp av SDK V1.8</span><span class="sxs-lookup"><span data-stu-id="43ec1-164">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="43ec1-165">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="43ec1-165">C\# example</span></span>

<span data-ttu-id="43ec1-166">Om du vill hämta mer information som rör reservationer för virtuella datorer från en rättighet anropar du den URI som exponeras under entitledArtifacts.link med artifactType = virtual_machine_reserved_instance.</span><span class="sxs-lookup"><span data-stu-id="43ec1-166">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="43ec1-167">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="43ec1-167">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="43ec1-168">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="43ec1-168">Response example</span></span>

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

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="43ec1-169">Hämta reservationsinformation från en rättighet med hjälp av SDK V1.9</span><span class="sxs-lookup"><span data-stu-id="43ec1-169">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="43ec1-170">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="43ec1-170">C\# example</span></span>

<span data-ttu-id="43ec1-171">Om du vill hämta mer information om reservationerna från en reserverad instansrättighet anropar du den URI som exponeras under ```entitledArtifacts.link``` med ```artifactType = reservedinstance``` .</span><span class="sxs-lookup"><span data-stu-id="43ec1-171">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="43ec1-172">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="43ec1-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="43ec1-173">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="43ec1-173">Response example</span></span>

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

### <a name="api-consumers"></a><span data-ttu-id="43ec1-174">API-konsumenter</span><span class="sxs-lookup"><span data-stu-id="43ec1-174">API Consumers</span></span>

<span data-ttu-id="43ec1-175">Partner som använder API:et för att fråga berättiganden för reserverade instanser för virtuella datorer – Uppdatera begärande-URI:n från **/customers/{customerId}/entitlements till /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** för att upprätthålla bakåtkompatibilitet.</span><span class="sxs-lookup"><span data-stu-id="43ec1-175">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="43ec1-176">Om du vill använda en virtuell dator eller Azure SQL med ett utökat kontrakt uppdaterar du begärande-URI:n till **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span><span class="sxs-lookup"><span data-stu-id="43ec1-176">To consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
