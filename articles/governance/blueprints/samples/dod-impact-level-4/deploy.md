---
title: DoD Impact Level 4-blauwdrukvoorbeeld
description: Implementeer stappen voor het DoD Impact Level 4-blauwdrukvoorbeeld, inclusief de parametergegevens voor blauwdrukartefacten.
ms.date: 01/08/2021
ms.topic: sample
ms.openlocfilehash: 40f45d1194ae089010edf308c3b110bc97591613
ms.sourcegitcommit: c4c554db636f829d7abe70e2c433d27281b35183
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/08/2021
ms.locfileid: "98033758"
---
# <a name="deploy-the-dod-impact-level-4-blueprint-sample"></a>Het DoD Impact Level 4-blauwdrukvoorbeeld implementeren

Als u het DoD IL 4-blauwdrukvoorbeeld (Department of Defense Impact Level 4) van Azure Blueprints wilt implementeren, moet u de volgende stappen uitvoeren:

> [!div class="checklist"]
> - Een nieuwe blauwdruk maken op basis van het voorbeeld
> - Uw kopie van het voorbeeld markeren als **Gepubliceerd**
> - Uw kopie van de blauwdruk toewijzen aan een bestaand abonnement

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free) aan voordat u begint.

## <a name="create-blueprint-from-sample"></a>Een blauwdruk maken op basis van een voorbeeld

Implementeer eerst het blauwdrukvoorbeeld door een nieuwe blauwdruk in uw omgeving te maken op basis van het voorbeeld.

1. Selecteer **Alle services** in het linkerdeelvenster. Zoek en selecteer **Blauwdrukken**.

1. Op de pagina **Aan de slag** aan de linkerkant selecteert u de knop **Maken** onder _Een blauwdruk maken_.

1. Zoek het blauwdrukvoorbeeld **DoD Impact Level 4** onder _Andere voorbeelden_, en selecteer **Dit voorbeeld gebruiken**.

1. Voer de _Basisinstellingen_ van het blauwdrukvoorbeeld in:

   - **Naam van blauwdruk**: Geef een naam op voor uw kopie van het DoD Impact Level 4-blauwdrukvoorbeeld.
   - **Definitielocatie**: Gebruik het weglatingsteken en selecteer de beheergroep waarin u uw kopie van het voorbeeld wilt opslaan.

1. Selecteer het tabblad _Artefacten_ boven aan de pagina of kies **Volgende: Artefacten** onder aan de pagina.

1. Controleer de lijst met artefacten die samen het blauwdrukvoorbeeld vormen. Veel van de artefacten bevatten parameters die we later zullen definiëren. Selecteer **Concept opslaan** wanneer u klaar bent met het controleren van het blauwdrukvoorbeeld.

## <a name="publish-the-sample-copy"></a>De voorbeeldkopie publiceren

Uw kopie van het blauwdrukvoorbeeld is nu gemaakt in uw omgeving. De kopie is gemaakt in de **Concept**-modus en moet worden **Gepubliceerd** voordat deze kan worden toegewezen en geïmplementeerd. De kopie van het blauwdrukvoorbeeld kan worden aangepast aan uw omgeving en behoeften, maar door deze aanpassing is het mogelijk dat de kopie niet meer is afgestemd op de DoD Impact Level 4-beheeropties.

1. Selecteer **Alle services** in het linkerdeelvenster. Zoek en selecteer **Blauwdrukken**.

1. Selecteer de pagina **Blauwdrukdefinities** aan de linkerkant. Gebruik de filters om uw kopie van het blauwdrukvoorbeeld te zoeken en selecteer vervolgens uw kopie.

1. Selecteer **Blauwdruk publiceren** boven aan de pagina. Op de nieuwe pagina aan de rechterkant geeft u een **Versie** voor uw kopie van het blauwdrukvoorbeeld op. Deze eigenschap is handig als u later een aanpassing wilt maken. Geef **Notities over wijzigingen** op, zoals 'Eerste gepubliceerde versie op basis van het DoD IL 4-blauwdrukvoorbeeld'. Selecteer vervolgens **Publiceren** onder aan de pagina.

## <a name="assign-the-sample-copy"></a>De voorbeeldkopie toewijzen

Zodra de kopie van het blauwdrukvoorbeeld is **Gepubliceerd**, kan het worden toegewezen aan een abonnement binnen de beheergroep waarin de kopie is opgeslagen. Dit is de stap waarin parameters worden opgegeven om elke implementatie van de kopie van het blauwdrukvoorbeeld uniek te maken.

1. Selecteer **Alle services** in het linkerdeelvenster. Zoek en selecteer **Blauwdrukken**.

1. Selecteer de pagina **Blauwdrukdefinities** aan de linkerkant. Gebruik de filters om uw kopie van het blauwdrukvoorbeeld te zoeken en selecteer vervolgens uw kopie.

1. Selecteer **Blauwdruk toewijzen** boven aan de pagina Blauwdrukdefinitie.

1. Geef de parameterwaarden op voor de blauwdruktoewijzing:

   - Basisbeginselen

     - **Abonnementen**: Selecteer een of meer van de abonnementen in de beheergroep waarin u uw kopie van het blauwdrukvoorbeeld hebt opgeslagen. Als u meer dan één abonnement selecteert, wordt een toewijzing gemaakt voor elk abonnement waarvoor de ingevoerde parameters worden gebruikt.
     - **Naam van toewijzing**: De naam wordt vooraf voor u ingevuld op basis van de naam van de blauwdruk.
       Wijzig de naam als dat nodig is of gebruik de opgegeven naam.
     - **Locatie**: Selecteer een regio waarin u de beheerde identiteit wilt maken. Azure Blueprint gebruikt deze beheerde identiteit om alle artefacten in de toegewezen blauwdruk te implementeren. Zie [Beheerde identiteiten voor Azure-resources](../../../../active-directory/managed-identities-azure-resources/overview.md) voor meer informatie.
     - **Blauwdrukdefinitieversie**: Kies een **gepubliceerde** versie van uw kopie van het blauwdrukvoorbeeld.

   - Toewijzing vergrendelen

     Selecteer de instelling voor het vergrendelen van de blauwdruk voor uw omgeving. Zie voor meer informatie [Vergrendeling van blauwdrukresources](../../concepts/resource-locking.md).

   - Beheerde identiteit

     Laat de optie voor de standaard door het _systeem toegewezen_ beheerde identiteit staan.

   - Artefactparameters

     De parameters die in deze sectie worden gedefinieerd, zijn van toepassing op het artefact waaronder de parameter is gedefinieerd. Deze parameters zijn [dynamische parameters](../../concepts/parameters.md#dynamic-parameters), aangezien ze zijn gedefinieerd tijdens de toewijzing van de blauwdruk. Zie de [tabel met artefactparameters](#artifact-parameters-table) voor een volledige lijst met artefactparameters en hun beschrijvingen.

1. Zodra alle parameters zijn ingevoerd, selecteert u **Toewijzen** onder aan de pagina. De blauwdruktoewijzing wordt gemaakt en de implementatie van het artefact begint. De implementatie duurt circa één uur. Open de blauwdruktoewijzing om de status van de implementatie te controleren.

> [!WARNING]
> De Azure Blueprints-service en de ingebouwde blauwdrukvoorbeelden zijn **gratis**. Azure-resources zijn [geprijsd per product](https://azure.microsoft.com/pricing/). Gebruik de [prijscalculator](https://azure.microsoft.com/pricing/calculator/) om de kosten te schatten voor het uitvoeren van resources die door dit blauwdrukvoorbeeld zijn geïmplementeerd.

## <a name="artifact-parameters-table"></a>Tabel met artefactparameters

In de volgende tabel ziet u een lijst met de blauwdrukartefactparameters:

|Naam van het artefact|Type artefact|Parameternaam|Beschrijving|
|-|-|-|-|
|Toegestane locaties|Beleidstoewijzing|Toegestane locaties:|Met dit beleid kunt u de locaties beperken die uw organisatie kan opgeven tijdens het implementeren van resources. Dit beleid wordt gebruikt om uw geografische nalevingsvereisten af te dwingen.|
|Toegestane locaties voor resourcegroepen|Beleidstoewijzing |Toegestane locaties:|Met dit beleid kunt u de locaties beperken waarin uw organisatie resourcegroepen kan maken. Dit beleid wordt gebruikt om uw geografische nalevingsvereisten af te dwingen.|
|Controle op SQL-servers implementeren|Beleidstoewijzing|De waarde in dagen van de bewaarperiode (0 betekent een onbeperkte bewaarperiode)|Bewaarperiode in dagen (optioneel, 180 dagen als u niets opgeeft)|
|Controle op SQL-servers implementeren|Beleidstoewijzing|De resourcegroepnaam voor het opslagaccount voor SQL Server-controles|De controle schrijft databasegebeurtenissen naar een auditlogboek in uw Azure Storage-account (er wordt een opslagaccount aangemaakt in elke regio waarin een SQL-server wordt gemaakt die wordt gedeeld door alle servers in die regio). Belangrijk: voor de juiste werking van de controle mag u geen resourcegroepen of opslagaccounts verwijderen of hernoemen.|
|Diagnostische instellingen voor netwerkbeveiligingsgroepen implementeren|Beleidstoewijzing|Het voorvoegsel van het opslagaccount voor netwerkbeveiligingsgroepdiagnoses|Dit voorvoegsel vormt in combinatie met de locatie van de netwerkbeveiligingsgroep de naam van het gemaakte opslagaccount.|
|Diagnostische instellingen voor netwerkbeveiligingsgroepen implementeren|Beleidstoewijzing|De resourcegroepnaam voor het opslagaccount voor netwerkbeveiligingsgroepdiagnoses (moet bestaan)|De resourcegroep waarin het opslagaccount wordt gemaakt. Deze resourcegroep moet al bestaan.|
|Log Analytics-agent implementeren voor virtuele-machineschaalsets van Linux|Beleidstoewijzing|Log Analytics-werkruimte voor virtuele-machineschaalsets van Linux|Als deze werkruimte buiten het bereik van de toewijzing valt, moet u aan de principal-id van de beleidstoewijzing handmatig de rechten voor Inzender voor Log Analytics (of vergelijkbaar) toekennen.|
|Log Analytics-agent implementeren voor virtuele-machineschaalsets van Linux|Beleidstoewijzing|Optioneel: Lijst met VM-installatiekopieën met ondersteuning van het Linux-besturingssysteem die aan het bereik kunnen worden toegevoegd|Een lege matrix kan worden gebruikt om aan te geven dat er geen optionele parameters zijn: \[\]|
|Log Analytics-agent voor virtuele Linux-machines implementeren|Beleidstoewijzing|Log Analytics-werkruimte voor virtuele Linux-machines|Als deze werkruimte buiten het bereik van de toewijzing valt, moet u aan de principal-id van de beleidstoewijzing handmatig de rechten voor Inzender voor Log Analytics (of vergelijkbaar) toekennen.|
|Log Analytics-agent voor virtuele Linux-machines implementeren|Beleidstoewijzing|Optioneel: Lijst met VM-installatiekopieën met ondersteuning van het Linux-besturingssysteem die aan het bereik kunnen worden toegevoegd|Een lege matrix kan worden gebruikt om aan te geven dat er geen optionele parameters zijn: \[\]|
|Log Analytics-agent implementeren voor virtuele-machineschaalsets van Windows|Beleidstoewijzing|Log Analytics-werkruimte voor virtuele-machineschaalsets van Windows|Als deze werkruimte buiten het bereik van de toewijzing valt, moet u aan de principal-id van de beleidstoewijzing handmatig de rechten voor Inzender voor Log Analytics (of vergelijkbaar) toekennen.|
|Log Analytics-agent implementeren voor virtuele-machineschaalsets van Windows|Beleidstoewijzing|Optioneel: Lijst met VM-installatiekopieën met ondersteuning van het Windows-besturingssysteem die aan het bereik kunnen worden toegevoegd|Een lege matrix kan worden gebruikt om aan te geven dat er geen optionele parameters zijn: \[\]|
|Log Analytics-agent voor virtuele Windows-machines implementeren|Beleidstoewijzing|Log Analytics-werkruimte voor Windows-VM's|Als deze werkruimte buiten het bereik van de toewijzing valt, moet u aan de principal-id van de beleidstoewijzing handmatig de rechten voor Inzender voor Log Analytics (of vergelijkbaar) toekennen.|
|Log Analytics-agent voor virtuele Windows-machines implementeren|Beleidstoewijzing|Optioneel: Lijst met VM-installatiekopieën met ondersteuning van het Windows-besturingssysteem die aan het bereik kunnen worden toegevoegd|Een lege matrix kan worden gebruikt om aan te geven dat er geen optionele parameters zijn: \[\]|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Leden worden opgenomen in de lokale groep Administrators|Een lijst met leden die niet moeten worden opgenomen in de lokale groep beheerders, gescheiden door puntkomma's. Bijvoorbeeld: Beheerder; myUser1; myUser2|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Leden die moeten worden uitgesloten in de lokale groep Administrators|Een lijst met leden die moeten worden opgenomen in de lokale groep beheerders, gescheiden door puntkomma's. Bijvoorbeeld: Beheerder; myUser1; myUser2|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Lijst met resourcetypen waarvoor diagnostische logboeken moeten zijn ingeschakeld|Lijst met resourcetypen die moeten worden gecontroleerd als de instelling voor diagnostische logboeken niet is ingeschakeld. Acceptabele waarden vindt u in de [schema's van diagnostische logboeken van Azure Monitor](../../../../azure-monitor/platform/resource-logs-schema.md#service-specific-schemas).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Id van de Log Analytics-werkruimte waarvoor VM's moeten worden geconfigureerd|Dit is de id (GUID) van de Log Analytics-werkruimte waarvoor de VM's moeten worden geconfigureerd.|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Geografisch redundante back-up op de lange termijn moet zijn ingeschakeld voor Azure SQL Databases|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|De evaluatie van beveiligingsproblemen moet worden ingeschakeld voor uw beheerde SQL-exemplaren|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|De evaluatie van beveiligingsproblemen moet worden ingeschakeld op uw SQL-servers|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Geografisch redundante opslag moet zijn ingeschakeld voor opslagaccounts|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Geografisch redundante back-up moet zijn ingeschakeld voor Azure Database for MySQL|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Geografisch redundante back-up moet zijn ingeschakeld voor Azure Database for PostgreSQL|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Webtoepassing mag alleen toegankelijk zijn via HTTPS|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Functie-app mag alleen toegankelijk zijn via HTTPS|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Externe accounts met schrijfmachtigingen moeten worden verwijderd uit uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Externe accounts met leesmachtigingen moeten worden verwijderd uit uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Externe accounts met eigenaarsmachtigingen moeten worden verwijderd uit uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Afgeschafte accounts met eigenaarsmachtigingen moeten worden verwijderd uit uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Afgeschafte accounts moeten worden verwijderd uit uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|CORS mag niet toestaan dat elke bron toegang heeft tot uw webtoepassing|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|Systeemupdates op virtuele-machineschaalsets moeten worden geïnstalleerd|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|MFA moet zijn ingeschakeld voor accounts met leesmachtigingen voor uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|MFA moet zijn ingeschakeld voor accounts met eigenaarsmachtigingen voor uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|
|\[Preview\]: DoD Impact Level 4|Beleidstoewijzing|MFA moet zijn ingeschakeld voor accounts met schrijfmachtigingen voor uw abonnement|Informatie over de effecten van het beleid vindt u bij [Inzicht in de effecten van Azure Policy](../../../policy/concepts/effects.md).|

## <a name="next-steps"></a>Volgende stappen

Nu u de stappen voor het implementeren van het DoD Impact Level 4-blauwdrukvoorbeeld hebt bekeken, raadpleegt u de volgende artikelen voor informatie over de blauwdruk en de toewijzing van besturingselementen:

> [!div class="nextstepaction"]
> [DoD Impact Level 4-blauwdruk - overzicht](./index.md)
> [DoD Impact Level 4-blauwdruk - toewijzing van beheeropties](./control-mapping.md)

Aanvullende artikelen over blauwdrukken en het gebruik hiervan:

- Meer informatie over de [levenscyclus van een blauwdruk](../../concepts/lifecycle.md).
- Meer informatie over hoe u [statische en dynamische parameters](../../concepts/parameters.md) gebruikt.
- Meer informatie over hoe u de [blauwdrukvolgorde](../../concepts/sequencing-order.md) aanpast.
- Meer informatie over hoe u gebruikmaakt van [resourcevergrendeling in blauwdrukken](../../concepts/resource-locking.md).
- Meer informatie over hoe u [bestaande toewijzingen bijwerkt](../../how-to/update-existing-assignments.md).
