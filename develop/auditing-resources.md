---
title: Granska resurser
description: 'Lär dig mer om granskningsresurser i Partnercenter-API: et, till exempel AuditRecord, som du kan använda för att hämta en post för partnercenteraktiviteten.'
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d78a305c2d27dc692c609e30817b34b1f814157
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974360"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Granskningsresurser som hjälper dig att få en post med Partnercenter-aktivitet

Du kan använda följande resurser med granskningsåtgärder.

## <a name="auditrecord"></a>AuditRecord

Representerar en post för en åtgärd som utförs av en partneranvändare eller ett program.

| Egenskap | Typ | Beskrivning |
| --- | --- | ---|
| customerId | sträng | En GUID-formaterad sträng som identifierar kunden. |
| customerName | sträng | Kundens namn. |
| userPrincipalName | sträng | Användarens huvudnamn eller användaridentifierare. Normalt är den här egenskapen ett inloggningsnamn i Internet-format för en användare i ett e-postadressformat baserat på Internet standard RFC 822. |
| applicationId | sträng | En sträng som identifierar programmet som utförde åtgärden. |
| resourceType | sträng | Den typ av resurs som åtgärden åtgärdar. Möjliga värden: `customer` , , , , , , , , `customer_user` , , , `order` , , `subscription` , `license` , `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` `partner_customer_dap` `customer_directory_role` . |
| resourceOldValue | sträng | Det gamla värdet för resursen. |
| resourceNewValue | sträng | Det nya värdet för resursen. |
| operationType | sträng | Typ av åtgärd som utförs. Möjliga värden: `update_customer_qualification` , , , , , , , `update_subscription` , `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` (endast sandbox-konton), `remove_partner_customer_relationship` , , , `create_order` `update_order` , , `create_customer_user` `delete_customer_user` `update_customer_user` , , `update_customer_user_licenses` , , `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` , `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` , `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` `add_user_member` `remove_user_member` . |
| operationDate | sträng i UTC-datum/tid-format | Datum och tid då åtgärden utfördes. |
| operationStatus | sträng | Status för den åtgärd som granskas. Möjliga värden: `succeeded` , eller , vilket innebär att åtgärden fortfarande `failed` `progress` pågår. |
| customizedData  | matris med objekt | Ytterligare information. Varje objekt innehåller två JSON-nyckel/värde-par: det första är och `key` ett strängvärde, det andra är och ett `value` strängvärde. Antalet objekt i matrisen beror på vilken typ av åtgärd som utfördes. |
| Attribut | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen. |
