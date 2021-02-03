---
title: Hämta en kunds användningsposter för Azure
description: Du kan använda Azures användnings-API för att hämta användnings posterna för en kunds Azure-prenumeration under en angiven tids period.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769342"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="8f19b-103">Hämta en kunds användningsposter för Azure</span><span class="sxs-lookup"><span data-stu-id="8f19b-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="8f19b-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="8f19b-104">**Applies to:**</span></span>

- <span data-ttu-id="8f19b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="8f19b-105">Partner Center</span></span>
- <span data-ttu-id="8f19b-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="8f19b-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8f19b-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8f19b-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8f19b-108">Du kan hämta användnings posterna för en kunds Azure-prenumeration under en viss tids period med hjälp av API: et för Azure-användning.</span><span class="sxs-lookup"><span data-stu-id="8f19b-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f19b-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8f19b-109">Prerequisites</span></span>

- <span data-ttu-id="8f19b-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8f19b-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f19b-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8f19b-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="8f19b-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f19b-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8f19b-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="8f19b-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8f19b-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="8f19b-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8f19b-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="8f19b-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8f19b-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="8f19b-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8f19b-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f19b-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8f19b-118">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="8f19b-118">A subscription identifier.</span></span>

<span data-ttu-id="8f19b-119">Det här API: et returnerar en daglig och en Tim Beräknad förbrukning för ett godtyckligt tidsintervall.</span><span class="sxs-lookup"><span data-stu-id="8f19b-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="8f19b-120">*Detta API stöds dock inte för Azure-planer*.</span><span class="sxs-lookup"><span data-stu-id="8f19b-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="8f19b-121">Om du har en Azure-prenumeration kan du läsa artikeln [få faktura om ej fakturerade förbruknings artiklar](get-invoice-unbilled-consumption-lineitems.md) och [Hämta faktura förbruknings artiklar](get-invoice-billed-consumption-lineitems.md) i stället.</span><span class="sxs-lookup"><span data-stu-id="8f19b-121">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="8f19b-122">I de här artiklarna beskrivs hur du får Beräknad förbrukning på en daglig nivå per mätning per resurs.</span><span class="sxs-lookup"><span data-stu-id="8f19b-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="8f19b-123">Den här pris förbrukningen motsvarar den dagliga kornig data som tillhandahålls av Azures användnings-API.</span><span class="sxs-lookup"><span data-stu-id="8f19b-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="8f19b-124">Du måste använda faktura identifieraren för att hämta fakturerings användnings data.</span><span class="sxs-lookup"><span data-stu-id="8f19b-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="8f19b-125">Eller så kan du använda aktuella och föregående perioder för att få ej fakturerade användnings beräkningar.</span><span class="sxs-lookup"><span data-stu-id="8f19b-125">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="8f19b-126">*Data för varje timmes kornig het och godtyckliga datum intervall filter stöds inte för närvarande för Azure plan-prenumerations resurser*.</span><span class="sxs-lookup"><span data-stu-id="8f19b-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="8f19b-127">API för Azure-användning</span><span class="sxs-lookup"><span data-stu-id="8f19b-127">Azure utilization API</span></span>

<span data-ttu-id="8f19b-128">Detta API för Azure-användning ger till gång till användnings poster för en tids period som representerar när användningen rapporterades i fakturerings systemet.</span><span class="sxs-lookup"><span data-stu-id="8f19b-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="8f19b-129">Den ger åtkomst till samma användnings data som används för att skapa och beräkna avstämnings filen.</span><span class="sxs-lookup"><span data-stu-id="8f19b-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="8f19b-130">Den har dock inte kunskap om fil logik för fakturerings system.</span><span class="sxs-lookup"><span data-stu-id="8f19b-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="8f19b-131">Du bör inte förvänta dig att matcha resultatet från det här API: et för samma tids period.</span><span class="sxs-lookup"><span data-stu-id="8f19b-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="8f19b-132">Till exempel tar fakturerings systemet samma användnings data och tillämpar regler för att fastställa vad som redovisas i en avstämnings fil.</span><span class="sxs-lookup"><span data-stu-id="8f19b-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="8f19b-133">När en fakturerings period stängs tas all användning fram till slutet av den dag som fakturerings perioden upphör att ingå i avstämnings filen.</span><span class="sxs-lookup"><span data-stu-id="8f19b-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="8f19b-134">All sent användning inom den fakturerings period som rapporteras inom 24 timmar efter fakturerings perioden upphör att gälla i nästa avstämning fil.</span><span class="sxs-lookup"><span data-stu-id="8f19b-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="8f19b-135">För reglerna om sena regler för hur partnern faktureras, se [Hämta förbruknings data för en Azure-prenumeration](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="8f19b-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="8f19b-136">Den här REST API är växlad.</span><span class="sxs-lookup"><span data-stu-id="8f19b-136">This REST API is paged.</span></span> <span data-ttu-id="8f19b-137">Om nytto lasten för svar är större än en sida måste du följa nästa länk för att få nästa sida med användnings poster.</span><span class="sxs-lookup"><span data-stu-id="8f19b-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

## <a name="c"></a><span data-ttu-id="8f19b-138">C\#</span><span class="sxs-lookup"><span data-stu-id="8f19b-138">C\#</span></span>

<span data-ttu-id="8f19b-139">Så här hämtar du Azures användnings poster:</span><span class="sxs-lookup"><span data-stu-id="8f19b-139">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="8f19b-140">Hämta kund-ID och prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="8f19b-140">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="8f19b-141">Anropa metoden [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) för att returnera en [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) som innehåller användnings posterna.</span><span class="sxs-lookup"><span data-stu-id="8f19b-141">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="8f19b-142">Hämta en uppräknare för Azures användnings poster för att passera användnings sidorna.</span><span class="sxs-lookup"><span data-stu-id="8f19b-142">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="8f19b-143">Det här steget är obligatoriskt eftersom resurs samlingen är växlad.</span><span class="sxs-lookup"><span data-stu-id="8f19b-143">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="8f19b-144">**Exempel**: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="8f19b-144">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="8f19b-145">**Projekt**: SDK-exempel för partner Center</span><span class="sxs-lookup"><span data-stu-id="8f19b-145">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="8f19b-146">**Klass**: GetAzureSubscriptionUtilization.CS</span><span class="sxs-lookup"><span data-stu-id="8f19b-146">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a><span data-ttu-id="8f19b-147">Java</span><span class="sxs-lookup"><span data-stu-id="8f19b-147">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="8f19b-148">För att kunna hämta Azures användnings poster behöver du först ett kund-ID och ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="8f19b-148">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="8f19b-149">Sedan anropar du funktionen **IAzureUtilizationCollection. Query** för att returnera en **ResourceCollection** som innehåller användnings posterna.</span><span class="sxs-lookup"><span data-stu-id="8f19b-149">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="8f19b-150">Eftersom resurs samlingen är växlad måste du hämta en uppräknare för Azures användnings post för att kunna passera användnings sidorna.</span><span class="sxs-lookup"><span data-stu-id="8f19b-150">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="8f19b-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f19b-151">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="8f19b-152">För att kunna hämta Azures användnings poster behöver du först ett kund-ID och ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="8f19b-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="8f19b-153">Sedan anropar du kommandot [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span><span class="sxs-lookup"><span data-stu-id="8f19b-153">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="8f19b-154">Det här kommandot returnerar alla poster som är tillgängliga under den angivna tids perioden.</span><span class="sxs-lookup"><span data-stu-id="8f19b-154">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="8f19b-155">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8f19b-155">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f19b-156">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="8f19b-156">Request syntax</span></span>

| <span data-ttu-id="8f19b-157">Metod</span><span class="sxs-lookup"><span data-stu-id="8f19b-157">Method</span></span> | <span data-ttu-id="8f19b-158">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8f19b-158">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="8f19b-159">**TA**</span><span class="sxs-lookup"><span data-stu-id="8f19b-159">**GET**</span></span> | <span data-ttu-id="8f19b-160">*{baseURL}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/utilizations/Azure? Start \_ tid = {start tid} &slut \_ tid = {slut tid} &granularitet = {kornig het} &Visa \_ information = {True}</span><span class="sxs-lookup"><span data-stu-id="8f19b-160">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8f19b-161">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="8f19b-161">URI parameters</span></span>

<span data-ttu-id="8f19b-162">Använd följande sökväg och frågeparametrar för att hämta användnings posterna.</span><span class="sxs-lookup"><span data-stu-id="8f19b-162">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="8f19b-163">Namn</span><span class="sxs-lookup"><span data-stu-id="8f19b-163">Name</span></span> | <span data-ttu-id="8f19b-164">Typ</span><span class="sxs-lookup"><span data-stu-id="8f19b-164">Type</span></span> | <span data-ttu-id="8f19b-165">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8f19b-165">Required</span></span> | <span data-ttu-id="8f19b-166">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8f19b-166">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="8f19b-167">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="8f19b-167">customer-tenant-id</span></span> | <span data-ttu-id="8f19b-168">sträng</span><span class="sxs-lookup"><span data-stu-id="8f19b-168">string</span></span> | <span data-ttu-id="8f19b-169">Yes</span><span class="sxs-lookup"><span data-stu-id="8f19b-169">Yes</span></span> | <span data-ttu-id="8f19b-170">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="8f19b-170">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="8f19b-171">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="8f19b-171">subscription-id</span></span> | <span data-ttu-id="8f19b-172">sträng</span><span class="sxs-lookup"><span data-stu-id="8f19b-172">string</span></span> | <span data-ttu-id="8f19b-173">Yes</span><span class="sxs-lookup"><span data-stu-id="8f19b-173">Yes</span></span> | <span data-ttu-id="8f19b-174">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="8f19b-174">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="8f19b-175">start_time</span><span class="sxs-lookup"><span data-stu-id="8f19b-175">start_time</span></span> | <span data-ttu-id="8f19b-176">sträng i UTC-datum-och tids förskjutnings format</span><span class="sxs-lookup"><span data-stu-id="8f19b-176">string in UTC date-time offset format</span></span> | <span data-ttu-id="8f19b-177">Yes</span><span class="sxs-lookup"><span data-stu-id="8f19b-177">Yes</span></span> | <span data-ttu-id="8f19b-178">Början av tidsintervallet som representerar när användningen rapporterades i fakturerings systemet.</span><span class="sxs-lookup"><span data-stu-id="8f19b-178">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="8f19b-179">end_time</span><span class="sxs-lookup"><span data-stu-id="8f19b-179">end_time</span></span> | <span data-ttu-id="8f19b-180">sträng i UTC-datum-och tids förskjutnings format</span><span class="sxs-lookup"><span data-stu-id="8f19b-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="8f19b-181">Yes</span><span class="sxs-lookup"><span data-stu-id="8f19b-181">Yes</span></span> | <span data-ttu-id="8f19b-182">Slutet av tidsintervallet som representerar när användningen rapporterades i fakturerings systemet.</span><span class="sxs-lookup"><span data-stu-id="8f19b-182">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="8f19b-183">kornig het</span><span class="sxs-lookup"><span data-stu-id="8f19b-183">granularity</span></span> | <span data-ttu-id="8f19b-184">sträng</span><span class="sxs-lookup"><span data-stu-id="8f19b-184">string</span></span> | <span data-ttu-id="8f19b-185">No</span><span class="sxs-lookup"><span data-stu-id="8f19b-185">No</span></span> | <span data-ttu-id="8f19b-186">Definierar kornig het för användnings agg regeringar.</span><span class="sxs-lookup"><span data-stu-id="8f19b-186">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="8f19b-187">Tillgängliga alternativ är: `daily` (standard) och `hourly` .</span><span class="sxs-lookup"><span data-stu-id="8f19b-187">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="8f19b-188">show_details</span><span class="sxs-lookup"><span data-stu-id="8f19b-188">show_details</span></span> | <span data-ttu-id="8f19b-189">boolean</span><span class="sxs-lookup"><span data-stu-id="8f19b-189">boolean</span></span> | <span data-ttu-id="8f19b-190">No</span><span class="sxs-lookup"><span data-stu-id="8f19b-190">No</span></span> | <span data-ttu-id="8f19b-191">Anger om du vill hämta användnings information på instans nivå.</span><span class="sxs-lookup"><span data-stu-id="8f19b-191">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="8f19b-192">Standardvärdet är `true`.</span><span class="sxs-lookup"><span data-stu-id="8f19b-192">The default is `true`.</span></span> |
| <span data-ttu-id="8f19b-193">ikoner</span><span class="sxs-lookup"><span data-stu-id="8f19b-193">size</span></span> | <span data-ttu-id="8f19b-194">antal</span><span class="sxs-lookup"><span data-stu-id="8f19b-194">number</span></span> | <span data-ttu-id="8f19b-195">No</span><span class="sxs-lookup"><span data-stu-id="8f19b-195">No</span></span> | <span data-ttu-id="8f19b-196">Anger antalet agg regeringar som returneras av ett enda API-anrop.</span><span class="sxs-lookup"><span data-stu-id="8f19b-196">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="8f19b-197">Standardvärdet är 1000.</span><span class="sxs-lookup"><span data-stu-id="8f19b-197">The default is 1000.</span></span> <span data-ttu-id="8f19b-198">Max värdet är 1000.</span><span class="sxs-lookup"><span data-stu-id="8f19b-198">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8f19b-199">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8f19b-199">Request headers</span></span>

<span data-ttu-id="8f19b-200">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8f19b-200">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8f19b-201">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8f19b-201">Request body</span></span>

<span data-ttu-id="8f19b-202">Inget</span><span class="sxs-lookup"><span data-stu-id="8f19b-202">None</span></span>

### <a name="request-example"></a><span data-ttu-id="8f19b-203">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8f19b-203">Request example</span></span>

<span data-ttu-id="8f19b-204">Följande exempel förfrågan ger resultat liknande vad som visas i avstämnings filen för perioden 7/2-8/1.</span><span class="sxs-lookup"><span data-stu-id="8f19b-204">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="8f19b-205">De här resultaten matchar kanske inte exakt (se avsnittet [Azures användnings-API](#azure-utilization-api) för mer information).</span><span class="sxs-lookup"><span data-stu-id="8f19b-205">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="8f19b-206">I den här exempel förfrågan returneras användnings data som rapporter ATS i fakturerings systemet mellan 7/2 kl. 12 (UTC) och 8/2 kl. 12 (UTC).</span><span class="sxs-lookup"><span data-stu-id="8f19b-206">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8f19b-207">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8f19b-207">REST response</span></span>

<span data-ttu-id="8f19b-208">Om det lyckas returnerar den här metoden en samling [Azures användnings post](azure-utilization-record-resources.md) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="8f19b-208">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="8f19b-209">Om Azures användnings data ännu inte är klara i ett beroende system returnerar den här metoden en HTTP-statuskod 204 med ett Retry-After-huvud.</span><span class="sxs-lookup"><span data-stu-id="8f19b-209">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f19b-210">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8f19b-210">Response success and error codes</span></span>

<span data-ttu-id="8f19b-211">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="8f19b-211">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f19b-212">Använd ett verktyg för nätverks spårning för att läsa HTTP-statuskod, [fel kods typ](error-codes.md)och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8f19b-212">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="8f19b-213">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8f19b-213">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
