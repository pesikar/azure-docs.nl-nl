---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 01/29/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: e82953bf8aae3d24f058d1cf28e09afe61c92fba
ms.sourcegitcommit: 54e1d4cdff28c2fd88eca949c2190da1b09dca91
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/31/2021
ms.locfileid: "99220417"
---
|Naam<br /><sub>(Azure-portal)</sub> |Beschrijving |Gevolg(en) |Versie<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Alle autorisatieregels met uitzondering van RootManageSharedAccessKey moeten worden verwijderd uit Service Bus-naamruimte](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1817ec0-a368-432a-8057-8371e17ac6ee) |Service Bus-clients mogen geen toegangsbeleid op naamruimteniveau gebruiken dat toegang biedt tot alle wachtrijen en onderwerpen in een naamruimte. Overeenkomstig het beveiligingsmodel met minimale bevoegdheden, moet u voor wachtrijen en onderwerpen toegangsbeleid maken op entiteitsniveau, om alleen toegang te verlenen aan de specifieke entiteit |Controleren, Weigeren, Uitgeschakeld |[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Service%20Bus/ServiceBus_AuditNamespaceAccessRules_Audit.json) |
|[Diagnostische logboeken in Service Bus moeten zijn ingeschakeld](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff8d36e2f-389b-4ee4-898d-21aeb69a0f45) |Inschakeling van diagnostische logboeken controleren. Hiermee kunt u een activiteitenspoor opnieuw maken om te gebruiken voor onderzoeksdoeleinden wanneer een beveiligingsincident optreedt of wanneer uw netwerk is aangetast |AuditIfNotExists, uitgeschakeld |[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Service%20Bus/ServiceBus_AuditDiagnosticLog_Audit.json) |
|[Service Bus Premium-naam ruimten moeten een door de klant beheerde sleutel gebruiken voor versleuteling](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F295fc8b1-dc9f-4f53-9c61-3f313ceab40a) |Azure Service Bus ondersteunt de mogelijkheid om gegevens in rust te versleutelen met door micro soft beheerde sleutels (standaard) of door de klant beheerde sleutels. Als u ervoor kiest om gegevens te versleutelen met door de klant beheerde sleutels, kunt u toegang tot de sleutels toewijzen, draaien, uitschakelen en intrekken die Service Bus gebruiken om gegevens in uw naam ruimte te versleutelen. Houd er rekening mee dat Service Bus alleen versleuteling met door de klant beheerde sleutels voor Premium-naam ruimten ondersteunt. |Controle, uitgeschakeld |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Service%20Bus/ServiceBus_CustomerManagedKeyEnabled_Audit.json) |
