---
title: Partnercenter – webhooks
description: Med webhooks kan partner registrera sig för resursändringshändelser.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 74d5981436ba29ea4f6f93a5693ec6da82777eb4
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547758"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="3ca1d-103">Partnercenter – webhooks</span><span class="sxs-lookup"><span data-stu-id="3ca1d-103">Partner Center webhooks</span></span>

<span data-ttu-id="3ca1d-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3ca1d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3ca1d-105">Med Webhook-API:erna i Partnercenter kan partner registrera sig för resursändringshändelser.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-105">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="3ca1d-106">Dessa händelser levereras i form av HTTP-POST:er till partnerns registrerade URL.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-106">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="3ca1d-107">För att ta emot en händelse från Partnercenter är partner värd för ett återanrop där Partnercenter kan PUBLICERA resursändringshändelsen.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-107">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="3ca1d-108">Händelsen signeras digitalt så att partnern kan verifiera att den skickades från Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-108">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="3ca1d-109">Partner kan välja bland Webhook-händelser, som i följande exempel, som stöds av Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-109">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="3ca1d-110">**Testhändelse ("testskapad")**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-110">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="3ca1d-111">Med den här händelsen kan du registrera dig själv och testa registreringen genom att begära en testhändelse och sedan spåra förloppet.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-111">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="3ca1d-112">Du kan se felmeddelanden som tas emot från Microsoft när du försöker leverera händelsen.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-112">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="3ca1d-113">Den här begränsningen gäller endast för "testskapade" händelser.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-113">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="3ca1d-114">Data som är äldre än sju dagar rensas.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-114">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="3ca1d-115">**Händelse med uppdaterad prenumeration ("prenumerations uppdaterad")**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-115">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="3ca1d-116">Den här händelsen utlöses när prenumerationen ändras.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-116">This event is raised when the subscription changes.</span></span> <span data-ttu-id="3ca1d-117">Dessa händelser genereras när det sker en intern ändring utöver när ändringar görs via Partner Center-API:et.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-117">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3ca1d-118">Det finns en fördröjning på upp till 48 timmar mellan den tidpunkt då en prenumeration ändras och när den uppdaterade prenumerationshändelsen utlöses.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-118">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="3ca1d-119">**Tröskel överskred händelse ("usagerecords-thresholdExceeded")**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-119">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="3ca1d-120">Den här händelsen utlöses när mängden Microsoft Azure för en kund överskrider sin utgiftsbudget för användning (deras tröskelvärde).</span><span class="sxs-lookup"><span data-stu-id="3ca1d-120">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="3ca1d-121">Mer information finns i [Ange en Azure-utgiftsbudget för dina kunder/partnercenter/set-an-azure-spending-budget-for-your-customers).</span><span class="sxs-lookup"><span data-stu-id="3ca1d-121">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="3ca1d-122">**Skapad referenshändelse ("hänvisningsskapad")**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-122">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="3ca1d-123">Den här händelsen utlöses när hänvisningen skapas.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-123">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="3ca1d-124">**Uppdaterad referenshändelse ("hänvisnings uppdaterad")**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-124">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="3ca1d-125">Den här händelsen utlöses när hänvisningen uppdateras.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-125">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="3ca1d-126">**Fakturaklar händelse ("fakturaklar")**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-126">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="3ca1d-127">Den här händelsen utlöses när den nya fakturan är klar.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-127">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="3ca1d-128">Framtida Webhook-händelser läggs till för resurser som ändras i systemet som partnern inte har kontroll över, och ytterligare uppdateringar kommer att göras för att få dessa händelser så nära "realtid" som möjligt.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-128">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="3ca1d-129">Feedback från partner om vilka händelser som tillför värde i verksamheten är användbart för att avgöra vilka nya händelser som ska läggas till.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-129">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="3ca1d-130">En fullständig lista över Webhook-händelser som stöds av Partnercenter finns i [Webhook-händelser i Partnercenter.](partner-center-webhook-events.md)</span><span class="sxs-lookup"><span data-stu-id="3ca1d-130">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ca1d-131">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3ca1d-131">Prerequisites</span></span>

- <span data-ttu-id="3ca1d-132">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3ca1d-132">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3ca1d-133">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-133">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="3ca1d-134">Ta emot händelser från Partnercenter</span><span class="sxs-lookup"><span data-stu-id="3ca1d-134">Receiving events from Partner Center</span></span>

<span data-ttu-id="3ca1d-135">Om du vill ta emot händelser från Partnercenter måste du exponera en offentligt tillgänglig slutpunkt.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-135">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="3ca1d-136">Eftersom den här slutpunkten exponeras måste du verifiera att kommunikationen kommer från Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-136">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="3ca1d-137">Alla Webhook-händelser som du får är digitalt signerade med ett certifikat som är kedjor till Microsoft Root.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-137">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="3ca1d-138">En länk till certifikatet som används för att signera händelsen tillhandahålls också.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-138">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="3ca1d-139">Detta gör att certifikatet kan förnyas utan att du behöver distribuera om eller konfigurera om tjänsten.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-139">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="3ca1d-140">Partnercenter gör 10 försök att leverera händelsen.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-140">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="3ca1d-141">Om händelsen fortfarande inte levereras efter 10 försök flyttas den till en offlinekö och inga ytterligare försök görs vid leverans.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-141">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="3ca1d-142">I följande exempel visas en händelse som publicerats från Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-142">The following sample shows an event posted from Partner Center.</span></span>

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

>[!NOTE]
><span data-ttu-id="3ca1d-143">Auktoriseringsrubriken har schemat "Signatur".</span><span class="sxs-lookup"><span data-stu-id="3ca1d-143">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="3ca1d-144">Det här är en base64-kodad signatur för innehållet.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-144">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="3ca1d-145">Så här autentiserar du motringning</span><span class="sxs-lookup"><span data-stu-id="3ca1d-145">How to authenticate the callback</span></span>

<span data-ttu-id="3ca1d-146">Följ dessa steg om du vill autentisera återanropshändelsen som tas emot från Partnercenter:</span><span class="sxs-lookup"><span data-stu-id="3ca1d-146">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="3ca1d-147">Kontrollera att de nödvändiga huvudena finns (Auktorisering, x-ms-certificate-url, x-ms-signature-algorithm).</span><span class="sxs-lookup"><span data-stu-id="3ca1d-147">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="3ca1d-148">Ladda ned certifikatet som används för att signera innehållet (x-ms-certificate-url).</span><span class="sxs-lookup"><span data-stu-id="3ca1d-148">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="3ca1d-149">Verifiera certifikatkedjan.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-149">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="3ca1d-150">Kontrollera certifikatets "organisation".</span><span class="sxs-lookup"><span data-stu-id="3ca1d-150">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="3ca1d-151">Läs innehållet med UTF8-kodning i en buffert.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-151">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="3ca1d-152">Skapa en RSA Crypto-provider.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-152">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="3ca1d-153">Kontrollera att data matchar det som signerats med den angivna hash-algoritmen (till exempel SHA256).</span><span class="sxs-lookup"><span data-stu-id="3ca1d-153">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="3ca1d-154">Om verifieringen lyckas bearbetar du meddelandet.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-154">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="3ca1d-155">Som standard skickas signaturtoken i ett auktoriseringshuvud.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-155">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="3ca1d-156">Om du ställer in **SignatureTokenToMsSignatureHeader** på true i din registrering skickas signaturtoken i huvudet x-ms-signature i stället.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-156">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="3ca1d-157">Händelsemodell</span><span class="sxs-lookup"><span data-stu-id="3ca1d-157">Event model</span></span>

<span data-ttu-id="3ca1d-158">I följande tabell beskrivs egenskaperna för en Partnercenter-händelse.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-158">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="3ca1d-159">Egenskaper</span><span class="sxs-lookup"><span data-stu-id="3ca1d-159">Properties</span></span>

| <span data-ttu-id="3ca1d-160">Name</span><span class="sxs-lookup"><span data-stu-id="3ca1d-160">Name</span></span>                      | <span data-ttu-id="3ca1d-161">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3ca1d-161">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="3ca1d-162">**EventName**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-162">**EventName**</span></span>             | <span data-ttu-id="3ca1d-163">Namnet på händelsen.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-163">The name of the event.</span></span> <span data-ttu-id="3ca1d-164">I formuläret {resource}-{action}.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-164">In the form {resource}-{action}.</span></span> <span data-ttu-id="3ca1d-165">Till exempel "test-created".</span><span class="sxs-lookup"><span data-stu-id="3ca1d-165">For example, "test-created".</span></span>  |
| <span data-ttu-id="3ca1d-166">**ResourceUri**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-166">**ResourceUri**</span></span>           | <span data-ttu-id="3ca1d-167">URI:en för resursen som ändrades.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-167">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="3ca1d-168">**ResourceName**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-168">**ResourceName**</span></span>          | <span data-ttu-id="3ca1d-169">Namnet på den resurs som ändrades.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-169">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="3ca1d-170">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-170">**AuditUrl**</span></span>              | <span data-ttu-id="3ca1d-171">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-171">Optional.</span></span> <span data-ttu-id="3ca1d-172">URI för granskningsposten.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-172">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="3ca1d-173">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="3ca1d-173">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="3ca1d-174">Datum och tid, i UTC-format, när resursändringen inträffade.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-174">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="3ca1d-175">Exempel</span><span class="sxs-lookup"><span data-stu-id="3ca1d-175">Sample</span></span>

<span data-ttu-id="3ca1d-176">I följande exempel visas strukturen för en Partnercenter-händelse.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-176">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="3ca1d-177">Webhook-API:er</span><span class="sxs-lookup"><span data-stu-id="3ca1d-177">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="3ca1d-178">Autentisering</span><span class="sxs-lookup"><span data-stu-id="3ca1d-178">Authentication</span></span>

<span data-ttu-id="3ca1d-179">Alla anrop till Webhook-API:erna autentiseras med hjälp av bearer-token i auktoriseringshuvudet.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-179">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="3ca1d-180">Hämta en åtkomsttoken för att få åtkomst `https://api.partnercenter.microsoft.com` till .</span><span class="sxs-lookup"><span data-stu-id="3ca1d-180">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="3ca1d-181">Den här token är samma token som används för att komma åt resten av Partner Center-API:erna.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-181">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="3ca1d-182">Hämta en lista över händelser</span><span class="sxs-lookup"><span data-stu-id="3ca1d-182">Get a list of events</span></span>

<span data-ttu-id="3ca1d-183">Returnerar en lista över de händelser som för närvarande stöds av Webhook-API:erna.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-183">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="3ca1d-184">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="3ca1d-184">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="3ca1d-185">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3ca1d-185">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="3ca1d-186">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3ca1d-186">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US

[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```

### <a name="register-to-receive-events"></a><span data-ttu-id="3ca1d-187">Registrera dig för att ta emot händelser</span><span class="sxs-lookup"><span data-stu-id="3ca1d-187">Register to receive events</span></span>

<span data-ttu-id="3ca1d-188">Registrerar en klientorganisation för att ta emot de angivna händelserna.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-188">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3ca1d-189">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="3ca1d-189">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="3ca1d-190">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3ca1d-190">Request example</span></span>

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a><span data-ttu-id="3ca1d-191">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3ca1d-191">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="view-a-registration"></a><span data-ttu-id="3ca1d-192">Visa en registrering</span><span class="sxs-lookup"><span data-stu-id="3ca1d-192">View a registration</span></span>

<span data-ttu-id="3ca1d-193">Returnerar webhooks-händelseregistreringen för en klientorganisation.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-193">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3ca1d-194">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="3ca1d-194">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="3ca1d-195">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3ca1d-195">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="3ca1d-196">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3ca1d-196">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="update-an-event-registration"></a><span data-ttu-id="3ca1d-197">Uppdatera en händelseregistrering</span><span class="sxs-lookup"><span data-stu-id="3ca1d-197">Update an event registration</span></span>

<span data-ttu-id="3ca1d-198">Uppdaterar en befintlig händelseregistrering.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-198">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3ca1d-199">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="3ca1d-199">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="3ca1d-200">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3ca1d-200">Request example</span></span>

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a><span data-ttu-id="3ca1d-201">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3ca1d-201">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="3ca1d-202">Skicka en testhändelse för att verifiera registreringen</span><span class="sxs-lookup"><span data-stu-id="3ca1d-202">Send a test event to validate your registration</span></span>

<span data-ttu-id="3ca1d-203">Genererar en testhändelse för att verifiera Webhooks-registreringen.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-203">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="3ca1d-204">Det här testet är avsett att verifiera att du kan ta emot händelser från Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-204">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="3ca1d-205">Data för dessa händelser tas bort sju dagar efter att den första händelsen har skapats.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-205">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="3ca1d-206">Du måste vara registrerad för händelsen "test-created" med hjälp av registrerings-API:et innan du skickar en valideringshändelse.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-206">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="3ca1d-207">Det finns en begränsning på 2 begäranden per minut när du publicerar en valideringshändelse.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-207">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3ca1d-208">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="3ca1d-208">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="3ca1d-209">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3ca1d-209">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="3ca1d-210">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3ca1d-210">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="3ca1d-211">Kontrollera att händelsen har levererats</span><span class="sxs-lookup"><span data-stu-id="3ca1d-211">Verify that the event was delivered</span></span>

<span data-ttu-id="3ca1d-212">Returnerar det aktuella tillståndet för valideringshändelsen.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-212">Returns the current state of the validation event.</span></span> <span data-ttu-id="3ca1d-213">Den här verifieringen kan vara användbar vid felsökning av problem med händelseleverans.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-213">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="3ca1d-214">Svaret innehåller ett resultat för varje försök att leverera händelsen.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-214">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3ca1d-215">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="3ca1d-215">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="3ca1d-216">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3ca1d-216">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="3ca1d-217">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3ca1d-217">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```

## <a name="example-for-signature-validation"></a><span data-ttu-id="3ca1d-218">Exempel för signaturverifiering</span><span class="sxs-lookup"><span data-stu-id="3ca1d-218">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="3ca1d-219">Exempel på återanropskontrollantsignatur (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="3ca1d-219">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="3ca1d-220">Signaturvalidering</span><span class="sxs-lookup"><span data-stu-id="3ca1d-220">Signature Validation</span></span>

<span data-ttu-id="3ca1d-221">I följande exempel visas hur du lägger till ett auktoriseringsattribut till kontrollanten som tar emot återanrop från Webhook-händelser.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-221">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // for example RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
