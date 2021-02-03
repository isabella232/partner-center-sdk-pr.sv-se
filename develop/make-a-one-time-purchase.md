---
title: Gör ett engångsköp
description: Så här gör du ett engångs köp av program varu-och reservations produkter, till exempel program varu prenumerationer, beständig program vara och virtuella Azure-instanser (VM), med hjälp av Partner Center API.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17a5f5c1e845ba36a94d7ce909df30e0146ba448
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768901"
---
# <a name="make-a-one-time-purchase"></a>Gör ett engångsköp

**Gäller för**

- Partnercenter
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här gör du ett engångs köp av program varu-och reservations produkter, till exempel program varu prenumerationer, beständig program vara och virtuella Azure-instanser (VM), med hjälp av Partner Center API.

> [!NOTE]
> Program varu prenumerationer är inte tillgängliga på följande marknader:
>
> | Ej tillgängliga marknader            | Ej tillgängliga marknader (fortsatte...) | Ej tillgängliga marknader (fortsatte...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Åland                  | Grönland                         | Papua Nya Guinea                         |
> | Amerikanska Samoa                 | Grenada                           | Pitcairn                         |
> | Andorra                        | Guadeloupe                        | Réunion                                  |
> | Anguilla                       | Guam                              | Ryska federationen                       |
> | Antarktis                     | Guernsey                          | Saba                                     |
> | Antigua och Barbuda            | Guinea                            | Saint Barthélemy                         |
> | Aruba                          | Guinea-Bissau                     | Saint Lucia                              |
> | Benin                          | Guyana                            | Saint Martin                             |
> | Bhutan                         | Haiti                             | Saint-Pierre och Miquelon                |
> | Bonaire                        | Heard- och McDonaldöarna | Saint Vincent och Grenadinerna         |
> | Bouvetön                  | Isle of Man                       | Samoa                                    |
> | Brasilien                         | Jan Mayen                         | San Marino                               |
> | Brittiska territoriet i Indiska Oceanen | Jersey                            | São Tomé och Príncipe                    |
> | Brittiska Jungfruöarna         | Kiribati                          | Seychellerna                               |
> | Burkina Faso                   | Kosovo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Sint Eustatius                           |
> | Kambodja                       | Lesotho                           | Sint Maarten                             |
> | Centralafrikanska Republiken       | Liberia                           | Solomonöarna                          |
> | Tchad                           | Madagaskar                        | Somalia                                  |
> | Kina                          | Malawi                            | Sydgeorgien och Sydsandwichöarna |
> | Julön               | Maldiverna                          | Sydsudan                              |
> | Kokosöarna        | Mali                              | Saint Helena, Ascension, Tristan da Cunha   |
> | Komorerna                        | Marshallöarna                  | Surinam                                 |
> | Kongo                          | Martinique                        | Svalbard                                 |
> | Kongo (DR)                    | Mauretanien                        | Swaziland                                |
> | Cooköarna                   | Mayotte                           | Timor-Leste                              |
> | Djibouti                       | Mikronesien                        | Togo                                     |
> | Dominica                       | Montserrat                        | Tokelau                                  |
> | Ekvatorialguinea              | Moçambique                        | Tonga                                    |
> | Eritrea                        | Myanmar                           | Turks- och Caicosöarna                 |
> | Falklandsöarna               | Nauru                             | Tuvalu                                   |
> | Franska Guyana                  | Nya Kaledonien                     | Amerikanska öar                    |
> | Franska Polynesien               | Niger                             | Vanuatu                                  |
> | Franska sydterritorierna    | Niue                              | Vatikanstaten                             |
> | Gabon                          | Norfolkön                    | Wallis och Futuna                        |
> | Gambia                         | Nordmarianerna          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>
&nbsp;
> [!NOTE]
> För att kunna köpa beständig program vara måste du ha kvalificerats tidigare. Kontakta supporten om du vill ha mer information.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Göra ett engångs köp

Använd följande steg för att göra ett engångs köp:

1. [Aktivering](#enablement) – (endast Azure reserverad VM-instans) registrera en aktiv CSP Azure-prenumeration så att den kan köpa en reservations produkt.

2. [Identifiering](#discovery) – hitta och välj de produkter och SKU: er som du vill köpa och kontrol lera deras tillgänglighet.

3. [Order sändning](#order-submission) – skapa en Shopping vagn med objekten i din beställning och skicka den.

4. [Hämta beställnings information](#get-order-details) – granska information om en order, alla beställningar för en kund eller Visa beställningar efter fakturerings cykel typ.

När du har gjort en engångs köpet visar följande scenarier hur du hanterar livs cykeln för dina produkter genom att hämta information om dina rättigheter och hur du hämtar balans räkningar, fakturor och faktura sammanfattningar.

- [Livs cykel hantering](#lifecycle-management)

- [Faktura och avstämning](#invoice-and-reconciliation)

## <a name="enablement"></a>Aktivering

När du har identifierat den aktiva prenumeration som du vill lägga till den reserverade virtuella Azure-instansen i måste du registrera prenumerationen så att den är aktive rad. Om du vill registrera en befintlig [prenumerations](subscription-resources.md) resurs så att den är aktive rad, se [Registrera en prenumeration](register-a-subscription.md).

När du har registrerat din prenumeration bör du kontrol lera att registrerings processen har slutförts genom att kontrol lera registrerings statusen. Det här steget finns i [Hämta status för prenumerations registrering](get-subscription-registration-status.md).

## <a name="discovery"></a>Identifiering

När prenumerationen har Aktiver ATS är du redo att välja produkter och SKU: er och kontrol lera deras tillgänglighet med hjälp av följande Partner Center API-modeller:

- [Produkt](product-resources.md#product) – en grupperings konstruktion för köpbara-varor eller-tjänster. En produkt som själva är inte ett köpbara-objekt.

- [SKU](product-resources.md#sku) – en köpbara lagerhållnings enhet (SKU) under en produkt. SKU: er representerar olika former av produkten.

- [Tillgänglighet](product-resources.md#availability) – en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta och bransch segment).

Slutför följande steg innan du gör ett engångs köp:

1. Identifiera och hämta den produkt och SKU som du vill köpa. Du kan göra det här steget genom att först lista produkterna och SKU: erna, eller om du redan känner till ID: n för produkten och SKU: n, väljer du dem.

   - [Hämta en lista över produkter](get-a-list-of-products.md)
   - [Hämta en produkt med produkt-ID](get-a-product-by-id.md)
   - [Hämta en lista över SKU: er för en produkt](get-a-list-of-skus-for-a-product.md)
   - [Hämta en SKU med SKU-ID](get-a-sku-by-id.md)

2. Kontrol lera inventeringen för en SKU. Det här steget behövs bara för SKU: er som är taggade med en **InventoryCheck** -förutsättning.

   - [Kontrollera lager](check-inventory.md)

3. Hämta [tillgänglighet](product-resources.md#availability) för SKU: [n](product-resources.md#sku). Du behöver **CatalogItemId** av tillgängligheten när du placerar ordern. Använd något av följande API: er för att hämta det här värdet:

   - [Hämta en lista över tillgänglighet för en SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Få en tillgänglighet med tillgänglighets-ID: t](get-an-availability-by-id.md)

## <a name="order-submission"></a>Order överföring

Följ dessa steg om du vill skicka in din beställning:

1. Skapa en vagn som innehåller den samling av katalog objekt som du vill köpa. När du skapar en [varukorg](cart-resources.md)grupperas [vagnens rad objekt](cart-resources.md#cartlineitem) automatiskt utifrån vad som kan köpas tillsammans i samma [ordning](order-resources.md).

   - [Skapa en Shopping vagn](create-a-cart.md)
   - [Uppdatera en Shopping vagn](update-a-cart.md)

2. Kolla in vagnen. Att checka ut en vagns resultat i skapandet av en [order](order-resources.md).

   - [Checka ut vagnen](checkout-a-cart.md)

## <a name="get-order-details"></a>Hämta beställnings information

När du har skapat din beställning kan du hämta information om en enskild order med order-ID: t eller hämta en lista över beställningar för en kund. Det finns en fördröjning på upp till 15 minuter mellan tiden som en beställning skickas och när den visas i en lista över en kunds beställningar.

- Så här hämtar du information om en enskild order med order-ID: t. Se, [Hämta en order efter ID](get-an-order-by-id.md).

- Så här hämtar du en lista över beställningar för en kund med kund-ID. Se, [Hämta alla kund order](get-all-of-a-customer-s-orders.md).

- För att hämta en lista över beställningar för en kund efter [fakturerings cykel typ](product-resources.md#billingcycletype) , så att du kan lista beställningar (engångs avgifter) och årliga eller månatliga fakturerade beställningar separat. Se, [Hämta en lista över beställningar efter kund-och fakturerings cykel typ](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Livs cykel hantering

Som en del i hanteringen av livs cykeln för dina Engångs köp i Partner Center kan du hämta information om dina [rättigheter](entitlement-resources.md)och få reservations information med hjälp av reservations orderns ID. Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Följande scenarier visar hur du program mässigt visar din kunds [fakturor](invoice-resources.md)och hur du får dina konto balanser och sammanfattningar som omfattar engångs kostnader.

### <a name="balance-and-payment"></a>Saldo och betalning

Om du vill hämta aktuellt konto saldo i din standard valuta typ som är en balans mellan både återkommande och engångs kostnad, se [Hämta ditt aktuella konto saldo](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo och betalning för flera valutor

Om du vill hämta ditt aktuella konto saldo och en samling av faktura sammanfattningar som innehåller en faktura sammanfattning med både återkommande och engångs kostnader för var och en av kundens valuta typer, se [Hämta faktura sammanfattningar](get-invoice-summaries.md).

### <a name="invoices"></a>Fakturor

Om du vill hämta en samling fakturor som visar både återkommande och en tids avgift, se [Hämta en samling fakturor](get-a-collection-of-invoices.md).

### <a name="single-invoice"></a>Enskild faktura

Information om hur du hämtar en speciell faktura med hjälp av faktura-ID finns i [Hämta en faktura efter ID](get-invoice-by-id.md).

### <a name="reconciliation"></a>Konto

Information om hur du hämtar information om faktura rads objekt (avstämnings rad objekt) för ett angivet faktura-ID finns i [Hämta faktura rads objekt](get-invoiceline-items.md).

### <a name="download-an-invoice-as-a-pdf"></a>Ladda ned en faktura som en PDF

Information om hur du hämtar ett faktura uttryck i PDF-formulär med hjälp av ett faktura-ID finns i [Hämta en faktura instruktion](get-invoice-statement.md).
