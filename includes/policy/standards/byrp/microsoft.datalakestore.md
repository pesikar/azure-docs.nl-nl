---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 01/29/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 90372763ebd6c22cf5a819864f814a14605136d6
ms.sourcegitcommit: b4e6b2627842a1183fce78bce6c6c7e088d6157b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/30/2021
ms.locfileid: "99091129"
---
## <a name="azure-security-benchmark"></a>Azure Security-benchmark

De [Azure Security-benchmark](../../../../articles/security/benchmarks/overview.md) biedt aanbevelingen voor hoe u uw cloudoplossingen in Azure kunt beveiligen. Bekijk de [toewijzingsbestanden van de Azure Security-benchmark](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines) om te zien hoe deze service volledig is toegewezen aan de Azure Security-benchmark.

Raadpleeg [Naleving van Azure Policy-regelgeving - Azure Security-benchmark](../../../../articles/governance/policy/samples/azure-security-benchmark.md) om te zien hoe de beschikbare ingebouwde modules voor Azure Policy voor alle Azure-services zijn toegewezen aan deze nalevingsstandaard.

|Domain |Id van besturingselement |Titel van besturingselement |Beleid<br /><sub>(Azure-portal)</sub> |Beleidsversie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Logboekregistratie en detectie van bedreigingen |LT-4 |Logboek registratie inschakelen voor Azure-resources |[Diagnostische logboeken in Azure Data Lake Store moeten zijn ingeschakeld](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F057ef27e-665e-4328-8ea3-04b3122bd9fb) |[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Lake/DataLakeStore_AuditDiagnosticLog_Audit.json) |

## <a name="azure-security-benchmark-v1"></a>Azure Security Benchmark v1

De [Azure Security-benchmark](../../../../articles/security/benchmarks/overview.md) biedt aanbevelingen voor hoe u uw cloudoplossingen in Azure kunt beveiligen. Bekijk de [toewijzingsbestanden van de Azure Security-benchmark](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines) om te zien hoe deze service volledig is toegewezen aan de Azure Security-benchmark.

Raadpleeg [Naleving van Azure Policy-regelgeving - Azure Security-benchmark](../../../../articles/governance/policy/samples/azure-security-benchmark.md) om te zien hoe de beschikbare ingebouwde modules voor Azure Policy voor alle Azure-services zijn toegewezen aan deze nalevingsstandaard.

|Domain |Id van besturingselement |Titel van besturingselement |Beleid<br /><sub>(Azure-portal)</sub> |Beleidsversie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Logboekregistratie en bewaking |2.3 |Auditlogboekregistratie voor Azure-resources inschakelen |[Diagnostische logboeken in Azure Data Lake Store moeten zijn ingeschakeld](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F057ef27e-665e-4328-8ea3-04b3122bd9fb) |[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Lake/DataLakeStore_AuditDiagnosticLog_Audit.json) |

## <a name="cmmc-level-3"></a>CMMC niveau 3

Zie [Azure Policy regelgevings naleving-CMMC niveau 3](../../../../articles/governance/policy/samples/cmmc-l3.md)als u wilt weten hoe de beschik bare Azure Policy ingebouwde invoeg toepassingen voor alle Azure-Services zijn gekoppeld aan deze nalevings standaard.
Zie [Cyber beveiliging rijpheid-model certificering (CMMC)](https://www.acq.osd.mil/cmmc/docs/CMMC_Model_Main_20200203.pdf)voor meer informatie over deze nalevings standaard.

|Domain |Id van besturingselement |Titel van besturingselement |Beleid<br /><sub>(Azure-portal)</sub> |Beleidsversie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Systeem- en communicatiebeveiliging |SC. 3.177 |Gebruik FIPS-gevalideerde crypto grafie voor het beveiligen van de vertrouwelijkheid van CUI. |[Versleuteling van Data Lake Store-accounts vereisen](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa7ff3161-0087-490a-9ad9-ad6217f4f43a) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Lake/DataLakeStoreEncryption_Deny.json) |
|Systeem- en communicatiebeveiliging |SC. 3.191 |De vertrouwelijkheid van inactieve CUI beschermen. |[Versleuteling van Data Lake Store-accounts vereisen](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa7ff3161-0087-490a-9ad9-ad6217f4f43a) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Lake/DataLakeStoreEncryption_Deny.json) |

## <a name="hipaa-hitrust-92"></a>HIPAA HITRUST 9.2

Raadpleeg [Naleving van Azure Policy-regelgeving - HIPAA HITRUST 9.2](../../../../articles/governance/policy/samples/hipaa-hitrust-9-2.md) om te zien hoe de beschikbare ingebouwde modules voor Azure Policy voor alle Azure-services zijn toegewezen aan deze nalevingsstandaard.
Zie [HIPAA HITRUST 9.2](https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html) voor meer informatie over deze nalevingsstandaard.

|Domain |Id van besturingselement |Titel van besturingselement |Beleid<br /><sub>(Azure-portal)</sub> |Beleidsversie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Auditlogboekregistratie |1202.09aa1System.1 - 09.aa |Er wordt een beveiligd controlerecord gemaakt voor elke activiteit in het systeem (maken, lezen, bijwerken, verwijderen) met betrekking tot gedekte informatie. |[Diagnostische logboeken in Azure Data Lake Store moeten zijn ingeschakeld](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F057ef27e-665e-4328-8ea3-04b3122bd9fb) |[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Lake/DataLakeStore_AuditDiagnosticLog_Audit.json) |
|Beheer van verwisselbare media |0304.09o3Organizational.1 - 09.o |De organisatie beperkt het gebruik van schrijfbare, verwisselbare media en persoonlijke verwisselbare in organisatiesystemen. |[Versleuteling van Data Lake Store-accounts vereisen](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa7ff3161-0087-490a-9ad9-ad6217f4f43a) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Lake/DataLakeStoreEncryption_Deny.json) |

