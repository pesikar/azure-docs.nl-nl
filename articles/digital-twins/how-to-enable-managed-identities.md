---
title: Een beheerde identiteit voor routerings gebeurtenissen inschakelen (preview)
titleSuffix: Azure Digital Twins
description: Zie een door het systeem toegewezen identiteit inschakelen voor Azure Digital Apparaatdubbels en deze gebruiken om gebeurtenissen door te sturen.
author: baanders
ms.author: baanders
ms.date: 1/21/2021
ms.topic: how-to
ms.service: digital-twins
ms.openlocfilehash: 7de8e1eb1fd5311059bfb35d22b679a8c1f5ba9d
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/28/2021
ms.locfileid: "98948783"
---
# <a name="enable-a-managed-identity-for-routing-azure-digital-twins-events-preview"></a>Een beheerde identiteit inschakelen voor het routeren van Azure Digital Apparaatdubbels-gebeurtenissen (preview-versie)

In dit artikel wordt beschreven hoe u een door het [systeem toegewezen identiteit kunt inschakelen voor een Azure Digital apparaatdubbels-exemplaar](concepts-security.md#managed-identity-for-accessing-other-resources-preview) (momenteel in de preview-versie) en hoe u de identiteit gebruikt bij het door sturen van gebeurtenissen naar ondersteunde doelen, zoals [Event hub](../event-hubs/event-hubs-about.md), [Service Bus](../service-bus-messaging/service-bus-messaging-overview.md)   doelen en [Azure storage container](../storage/blobs/storage-blobs-introduction.md).

Hier volgen de stappen die in dit artikel worden behandeld: 

1. Een Azure Digital Apparaatdubbels-exemplaar maken met een door het systeem toegewezen identiteit of door het systeem toegewezen identiteit in te scha kelen voor een bestaand exemplaar van Azure Digital Apparaatdubbels. 
1. Een geschikte rol of rollen toevoegen aan de identiteit. Wijs bijvoorbeeld de rol **Azure Event hub data Sender** toe aan de identiteit als het eind punt Event hub is of **Azure service bus rol gegevens afzender** als het eind punt service bus is.
1. Een eind punt maken in azure Digital Apparaatdubbels dat door het systeem toegewezen identiteiten kan gebruiken voor verificatie.

## <a name="enable-system-managed-identities-for-an-instance"></a>Door systeem beheerde identiteiten inschakelen voor een exemplaar 

Wanneer u een door het systeem toegewezen identiteit inschakelt voor uw Azure Digital Apparaatdubbels-exemplaar, wordt er in azure automatisch een identiteit voor gemaakt in [Azure Active Directory (Azure AD)](../active-directory/fundamentals/active-directory-whatis.md). Deze identiteit kan vervolgens worden gebruikt om te verifiëren bij Azure Digital Apparaatdubbels-eind punten voor het door sturen van gebeurtenissen.

U kunt door het systeem beheerde identiteiten inschakelen voor een Azure Digital Apparaatdubbels-exemplaar **als onderdeel van de eerste installatie van het exemplaar**, of **het later inschakelen voor een exemplaar dat al bestaat**.

Een van deze aanmaak methoden biedt dezelfde configuratie opties en hetzelfde eind resultaat voor uw exemplaar. In deze sectie wordt beschreven hoe u dit doet.

### <a name="add-a-system-managed-identity-during-instance-creation"></a>Een door een systeem beheerde identiteit toevoegen tijdens het maken van een exemplaar

In deze sectie leert u hoe u een door een systeem beheerde identiteit inschakelt op een Azure Digital Apparaatdubbels-exemplaar dat momenteel wordt gemaakt. In deze sectie wordt aandacht besteed aan de stap beheerde identiteit van het aanmaak proces. voor een volledig overzicht van het maken van een nieuw exemplaar van de Azure Digital Apparaatdubbels raadpleegt u [*How to: een exemplaar en verificatie instellen*](how-to-set-up-instance-portal.md).

De optie door het systeem beheerde identiteit bevindt zich op het tabblad **Geavanceerd** van de installatie van Setup.

Selecteer op dit tabblad de optie **aan voor door** het **systeem beheerde identiteit** om deze functie in te scha kelen.

:::image type="content" source="media/how-to-enable-managed-identities/create-instance-advanced.png" alt-text="Scherm afbeelding van de Azure Portal het tabblad Geavanceerd van het dialoog venster Resource maken voor Azure Digital Apparaatdubbels weer gegeven. Er is een hooglicht rond de naam van het tabblad, de optie aan voor door het systeem beheerde identiteit en de navigatie knoppen (bekijken + maken, vorige, volgende: Geavanceerd).":::

U kunt vervolgens de onderste navigatie knoppen gebruiken om door te gaan met de rest van de installatie van het exemplaar.

### <a name="add-a-system-managed-identity-to-an-existing-instance"></a>Een door een systeem beheerde identiteit toevoegen aan een bestaand exemplaar

In deze sectie gebruikt u de [Azure Portal](https://portal.azure.com) om een door het systeem beheerde identiteit toe te voegen aan een Azure Digital apparaatdubbels-exemplaar dat al bestaat.

1. Ga eerst naar de [Azure Portal](https://portal.azure.com) in een browser.

1. Zoek de naam van uw instantie in de zoek balk van de portal en selecteer deze om de details ervan weer te geven.

1. Selecteer **identiteit (preview)** in het menu aan de linkerkant.

1. Selecteer op deze pagina de optie **op** om deze functie in te scha kelen.

1. Klik op de knop **Opslaan** en **Ja** om te bevestigen.

    :::image type="content" source="media/how-to-enable-managed-identities/identity-digital-twins.png" alt-text="Scherm afbeelding van de Azure Portal de pagina identiteit (preview) voor een Azure Digital Apparaatdubbels-exemplaar weer te geven. Er is een markering rond de naam van de pagina in het menu van het Azure Digital Apparaatdubbels-exemplaar, de optie op voor status, de knop Opslaan en de knop Ja bevestigen.":::

Nadat de wijziging is opgeslagen, worden er meer velden op deze pagina weer gegeven voor de **object-id** en **machtigingen** van de nieuwe identiteit.

U kunt de **object-id** indien nodig kopiëren en de **machtigingen** knop gebruiken om de Azure-rollen weer te geven die aan de identiteit zijn toegewezen. Voor het instellen van sommige rollen gaat u verder met de volgende sectie.

## <a name="assign-azure-roles-to-the-identity"></a>Azure-rollen toewijzen aan de identiteit 

Zodra een door het systeem toegewezen identiteit is gemaakt voor uw Azure Digital Apparaatdubbels-exemplaar, moet u de juiste rollen toewijzen voor verificatie met verschillende typen [eind punten](concepts-route-events.md) voor het door sturen van gebeurtenissen naar ondersteunde bestemmingen. In deze sectie worden de opties voor de functie beschreven en wordt uitgelegd hoe u deze toewijst aan de door het systeem toegewezen identiteit.

>[!NOTE]
> Dit is een belang rijke stap, zonder IT, de identiteit heeft geen toegang tot uw eind punten en gebeurtenissen worden niet bezorgd.

### <a name="supported-destinations-and-azure-roles"></a>Ondersteunde doelen en Azure-rollen 

Hier volgen de minimale rollen die een identiteit nodig heeft voor toegang tot een eind punt, afhankelijk van het type bestemming. Rollen met hogere machtigingen (zoals rollen van de eigenaar van gegevens) werken ook.

| Doel | Azure-rol |
| --- | --- |
| Azure Event Hubs | Afzender van Azure Event Hubs gegevens |
| Azure Service Bus | Afzender van Azure Service Bus gegevens |
| Azure storage-container | Inzender voor Storage Blob-gegevens |

Zie voor meer informatie over eind punten, routes en de typen bestemmingen die worden ondersteund voor route ring in azure Digital Apparaatdubbels de [*concepten: gebeurtenis routes*](concepts-route-events.md).

### <a name="assign-the-role"></a>De rol toewijzen

>[!NOTE]
> Deze sectie moet worden uitgevoerd door een Azure-gebruiker met machtigingen voor het beheren van de gebruikers toegang tot Azure-resources (inclusief het verlenen en delegeren van machtigingen). Algemene rollen die aan deze vereiste voldoen, zijn *eigenaar*, *account beheerder* of de combi natie van beheerder en *mede werker* van de *gebruikers toegang* . Zie [*How-to: instance en Authentication instellen*](how-to-set-up-instance-portal.md#prerequisites-permission-requirements)voor meer informatie over machtigings vereisten voor Azure Digital apparaatdubbels-rollen.

Als u een rol aan de identiteit wilt toewijzen, moet u eerst de [Azure Portal](https://portal.azure.com)openen.

1. Navigeer naar uw eindpunt resource (uw Event Hub, Service Bus onderwerp of opslag container) door de naam te zoeken in de zoek balk van de portal. 
1. Selecteer **toegangs beheer (IAM)** in het menu aan de linkerkant.
1. Selecteer de knop **+ toevoegen** om een nieuwe roltoewijzing toe te voegen.

    :::image type="content" source="media/how-to-enable-managed-identities/add-role-assignment-1.png" alt-text="Scherm afbeelding van de Azure Portal de IAM-pagina (Access Control) voor een Event Hub wordt weer gegeven. De knop + toevoegen is gemarkeerd." lightbox="media/how-to-enable-managed-identities/add-role-assignment-1.png":::

1. Vul op de volgende pagina **roltoewijzing toevoegen** de waarden in:
    * **Rol**: Selecteer de gewenste rol in het vervolg keuzemenu
    * **Toegang toewijzen aan**: Kies **gebruiker, groep of Service-Principal**
    * **Select**: hier selecteert u de beheerde identiteit van uw Azure Digital apparaatdubbels-exemplaar waaraan de rol wordt toegewezen. De naam van de beheerde identiteit komt overeen met de naam van het exemplaar, dus zoek de naam van uw Azure Digital Apparaatdubbels-exemplaar. Wanneer u het resultaat selecteert, wordt de identiteit van de instantie weer gegeven in de sectie **geselecteerde leden** .

    :::row:::
        :::column:::
            :::image type="content" source="media/how-to-enable-managed-identities/add-role-assignment-2.png" alt-text="De vermelde velden invullen in het dialoog venster functie toewijzing toevoegen":::
        :::column-end:::
        :::column:::
        :::column-end:::
    :::row-end:::

Wanneer u klaar bent met het invoeren van de details, selecteert u **Opslaan**.

## <a name="create-an-endpoint-with-identity-based-authorization"></a>Een eind punt maken met autorisatie op basis van een identiteit

Nadat u een door een systeem beheerde identiteit hebt ingesteld voor uw Azure Digital Apparaatdubbels-exemplaar en de juiste rol (len) hebt toegewezen, kunt u Azure Digital Apparaatdubbels- [eind punten](how-to-manage-routes-portal.md#create-an-endpoint-for-azure-digital-twins) maken die de identiteit kunnen gebruiken voor verificatie. Deze optie is alleen beschikbaar voor Event hub-en Service Bus-type-eind punten (wordt niet ondersteund voor Event Grid).

>[!NOTE]
> U kunt een eind punt dat al is gemaakt met een op de sleutel gebaseerde identiteit niet bewerken om te wijzigen in verificatie op basis van identiteit. U moet het verificatie type kiezen wanneer het eind punt voor het eerst wordt gemaakt.

Volg de [instructies voor het maken van een Azure Digital apparaatdubbels-eind punt](how-to-manage-routes-portal.md#create-an-endpoint-for-azure-digital-twins).

Wanneer u de stap van het volt ooien van de vereiste gegevens voor het type eind punt krijgt, moet u ervoor zorgen dat u op basis van de **identiteit** een verificatie type selecteert.

:::row:::
    :::column:::
        :::image type="content" source="media/how-to-manage-routes-portal/create-endpoint-event-hub-authentication.png" alt-text="Scherm opname van het maken van een eind punt van het type Event hub." lightbox="media/how-to-manage-routes-portal/create-endpoint-event-hub-authentication.png":::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Voltooi het instellen van uw eind punt en selecteer **Opslaan**.

## <a name="considerations-for-disabling-system-managed-identities"></a>Overwegingen voor het uitschakelen van door het systeem beheerde identiteiten

Omdat een identiteit afzonderlijk wordt beheerd vanuit de eind punten die deze gebruiken, is het belang rijk om te overwegen wat de gevolgen zijn van wijzigingen aan de identiteit of hun rollen op de eind punten in uw Azure Digital Apparaatdubbels-exemplaar. Als de identiteit is uitgeschakeld of een vereiste rol voor een eind punt wordt verwijderd, kan het eind punt ontoegankelijk worden en wordt de stroom van gebeurtenissen onderbroken.

Als u een eind punt wilt blijven gebruiken dat is ingesteld met een beheerde identiteit die nu is uitgeschakeld, moet u het eind punt verwijderen en [opnieuw maken](how-to-manage-routes-portal.md#create-an-endpoint-for-azure-digital-twins) met een ander verificatie type. Het kan tot een uur duren voordat gebeurtenissen na deze wijziging naar het eind punt worden hervat.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over beheerde identiteiten in azure AD: 
* [*Beheerde identiteiten voor Azure-resources*](../active-directory/managed-identities-azure-resources/overview.md)