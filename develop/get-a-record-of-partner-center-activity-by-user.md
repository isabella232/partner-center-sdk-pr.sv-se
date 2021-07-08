---
title: Hämta en post för Partnercenter-aktivitet
description: Så här hämtar du en post med åtgärder som utförs av en partneranvändare eller ett program under en viss tidsperiod.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aec933d4b681d99080619505792bde56bdd25580
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873980"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="752f4-103">Hämta en post för Partnercenter-aktivitet</span><span class="sxs-lookup"><span data-stu-id="752f4-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="752f4-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="752f4-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="752f4-105">I den här artikeln beskrivs hur du hämtar en post med åtgärder som har utförts av en partneranvändare eller ett program under en viss tidsperiod.</span><span class="sxs-lookup"><span data-stu-id="752f4-105">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="752f4-106">Använd det här API:et för att hämta granskningsposter för de senaste 30 dagarna från det aktuella datumet eller för ett datumintervall som anges genom att inkludera startdatumet och/eller slutdatumet.</span><span class="sxs-lookup"><span data-stu-id="752f4-106">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="752f4-107">Observera dock att tillgängligheten för aktivitetsloggdata av prestandaskäl är begränsad till de senaste 90 dagarna.</span><span class="sxs-lookup"><span data-stu-id="752f4-107">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="752f4-108">Begäranden med ett startdatum som är större än 90 dagar före det aktuella datumet får ett undantag för felaktig begäran (felkod: 400) och ett lämpligt meddelande.</span><span class="sxs-lookup"><span data-stu-id="752f4-108">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="752f4-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="752f4-109">Prerequisites</span></span>

- <span data-ttu-id="752f4-110">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="752f4-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="752f4-111">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="752f4-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="752f4-112">C\#</span><span class="sxs-lookup"><span data-stu-id="752f4-112">C\#</span></span>

<span data-ttu-id="752f4-113">Om du vill hämta en post för Partner Center-åtgärder måste du först upprätta datumintervallet för de poster som du vill hämta.</span><span class="sxs-lookup"><span data-stu-id="752f4-113">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="752f4-114">I följande kodexempel används bara ett startdatum, men du kan även inkludera ett slutdatum.</span><span class="sxs-lookup"><span data-stu-id="752f4-114">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="752f4-115">Mer information finns i [**Frågemetod.**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query)</span><span class="sxs-lookup"><span data-stu-id="752f4-115">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="752f4-116">Skapa sedan de variabler som du behöver för den typ av filter som du vill använda och tilldela lämpliga värden.</span><span class="sxs-lookup"><span data-stu-id="752f4-116">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="752f4-117">Om du till exempel vill filtrera efter företagsnamnsundersträng skapar du en variabel som ska innehålla delsträngen.</span><span class="sxs-lookup"><span data-stu-id="752f4-117">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="752f4-118">Om du vill filtrera efter kund-ID skapar du en variabel som ska innehålla ID:t.</span><span class="sxs-lookup"><span data-stu-id="752f4-118">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="752f4-119">I följande exempel tillhandahålls exempelkod för att filtrera efter en delsträng för företagsnamn, kund-ID eller resurstyp.</span><span class="sxs-lookup"><span data-stu-id="752f4-119">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="752f4-120">Välj en och kommentera ut de andra.</span><span class="sxs-lookup"><span data-stu-id="752f4-120">Choose one and comment out the others.</span></span> <span data-ttu-id="752f4-121">I varje fall instansierar du först ett [**SimpleFieldFilter-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) med dess [**standardkonstruktor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) för att skapa filtret.</span><span class="sxs-lookup"><span data-stu-id="752f4-121">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="752f4-122">Du måste skicka en sträng som innehåller fältet att söka efter, och lämplig operator att tillämpa, som du ser i bilden.</span><span class="sxs-lookup"><span data-stu-id="752f4-122">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="752f4-123">Du måste också ange strängen att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="752f4-123">You also must provide the string to filter by.</span></span>

<span data-ttu-id="752f4-124">Använd sedan egenskapen [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) för att hämta ett gränssnitt [](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) för att granska poståtgärder och anropa query- eller [**QueryAsync-metoden**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) för att köra filtret och hämta samlingen [**av AuditRecords**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) som representerar den första sidan i resultatet.</span><span class="sxs-lookup"><span data-stu-id="752f4-124">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="752f4-125">Skicka metoden startdatumet, ett valfritt slutdatum som inte används i exemplet här och ett [**IQuery-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) som representerar en fråga på en entitet.</span><span class="sxs-lookup"><span data-stu-id="752f4-125">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="752f4-126">IQuery-objektet skapas genom att skicka filtret som skapats ovan till [**QueryFactorys**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery-metod.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)</span><span class="sxs-lookup"><span data-stu-id="752f4-126">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="752f4-127">När du har den första sidan med objekt använder du metoden [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) för att skapa en uppräkning som du kan använda för att iterera genom återstående sidor.</span><span class="sxs-lookup"><span data-stu-id="752f4-127">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

<span data-ttu-id="752f4-128">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="752f4-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="752f4-129">**Project:** Partnercenter-SDK **exempelmapp:** Granskning</span><span class="sxs-lookup"><span data-stu-id="752f4-129">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="752f4-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="752f4-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="752f4-131">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="752f4-131">Request syntax</span></span>

| <span data-ttu-id="752f4-132">Metod</span><span class="sxs-lookup"><span data-stu-id="752f4-132">Method</span></span>  | <span data-ttu-id="752f4-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="752f4-133">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="752f4-134">**Få**</span><span class="sxs-lookup"><span data-stu-id="752f4-134">**GET**</span></span> | <span data-ttu-id="752f4-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="752f4-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="752f4-136">**Få**</span><span class="sxs-lookup"><span data-stu-id="752f4-136">**GET**</span></span> | <span data-ttu-id="752f4-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="752f4-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="752f4-138">**Få**</span><span class="sxs-lookup"><span data-stu-id="752f4-138">**GET**</span></span> | <span data-ttu-id="752f4-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="752f4-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="752f4-140">**Få**</span><span class="sxs-lookup"><span data-stu-id="752f4-140">**GET**</span></span> | <span data-ttu-id="752f4-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="752f4-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="752f4-142">**Få**</span><span class="sxs-lookup"><span data-stu-id="752f4-142">**GET**</span></span> | <span data-ttu-id="752f4-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="752f4-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="752f4-144">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="752f4-144">URI parameter</span></span>

<span data-ttu-id="752f4-145">Använd följande frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="752f4-145">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="752f4-146">Namn</span><span class="sxs-lookup"><span data-stu-id="752f4-146">Name</span></span>      | <span data-ttu-id="752f4-147">Typ</span><span class="sxs-lookup"><span data-stu-id="752f4-147">Type</span></span>   | <span data-ttu-id="752f4-148">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="752f4-148">Required</span></span> | <span data-ttu-id="752f4-149">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="752f4-149">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="752f4-150">Startdate</span><span class="sxs-lookup"><span data-stu-id="752f4-150">startDate</span></span> | <span data-ttu-id="752f4-151">date</span><span class="sxs-lookup"><span data-stu-id="752f4-151">date</span></span>   | <span data-ttu-id="752f4-152">Inga</span><span class="sxs-lookup"><span data-stu-id="752f4-152">No</span></span>       | <span data-ttu-id="752f4-153">Startdatumet i formatet yyyy-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="752f4-153">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="752f4-154">Om inget anges får resultatuppsättningen standardvärdet 30 dagar före begärandedatumet.</span><span class="sxs-lookup"><span data-stu-id="752f4-154">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="752f4-155">Den här parametern är valfri när ett filter anges.</span><span class="sxs-lookup"><span data-stu-id="752f4-155">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="752f4-156">endDate</span><span class="sxs-lookup"><span data-stu-id="752f4-156">endDate</span></span>   | <span data-ttu-id="752f4-157">date</span><span class="sxs-lookup"><span data-stu-id="752f4-157">date</span></span>   | <span data-ttu-id="752f4-158">Inga</span><span class="sxs-lookup"><span data-stu-id="752f4-158">No</span></span>       | <span data-ttu-id="752f4-159">Slutdatumet i formatet yyyy-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="752f4-159">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="752f4-160">Den här parametern är valfri när ett filter anges.</span><span class="sxs-lookup"><span data-stu-id="752f4-160">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="752f4-161">När slutdatumet utelämnas eller anges till null returnerar begäran det maximala fönstret eller använder idag som slutdatum, beroende på vilket som är mindre.</span><span class="sxs-lookup"><span data-stu-id="752f4-161">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="752f4-162">filter</span><span class="sxs-lookup"><span data-stu-id="752f4-162">filter</span></span>    | <span data-ttu-id="752f4-163">sträng</span><span class="sxs-lookup"><span data-stu-id="752f4-163">string</span></span> | <span data-ttu-id="752f4-164">No</span><span class="sxs-lookup"><span data-stu-id="752f4-164">No</span></span>       | <span data-ttu-id="752f4-165">Filtret som ska tillämpas.</span><span class="sxs-lookup"><span data-stu-id="752f4-165">The filter to apply.</span></span> <span data-ttu-id="752f4-166">Den här parametern måste vara en kodad sträng.</span><span class="sxs-lookup"><span data-stu-id="752f4-166">This parameter must be an encoded string.</span></span> <span data-ttu-id="752f4-167">Den här parametern är valfri när startdatumet eller slutdatumet anges.</span><span class="sxs-lookup"><span data-stu-id="752f4-167">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="752f4-168">Filtersyntax</span><span class="sxs-lookup"><span data-stu-id="752f4-168">Filter syntax</span></span>
<span data-ttu-id="752f4-169">Du måste skriva filterparametern som en serie kommaavgränsade nyckel/värde-par.</span><span class="sxs-lookup"><span data-stu-id="752f4-169">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="752f4-170">Varje nyckel och värde måste anges individuellt och avgränsas med ett kolon.</span><span class="sxs-lookup"><span data-stu-id="752f4-170">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="752f4-171">Hela filtret måste vara kodat.</span><span class="sxs-lookup"><span data-stu-id="752f4-171">The entire filter must be encoded.</span></span>

<span data-ttu-id="752f4-172">Ett okodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="752f4-172">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="752f4-173">I följande tabell beskrivs de nyckel/värde-par som krävs:</span><span class="sxs-lookup"><span data-stu-id="752f4-173">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="752f4-174">Tangent</span><span class="sxs-lookup"><span data-stu-id="752f4-174">Key</span></span>                 | <span data-ttu-id="752f4-175">Värde</span><span class="sxs-lookup"><span data-stu-id="752f4-175">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="752f4-176">Fält</span><span class="sxs-lookup"><span data-stu-id="752f4-176">Field</span></span>               | <span data-ttu-id="752f4-177">Fältet som ska filtreras.</span><span class="sxs-lookup"><span data-stu-id="752f4-177">The field to filter.</span></span> <span data-ttu-id="752f4-178">Värdena som stöds finns i Request syntax (Begär [syntax).](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="752f4-178">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="752f4-179">Värde</span><span class="sxs-lookup"><span data-stu-id="752f4-179">Value</span></span>               | <span data-ttu-id="752f4-180">Värdet som ska filtreras efter.</span><span class="sxs-lookup"><span data-stu-id="752f4-180">The value to filter by.</span></span> <span data-ttu-id="752f4-181">Värdets fall ignoreras.</span><span class="sxs-lookup"><span data-stu-id="752f4-181">The case of the value is ignored.</span></span> <span data-ttu-id="752f4-182">Följande värdeparametrar stöds enligt [förfrågningssyntaxen:](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="752f4-182">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="752f4-183">*searchSubstring* – Ersätt med namnet på företaget.</span><span class="sxs-lookup"><span data-stu-id="752f4-183">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="752f4-184">Du kan ange en delsträng som matchar en del av företagsnamnet (till exempel `bri` matchar `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="752f4-184">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="752f4-185">**Exempel:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="752f4-185">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="752f4-186">*customerId* – Ersätt med en GUID-formaterad sträng som representerar kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="752f4-186">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="752f4-187">**Exempel:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="752f4-187">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="752f4-188">*resourceType* – Ersätt med den typ av resurs som du vill hämta granskningsposter för (till exempel Prenumeration).</span><span class="sxs-lookup"><span data-stu-id="752f4-188">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="752f4-189">De tillgängliga resurstyperna definieras i [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span><span class="sxs-lookup"><span data-stu-id="752f4-189">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="752f4-190">**Exempel:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="752f4-190">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="752f4-191">Operator</span><span class="sxs-lookup"><span data-stu-id="752f4-191">Operator</span></span>          | <span data-ttu-id="752f4-192">Operatorn som ska tillämpas.</span><span class="sxs-lookup"><span data-stu-id="752f4-192">The operator to apply.</span></span> <span data-ttu-id="752f4-193">Operatorerna som stöds finns i Request syntax (Begär [syntax).](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="752f4-193">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="752f4-194">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="752f4-194">Request headers</span></span>

- <span data-ttu-id="752f4-195">Mer information finns i [Parter Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="752f4-195">For more information, see [Parter Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="752f4-196">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="752f4-196">Request body</span></span>

<span data-ttu-id="752f4-197">Inga.</span><span class="sxs-lookup"><span data-stu-id="752f4-197">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="752f4-198">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="752f4-198">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="752f4-199">REST-svar</span><span class="sxs-lookup"><span data-stu-id="752f4-199">REST response</span></span>

<span data-ttu-id="752f4-200">Om det lyckas returnerar den här metoden en uppsättning aktiviteter som uppfyller filtren.</span><span class="sxs-lookup"><span data-stu-id="752f4-200">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="752f4-201">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="752f4-201">Response success and error codes</span></span>

<span data-ttu-id="752f4-202">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="752f4-202">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="752f4-203">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="752f4-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="752f4-204">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="752f4-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="752f4-205">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="752f4-205">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```