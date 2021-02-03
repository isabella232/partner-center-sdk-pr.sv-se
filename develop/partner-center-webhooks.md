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
# <a name="partner-center-webhooks"></a>Partnercenter – webhooks

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

API: erna för webhook i Partner Center gör att partner kan registrera sig för resurs ändrings händelser. Dessa händelser levereras i form av HTTP-inlägg till partnerns registrerade URL. För att ta emot en händelse från Partner Center, kommer partner att vara värd för ett återanrop där Partner Center kan publicera resurs ändrings händelsen. Händelsen signeras digitalt så att partnern kan verifiera att den har skickats från Partner Center.

Partner kan välja mellan webhook-händelser, som följande exempel, som stöds av Partner Center.

- **Test event ("test-created")**

    Med den här händelsen kan du själv publicera och testa registreringen genom att begära ett test händelser och sedan följa förloppet. Du kan se de fel meddelanden som tas emot från Microsoft när du försöker leverera evenemanget. Den här begränsningen gäller endast för "test-skapade"-händelser. Data som är äldre än sju dagar rensas.

- **Prenumerationen har uppdaterats ("prenumerationen har uppdaterats")**

    Den här händelsen inträffar när prenumerationen ändras. Dessa händelser genereras när det finns en intern ändring utöver när ändringar görs via partner Center-API: et.

    >[!NOTE]
    >Det finns en fördröjning på upp till 48 timmar mellan den tidpunkt då en prenumeration ändras och när händelsen uppdatering av prenumeration utlöses.

- **Tröskeln överskreds för händelsen ("usagerecords-thresholdExceeded")**

    Den här händelsen inträffar när mängden Microsoft Azure användning för en kund överskrider deras användnings utgifts budget (tröskel). Mer information finns i [ställa in en Azure utgifts budget för dina kunder/Partner Center/set-a-Azure-utgifter-budget – för-kunder).

- **Händelse som skapats av hänvisning ("hänvisning skapad")**

    Den här händelsen inträffar när referensen skapas.

- **Referens för uppdaterad händelse ("hänvisning – uppdaterad")**

    Den här händelsen utlöses när hänvisningen uppdateras.

- **Faktura klar händelse ("faktura klar")**

    Den här händelsen inträffar när den nya fakturan är klar.

Framtida webhook-händelser kommer att läggas till för resurser som ändras i systemet som partnern inte har kontroll över, och ytterligare uppdateringar görs för att få dessa händelser så nära "real tid" som möjligt. Feedback från partner på vilka händelser som lägger till värde i deras verksamhet är användbara när du ska avgöra vilka nya händelser som ska läggas till.

En fullständig lista med webhook-händelser som stöds av Partner Center finns i [partner Center webhook-händelser](partner-center-webhook-events.md).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

## <a name="receiving-events-from-partner-center"></a>Ta emot händelser från Partner Center

För att ta emot händelser från Partner Center måste du exponera en offentligt tillgänglig slut punkt. Eftersom den här slut punkten visas måste du kontrol lera att kommunikationen är från Partner Center. Alla webhook-händelser som du får är digitalt signerade med ett certifikat som är kopplat till Microsoft-roten. En länk till certifikatet som används för att signera händelsen kommer också att tillhandahållas. Detta gör att certifikatet kan förnyas utan att du behöver distribuera om eller konfigurera om tjänsten. Partner Center kommer att göra 10 försök att leverera händelsen. Om händelsen fortfarande inte levereras efter 10 försök kommer den att flyttas till en offline-kö och inga ytterligare försök görs vid leverans.

I följande exempel visas en händelse som publicerats från Partner Center.

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
>Authorization-huvudet har ett schema för "signatur". Det här är en Base64-kodad signatur för innehållet.

## <a name="how-to-authenticate-the-callback"></a>Så här autentiserar du motringningen

Följ dessa steg om du vill autentisera återanrops händelsen som tas emot från Partner Center:

1. Kontrol lera att de nödvändiga rubrikerna finns (auktorisering, x-MS-Certificate-URL, x-MS-Signature-Algorithm).

2. Hämta certifikatet som används för att signera innehållet (x-MS-Certificate-URL).

3. Verifiera certifikat kedjan.

4. Kontrol lera "organisationen" för certifikatet.

5. Läs innehållet med UTF8-kodning i en buffert.

6. Skapa en RSA-Krypto-Provider.

7. Kontrol lera att data matchar vad som har signerats med angiven hash-algoritm (till exempel SHA256).

8. Om verifieringen lyckas, behandla meddelandet.

> [!NOTE]
> Som standard skickas signaturens token i ett Authorization-huvud. Om du anger **SignatureTokenToMsSignatureHeader** till sant i registreringen skickas signaturens token i huvudet x-MS-signatur i stället.

## <a name="event-model"></a>Händelse modell

I följande tabell beskrivs egenskaperna för ett partner Center-evenemang.

### <a name="properties"></a>Egenskaper

| Name                      | Beskrivning                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | Händelsens namn. I formatet {Resource}-{action}. Till exempel "test-created".  |
| **ResourceUri**           | URI för den resurs som ändrades.                                                 |
| **ResourceName**          | Namnet på den resurs som ändrades.                                                |
| **AuditUrl**              | Valfritt. Gransknings postens URI.                                                |
| **ResourceChangeUtcDate** | Datum och tid i UTC-format när resurs ändringen utfördes.                  |

### <a name="sample"></a>Exempel

Följande exempel visar strukturen för ett partner Center-evenemang.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a>Webhook-API: er

### <a name="authentication"></a>Autentisering

Alla anrop till webhook-API: erna autentiseras med hjälp av Bearer-token i Authorization-huvudet. Hämta en åtkomsttoken för åtkomst `https://api.partnercenter.microsoft.com` . Denna token är samma token som används för att få åtkomst till resten av API: erna för partner Center.

### <a name="get-a-list-of-events"></a>Hämta en lista över händelser

Returnerar en lista med händelser som för närvarande stöds av webhook-API: erna.

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

Registrerar en klient för att ta emot de angivna händelserna.

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

Returnerar en klients händelse registrering för webhookar.

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

### <a name="update-an-event-registration"></a>Uppdatera en händelse registrering

Uppdaterar en befintlig händelse registrering.

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

### <a name="send-a-test-event-to-validate-your-registration"></a>Skicka en test händelse för att verifiera registreringen

Genererar en test händelse för att verifiera Webhooks-registreringen. Det här testet är avsett att verifiera att du kan ta emot händelser från Partner Center. Data för de här händelserna tas bort sju dagar efter det att den första händelsen har skapats. Du måste vara registrerad för händelsen "test-created", med hjälp av registrerings-API: et, innan du skickar en verifierings händelse.

>[!NOTE]
>Det finns en begränsning på 2 begär Anden per minut vid bokföring av en validerings händelse.

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

### <a name="verify-that-the-event-was-delivered"></a>Kontrol lera att händelsen har levererats

Returnerar det aktuella läget för verifierings händelsen. Den här verifieringen kan vara till hjälp vid fel sökning av händelse leverans problem. Svaret innehåller ett resultat för varje försök som görs för att leverera händelsen.

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

## <a name="example-for-signature-validation"></a>Exempel på verifiering av signatur

### <a name="sample-callback-controller-signature-aspnet"></a>Exempel på signatur för återanrops kontroll (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>Verifiering av signatur

I följande exempel visas hur du lägger till ett Authorization-attribut till den kontroll enhet som tar emot återanrop från webhook-händelser.

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
