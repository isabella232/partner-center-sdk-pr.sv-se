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
# <a name="partner-center-webhooks"></a>Partnercenter – webhooks

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Med Webhook-API:erna i Partnercenter kan partner registrera sig för resursändringshändelser. Dessa händelser levereras i form av HTTP-POST:er till partnerns registrerade URL. För att ta emot en händelse från Partnercenter är partner värd för ett återanrop där Partnercenter kan PUBLICERA resursändringshändelsen. Händelsen signeras digitalt så att partnern kan verifiera att den skickades från Partnercenter.

Partner kan välja bland Webhook-händelser, som i följande exempel, som stöds av Partnercenter.

- **Testhändelse ("testskapad")**

    Med den här händelsen kan du registrera dig själv och testa registreringen genom att begära en testhändelse och sedan spåra förloppet. Du kan se felmeddelanden som tas emot från Microsoft när du försöker leverera händelsen. Den här begränsningen gäller endast för "testskapade" händelser. Data som är äldre än sju dagar rensas.

- **Händelse med uppdaterad prenumeration ("prenumerations uppdaterad")**

    Den här händelsen utlöses när prenumerationen ändras. Dessa händelser genereras när det sker en intern ändring utöver när ändringar görs via Partner Center-API:et.

    >[!NOTE]
    >Det finns en fördröjning på upp till 48 timmar mellan den tidpunkt då en prenumeration ändras och när den uppdaterade prenumerationshändelsen utlöses.

- **Tröskel överskred händelse ("usagerecords-thresholdExceeded")**

    Den här händelsen utlöses när mängden Microsoft Azure för en kund överskrider sin utgiftsbudget för användning (deras tröskelvärde). Mer information finns i [Ange en Azure-utgiftsbudget för dina kunder/partnercenter/set-an-azure-spending-budget-for-your-customers).

- **Skapad referenshändelse ("hänvisningsskapad")**

    Den här händelsen utlöses när hänvisningen skapas.

- **Uppdaterad referenshändelse ("hänvisnings uppdaterad")**

    Den här händelsen utlöses när hänvisningen uppdateras.

- **Fakturaklar händelse ("fakturaklar")**

    Den här händelsen utlöses när den nya fakturan är klar.

Framtida Webhook-händelser läggs till för resurser som ändras i systemet som partnern inte har kontroll över, och ytterligare uppdateringar kommer att göras för att få dessa händelser så nära "realtid" som möjligt. Feedback från partner om vilka händelser som tillför värde i verksamheten är användbart för att avgöra vilka nya händelser som ska läggas till.

En fullständig lista över Webhook-händelser som stöds av Partnercenter finns i [Webhook-händelser i Partnercenter.](partner-center-webhook-events.md)

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

## <a name="receiving-events-from-partner-center"></a>Ta emot händelser från Partnercenter

Om du vill ta emot händelser från Partnercenter måste du exponera en offentligt tillgänglig slutpunkt. Eftersom den här slutpunkten exponeras måste du verifiera att kommunikationen kommer från Partnercenter. Alla Webhook-händelser som du får är digitalt signerade med ett certifikat som är kedjor till Microsoft Root. En länk till certifikatet som används för att signera händelsen tillhandahålls också. Detta gör att certifikatet kan förnyas utan att du behöver distribuera om eller konfigurera om tjänsten. Partnercenter gör 10 försök att leverera händelsen. Om händelsen fortfarande inte levereras efter 10 försök flyttas den till en offlinekö och inga ytterligare försök görs vid leverans.

I följande exempel visas en händelse som publicerats från Partnercenter.

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
>Auktoriseringsrubriken har schemat "Signatur". Det här är en base64-kodad signatur för innehållet.

## <a name="how-to-authenticate-the-callback"></a>Så här autentiserar du motringning

Följ dessa steg om du vill autentisera återanropshändelsen som tas emot från Partnercenter:

1. Kontrollera att de nödvändiga huvudena finns (Auktorisering, x-ms-certificate-url, x-ms-signature-algorithm).

2. Ladda ned certifikatet som används för att signera innehållet (x-ms-certificate-url).

3. Verifiera certifikatkedjan.

4. Kontrollera certifikatets "organisation".

5. Läs innehållet med UTF8-kodning i en buffert.

6. Skapa en RSA Crypto-provider.

7. Kontrollera att data matchar det som signerats med den angivna hash-algoritmen (till exempel SHA256).

8. Om verifieringen lyckas bearbetar du meddelandet.

> [!NOTE]
> Som standard skickas signaturtoken i ett auktoriseringshuvud. Om du ställer in **SignatureTokenToMsSignatureHeader** på true i din registrering skickas signaturtoken i huvudet x-ms-signature i stället.

## <a name="event-model"></a>Händelsemodell

I följande tabell beskrivs egenskaperna för en Partnercenter-händelse.

### <a name="properties"></a>Egenskaper

| Name                      | Beskrivning                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | Namnet på händelsen. I formuläret {resource}-{action}. Till exempel "test-created".  |
| **ResourceUri**           | URI:en för resursen som ändrades.                                                 |
| **ResourceName**          | Namnet på den resurs som ändrades.                                                |
| **AuditUrl**              | Valfritt. URI för granskningsposten.                                                |
| **ResourceChangeUtcDate** | Datum och tid, i UTC-format, när resursändringen inträffade.                  |

### <a name="sample"></a>Exempel

I följande exempel visas strukturen för en Partnercenter-händelse.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a>Webhook-API:er

### <a name="authentication"></a>Autentisering

Alla anrop till Webhook-API:erna autentiseras med hjälp av bearer-token i auktoriseringshuvudet. Hämta en åtkomsttoken för att få åtkomst `https://api.partnercenter.microsoft.com` till . Den här token är samma token som används för att komma åt resten av Partner Center-API:erna.

### <a name="get-a-list-of-events"></a>Hämta en lista över händelser

Returnerar en lista över de händelser som för närvarande stöds av Webhook-API:erna.

### <a name="resource-url"></a>Resurs-URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a>Exempel på begäran

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Exempel på svar

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

### <a name="register-to-receive-events"></a>Registrera dig för att ta emot händelser

Registrerar en klientorganisation för att ta emot de angivna händelserna.

#### <a name="resource-url"></a>Resurs-URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Exempel på begäran

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

### <a name="response-example"></a>Exempel på svar

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

### <a name="view-a-registration"></a>Visa en registrering

Returnerar webhooks-händelseregistreringen för en klientorganisation.

#### <a name="resource-url"></a>Resurs-URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Exempel på begäran

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Exempel på svar

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

### <a name="update-an-event-registration"></a>Uppdatera en händelseregistrering

Uppdaterar en befintlig händelseregistrering.

#### <a name="resource-url"></a>Resurs-URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Exempel på begäran

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

### <a name="response-example"></a>Exempel på svar

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

### <a name="send-a-test-event-to-validate-your-registration"></a>Skicka en testhändelse för att verifiera registreringen

Genererar en testhändelse för att verifiera Webhooks-registreringen. Det här testet är avsett att verifiera att du kan ta emot händelser från Partnercenter. Data för dessa händelser tas bort sju dagar efter att den första händelsen har skapats. Du måste vara registrerad för händelsen "test-created" med hjälp av registrerings-API:et innan du skickar en valideringshändelse.

>[!NOTE]
>Det finns en begränsning på 2 begäranden per minut när du publicerar en valideringshändelse.

#### <a name="resource-url"></a>Resurs-URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a>Exempel på begäran

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a>Exempel på svar

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

### <a name="verify-that-the-event-was-delivered"></a>Kontrollera att händelsen har levererats

Returnerar det aktuella tillståndet för valideringshändelsen. Den här verifieringen kan vara användbar vid felsökning av problem med händelseleverans. Svaret innehåller ett resultat för varje försök att leverera händelsen.

#### <a name="resource-url"></a>Resurs-URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a>Exempel på begäran

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Exempel på svar

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

## <a name="example-for-signature-validation"></a>Exempel för signaturverifiering

### <a name="sample-callback-controller-signature-aspnet"></a>Exempel på återanropskontrollantsignatur (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>Signaturvalidering

I följande exempel visas hur du lägger till ett auktoriseringsattribut till kontrollanten som tar emot återanrop från Webhook-händelser.

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
