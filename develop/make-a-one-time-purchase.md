---
title: Gör ett engångsköp
description: Gör ett enda köp av programvara och reservationsprodukter, till exempel programvaruprenumerationer, permanent programvara och Azure Reserved Virtual Machine-instanser (VM) med hjälp av Partner Center-API:et.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: baf0b5d4aaa8957874ab019359aca2662a76194387e0cd06999b0bb329076c80
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994446"
---
# <a name="make-a-one-time-purchase"></a>Gör ett engångsköp

**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud for US Government

Gör ett enda köp av programvara och reservationsprodukter, till exempel programvaruprenumerationer, permanent programvara och Azure Reserved Virtual Machine-instanser (VM) med hjälp av Partner Center-API:et.

> [!NOTE]
> Programvaruprenumerationer är inte tillgängliga på följande marknader:
>
> | Otillgängliga marknader            | Otillgängliga marknader (forts....) | Otillgängliga marknader (forts....)      |
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
> | Brittiska territoriet i Indiska Oceanen | Jersey                            | Séo Tomé och Prñncipe                    |
> | Brittiska Jungfruöarna         | Kiribati                          | Seychellerna                               |
> | Burkina Faso                   | Kosovo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Sint Eustatius                           |
> | Kambodja                       | Lesotho                           | Sint Maarten                             |
> | Centralafrikanska Republiken       | Liberia                           | Solomonöarna                          |
> | Tchad                           | Madagaskar                        | Somalia                                  |
> | Kina                          | Malawi                            | Sydgeorgien och Sydsandwichöarna |
> | Julön               | Maldiverna                          | Sydsudan                              |
> | Kokosöarna        | Mali                              | StDirigering, Ascension, Tristan da Cunha   |
> | Komorerna                        | Marshallöarna                  | Surinam                                 |
> | Kongo                          | Martinique                        | Svalbard                                 |
> | Kongo (DR)                    | Mauretanien                        | Swaziland                                |
> | Cooköarna                   | Mayotte                           | Timor-Leste                              |
> | Djibouti                       | Mikronesien                        | Togo                                     |
> | Dominica                       | Montserrat                        | Tokelau                                  |
> | Ekvatorialguinea              | Moçambique                        | Tonga                                    |
> | Eritrea                        | Myanmar                           | Turks- och Caicosöarna                 |
> | Falklandsöarna               | Nauru                             | Tuvalu                                   |
> | Franska Guyana                  | Nya Kaledonien                     | U.S. Outlying Islands                    |
> | Franska Polynesien               | Niger                             | Vanuatu                                  |
> | Franska sydterritorierna    | Niue                              | Vatikanstaten                             |
> | Gabon                          | Norfolkön                    | Wallis och Spanuna                        |
> | Gambia                         | Nordmarianerna          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>
&nbsp;
> [!NOTE]
> Om du vill köpa permanent programvara måste du ha kvalificerats tidigare. Kontakta supporten om du vill ha mer information.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Göra ett köp en gång

Använd följande steg om du vill göra ett köp en gång:

1. [Aktivera –](#enablement) (endast Azure Reserved VM Instance) Registrera en aktiv CSP Azure-prenumeration så att den kan köpa en reservationsprodukt.

2. [Identifiering](#discovery) – Hitta och välj de produkter och SKU:er som du vill köpa och kontrollera deras tillgänglighet.

3. [Skicka order](#order-submission) – Skapa en kundvagn med artiklarna i din beställning och skicka den.

4. [Hämta beställningsinformation](#get-order-details) – Granska informationen om en order, alla order för en kund eller visa beställningar efter faktureringsperiodtyp.

När du har gjort ett enda köp visar följande scenarier hur du hanterar livscykeln för dina produkter genom att hämta information om dina rättigheter och hur du hämtar saldoutdrag, fakturor och fakturasammanfattningar.

- [Livscykelhantering](#lifecycle-management)

- [Faktura och avstämning](#invoice-and-reconciliation)

## <a name="enablement"></a>Aktivering

När du har identifierat den aktiva prenumerationen som du vill lägga till den reserverade Azure VM-instansen i måste du registrera prenumerationen så att den aktiveras. Information om hur du registrerar [en befintlig](subscription-resources.md) prenumerationsresurs så att den är aktiverad finns i Registrera [en prenumeration.](register-a-subscription.md)

När du har registrerat din prenumeration bör du bekräfta att registreringen har slutförts genom att kontrollera registreringsstatusen. Om du vill göra det här steget kan [du läsa Hämta prenumerationsregistreringsstatus](get-subscription-registration-status.md).

## <a name="discovery"></a>Identifiering

När prenumerationen är aktiverad är du redo att välja produkter och SKU:er och kontrollera deras tillgänglighet med hjälp av följande Partner Center API-modeller:

- [Produkt](product-resources.md#product) – en grupperingskonstruktion för köpbara varor eller tjänster. En produkt i sig är inte ett köpbart objekt.

- [SKU](product-resources.md#sku) – en köpbar lagerhållningsenhet (SKU) under en produkt. SKU:er representerar olika former av produkten.

- [Tillgänglighet](product-resources.md#availability) – En konfiguration där en SKU är tillgänglig för inköp (till exempel land, valuta och branschsegment).

Slutför följande steg innan du genomför ett köp en gång:

1. Identifiera och hämta den produkt och SKU som du vill köpa. Du kan göra det här steget genom att först visa produkter och SKU:er, eller välja dem om du redan känner till produktens och SKU:ns.

   - [Hämta en lista över produkter](get-a-list-of-products.md)
   - [Hämta en produkt med hjälp av produkt-ID:t](get-a-product-by-id.md)
   - [Hämta en lista över SKU:er för en produkt](get-a-list-of-skus-for-a-product.md)
   - [Hämta en SKU med hjälp av SKU-ID:t](get-a-sku-by-id.md)

2. Kontrollera inventeringen för en SKU. Det här steget behövs bara för SKU:er som är taggade med en **InventoryCheck-förutsättning.**

   - [Kontrollera lager](check-inventory.md)

3. Hämta [tillgängligheten](product-resources.md#availability) för [SKU:n](product-resources.md#sku). Du behöver **CatalogItemId för** tillgängligheten när du gör beställningen. Använd något av följande API:er för att hämta det här värdet:

   - [Hämta en lista över tillgänglighet för en SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Hämta en tillgänglighet med hjälp av tillgänglighets-ID:t](get-an-availability-by-id.md)

## <a name="order-submission"></a>Skicka order

Följ dessa steg om du vill skicka in din beställning:

1. Skapa en kundvagn för den samling katalogobjekt som du tänker köpa. När du skapar [en kundvagn](cart-resources.md) [grupperas kundvagnsraderna](cart-resources.md#cartlineitem) automatiskt baserat på vad som kan köpas tillsammans i samma [order.](order-resources.md)

   - [Skapa en kundvagn](create-a-cart.md)
   - [Uppdatera en kundvagn](update-a-cart.md)

2. Kolla in kundvagnen. När du checkar ut en kundvagn skapas en [order.](order-resources.md)

   - [Checka ut kundvagnen](checkout-a-cart.md)

## <a name="get-order-details"></a>Hämta beställningsinformation

När du har skapat din beställning kan du hämta information om en enskild order med hjälp av order-ID:t eller hämta en lista över beställningar för en kund. Det finns en fördröjning på upp till 15 minuter från det att en order skickas tills den visas i en lista över en kunds beställningar.

- Hämta information om en enskild order med hjälp av order-ID:t. Se Hämta [en order efter ID.](get-an-order-by-id.md)

- Så här hämtar du en lista över beställningar för en kund med hjälp av kund-ID:t. Se [Hämta alla en kunds beställningar.](get-all-of-a-customer-s-orders.md)

- Om du vill hämta en [](product-resources.md#billingcycletype) lista över beställningar för en kund efter faktureringscykeltyp kan du visa en lista med beställningar (en gång-avgifter) och årliga eller månatliga fakturerade beställningar separat. Se Hämta [en lista över beställningar efter kund och faktureringscykel av typen](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Livscykelhantering

Som en del av att hantera livscykeln för dina köp vid [](entitlement-resources.md)ett tillfälle i Partnercenter kan du hämta information om dina berättiganden och hämta reservationsinformation med hjälp av reservationsbeställnings-ID:t. Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Följande scenarier visar hur du programmatiskt visar kundens fakturor [och](invoice-resources.md)hämtar dina kontosaldon och sammanfattningar som inkluderar engångsavgifter.

### <a name="balance-and-payment"></a>Saldo och betalning

Information om hur du hämtar aktuellt kontosaldo i din standardvalutatyp som är ett saldo för både återkommande avgifter och engångsavgifter finns i [Hämta ditt aktuella kontosaldo](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo och betalning i flera valutor

Information om hur du hämtar ditt aktuella kontosaldo och en samling fakturasammanfattningar som innehåller en fakturasammanfattning med både återkommande avgifter och engångsavgifter för var och en av kundens valutatyper finns i [Hämta fakturasammanfattningar.](get-invoice-summaries.md)

### <a name="invoices"></a>Fakturor

Information om hur du hämtar en samling fakturor som visar både återkommande och engångsavgifter finns i [Hämta en samling fakturor.](get-a-collection-of-invoices.md)

### <a name="single-invoice"></a>Enskild faktura

Information om hur du hämtar en specifik faktura med hjälp av faktura-ID:t [finns i Hämta en faktura via ID](get-invoice-by-id.md).

### <a name="reconciliation"></a>Försoning

Information om en samling fakturaradsobjekt (avstämningsradsobjekt) för ett specifikt faktura-ID finns i [Hämta fakturaradsobjekt.](get-invoiceline-items.md)

### <a name="download-an-invoice-as-a-pdf"></a>Ladda ned en faktura som en PDF

Information om hur du hämtar ett fakturautdrag i PDF-format med hjälp av ett faktura-ID finns [i Hämta ett fakturautdrag](get-invoice-statement.md).
