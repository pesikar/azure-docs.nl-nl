---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 01/29/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 8cfeb5f6f22156aacb03a0fd327c0918f182369f
ms.sourcegitcommit: b4e6b2627842a1183fce78bce6c6c7e088d6157b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/30/2021
ms.locfileid: "99214671"
---
|Naam<br /><sub>(Azure-portal)</sub> |Beschrijving |Gevolg(en) |Versie<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Gedeelde dashboards mogen geen Markdown-tegels met inline-inhoud bevatten](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F04c655fe-0ac7-48ae-9a32-3a2e208c7624) |Hiermee staat u niet toe dat een gedeeld dashboard met inline-inhoud op Markdown-tegels kan worden gemaakt en dwingt u af dat de inhoud moet worden opgeslagen als een Markdown-bestand dat online wordt gehost. Als u in de Markdown-tegel inline-inhoud gebruikt, kunt u de versleuteling van de inhoud niet beheren. Door uw eigen opslag te configureren, kunt u versleuteling, dubbele versleuteling en zelfs uw eigen sleutels gebruiken. Als u dit beleid inschakelt, worden gebruikers beperkt tot het gebruik van de versie 2020-09-01-preview of een hogere versie van de REST API voor gedeelde dashboards. |Controleren, Weigeren, Uitgeschakeld |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Portal/SharedDashboardInlineContent_Deny.json) |
