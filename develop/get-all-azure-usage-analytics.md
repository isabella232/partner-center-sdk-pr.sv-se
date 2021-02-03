---
title: Hämta all information om Azure-användningsanalys
description: Så här hämtar du all information om användnings analys i Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769441"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="d642f-103">Hämta all information om Azure-användningsanalys</span><span class="sxs-lookup"><span data-stu-id="d642f-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="d642f-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="d642f-104">**Applies To**</span></span>

- <span data-ttu-id="d642f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d642f-105">Partner Center</span></span>
- <span data-ttu-id="d642f-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d642f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d642f-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="d642f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d642f-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d642f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d642f-109">Så här hämtar du all information om Azures användnings analys för dina kunder.</span><span class="sxs-lookup"><span data-stu-id="d642f-109">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d642f-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d642f-110">Prerequisites</span></span>

- <span data-ttu-id="d642f-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d642f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d642f-112">Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d642f-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d642f-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d642f-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d642f-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d642f-114">Request syntax</span></span>

| <span data-ttu-id="d642f-115">Metod</span><span class="sxs-lookup"><span data-stu-id="d642f-115">Method</span></span>  | <span data-ttu-id="d642f-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d642f-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="d642f-117">**TA**</span><span class="sxs-lookup"><span data-stu-id="d642f-117">**GET**</span></span> | <span data-ttu-id="d642f-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Usage/Azure http/1.1</span><span class="sxs-lookup"><span data-stu-id="d642f-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="d642f-119">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="d642f-119">URI parameters</span></span>

|<span data-ttu-id="d642f-120">Parameter</span><span class="sxs-lookup"><span data-stu-id="d642f-120">Parameter</span></span>        |<span data-ttu-id="d642f-121">Typ</span><span class="sxs-lookup"><span data-stu-id="d642f-121">Type</span></span>                        |<span data-ttu-id="d642f-122">Description</span><span class="sxs-lookup"><span data-stu-id="d642f-122">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="d642f-123">top</span><span class="sxs-lookup"><span data-stu-id="d642f-123">top</span></span>              | <span data-ttu-id="d642f-124">sträng</span><span class="sxs-lookup"><span data-stu-id="d642f-124">string</span></span>                     | <span data-ttu-id="d642f-125">Det antal rader med data som ska returneras i begäran.</span><span class="sxs-lookup"><span data-stu-id="d642f-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="d642f-126">Det maximala värdet och standardvärdet om det inte anges är 10000.</span><span class="sxs-lookup"><span data-stu-id="d642f-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="d642f-127">Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data.</span><span class="sxs-lookup"><span data-stu-id="d642f-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="d642f-128">hoppa över</span><span class="sxs-lookup"><span data-stu-id="d642f-128">skip</span></span>             | <span data-ttu-id="d642f-129">int</span><span class="sxs-lookup"><span data-stu-id="d642f-129">int</span></span>                        | <span data-ttu-id="d642f-130">Antalet rader som ska hoppas över i frågan.</span><span class="sxs-lookup"><span data-stu-id="d642f-130">The number of rows to skip in the query.</span></span> <span data-ttu-id="d642f-131">Använd den här parametern för att växla mellan stora data mängder.</span><span class="sxs-lookup"><span data-stu-id="d642f-131">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="d642f-132">Hämtar till exempel `top=10000 and skip=0` de första 10000 raderna med data, `top=10000 and skip=10000` hämtar nästa 10000 rader med data och så vidare.</span><span class="sxs-lookup"><span data-stu-id="d642f-132">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="d642f-133">filter</span><span class="sxs-lookup"><span data-stu-id="d642f-133">filter</span></span>           | <span data-ttu-id="d642f-134">sträng</span><span class="sxs-lookup"><span data-stu-id="d642f-134">string</span></span>                     | <span data-ttu-id="d642f-135">*Filter* parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret.</span><span class="sxs-lookup"><span data-stu-id="d642f-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="d642f-136">Varje instruktion innehåller ett fält och ett värde som är associerat `eq` med `ne` operatorerna or och som kan kombineras med hjälp av `and` eller `or` .</span><span class="sxs-lookup"><span data-stu-id="d642f-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="d642f-137">Du kan ange följande strängar:</span><span class="sxs-lookup"><span data-stu-id="d642f-137">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="d642f-138">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="d642f-138">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="d642f-139">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="d642f-139">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="d642f-140">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="d642f-140">aggregationLevel</span></span> | <span data-ttu-id="d642f-141">sträng</span><span class="sxs-lookup"><span data-stu-id="d642f-141">string</span></span>                    | <span data-ttu-id="d642f-142">Anger det tidsintervall som aggregerade data ska hämtas från.</span><span class="sxs-lookup"><span data-stu-id="d642f-142">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="d642f-143">Kan vara en av följande strängar: `day` , `week` , eller `month` .</span><span class="sxs-lookup"><span data-stu-id="d642f-143">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="d642f-144">Om inget anges är standardvärdet `day` .</span><span class="sxs-lookup"><span data-stu-id="d642f-144">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="d642f-145">`aggregationLevel`Parametern stöds inte utan en `groupby` .</span><span class="sxs-lookup"><span data-stu-id="d642f-145">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="d642f-146">`aggregationLevel`Parametern gäller för alla datum fält som finns i `groupby` .</span><span class="sxs-lookup"><span data-stu-id="d642f-146">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="d642f-147">OrderBy</span><span class="sxs-lookup"><span data-stu-id="d642f-147">orderby</span></span>          |<span data-ttu-id="d642f-148">sträng</span><span class="sxs-lookup"><span data-stu-id="d642f-148">string</span></span>                     | <span data-ttu-id="d642f-149">En instruktion som ordnar resultat data värden för varje installation.</span><span class="sxs-lookup"><span data-stu-id="d642f-149">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="d642f-150">Syntax: `...&orderby=field [order],field [order],...`.</span><span class="sxs-lookup"><span data-stu-id="d642f-150">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="d642f-151">`field`Parametern kan vara en av följande strängar:</span><span class="sxs-lookup"><span data-stu-id="d642f-151">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="d642f-152">*Sorterings* parametern är valfri och kan vara `asc` eller `desc` Ange stigande eller fallande ordning för respektive fält.</span><span class="sxs-lookup"><span data-stu-id="d642f-152">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="d642f-153">Standardvärdet är `asc`.</span><span class="sxs-lookup"><span data-stu-id="d642f-153">The default is `asc`.</span></span><br/><br/><span data-ttu-id="d642f-154">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="d642f-154">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="d642f-155">groupby</span><span class="sxs-lookup"><span data-stu-id="d642f-155">groupby</span></span>          |<span data-ttu-id="d642f-156">sträng</span><span class="sxs-lookup"><span data-stu-id="d642f-156">string</span></span>                    | <span data-ttu-id="d642f-157">En instruktion som endast tillämpar data agg regering på de angivna fälten.</span><span class="sxs-lookup"><span data-stu-id="d642f-157">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="d642f-158">Du kan ange följande fält:</span><span class="sxs-lookup"><span data-stu-id="d642f-158">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="d642f-159">De returnerade data raderna innehåller fälten som anges i `groupby`  parametern samt *kvantiteten*.</span><span class="sxs-lookup"><span data-stu-id="d642f-159">The returned data rows will contain the fields specified in the `groupby`  parameter as well as the *Quantity*.</span></span><br/><br/><span data-ttu-id="d642f-160">`groupby`Parametern kan användas med `aggregationLevel` parametern.</span><span class="sxs-lookup"><span data-stu-id="d642f-160">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="d642f-161">**Exempel:**</span><span class="sxs-lookup"><span data-stu-id="d642f-161">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="d642f-162">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d642f-162">Request headers</span></span>

<span data-ttu-id="d642f-163">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d642f-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d642f-164">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d642f-164">Request body</span></span>

<span data-ttu-id="d642f-165">Inga.</span><span class="sxs-lookup"><span data-stu-id="d642f-165">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d642f-166">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d642f-166">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="d642f-167">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d642f-167">REST response</span></span>

<span data-ttu-id="d642f-168">Om det lyckas innehåller svars texten en samling [Azures användnings](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resurser.</span><span class="sxs-lookup"><span data-stu-id="d642f-168">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d642f-169">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d642f-169">Response success and error codes</span></span>

<span data-ttu-id="d642f-170">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d642f-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d642f-171">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d642f-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d642f-172">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d642f-172">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d642f-173">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d642f-173">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="d642f-174">Se även</span><span class="sxs-lookup"><span data-stu-id="d642f-174">See also</span></span>

- [<span data-ttu-id="d642f-175">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="d642f-175">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
