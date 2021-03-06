---
title: Azure Security Bench Mark v2-Endpoint Security
description: Azure Security Bench Mark v2 Endpoint Security
author: msmbaldwin
ms.service: security
ms.topic: conceptual
ms.date: 09/20/2020
ms.author: mbaldwin
ms.custom: security-benchmark
ms.openlocfilehash: 937d0b379c4f669e5b57e5053d5e3bffeb091e78
ms.sourcegitcommit: 1bdcaca5978c3a4929cccbc8dc42fc0c93ca7b30
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/13/2020
ms.locfileid: "97368950"
---
# <a name="security-control-v2-endpoint-security"></a>Beveiligings controle v2: Endpoint Security

Endpoint Security heeft betrekking op besturings elementen in eindpunt detectie en-antwoord. Dit omvat het gebruik van de eindpunt detectie en respons (EDR) en anti-malware-service voor eind punten in azure-omgevingen.

## <a name="es-1-use-endpoint-detection-and-response-edr"></a>ES-1: eindpunt detectie en-antwoord gebruiken (EDR)

| Azure-ID | CIS-besturings elementen v 7.1-ID ('s) | NIST SP 800-53 R4-ID ('s) |
|--|--|--|--|
| ES-1 | 8.1 | SI-2, SI-3, SC-3 |

Schakel de functionaliteit voor eindpunt detectie en-antwoorden (EDR) voor servers en clients in en integreer met SIEM-en beveiligings processen.

Micro soft Defender Advanced Threat Protection biedt een EDR-mogelijkheid als onderdeel van een Enter prise Endpoint Security-platform om geavanceerde bedreigingen te voor komen, te detecteren, te onderzoeken en erop te reageren. 

- [Overzicht van micro soft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Micro soft Defender ATP-service voor Windows-servers](/windows/security/threat-protection/microsoft-defender-atp/configure-server-endpoints)

- [Micro soft Defender ATP-service voor niet-Windows-servers](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-non-windows)

**Verantwoordelijkheid**: Klant

**Beveiligings belanghebbenden van klanten** ([meer informatie](/azure/cloud-adoption-framework/organize/cloud-security#security-functions)):

- [Infrastructuur- en eindpuntbeveiliging](/azure/cloud-adoption-framework/organize/cloud-security)

- [Informatie over bedreigingen](/azure/cloud-adoption-framework/organize/cloud-security-threat-intelligence)

- [Beheer van beveiligings naleving](/azure/cloud-adoption-framework/organize/cloud-security-compliance-management)

- [Postuurbeheer](/azure/cloud-adoption-framework/organize/cloud-security-compliance-management)

## <a name="es-2-use-centrally-managed-modern-anti-malware-software"></a>ES-2: centraal beheerde moderne anti-malware-software gebruiken

| Azure-ID | CIS-besturings elementen v 7.1-ID ('s) | NIST SP 800-53 R4-ID ('s) |
|--|--|--|--|
| ES-2 | 8.1 | SI-2, SI-3, SC-3 |

Gebruik een centraal beheerde anti-malware-oplossing die kan worden gebruikt in realtime en periodieke scans

Azure Security Center kunt het gebruik van een aantal populaire oplossingen voor anti-malware voor uw virtuele machines automatisch identificeren en de status van de Endpoint Protection-uitvoering melden en aanbevelingen doen. 

Micro soft antimalware voor Azure Cloud Services is de standaard anti-malware voor virtuele Windows-machines (Vm's). Voor virtuele Linux-machines gebruikt u een antimalware-oplossing van derden.  U kunt ook de bedreigings detectie van Azure Security Center voor gegevens Services gebruiken om malware te detecteren die is geüpload naar Azure Storage accounts. 

- [Micro soft antimalware configureren voor Cloud Services en Virtual Machines](../fundamentals/antimalware.md)

- [Ondersteunde Endpoint Protection-oplossingen](../../security-center/security-center-services.md?tabs=features-windows#supported-endpoint-protection-solutions-)

**Verantwoordelijkheid**: Klant

**Beveiligings belanghebbenden van klanten** ([meer informatie](/azure/cloud-adoption-framework/organize/cloud-security#security-functions)):

- [Infrastructuur- en eindpuntbeveiliging](/azure/cloud-adoption-framework/organize/cloud-security)

- [Informatie over bedreigingen](/azure/cloud-adoption-framework/organize/cloud-security-threat-intelligence)

- [Beheer van beveiligings naleving](/azure/cloud-adoption-framework/organize/cloud-security-compliance-management)

- [Postuurbeheer](/azure/cloud-adoption-framework/organize/cloud-security-compliance-management)

## <a name="es-3-ensure-anti-malware-software-and-signatures-are-updated"></a>ES-3: controleren of anti-malware-software en hand tekeningen zijn bijgewerkt

| Azure-ID | CIS-besturings elementen v 7.1-ID ('s) | NIST SP 800-53 R4-ID ('s) |
|--|--|--|--|
| ES-3 | 8,2 | SI-2, SI-3 |

Zorg ervoor dat anti-malware-hand tekeningen snel en consistent worden bijgewerkt. 

Volg de aanbevelingen in Azure Security Center: "COMPUTE &amp; apps" om ervoor te zorgen dat alle eind punten up-to-date zijn met de nieuwste hand tekeningen. Micro soft antimalware installeert standaard automatisch de nieuwste hand tekeningen en engine-updates. Gebruik voor Linux een oplossing van antimalware van derden.

- [Micro soft antimalware implementeren voor Azure Cloud Services en Virtual Machines](../fundamentals/antimalware.md)

**Verantwoordelijkheid**: Klant

**Beveiligings belanghebbenden van klanten** ([meer informatie](/azure/cloud-adoption-framework/organize/cloud-security#security-functions)):

- [Infrastructuur- en eindpuntbeveiliging](/azure/cloud-adoption-framework/organize/cloud-security)

- [Informatie over bedreigingen](/azure/cloud-adoption-framework/organize/cloud-security-threat-intelligence)

- [Beheer van beveiligings naleving](/azure/cloud-adoption-framework/organize/cloud-security-compliance-management)

- [Postuurbeheer](/azure/cloud-adoption-framework/organize/cloud-security-compliance-management)

- [Endpoint Protection-evaluatie en aanbevelingen in Azure Security Center](../../security-center/security-center-endpoint-protection.md)