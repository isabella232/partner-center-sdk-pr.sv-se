---
title: Hämta en kunds användningsposter för Azure
description: Du kan använda API:et för Azure-användning för att hämta användningsposter för en kunds Azure-prenumeration under en angiven tidsperiod.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7024bc65976a9b43a62b66c529d271519181ab23
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874932"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="ef623-103">Hämta en kunds användningsposter för Azure</span><span class="sxs-lookup"><span data-stu-id="ef623-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="ef623-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ef623-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ef623-105">Du kan hämta användningsposter för en kunds Azure-prenumeration under en angiven tidsperiod med hjälp av API:et för Azure-användning.</span><span class="sxs-lookup"><span data-stu-id="ef623-105">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef623-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ef623-106">Prerequisites</span></span>

- <span data-ttu-id="ef623-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ef623-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ef623-108">Det här scenariot stöder autentisering med både fristående app och autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="ef623-108">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="ef623-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ef623-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ef623-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ef623-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ef623-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="ef623-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ef623-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="ef623-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ef623-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="ef623-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ef623-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ef623-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ef623-115">En prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="ef623-115">A subscription identifier.</span></span>

<span data-ttu-id="ef623-116">Det här API:et returnerar förbrukningen per dag och timme för ett godtyckligt tidsintervall.</span><span class="sxs-lookup"><span data-stu-id="ef623-116">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="ef623-117">Det här *API:et stöds dock inte för Azure-planer.*</span><span class="sxs-lookup"><span data-stu-id="ef623-117">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="ef623-118">Om du har en Azure-plan kan du läsa artiklarna Get [invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) (Hämta faktura, ej fakturerade förbrukningsradsobjekt) och Get invoice billed consumption line items instead (Hämta [fakturerade förbrukningsradobjekt i](get-invoice-billed-consumption-lineitems.md) stället).</span><span class="sxs-lookup"><span data-stu-id="ef623-118">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="ef623-119">De här artiklarna beskriver hur du hämtar klassificerad förbrukning på en daglig nivå per mätare per resurs.</span><span class="sxs-lookup"><span data-stu-id="ef623-119">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="ef623-120">Den här förbrukningen motsvarar dagliga kornighetsdata som tillhandahålls av API:et för Azure-användning.</span><span class="sxs-lookup"><span data-stu-id="ef623-120">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="ef623-121">Du måste använda fakturaidentifieraren för att hämta fakturerade användningsdata.</span><span class="sxs-lookup"><span data-stu-id="ef623-121">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="ef623-122">Eller så kan du använda aktuella och tidigare perioder för att få uppskattningar av ej fakturerad användning.</span><span class="sxs-lookup"><span data-stu-id="ef623-122">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="ef623-123">*Intervalldata per timme och filter för godtyckligt datumintervall stöds för närvarande inte för Prenumerationsresurser för Azure-plan.*</span><span class="sxs-lookup"><span data-stu-id="ef623-123">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="ef623-124">API för Azure-användning</span><span class="sxs-lookup"><span data-stu-id="ef623-124">Azure utilization API</span></span>

<span data-ttu-id="ef623-125">Det här API:et för Azure-användning ger åtkomst till användningsposter under en tidsperiod som representerar när användningen rapporterades i faktureringssystemet.</span><span class="sxs-lookup"><span data-stu-id="ef623-125">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="ef623-126">Den ger åtkomst till samma användningsdata som används för att skapa och beräkna avstämningsfilen.</span><span class="sxs-lookup"><span data-stu-id="ef623-126">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="ef623-127">Den har dock inte kunskap om fillogik för faktureringssystemavstämning.</span><span class="sxs-lookup"><span data-stu-id="ef623-127">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="ef623-128">Du bör inte förvänta dig att sammanfattningsresultaten för avstämningsfilen matchar resultatet som hämtats från det här API:et exakt under samma tidsperiod.</span><span class="sxs-lookup"><span data-stu-id="ef623-128">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="ef623-129">Faktureringssystemet använder till exempel samma användningsdata och tillämpar regler för senhet för att fastställa vad som redovisas i en avstämningsfil.</span><span class="sxs-lookup"><span data-stu-id="ef623-129">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="ef623-130">När en faktureringsperiod stängs inkluderas all användning fram till slutet av den dag då faktureringsperioden slutar i avstämningsfilen.</span><span class="sxs-lookup"><span data-stu-id="ef623-130">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="ef623-131">Sen användning inom faktureringsperioden som rapporteras inom 24 timmar efter faktureringsperiodens slut redovisas i nästa avstämningsfil.</span><span class="sxs-lookup"><span data-stu-id="ef623-131">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="ef623-132">Information om lateness-reglerna för hur partnern faktureras finns i [Hämta förbrukningsdata för en Azure-prenumeration.](/previous-versions/azure/reference/mt219001(v=azure.100))</span><span class="sxs-lookup"><span data-stu-id="ef623-132">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="ef623-133">Den REST API är sidindelade.</span><span class="sxs-lookup"><span data-stu-id="ef623-133">This REST API is paged.</span></span> <span data-ttu-id="ef623-134">Om svarsnyttolasten är större än en enda sida måste du följa nästa länk för att hämta nästa sida med användningsposter.</span><span class="sxs-lookup"><span data-stu-id="ef623-134">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

### <a name="scenario-partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a><span data-ttu-id="ef623-135">Scenario: Partner A har överfört faktureringsägarskapet för den äldre Azure-prenumerationen (145P) till Partner B</span><span class="sxs-lookup"><span data-stu-id="ef623-135">Scenario: Partner A has transferred billing ownership of Azure Legacy Subscription (145P) to Partner B</span></span>

<span data-ttu-id="ef623-136">Om en partner överför faktureringsägarskapet för en äldre Azure-prenumeration till en annan partner måste den nya partnern, när den nya partnern anropar Utilization API för den överförda prenumerationen, använda Commerce Subscription ID (som visas i partnercenterkontot) i stället för Azure-berättigande-ID:t.</span><span class="sxs-lookup"><span data-stu-id="ef623-136">If a partner transfers billing ownership of an Azure legacy subscription to another partner, when new the new partner calls Utilization API for transferred subscription they have to use Commerce Subscription ID (which shows up in their Partner Center account) rather than the Azure Entitlement ID.</span></span> <span data-ttu-id="ef623-137">Azure-berättigande-ID visas endast för Partner B när de är administratör för (AOBO) till kundens Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ef623-137">Azure Entitlement ID appears for Partner B only when they are Admin on behalf of (AOBO) to Customer's Azure portal.</span></span> 

<span data-ttu-id="ef623-138">För att kunna anropa utilization-API:et för den överförda prenumerationen måste den nya partnern använda commerce-prenumerations-ID:t.</span><span class="sxs-lookup"><span data-stu-id="ef623-138">To successfully call the Utilization API for the transferred subscription, the new partner needs to use the Commerce Subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="ef623-139">C\#</span><span class="sxs-lookup"><span data-stu-id="ef623-139">C\#</span></span>

<span data-ttu-id="ef623-140">Så här hämtar du Azure-användningsposterna:</span><span class="sxs-lookup"><span data-stu-id="ef623-140">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="ef623-141">Hämta kund-ID och prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="ef623-141">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="ef623-142">Anropa metoden [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) för att returnera [**en ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) som innehåller användningsposterna.</span><span class="sxs-lookup"><span data-stu-id="ef623-142">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="ef623-143">Hämta en uppräkning av Azure-användningsposten för att bläddra bland användningssidorna.</span><span class="sxs-lookup"><span data-stu-id="ef623-143">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="ef623-144">Det här steget krävs eftersom resurssamlingen är sidindelade.</span><span class="sxs-lookup"><span data-stu-id="ef623-144">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="ef623-145">**Exempel:** [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ef623-145">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ef623-146">**Project:** Partnercenter-SDK exempel</span><span class="sxs-lookup"><span data-stu-id="ef623-146">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="ef623-147">**Klass:** GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="ef623-147">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

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

## <a name="java"></a><span data-ttu-id="ef623-148">Java</span><span class="sxs-lookup"><span data-stu-id="ef623-148">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="ef623-149">För att hämta Azure-användningsposterna behöver du först en kundidentifierare och en prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="ef623-149">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="ef623-150">Sedan anropar du **funktionen IAzureUtilizationCollection.query** för att returnera **en ResourceCollection** som innehåller användningsposterna.</span><span class="sxs-lookup"><span data-stu-id="ef623-150">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="ef623-151">Eftersom resurssamlingen är sidindelade måste du hämta en uppräkning av Azure-användningsposten för att gå igenom användningssidorna.</span><span class="sxs-lookup"><span data-stu-id="ef623-151">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="ef623-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef623-152">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="ef623-153">För att hämta Azure-användningsposterna behöver du först en kundidentifierare och en prenumerationsidentifierare.</span><span class="sxs-lookup"><span data-stu-id="ef623-153">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="ef623-154">Sedan anropar du [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span><span class="sxs-lookup"><span data-stu-id="ef623-154">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="ef623-155">Det här kommandot returnerar alla poster som är tillgängliga under den angivna tidsperioden.</span><span class="sxs-lookup"><span data-stu-id="ef623-155">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="ef623-156">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ef623-156">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ef623-157">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ef623-157">Request syntax</span></span>

| <span data-ttu-id="ef623-158">Metod</span><span class="sxs-lookup"><span data-stu-id="ef623-158">Method</span></span> | <span data-ttu-id="ef623-159">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ef623-159">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="ef623-160">**Få**</span><span class="sxs-lookup"><span data-stu-id="ef623-160">**GET**</span></span> | <span data-ttu-id="ef623-161">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start \_ time={start-time}&end \_ time={end-time}&granularity={granularity}&show \_ details={True}</span><span class="sxs-lookup"><span data-stu-id="ef623-161">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="ef623-162">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="ef623-162">URI parameters</span></span>

<span data-ttu-id="ef623-163">Använd följande sökväg och frågeparametrar för att hämta användningsposterna.</span><span class="sxs-lookup"><span data-stu-id="ef623-163">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="ef623-164">Namn</span><span class="sxs-lookup"><span data-stu-id="ef623-164">Name</span></span> | <span data-ttu-id="ef623-165">Typ</span><span class="sxs-lookup"><span data-stu-id="ef623-165">Type</span></span> | <span data-ttu-id="ef623-166">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ef623-166">Required</span></span> | <span data-ttu-id="ef623-167">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ef623-167">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="ef623-168">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="ef623-168">customer-tenant-id</span></span> | <span data-ttu-id="ef623-169">sträng</span><span class="sxs-lookup"><span data-stu-id="ef623-169">string</span></span> | <span data-ttu-id="ef623-170">Ja</span><span class="sxs-lookup"><span data-stu-id="ef623-170">Yes</span></span> | <span data-ttu-id="ef623-171">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="ef623-171">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="ef623-172">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="ef623-172">subscription-id</span></span> | <span data-ttu-id="ef623-173">sträng</span><span class="sxs-lookup"><span data-stu-id="ef623-173">string</span></span> | <span data-ttu-id="ef623-174">Ja</span><span class="sxs-lookup"><span data-stu-id="ef623-174">Yes</span></span> | <span data-ttu-id="ef623-175">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="ef623-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="ef623-176">start_time</span><span class="sxs-lookup"><span data-stu-id="ef623-176">start_time</span></span> | <span data-ttu-id="ef623-177">sträng i UTC-format för datum/tid-förskjutning</span><span class="sxs-lookup"><span data-stu-id="ef623-177">string in UTC date-time offset format</span></span> | <span data-ttu-id="ef623-178">Ja</span><span class="sxs-lookup"><span data-stu-id="ef623-178">Yes</span></span> | <span data-ttu-id="ef623-179">Starten av det tidsperiod som representerar när användningen rapporterades i faktureringssystemet.</span><span class="sxs-lookup"><span data-stu-id="ef623-179">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="ef623-180">end_time</span><span class="sxs-lookup"><span data-stu-id="ef623-180">end_time</span></span> | <span data-ttu-id="ef623-181">sträng i UTC-format för datum/tid-förskjutning</span><span class="sxs-lookup"><span data-stu-id="ef623-181">string in UTC date-time offset format</span></span> | <span data-ttu-id="ef623-182">Ja</span><span class="sxs-lookup"><span data-stu-id="ef623-182">Yes</span></span> | <span data-ttu-id="ef623-183">Slutet av det tidsperiod som representerar när användningen rapporterades i faktureringssystemet.</span><span class="sxs-lookup"><span data-stu-id="ef623-183">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="ef623-184">Granularitet</span><span class="sxs-lookup"><span data-stu-id="ef623-184">granularity</span></span> | <span data-ttu-id="ef623-185">sträng</span><span class="sxs-lookup"><span data-stu-id="ef623-185">string</span></span> | <span data-ttu-id="ef623-186">No</span><span class="sxs-lookup"><span data-stu-id="ef623-186">No</span></span> | <span data-ttu-id="ef623-187">Definierar kornigheten för användningsaggregeringar.</span><span class="sxs-lookup"><span data-stu-id="ef623-187">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="ef623-188">Tillgängliga alternativ är: `daily` (standard) och `hourly` .</span><span class="sxs-lookup"><span data-stu-id="ef623-188">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="ef623-189">show_details</span><span class="sxs-lookup"><span data-stu-id="ef623-189">show_details</span></span> | <span data-ttu-id="ef623-190">boolean</span><span class="sxs-lookup"><span data-stu-id="ef623-190">boolean</span></span> | <span data-ttu-id="ef623-191">Inga</span><span class="sxs-lookup"><span data-stu-id="ef623-191">No</span></span> | <span data-ttu-id="ef623-192">Anger om du vill hämta användningsinformation på instansnivå.</span><span class="sxs-lookup"><span data-stu-id="ef623-192">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="ef623-193">Standardvärdet är `true`.</span><span class="sxs-lookup"><span data-stu-id="ef623-193">The default is `true`.</span></span> |
| <span data-ttu-id="ef623-194">ikoner</span><span class="sxs-lookup"><span data-stu-id="ef623-194">size</span></span> | <span data-ttu-id="ef623-195">antal</span><span class="sxs-lookup"><span data-stu-id="ef623-195">number</span></span> | <span data-ttu-id="ef623-196">Inga</span><span class="sxs-lookup"><span data-stu-id="ef623-196">No</span></span> | <span data-ttu-id="ef623-197">Anger antalet aggregeringar som returneras av ett enda API-anrop.</span><span class="sxs-lookup"><span data-stu-id="ef623-197">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="ef623-198">Standardvärdet är 1000.</span><span class="sxs-lookup"><span data-stu-id="ef623-198">The default is 1000.</span></span> <span data-ttu-id="ef623-199">Max är 1 000.</span><span class="sxs-lookup"><span data-stu-id="ef623-199">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ef623-200">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ef623-200">Request headers</span></span>

<span data-ttu-id="ef623-201">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ef623-201">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ef623-202">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ef623-202">Request body</span></span>

<span data-ttu-id="ef623-203">Ingen</span><span class="sxs-lookup"><span data-stu-id="ef623-203">None</span></span>

### <a name="request-example"></a><span data-ttu-id="ef623-204">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ef623-204">Request example</span></span>

<span data-ttu-id="ef623-205">Följande exempelbegäran ger resultat som liknar det som avstämningsfilen visar för perioden 7/2–8/1.</span><span class="sxs-lookup"><span data-stu-id="ef623-205">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="ef623-206">Dessa resultat kanske inte matchar exakt (mer information finns i [avsnittet API för Azure-användning).](#azure-utilization-api)</span><span class="sxs-lookup"><span data-stu-id="ef623-206">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="ef623-207">Den här exempelbegäran returnerar användningsdata som rapporteras i faktureringssystemet mellan 7/2 kl. 12:00 (UTC) och 8/2 kl. 12:00 (UTC).</span><span class="sxs-lookup"><span data-stu-id="ef623-207">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ef623-208">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ef623-208">REST response</span></span>

<span data-ttu-id="ef623-209">Om det lyckas returnerar den här metoden en samling [Azure Utilization Record-resurser](azure-utilization-record-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="ef623-209">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="ef623-210">Om Azure-användningsdata ännu inte är redo i ett beroende system returnerar den här metoden HTTP-statuskod 204 med ett Retry-After huvud.</span><span class="sxs-lookup"><span data-stu-id="ef623-210">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ef623-211">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ef623-211">Response success and error codes</span></span>

<span data-ttu-id="ef623-212">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ef623-212">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ef623-213">Använd ett nätverksspårningsverktyg för att läsa HTTP-statuskoden, [felkodstypen](error-codes.md)och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ef623-213">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="ef623-214">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ef623-214">Response example</span></span>

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
