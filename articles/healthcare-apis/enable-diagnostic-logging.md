---
title: Diagnostische logboek registratie inschakelen in azure API voor FHIR
description: In dit artikel wordt uitgelegd hoe u diagnostische logboek registratie inschakelt in azure API voor FHIR®
services: healthcare-apis
ms.service: healthcare-apis
ms.subservice: fhir
ms.topic: conceptual
ms.reviewer: dseven
ms.author: cavoeg
author: CaitlinV39
ms.date: 11/01/2019
ms.openlocfilehash: 54119585d4f1377b60b85fbad01fe90f097a304f
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/25/2020
ms.locfileid: "95905171"
---
# <a name="enable-diagnostic-logging-in-azure-api-for-fhir"></a>Diagnostische logboek registratie inschakelen in azure API voor FHIR

In dit artikel wordt beschreven hoe u diagnostische logboek registratie inschakelt in azure API for FHIR en kunt u enkele voorbeeld query's voor deze logboeken bekijken. De toegang tot Diagnostische logboeken is essentieel voor elke gezondheids zorg waarbij naleving van wettelijke vereisten (zoals HIPAA) een moet zijn. De functie in azure API voor FHIR die Diagnostische logboeken mogelijk maakt, is de [**Diagnostische instellingen**](../azure-monitor/platform/diagnostic-settings.md) in de Azure Portal. 

## <a name="enable-audit-logs"></a>Audit logboeken inschakelen
1. Als u diagnostische logboek registratie in azure API voor FHIR wilt inschakelen, selecteert u uw Azure API for FHIR-service in de Azure Portal 
2. Navigeren naar Diagnostische instellingen voor **Diagnostische instellingen**  
 ![](media/diagnostic-logging/diagnostic-settings-screen.png) 

3. Selecteer **+ Diagnostische instelling toevoegen**

4. Voer een naam in voor de instelling

5. Selecteer de methode die u wilt gebruiken voor toegang tot uw Diagnostische logboeken:

    1. **Archiveren naar een opslag account** voor controle of hand matige inspectie. Het opslag account dat u wilt gebruiken, moet al zijn gemaakt.
    2. **Stroom om te Event hub** voor opname door een service van derden of een aangepaste analytische oplossing. Voordat u deze stap kunt configureren, moet u een Event Hub naam ruimte en Event Hub-beleid maken.
    3. **Streamen naar de log Analytics** -werk ruimte in azure monitor. U moet de werk ruimte voor logboek analyse maken voordat u deze optie kunt selecteren.

6. Selecteer **audit logs bevat** en alle metrische gegevens die u wilt vastleggen. Als u de Azure IoT-connector gebruikt voor FHIR, moet u **fouten, verkeer en latentie** voor metrische gegevens selecteren. 

   :::image type="content" source="media/iot-metrics-export/diagnostic-setting-add.png" alt-text="IoT-Connector2" lightbox="media/iot-metrics-export/diagnostic-setting-add.png":::

7. Selecteer **Opslaan**.


> [!Note] 
> Het kan tot vijf tien minuten duren voordat de eerste Logboeken in Log Analytics worden weer gegeven.  
 
Raadpleeg de documentatie van het [Azure-resource logboek](../azure-monitor/platform/platform-logs-overview.md) voor meer informatie over het werken met Diagnostische logboeken

## <a name="audit-log-details"></a>Details van controle logboek
Op dit moment retourneert de Azure API voor de FHIR-service de volgende velden in het audit logboek: 

|Veldnaam  |Type  |Opmerkingen  |
|---------|---------|---------|
|CallerIdentity|Dynamisch|Een algemene eigenschappen verzameling met identiteits gegevens
|CallerIdentityIssuer|Tekenreeks|Verlener 
|CallerIdentityObjectId|Tekenreeks|Object_Id 
|CallerIPAddress|Tekenreeks|Het IP-adres van de oproepende functie 
|CorrelationId|Tekenreeks| Correlatie-id
|FhirResourceType|Tekenreeks|Het resource type waarvoor de bewerking is uitgevoerd
|LogCategory|Tekenreeks|De logboek categorie (we retour neren momenteel ' audit logs bevat ' LogCategory)
|Locatie|Tekenreeks|De locatie van de server die de aanvraag heeft verwerkt (bijvoorbeeld Zuid-Centraal VS)
|OperationDuration|Int|De tijd die nodig was voor het volt ooien van deze aanvraag in seconden
|OperationName|Tekenreeks| Beschrijft het type bewerking (bijvoorbeeld update, Zoek type)
|RequestUri|Tekenreeks|De aanvraag-URI 
|ResultType|Tekenreeks|De beschik bare waarden zijn momenteel **gestart**, **geslaagd** of **mislukt**
|Status code|Int|De HTTP-status code. (bijvoorbeeld 200) 
|TimeGenerated|DateTime|Datum en tijd van de gebeurtenis|
|Eigenschappen|Tekenreeks| Beschrijft de eigenschappen van de fhirResourceType
|SourceSystem|Tekenreeks| Bron systeem (altijd Azure in dit geval)
|TenantId|Tekenreeks|Tenant-id
|Type|Tekenreeks|Type logboek (altijd MicrosoftHealthcareApisAuditLog in dit geval)
|_ResourceId|Tekenreeks|Details over de resource

## <a name="sample-queries"></a>Voorbeeldquery's

Hier volgen enkele eenvoudige Application Insights query's die u kunt gebruiken om uw logboek gegevens te verkennen.

Voer deze query uit om de **100 meest recente** logboeken te bekijken:

```Application Insights
MicrosoftHealthcareApisAuditLogs
| limit 100
```

Voer deze query uit om bewerkingen te groeperen op **resource type FHIR**:

```Application Insights
MicrosoftHealthcareApisAuditLogs 
| summarize count() by FhirResourceType
```

Deze query uitvoeren om alle **mislukte resultaten** op te halen

```Application Insights
MicrosoftHealthcareApisAuditLogs 
| where ResultType == "Failed" 
```

## <a name="conclusion"></a>Conclusie 
Toegang tot Diagnostische logboeken is essentieel voor het bewaken van een service en het leveren van nalevings rapporten. Met Azure API voor FHIR kunt u deze acties uitvoeren via Diagnostische logboeken. 
 
FHIR is het gedeponeerde handelsmerk van HL7 en wordt gebruikt met de toestemming van HL7.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe u audit logboeken voor Azure API kunt inschakelen voor FHIR. Vervolgens leert u meer over andere aanvullende instellingen die u kunt configureren in de Azure API voor FHIR
 
>[!div class="nextstepaction"]
>[Aanvullende instellingen](azure-api-for-fhir-additional-settings.md)
