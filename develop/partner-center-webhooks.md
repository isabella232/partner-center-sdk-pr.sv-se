---
title: Partnercenter – webhooks
description: Med Webhooks kan partner registrera sig för resurs ändrings händelser.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8225623ade7e922ac23ebf0ed9215686b0601244
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769225"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="75a3e-103">Partnercenter – webhooks</span><span class="sxs-lookup"><span data-stu-id="75a3e-103">Partner Center webhooks</span></span>

<span data-ttu-id="75a3e-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="75a3e-104">**Applies To**</span></span>

- <span data-ttu-id="75a3e-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="75a3e-105">Partner Center</span></span>
- <span data-ttu-id="75a3e-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="75a3e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="75a3e-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="75a3e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="75a3e-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="75a3e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="75a3e-109">API: erna för webhook i Partner Center gör att partner kan registrera sig för resurs ändrings händelser.</span><span class="sxs-lookup"><span data-stu-id="75a3e-109">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="75a3e-110">Dessa händelser levereras i form av HTTP-inlägg till partnerns registrerade URL.</span><span class="sxs-lookup"><span data-stu-id="75a3e-110">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="75a3e-111">För att ta emot en händelse från Partner Center, kommer partner att vara värd för ett återanrop där Partner Center kan publicera resurs ändrings händelsen.</span><span class="sxs-lookup"><span data-stu-id="75a3e-111">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="75a3e-112">Händelsen signeras digitalt så att partnern kan verifiera att den har skickats från Partner Center.</span><span class="sxs-lookup"><span data-stu-id="75a3e-112">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="75a3e-113">Partner kan välja mellan webhook-händelser, som följande exempel, som stöds av Partner Center.</span><span class="sxs-lookup"><span data-stu-id="75a3e-113">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="75a3e-114">**Test event ("test-created")**</span><span class="sxs-lookup"><span data-stu-id="75a3e-114">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="75a3e-115">Med den här händelsen kan du själv publicera och testa registreringen genom att begära ett test händelser och sedan följa förloppet.</span><span class="sxs-lookup"><span data-stu-id="75a3e-115">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="75a3e-116">Du kan se de fel meddelanden som tas emot från Microsoft när du försöker leverera evenemanget.</span><span class="sxs-lookup"><span data-stu-id="75a3e-116">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="75a3e-117">Den här begränsningen gäller endast för "test-skapade"-händelser.</span><span class="sxs-lookup"><span data-stu-id="75a3e-117">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="75a3e-118">Data som är äldre än sju dagar rensas.</span><span class="sxs-lookup"><span data-stu-id="75a3e-118">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="75a3e-119">**Prenumerationen har uppdaterats ("prenumerationen har uppdaterats")**</span><span class="sxs-lookup"><span data-stu-id="75a3e-119">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="75a3e-120">Den här händelsen inträffar när prenumerationen ändras.</span><span class="sxs-lookup"><span data-stu-id="75a3e-120">This event is raised when the subscription changes.</span></span> <span data-ttu-id="75a3e-121">Dessa händelser genereras när det finns en intern ändring utöver när ändringar görs via partner Center-API: et.</span><span class="sxs-lookup"><span data-stu-id="75a3e-121">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="75a3e-122">Det finns en fördröjning på upp till 48 timmar mellan den tidpunkt då en prenumeration ändras och när händelsen uppdatering av prenumeration utlöses.</span><span class="sxs-lookup"><span data-stu-id="75a3e-122">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="75a3e-123">**Tröskeln överskreds för händelsen ("usagerecords-thresholdExceeded")**</span><span class="sxs-lookup"><span data-stu-id="75a3e-123">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="75a3e-124">Den här händelsen inträffar när mängden Microsoft Azure användning för en kund överskrider deras användnings utgifts budget (tröskel).</span><span class="sxs-lookup"><span data-stu-id="75a3e-124">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="75a3e-125">Mer information finns i [ställa in en Azure utgifts budget för dina kunder/Partner Center/set-a-Azure-utgifter-budget – för-kunder).</span><span class="sxs-lookup"><span data-stu-id="75a3e-125">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="75a3e-126">**Händelse som skapats av hänvisning ("hänvisning skapad")**</span><span class="sxs-lookup"><span data-stu-id="75a3e-126">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="75a3e-127">Den här händelsen inträffar när referensen skapas.</span><span class="sxs-lookup"><span data-stu-id="75a3e-127">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="75a3e-128">**Referens för uppdaterad händelse ("hänvisning – uppdaterad")**</span><span class="sxs-lookup"><span data-stu-id="75a3e-128">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="75a3e-129">Den här händelsen utlöses när hänvisningen uppdateras.</span><span class="sxs-lookup"><span data-stu-id="75a3e-129">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="75a3e-130">**Faktura klar händelse ("faktura klar")**</span><span class="sxs-lookup"><span data-stu-id="75a3e-130">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="75a3e-131">Den här händelsen inträffar när den nya fakturan är klar.</span><span class="sxs-lookup"><span data-stu-id="75a3e-131">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="75a3e-132">Framtida webhook-händelser kommer att läggas till för resurser som ändras i systemet som partnern inte har kontroll över, och ytterligare uppdateringar görs för att få dessa händelser så nära "real tid" som möjligt.</span><span class="sxs-lookup"><span data-stu-id="75a3e-132">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="75a3e-133">Feedback från partner på vilka händelser som lägger till värde i deras verksamhet är användbara när du ska avgöra vilka nya händelser som ska läggas till.</span><span class="sxs-lookup"><span data-stu-id="75a3e-133">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="75a3e-134">En fullständig lista med webhook-händelser som stöds av Partner Center finns i [partner Center webhook-händelser](partner-center-webhook-events.md).</span><span class="sxs-lookup"><span data-stu-id="75a3e-134">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75a3e-135">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="75a3e-135">Prerequisites</span></span>

- <span data-ttu-id="75a3e-136">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="75a3e-136">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="75a3e-137">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="75a3e-137">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="75a3e-138">Ta emot händelser från Partner Center</span><span class="sxs-lookup"><span data-stu-id="75a3e-138">Receiving events from Partner Center</span></span>

<span data-ttu-id="75a3e-139">För att ta emot händelser från Partner Center måste du exponera en offentligt tillgänglig slut punkt.</span><span class="sxs-lookup"><span data-stu-id="75a3e-139">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="75a3e-140">Eftersom den här slut punkten visas måste du kontrol lera att kommunikationen är från Partner Center.</span><span class="sxs-lookup"><span data-stu-id="75a3e-140">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="75a3e-141">Alla webhook-händelser som du får är digitalt signerade med ett certifikat som är kopplat till Microsoft-roten.</span><span class="sxs-lookup"><span data-stu-id="75a3e-141">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="75a3e-142">En länk till certifikatet som används för att signera händelsen kommer också att tillhandahållas.</span><span class="sxs-lookup"><span data-stu-id="75a3e-142">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="75a3e-143">Detta gör att certifikatet kan förnyas utan att du behöver distribuera om eller konfigurera om tjänsten.</span><span class="sxs-lookup"><span data-stu-id="75a3e-143">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="75a3e-144">Partner Center kommer att göra 10 försök att leverera händelsen.</span><span class="sxs-lookup"><span data-stu-id="75a3e-144">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="75a3e-145">Om händelsen fortfarande inte levereras efter 10 försök kommer den att flyttas till en offline-kö och inga ytterligare försök görs vid leverans.</span><span class="sxs-lookup"><span data-stu-id="75a3e-145">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="75a3e-146">I följande exempel visas en händelse som publicerats från Partner Center.</span><span class="sxs-lookup"><span data-stu-id="75a3e-146">The following sample shows an event posted from Partner Center.</span></span>

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
><span data-ttu-id="75a3e-147">Authorization-huvudet har ett schema för "signatur".</span><span class="sxs-lookup"><span data-stu-id="75a3e-147">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="75a3e-148">Det här är en Base64-kodad signatur för innehållet.</span><span class="sxs-lookup"><span data-stu-id="75a3e-148">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="75a3e-149">Så här autentiserar du motringningen</span><span class="sxs-lookup"><span data-stu-id="75a3e-149">How to authenticate the callback</span></span>

<span data-ttu-id="75a3e-150">Följ dessa steg om du vill autentisera återanrops händelsen som tas emot från Partner Center:</span><span class="sxs-lookup"><span data-stu-id="75a3e-150">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="75a3e-151">Kontrol lera att de nödvändiga rubrikerna finns (auktorisering, x-MS-Certificate-URL, x-MS-Signature-Algorithm).</span><span class="sxs-lookup"><span data-stu-id="75a3e-151">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="75a3e-152">Hämta certifikatet som används för att signera innehållet (x-MS-Certificate-URL).</span><span class="sxs-lookup"><span data-stu-id="75a3e-152">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="75a3e-153">Verifiera certifikat kedjan.</span><span class="sxs-lookup"><span data-stu-id="75a3e-153">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="75a3e-154">Kontrol lera "organisationen" för certifikatet.</span><span class="sxs-lookup"><span data-stu-id="75a3e-154">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="75a3e-155">Läs innehållet med UTF8-kodning i en buffert.</span><span class="sxs-lookup"><span data-stu-id="75a3e-155">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="75a3e-156">Skapa en RSA-Krypto-Provider.</span><span class="sxs-lookup"><span data-stu-id="75a3e-156">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="75a3e-157">Kontrol lera att data matchar vad som har signerats med angiven hash-algoritm (till exempel SHA256).</span><span class="sxs-lookup"><span data-stu-id="75a3e-157">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="75a3e-158">Om verifieringen lyckas, behandla meddelandet.</span><span class="sxs-lookup"><span data-stu-id="75a3e-158">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="75a3e-159">Som standard skickas signaturens token i ett Authorization-huvud.</span><span class="sxs-lookup"><span data-stu-id="75a3e-159">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="75a3e-160">Om du anger **SignatureTokenToMsSignatureHeader** till sant i registreringen skickas signaturens token i huvudet x-MS-signatur i stället.</span><span class="sxs-lookup"><span data-stu-id="75a3e-160">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="75a3e-161">Händelse modell</span><span class="sxs-lookup"><span data-stu-id="75a3e-161">Event model</span></span>

<span data-ttu-id="75a3e-162">I följande tabell beskrivs egenskaperna för ett partner Center-evenemang.</span><span class="sxs-lookup"><span data-stu-id="75a3e-162">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="75a3e-163">Egenskaper</span><span class="sxs-lookup"><span data-stu-id="75a3e-163">Properties</span></span>

| <span data-ttu-id="75a3e-164">Name</span><span class="sxs-lookup"><span data-stu-id="75a3e-164">Name</span></span>                      | <span data-ttu-id="75a3e-165">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="75a3e-165">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="75a3e-166">**EventName**</span><span class="sxs-lookup"><span data-stu-id="75a3e-166">**EventName**</span></span>             | <span data-ttu-id="75a3e-167">Händelsens namn.</span><span class="sxs-lookup"><span data-stu-id="75a3e-167">The name of the event.</span></span> <span data-ttu-id="75a3e-168">I formatet {Resource}-{action}.</span><span class="sxs-lookup"><span data-stu-id="75a3e-168">In the form {resource}-{action}.</span></span> <span data-ttu-id="75a3e-169">Till exempel "test-created".</span><span class="sxs-lookup"><span data-stu-id="75a3e-169">For example, "test-created".</span></span>  |
| <span data-ttu-id="75a3e-170">**ResourceUri**</span><span class="sxs-lookup"><span data-stu-id="75a3e-170">**ResourceUri**</span></span>           | <span data-ttu-id="75a3e-171">URI för den resurs som ändrades.</span><span class="sxs-lookup"><span data-stu-id="75a3e-171">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="75a3e-172">**ResourceName**</span><span class="sxs-lookup"><span data-stu-id="75a3e-172">**ResourceName**</span></span>          | <span data-ttu-id="75a3e-173">Namnet på den resurs som ändrades.</span><span class="sxs-lookup"><span data-stu-id="75a3e-173">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="75a3e-174">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="75a3e-174">**AuditUrl**</span></span>              | <span data-ttu-id="75a3e-175">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="75a3e-175">Optional.</span></span> <span data-ttu-id="75a3e-176">Gransknings postens URI.</span><span class="sxs-lookup"><span data-stu-id="75a3e-176">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="75a3e-177">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="75a3e-177">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="75a3e-178">Datum och tid i UTC-format när resurs ändringen utfördes.</span><span class="sxs-lookup"><span data-stu-id="75a3e-178">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="75a3e-179">Exempel</span><span class="sxs-lookup"><span data-stu-id="75a3e-179">Sample</span></span>

<span data-ttu-id="75a3e-180">Följande exempel visar strukturen för ett partner Center-evenemang.</span><span class="sxs-lookup"><span data-stu-id="75a3e-180">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="75a3e-181">Webhook-API: er</span><span class="sxs-lookup"><span data-stu-id="75a3e-181">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="75a3e-182">Autentisering</span><span class="sxs-lookup"><span data-stu-id="75a3e-182">Authentication</span></span>

<span data-ttu-id="75a3e-183">Alla anrop till webhook-API: erna autentiseras med hjälp av Bearer-token i Authorization-huvudet.</span><span class="sxs-lookup"><span data-stu-id="75a3e-183">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="75a3e-184">Hämta en åtkomsttoken för åtkomst `https://api.partnercenter.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="75a3e-184">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="75a3e-185">Denna token är samma token som används för att få åtkomst till resten av API: erna för partner Center.</span><span class="sxs-lookup"><span data-stu-id="75a3e-185">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="75a3e-186">Hämta en lista över händelser</span><span class="sxs-lookup"><span data-stu-id="75a3e-186">Get a list of events</span></span>

<span data-ttu-id="75a3e-187">Returnerar en lista med händelser som för närvarande stöds av webhook-API: erna.</span><span class="sxs-lookup"><span data-stu-id="75a3e-187">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="75a3e-188">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="75a3e-188">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="75a3e-189">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="75a3e-189">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="75a3e-190">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="75a3e-190">Response example</span></span>

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

### <a name="register-to-receive-events"></a><span data-ttu-id="75a3e-191">Registrera dig för att ta emot händelser</span><span class="sxs-lookup"><span data-stu-id="75a3e-191">Register to receive events</span></span>

<span data-ttu-id="75a3e-192">Registrerar en klient för att ta emot de angivna händelserna.</span><span class="sxs-lookup"><span data-stu-id="75a3e-192">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="75a3e-193">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="75a3e-193">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="75a3e-194">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="75a3e-194">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="75a3e-195">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="75a3e-195">Response example</span></span>

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

### <a name="view-a-registration"></a><span data-ttu-id="75a3e-196">Visa en registrering</span><span class="sxs-lookup"><span data-stu-id="75a3e-196">View a registration</span></span>

<span data-ttu-id="75a3e-197">Returnerar en klients händelse registrering för webhookar.</span><span class="sxs-lookup"><span data-stu-id="75a3e-197">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="75a3e-198">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="75a3e-198">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="75a3e-199">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="75a3e-199">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="75a3e-200">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="75a3e-200">Response example</span></span>

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

### <a name="update-an-event-registration"></a><span data-ttu-id="75a3e-201">Uppdatera en händelse registrering</span><span class="sxs-lookup"><span data-stu-id="75a3e-201">Update an event registration</span></span>

<span data-ttu-id="75a3e-202">Uppdaterar en befintlig händelse registrering.</span><span class="sxs-lookup"><span data-stu-id="75a3e-202">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="75a3e-203">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="75a3e-203">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="75a3e-204">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="75a3e-204">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="75a3e-205">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="75a3e-205">Response example</span></span>

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

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="75a3e-206">Skicka en test händelse för att verifiera registreringen</span><span class="sxs-lookup"><span data-stu-id="75a3e-206">Send a test event to validate your registration</span></span>

<span data-ttu-id="75a3e-207">Genererar en test händelse för att verifiera Webhooks-registreringen.</span><span class="sxs-lookup"><span data-stu-id="75a3e-207">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="75a3e-208">Det här testet är avsett att verifiera att du kan ta emot händelser från Partner Center.</span><span class="sxs-lookup"><span data-stu-id="75a3e-208">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="75a3e-209">Data för de här händelserna tas bort sju dagar efter det att den första händelsen har skapats.</span><span class="sxs-lookup"><span data-stu-id="75a3e-209">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="75a3e-210">Du måste vara registrerad för händelsen "test-created", med hjälp av registrerings-API: et, innan du skickar en verifierings händelse.</span><span class="sxs-lookup"><span data-stu-id="75a3e-210">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="75a3e-211">Det finns en begränsning på 2 begär Anden per minut vid bokföring av en validerings händelse.</span><span class="sxs-lookup"><span data-stu-id="75a3e-211">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="75a3e-212">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="75a3e-212">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="75a3e-213">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="75a3e-213">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="75a3e-214">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="75a3e-214">Response example</span></span>

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

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="75a3e-215">Kontrol lera att händelsen har levererats</span><span class="sxs-lookup"><span data-stu-id="75a3e-215">Verify that the event was delivered</span></span>

<span data-ttu-id="75a3e-216">Returnerar det aktuella läget för verifierings händelsen.</span><span class="sxs-lookup"><span data-stu-id="75a3e-216">Returns the current state of the validation event.</span></span> <span data-ttu-id="75a3e-217">Den här verifieringen kan vara till hjälp vid fel sökning av händelse leverans problem.</span><span class="sxs-lookup"><span data-stu-id="75a3e-217">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="75a3e-218">Svaret innehåller ett resultat för varje försök som görs för att leverera händelsen.</span><span class="sxs-lookup"><span data-stu-id="75a3e-218">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="75a3e-219">Resurs-URL</span><span class="sxs-lookup"><span data-stu-id="75a3e-219">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="75a3e-220">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="75a3e-220">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="75a3e-221">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="75a3e-221">Response example</span></span>

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

## <a name="example-for-signature-validation"></a><span data-ttu-id="75a3e-222">Exempel på verifiering av signatur</span><span class="sxs-lookup"><span data-stu-id="75a3e-222">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="75a3e-223">Exempel på signatur för återanrops kontroll (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="75a3e-223">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="75a3e-224">Verifiering av signatur</span><span class="sxs-lookup"><span data-stu-id="75a3e-224">Signature Validation</span></span>

<span data-ttu-id="75a3e-225">I följande exempel visas hur du lägger till ett Authorization-attribut till den kontroll enhet som tar emot återanrop från webhook-händelser.</span><span class="sxs-lookup"><span data-stu-id="75a3e-225">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

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
