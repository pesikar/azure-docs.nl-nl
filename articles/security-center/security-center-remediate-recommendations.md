---
title: Aanbevelingen herstellen in Azure Security Center | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u reageert op aanbevelingen in Azure Security Center om uw resources te beschermen en te voldoen aan het beveiligings beleid.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 8be947cc-cc86-421d-87a6-b1e23077fd50
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/08/2020
ms.author: memildin
ms.openlocfilehash: dabd7e9e2c3c74225efc4611c7ad3523a6c76ba5
ms.sourcegitcommit: 02ed9acd4390b86c8432cad29075e2204f6b1bc3
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807987"
---
# <a name="remediate-recommendations-in-azure-security-center"></a>Aanbevelingen oplossen in Azure Security Center

Aanbevelingen bieden suggesties voor een betere beveiliging van uw resources. U implementeert een aanbeveling door de herstels tappen te volgen die worden beschreven in de aanbeveling.

## <a name="remediation-steps"></a>Herstels tappen <a name="remediation-steps"></a>

Nadat u alle aanbevelingen hebt bekeken, moet u bepalen welke u het eerst wilt herstellen. We raden u aan de beveiligings maatregelen te priori teren met het hoogste potentieel om uw beveiligde score te verhogen.

1. Selecteer een aanbeveling in de lijst.

1. Volg de instructies in de sectie **herstel stappen** . Elke aanbeveling heeft een eigen set instructies. De volgende scherm afbeelding toont herbemiddelings stappen voor het configureren van toepassingen zodat alleen verkeer via HTTPS wordt toegestaan.

    :::image type="content" source="./media/security-center-remediate-recommendations/security-center-remediate-recommendation.png" alt-text="Hand matige herstel stappen voor een aanbeveling" lightbox="./media/security-center-remediate-recommendations/security-center-remediate-recommendation.png":::

1. Zodra dit is voltooid, wordt een melding weer gegeven waarin wordt gemeld of het probleem is opgelost.

## <a name="quick-fix-remediation"></a>Snel herstel oplossen

Om het herstel te vereenvoudigen en de beveiliging van uw omgeving te verbeteren (en uw veilige score te verg Roten), bevatten veel aanbevelingen een optie voor snel oplossen.

Met snelle oplossing kunt u snel een aanbeveling op meerdere resources herstellen.

> [!TIP]
> Oplossingen voor snel oplossen zijn alleen beschikbaar voor specifieke aanbevelingen. Als u de aanbevelingen met een beschik bare snelle oplossing wilt vinden, gebruikt u het filter **antwoord acties** voor de lijst met aanbevelingen:
> 
> :::image type="content" source="media/security-center-remediate-recommendations/quick-fix-filter.png" alt-text="Gebruik de filters boven de lijst met aanbevelingen om aanbevelingen met de optie snel herstellen te vinden.":::

Voor het implementeren van een oplossing voor snel oplossen:

1. In de lijst met aanbevelingen waarvoor de **snelle oplossing** is geïnstalleerd. Selecteer een aanbeveling.

    [![Selecteer snelle oplossing.](media/security-center-remediate-recommendations/security-center-quick-fix-select.png)](media/security-center-remediate-recommendations/security-center-quick-fix-select.png#lightbox)

1. Op het tabblad **beschadigde bronnen** selecteert u de resources waarvoor u de aanbeveling wilt implementeren en selecteert u **herstellen**.

    > [!NOTE]
    > Sommige van de vermelde bronnen zijn mogelijk uitgeschakeld, omdat u niet over de juiste machtigingen beschikt om deze te wijzigen.

1. In het bevestigings venster leest u de details van het herstel en de implicaties.

    ![Snel oplossen](./media/security-center-remediate-recommendations/security-center-quick-fix-view.png)

    > [!NOTE]
    > De implicaties worden weer gegeven in het grijze vak in het venster **resources herstellen** dat wordt geopend nadat u op **herstellen** hebt geklikt. Ze geven een lijst weer met de wijzigingen die worden aangebracht wanneer u doorgaat met het oplossen van problemen met snel herstel.

1. Voer indien nodig de relevante para meters in en goed keuring van het herstel.

    > [!NOTE]
    > Het kan enkele minuten duren voordat het herstel is voltooid om de resources te bekijken op het tabblad onterecht **resources** . Controleer het [activiteiten logboek](#activity-log)om de herstel acties weer te geven.

1. Zodra dit is voltooid, wordt een melding weer gegeven dat u wordt geïnformeerd als het herstel is geslaagd.

## <a name="quick-fix-remediation-logging-in-the-activity-log"></a>Snel herstel logboek registratie in het activiteiten logboek <a name="activity-log"></a>

Voor de herstel bewerking wordt gebruikgemaakt van een sjabloon implementatie of REST PATCH-API-aanroep om de configuratie van de bron toe te passen. Deze bewerkingen worden geregistreerd in het [Azure-activiteiten logboek](../azure-resource-manager/management/view-activity-logs.md).


## <a name="next-steps"></a>Volgende stappen

In dit document hebt u geleerd hoe u aanbevelingen in Security Center kunt herstellen. Zie de volgende pagina's voor meer informatie over het Security Center:

* [Beveiligings beleid instellen in azure Security Center](tutorial-security-policy.md) -meer informatie over het configureren van beveiligings beleid voor uw Azure-abonnementen en-resource groepen.
* [Beveiligingsstatus controleren in Azure Security Center](security-center-monitoring.md): meer informatie over het controleren van de status van uw Azure-resources.
