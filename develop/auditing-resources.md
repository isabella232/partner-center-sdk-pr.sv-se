---
title: Granska resurser
description: Lär dig om gransknings resurser i Partner Center API, som AuditRecord, som du kan använda för att hämta en post för partner Center-aktivitet.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 31832492913e866b078c3c638e22c1a4b8d5e7e6
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770005"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Gransknings resurser som hjälper dig att få en post för partner Center-aktivitet

**Gäller för:**

- Partnercenter

Du kan använda följande resurser med gransknings åtgärder.

## <a name="auditrecord"></a>AuditRecord

Representerar en post för en åtgärd som utförs av en partner användare eller ett program.

| Egenskap | Typ | Description |
| --- | --- | ---|
| customerId | sträng | En GUID-formaterad sträng som identifierar kunden. |
| customerName | sträng | Kundens namn. |
| userPrincipalName | sträng | User Principal Name-eller användar identifieraren. Den här egenskapen är vanligt vis ett inloggnings namn för en användare i ett e-postformat baserat på Internet standard RFC 822. |
| applicationId | sträng | En sträng som identifierar det program som utförde åtgärden. |
| resourceType | sträng | Den typ av resurs som åtgärdades vid åtgärden. Möjliga värden:,,,,,,,,,, `customer` `customer_user` `order` `subscription` `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` . |
| resourceOldValue | sträng | Resursens gamla värde. |
| resourceNewValue | sträng | Resursens nya värde. |
| operationType | sträng | Typ av åtgärd som utförs. Möjliga värden:,,,,,,, `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` (endast sandbox-integrations konton) `remove_partner_customer_relationship` , `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,, |
| operationDate | sträng i UTC-datum/tid-format | Datum och tid när åtgärden utfördes. |
| operationStatus | sträng | Status för den åtgärd som granskas. Möjliga värden: `succeeded` , `failed` , eller `progress` , vilket innebär att åtgärden fortfarande pågår. |
| customizedData  | objekt mat ris | Ytterligare information. Varje-objekt innehåller två JSON-nyckel/värde-par: det första är `key` och ett sträng värde, det andra är `value` och ett sträng värde. Antalet objekt i matrisen beror på vilken typ av åtgärd som utfördes. |
| dokumentattribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Attribut för metadata. |
