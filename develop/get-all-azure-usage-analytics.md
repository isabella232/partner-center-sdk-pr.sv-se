---
title: Hämta all information om Azure-användningsanalys
description: Så här hämtar du all information om Azure-användningsanalys.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 7fe987c7dc50d55b26cd72d5aead52963eb1cfbe
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760223"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="8941a-103">Hämta all information om Azure-användningsanalys</span><span class="sxs-lookup"><span data-stu-id="8941a-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="8941a-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8941a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8941a-105">Så här hämtar du all information om Azure-användningsanalys för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="8941a-105">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8941a-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8941a-106">Prerequisites</span></span>

- <span data-ttu-id="8941a-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8941a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8941a-108">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8941a-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8941a-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8941a-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8941a-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="8941a-110">Request syntax</span></span>

| <span data-ttu-id="8941a-111">Metod</span><span class="sxs-lookup"><span data-stu-id="8941a-111">Method</span></span>  | <span data-ttu-id="8941a-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8941a-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="8941a-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="8941a-113">**GET**</span></span> | <span data-ttu-id="8941a-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8941a-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="8941a-115">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="8941a-115">URI parameters</span></span>

|<span data-ttu-id="8941a-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="8941a-116">Parameter</span></span>        |<span data-ttu-id="8941a-117">Typ</span><span class="sxs-lookup"><span data-stu-id="8941a-117">Type</span></span>                        |<span data-ttu-id="8941a-118">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8941a-118">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="8941a-119">top</span><span class="sxs-lookup"><span data-stu-id="8941a-119">top</span></span>              | <span data-ttu-id="8941a-120">sträng</span><span class="sxs-lookup"><span data-stu-id="8941a-120">string</span></span>                     | <span data-ttu-id="8941a-121">Antalet rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="8941a-121">The number of rows of data to return in the request.</span></span> <span data-ttu-id="8941a-122">Det högsta värdet och standardvärdet om inget värde anges är 10000.</span><span class="sxs-lookup"><span data-stu-id="8941a-122">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="8941a-123">Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="8941a-123">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="8941a-124">hoppa över</span><span class="sxs-lookup"><span data-stu-id="8941a-124">skip</span></span>             | <span data-ttu-id="8941a-125">int</span><span class="sxs-lookup"><span data-stu-id="8941a-125">int</span></span>                        | <span data-ttu-id="8941a-126">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="8941a-126">The number of rows to skip in the query.</span></span> <span data-ttu-id="8941a-127">Använd den här parametern för att bläddra igenom stora datamängder.</span><span class="sxs-lookup"><span data-stu-id="8941a-127">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="8941a-128">Hämtar till exempel de första `top=10000 and skip=0` 10 000 raderna med data, hämtar de `top=10000 and skip=10000` kommande 10 000 raderna med data och så vidare.</span><span class="sxs-lookup"><span data-stu-id="8941a-128">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="8941a-129">filter</span><span class="sxs-lookup"><span data-stu-id="8941a-129">filter</span></span>           | <span data-ttu-id="8941a-130">sträng</span><span class="sxs-lookup"><span data-stu-id="8941a-130">string</span></span>                     | <span data-ttu-id="8941a-131">*Filterparametern* för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="8941a-131">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="8941a-132">Varje -instruktion innehåller ett fält och värde som är associerade med `eq` `ne` operatorerna eller , och -instruktioner kan kombineras med hjälp av `and` eller `or` .</span><span class="sxs-lookup"><span data-stu-id="8941a-132">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="8941a-133">Du kan ange följande strängar:</span><span class="sxs-lookup"><span data-stu-id="8941a-133">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="8941a-134">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="8941a-134">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="8941a-135">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="8941a-135">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="8941a-136">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="8941a-136">aggregationLevel</span></span> | <span data-ttu-id="8941a-137">sträng</span><span class="sxs-lookup"><span data-stu-id="8941a-137">string</span></span>                    | <span data-ttu-id="8941a-138">Anger det tidsperiod som aggregerade data ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="8941a-138">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="8941a-139">Kan vara någon av följande strängar: `day` , `week` eller `month` .</span><span class="sxs-lookup"><span data-stu-id="8941a-139">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="8941a-140">Om det inte anges är standardvärdet `day` .</span><span class="sxs-lookup"><span data-stu-id="8941a-140">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="8941a-141">Parametern `aggregationLevel` stöds inte utan `groupby` .</span><span class="sxs-lookup"><span data-stu-id="8941a-141">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="8941a-142">Parametern `aggregationLevel` gäller för alla datumfält som finns i `groupby` .</span><span class="sxs-lookup"><span data-stu-id="8941a-142">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="8941a-143">Orderby</span><span class="sxs-lookup"><span data-stu-id="8941a-143">orderby</span></span>          |<span data-ttu-id="8941a-144">sträng</span><span class="sxs-lookup"><span data-stu-id="8941a-144">string</span></span>                     | <span data-ttu-id="8941a-145">En instruktion som beställer resultatdatavärdena för varje installation.</span><span class="sxs-lookup"><span data-stu-id="8941a-145">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="8941a-146">Syntax: `...&orderby=field [order],field [order],...`.</span><span class="sxs-lookup"><span data-stu-id="8941a-146">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="8941a-147">Parametern `field` kan vara en av följande strängar:</span><span class="sxs-lookup"><span data-stu-id="8941a-147">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="8941a-148">*Orderparametern* är valfri och kan vara eller för att ange stigande eller fallande ordning för respektive `asc` `desc` fält.</span><span class="sxs-lookup"><span data-stu-id="8941a-148">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="8941a-149">Standardvärdet är `asc`.</span><span class="sxs-lookup"><span data-stu-id="8941a-149">The default is `asc`.</span></span><br/><br/><span data-ttu-id="8941a-150">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="8941a-150">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="8941a-151">groupby</span><span class="sxs-lookup"><span data-stu-id="8941a-151">groupby</span></span>          |<span data-ttu-id="8941a-152">sträng</span><span class="sxs-lookup"><span data-stu-id="8941a-152">string</span></span>                    | <span data-ttu-id="8941a-153">En instruktion som endast tillämpar dataaggregering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="8941a-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="8941a-154">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="8941a-154">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="8941a-155">De returnerade dataraderna innehåller de fält som anges i `groupby`  parametern och *Quantity*.</span><span class="sxs-lookup"><span data-stu-id="8941a-155">The returned data rows will contain the fields specified in the `groupby`  parameter and the *Quantity*.</span></span><br/><br/><span data-ttu-id="8941a-156">Parametern `groupby` kan användas med `aggregationLevel` parametern .</span><span class="sxs-lookup"><span data-stu-id="8941a-156">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="8941a-157">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="8941a-157">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="8941a-158">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8941a-158">Request headers</span></span>

<span data-ttu-id="8941a-159">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8941a-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8941a-160">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8941a-160">Request body</span></span>

<span data-ttu-id="8941a-161">Inga.</span><span class="sxs-lookup"><span data-stu-id="8941a-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8941a-162">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8941a-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="8941a-163">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8941a-163">REST response</span></span>

<span data-ttu-id="8941a-164">Om det lyckas innehåller svarstexten en samling [Azure-användningsresurser.](partner-center-analytics-resources.md#csp-program-azure-usage-analytics)</span><span class="sxs-lookup"><span data-stu-id="8941a-164">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8941a-165">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8941a-165">Response success and error codes</span></span>

<span data-ttu-id="8941a-166">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="8941a-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8941a-167">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8941a-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8941a-168">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8941a-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8941a-169">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8941a-169">Response example</span></span>

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a><span data-ttu-id="8941a-170">Se även</span><span class="sxs-lookup"><span data-stu-id="8941a-170">See also</span></span>

- [<span data-ttu-id="8941a-171">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="8941a-171">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
