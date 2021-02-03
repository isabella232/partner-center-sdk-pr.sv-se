---
title: Hämta en post för Partnercenter-aktivitet
description: Hur du hämtar en post med åtgärder, som utförs av en partner användare eller ett program, under en viss tids period.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f37eae8bb96c1c1e7008e8c566b085e25d8807d
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769531"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="992d0-103">Hämta en post för Partnercenter-aktivitet</span><span class="sxs-lookup"><span data-stu-id="992d0-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="992d0-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="992d0-104">**Applies To**</span></span>

- <span data-ttu-id="992d0-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="992d0-105">Partner Center</span></span>
- <span data-ttu-id="992d0-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="992d0-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="992d0-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="992d0-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="992d0-108">Den här artikeln beskriver hur du hämtar en post med åtgärder som utfördes av en partner användare eller ett program under en viss tids period.</span><span class="sxs-lookup"><span data-stu-id="992d0-108">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="992d0-109">Använd detta API för att hämta gransknings poster för de senaste 30 dagarna från det aktuella datumet eller för ett datum intervall som anges genom att inkludera start datum och/eller slutdatum.</span><span class="sxs-lookup"><span data-stu-id="992d0-109">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="992d0-110">Observera dock att data tillgänglighet för aktivitets loggen för prestanda orsaker är begränsad till föregående 90 dagar.</span><span class="sxs-lookup"><span data-stu-id="992d0-110">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="992d0-111">Begär Anden med ett start datum som är större än 90 dagar före det aktuella datumet får ett felaktigt undantag för begäran (felkod: 400) och ett lämpligt meddelande.</span><span class="sxs-lookup"><span data-stu-id="992d0-111">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="992d0-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="992d0-112">Prerequisites</span></span>

- <span data-ttu-id="992d0-113">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="992d0-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="992d0-114">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="992d0-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="992d0-115">C\#</span><span class="sxs-lookup"><span data-stu-id="992d0-115">C\#</span></span>

<span data-ttu-id="992d0-116">Om du vill hämta en post över partner Center-åtgärder måste du först fastställa datum intervallet för de poster som du vill hämta.</span><span class="sxs-lookup"><span data-stu-id="992d0-116">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="992d0-117">I följande kod exempel används endast start datum, men du kan även inkludera ett slutdatum.</span><span class="sxs-lookup"><span data-stu-id="992d0-117">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="992d0-118">Mer information finns i [**fråge**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) metoden.</span><span class="sxs-lookup"><span data-stu-id="992d0-118">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="992d0-119">Skapa sedan de variabler du behöver för den typ av filter som du vill använda och tilldela lämpliga värden.</span><span class="sxs-lookup"><span data-stu-id="992d0-119">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="992d0-120">Om du till exempel vill filtrera efter företagets namn under sträng skapar du en variabel som ska innehålla del strängen.</span><span class="sxs-lookup"><span data-stu-id="992d0-120">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="992d0-121">Om du vill filtrera efter kund-ID skapar du en variabel som innehåller ID: t.</span><span class="sxs-lookup"><span data-stu-id="992d0-121">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="992d0-122">I följande exempel finns exempel kod för att filtrera efter företagets namn under sträng, kund-ID eller resurs typ.</span><span class="sxs-lookup"><span data-stu-id="992d0-122">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="992d0-123">Välj en och kommentera ut de andra.</span><span class="sxs-lookup"><span data-stu-id="992d0-123">Choose one and comment out the others.</span></span> <span data-ttu-id="992d0-124">I varje fall instansierar du först ett [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) -objekt med [**Standardkonstruktorn**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) för att skapa filtret.</span><span class="sxs-lookup"><span data-stu-id="992d0-124">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="992d0-125">Du måste skicka en sträng som innehåller det fält som ska sökas och lämplig operator som ska användas, som visas.</span><span class="sxs-lookup"><span data-stu-id="992d0-125">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="992d0-126">Du måste också ange strängen för att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="992d0-126">You also must provide the string to filter by.</span></span>

<span data-ttu-id="992d0-127">Använd sedan egenskapen [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) för att hämta ett gränssnitt för att granska post åtgärder och anropa [**frågan**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) eller [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) -metoden för att köra filtret och hämta insamlingen av [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) som representerar den första sidan i resultatet.</span><span class="sxs-lookup"><span data-stu-id="992d0-127">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="992d0-128">Skicka metoden start datum, ett valfritt slutdatum som inte används i exemplet här och ett [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) -objekt som representerar en fråga på en entitet.</span><span class="sxs-lookup"><span data-stu-id="992d0-128">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="992d0-129">IQuery-objektet skapas genom att skicka filtret som skapats ovan till [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) - [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) -metoden.</span><span class="sxs-lookup"><span data-stu-id="992d0-129">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="992d0-130">När du har den första sidan med objekt använder du metoden [**enumerations. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) för att skapa en uppräknare som du kan använda för att iterera igenom de återstående sidorna.</span><span class="sxs-lookup"><span data-stu-id="992d0-130">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

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

<span data-ttu-id="992d0-131">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="992d0-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="992d0-132">**Projekt**: Partner Center SDK exempel **mapp**: granskning</span><span class="sxs-lookup"><span data-stu-id="992d0-132">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="992d0-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="992d0-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="992d0-134">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="992d0-134">Request syntax</span></span>

| <span data-ttu-id="992d0-135">Metod</span><span class="sxs-lookup"><span data-stu-id="992d0-135">Method</span></span>  | <span data-ttu-id="992d0-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="992d0-136">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="992d0-137">**TA**</span><span class="sxs-lookup"><span data-stu-id="992d0-137">**GET**</span></span> | <span data-ttu-id="992d0-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} http/1.1</span><span class="sxs-lookup"><span data-stu-id="992d0-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="992d0-139">**TA**</span><span class="sxs-lookup"><span data-stu-id="992d0-139">**GET**</span></span> | <span data-ttu-id="992d0-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {ENDDATE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="992d0-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="992d0-141">**TA**</span><span class="sxs-lookup"><span data-stu-id="992d0-141">**GET**</span></span> | <span data-ttu-id="992d0-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {endDate} &filter = {"Field": "företags namn", "värde": "{searchSubstring}", "Operator": "del sträng"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="992d0-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="992d0-143">**TA**</span><span class="sxs-lookup"><span data-stu-id="992d0-143">**GET**</span></span> | <span data-ttu-id="992d0-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {endDate} &filter = {"Field": "CustomerId", "värde": "{CustomerId}", "Operator": "är lika med"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="992d0-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="992d0-145">**TA**</span><span class="sxs-lookup"><span data-stu-id="992d0-145">**GET**</span></span> | <span data-ttu-id="992d0-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {endDate} &filter = {"Field": "resourcetype", "värde": "{resourcetype}", "Operator": "är lika med"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="992d0-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="992d0-147">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="992d0-147">URI parameter</span></span>

<span data-ttu-id="992d0-148">Använd följande frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="992d0-148">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="992d0-149">Namn</span><span class="sxs-lookup"><span data-stu-id="992d0-149">Name</span></span>      | <span data-ttu-id="992d0-150">Typ</span><span class="sxs-lookup"><span data-stu-id="992d0-150">Type</span></span>   | <span data-ttu-id="992d0-151">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="992d0-151">Required</span></span> | <span data-ttu-id="992d0-152">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="992d0-152">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="992d0-153">/SD</span><span class="sxs-lookup"><span data-stu-id="992d0-153">startDate</span></span> | <span data-ttu-id="992d0-154">date</span><span class="sxs-lookup"><span data-stu-id="992d0-154">date</span></span>   | <span data-ttu-id="992d0-155">No</span><span class="sxs-lookup"><span data-stu-id="992d0-155">No</span></span>       | <span data-ttu-id="992d0-156">Start datumet i formatet åååå-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="992d0-156">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="992d0-157">Om inget anges, kommer resultat uppsättningen att standardvärdet 30 dagar före datumet för begäran.</span><span class="sxs-lookup"><span data-stu-id="992d0-157">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="992d0-158">Den här parametern är valfri när ett filter anges.</span><span class="sxs-lookup"><span data-stu-id="992d0-158">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="992d0-159">endDate</span><span class="sxs-lookup"><span data-stu-id="992d0-159">endDate</span></span>   | <span data-ttu-id="992d0-160">date</span><span class="sxs-lookup"><span data-stu-id="992d0-160">date</span></span>   | <span data-ttu-id="992d0-161">No</span><span class="sxs-lookup"><span data-stu-id="992d0-161">No</span></span>       | <span data-ttu-id="992d0-162">Slutdatumet i åååå-mm-dd-format.</span><span class="sxs-lookup"><span data-stu-id="992d0-162">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="992d0-163">Den här parametern är valfri när ett filter anges.</span><span class="sxs-lookup"><span data-stu-id="992d0-163">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="992d0-164">När slutdatumet utelämnas eller är inställt på null, returnerar begäran Max fönstret eller använder dagens datum som slutdatum, beroende på vilket som är mindre.</span><span class="sxs-lookup"><span data-stu-id="992d0-164">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="992d0-165">filter</span><span class="sxs-lookup"><span data-stu-id="992d0-165">filter</span></span>    | <span data-ttu-id="992d0-166">sträng</span><span class="sxs-lookup"><span data-stu-id="992d0-166">string</span></span> | <span data-ttu-id="992d0-167">No</span><span class="sxs-lookup"><span data-stu-id="992d0-167">No</span></span>       | <span data-ttu-id="992d0-168">Filtret som ska användas.</span><span class="sxs-lookup"><span data-stu-id="992d0-168">The filter to apply.</span></span> <span data-ttu-id="992d0-169">Den här parametern måste vara en kodad sträng.</span><span class="sxs-lookup"><span data-stu-id="992d0-169">This parameter must be an encoded string.</span></span> <span data-ttu-id="992d0-170">Den här parametern är valfri när start datumet eller slutdatumet anges.</span><span class="sxs-lookup"><span data-stu-id="992d0-170">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="992d0-171">Filter-syntax</span><span class="sxs-lookup"><span data-stu-id="992d0-171">Filter syntax</span></span>
<span data-ttu-id="992d0-172">Du måste skapa filter parametern som en serie kommaavgränsade par med nyckel/värde-par.</span><span class="sxs-lookup"><span data-stu-id="992d0-172">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="992d0-173">Varje nyckel och värde måste anges individuellt och avgränsas med kolon.</span><span class="sxs-lookup"><span data-stu-id="992d0-173">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="992d0-174">Hela filtret måste vara kodat.</span><span class="sxs-lookup"><span data-stu-id="992d0-174">The entire filter must be encoded.</span></span>

<span data-ttu-id="992d0-175">Ett avkodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="992d0-175">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="992d0-176">I följande tabell beskrivs de nyckel/värde-par som krävs:</span><span class="sxs-lookup"><span data-stu-id="992d0-176">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="992d0-177">Tangent</span><span class="sxs-lookup"><span data-stu-id="992d0-177">Key</span></span>                 | <span data-ttu-id="992d0-178">Värde</span><span class="sxs-lookup"><span data-stu-id="992d0-178">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="992d0-179">Fält</span><span class="sxs-lookup"><span data-stu-id="992d0-179">Field</span></span>               | <span data-ttu-id="992d0-180">Det fält som ska filtreras.</span><span class="sxs-lookup"><span data-stu-id="992d0-180">The field to filter.</span></span> <span data-ttu-id="992d0-181">De värden som stöds finns i [syntaxen för begäran](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="992d0-181">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="992d0-182">Värde</span><span class="sxs-lookup"><span data-stu-id="992d0-182">Value</span></span>               | <span data-ttu-id="992d0-183">Värdet att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="992d0-183">The value to filter by.</span></span> <span data-ttu-id="992d0-184">Skift läget för värdet ignoreras.</span><span class="sxs-lookup"><span data-stu-id="992d0-184">The case of the value is ignored.</span></span> <span data-ttu-id="992d0-185">Följande värde parametrar stöds som visas i [syntaxen för begäran](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span><span class="sxs-lookup"><span data-stu-id="992d0-185">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="992d0-186">*searchSubstring* – Ersätt med namnet på företaget.</span><span class="sxs-lookup"><span data-stu-id="992d0-186">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="992d0-187">Du kan ange en under sträng som ska matcha en del av företags namnet (till exempel `bri` kommer att matcha `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="992d0-187">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="992d0-188">**Exempel:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="992d0-188">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="992d0-189">*customerId* – Ersätt med en GUID-formaterad sträng som representerar kund-ID: t.</span><span class="sxs-lookup"><span data-stu-id="992d0-189">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="992d0-190">**Exempel:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="992d0-190">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="992d0-191">*resourceType* – Ersätt med den typ av resurs som gransknings poster ska hämtas för (till exempel prenumeration).</span><span class="sxs-lookup"><span data-stu-id="992d0-191">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="992d0-192">Tillgängliga resurs typer definieras i [resourcetype](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span><span class="sxs-lookup"><span data-stu-id="992d0-192">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="992d0-193">**Exempel:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="992d0-193">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="992d0-194">Operator</span><span class="sxs-lookup"><span data-stu-id="992d0-194">Operator</span></span>          | <span data-ttu-id="992d0-195">Operatorn som ska användas.</span><span class="sxs-lookup"><span data-stu-id="992d0-195">The operator to apply.</span></span> <span data-ttu-id="992d0-196">De operatorer som stöds finns i [begärans syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="992d0-196">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="992d0-197">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="992d0-197">Request headers</span></span>

- <span data-ttu-id="992d0-198">Mer information finns i [delar av en del i mitten av rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="992d0-198">See [Parter Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="992d0-199">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="992d0-199">Request body</span></span>

<span data-ttu-id="992d0-200">Inga.</span><span class="sxs-lookup"><span data-stu-id="992d0-200">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="992d0-201">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="992d0-201">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="992d0-202">REST-svar</span><span class="sxs-lookup"><span data-stu-id="992d0-202">REST response</span></span>

<span data-ttu-id="992d0-203">Om det lyckas, returnerar den här metoden en uppsättning aktiviteter som uppfyller filtren.</span><span class="sxs-lookup"><span data-stu-id="992d0-203">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="992d0-204">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="992d0-204">Response success and error codes</span></span>

<span data-ttu-id="992d0-205">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="992d0-205">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="992d0-206">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="992d0-206">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="992d0-207">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="992d0-207">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="992d0-208">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="992d0-208">Response example</span></span>

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