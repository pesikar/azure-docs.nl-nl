---
title: Variabele activiteit instellen in Azure Data Factory
description: Meer informatie over het gebruik van de activiteit variabele instellen om de waarde in te stellen van een bestaande variabele die in een Data Factory pijp lijn is gedefinieerd
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 04/07/2020
author: dcstwh
ms.author: weetok
manager: jroth
ms.reviewer: maghan
ms.openlocfilehash: f3c1fae2cbf2a1ba8b71dcbc8f6639bda4765f5c
ms.sourcegitcommit: d60976768dec91724d94430fb6fc9498fdc1db37
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96498384"
---
# <a name="set-variable-activity-in-azure-data-factory"></a>Variabele activiteit instellen in Azure Data Factory
[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Gebruik de activiteit variabele instellen om de waarde in te stellen van een bestaande variabele van het type teken reeks, BOOL of matrix die in een Data Factory pijp lijn is gedefinieerd.

## <a name="type-properties"></a>Type-eigenschappen

Eigenschap | Beschrijving | Vereist
-------- | ----------- | --------
naam | De naam van de activiteit in de pijp lijn | ja
beschrijving | Tekst die beschrijft wat de activiteit doet | nee
type | Moet worden ingesteld op **SetVariable** | ja
waarde | Letterlijke teken reeks of waarde van het expressie object waaraan de variabele is toegewezen | ja
variableName | Naam van de variabele die door deze activiteit wordt ingesteld | ja

## <a name="incrementing-a-variable"></a>Een variabele verhogen

Een veelvoorkomend scenario waarbij variabelen in Azure Data Factory wordt gebruikt een variabele als een iterator binnen een activiteit tot of foreach. In een set variabele-activiteit kunt u niet verwijzen naar de variabele die in het veld is ingesteld `value` . Als u deze beperking wilt omzeilen, stelt u een tijdelijke variabele in en maakt u vervolgens een tweede set variabele-activiteit. Met de tweede set variabele activity wordt de waarde van de iterator ingesteld op de tijdelijke variabele. 

Hieronder ziet u een voor beeld van dit patroon:

![Toename variabele](media/control-flow-set-variable-activity/increment-variable.png "Toename variabele")

``` json
{
    "name": "pipeline3",
    "properties": {
        "activities": [
            {
                "name": "Set I",
                "type": "SetVariable",
                "dependsOn": [
                    {
                        "activity": "Increment J",
                        "dependencyConditions": [
                            "Succeeded"
                        ]
                    }
                ],
                "userProperties": [],
                "typeProperties": {
                    "variableName": "i",
                    "value": {
                        "value": "@variables('j')",
                        "type": "Expression"
                    }
                }
            },
            {
                "name": "Increment J",
                "type": "SetVariable",
                "dependsOn": [],
                "userProperties": [],
                "typeProperties": {
                    "variableName": "j",
                    "value": {
                        "value": "@string(add(int(variables('i')), 1))",
                        "type": "Expression"
                    }
                }
            }
        ],
        "variables": {
            "i": {
                "type": "String",
                "defaultValue": "0"
            },
            "j": {
                "type": "String",
                "defaultValue": "0"
            }
        },
        "annotations": []
    }
}
```


## <a name="next-steps"></a>Volgende stappen
Meer informatie over een gerelateerde controle stroom activiteit die wordt ondersteund door Data Factory: 

- [Activiteit variabele toevoegen](control-flow-append-variable-activity.md)
