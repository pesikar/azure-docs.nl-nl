---
title: 'Zelfstudie: Gesimuleerde antwoorden van een API in API Management - Azure-portal | Microsoft Docs'
description: In deze zelf studie gebruikt u API Management om een beleid in te stellen voor een API zodat deze een gesimuleerd antwoord retourneert als de back-end niet beschikbaar is voor het verzenden van echte antwoorden.
author: vladvino
ms.service: api-management
ms.custom: mvc
ms.topic: tutorial
ms.date: 09/30/2020
ms.author: apimpm
ms.openlocfilehash: 231ce9d946a2fb6650f25d90aaa423d1c95fb106
ms.sourcegitcommit: 50802bffd56155f3b01bfb4ed009b70045131750
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "91930710"
---
# <a name="tutorial-mock-api-responses"></a>Zelfstudie: Gesimuleerde antwoorden van een API

Back-end API's worden geïmporteerd in een APIM-API (API Management) of handmatig gemaakt en beheerd. Met de stappen in deze zelfstudie leert u hoe u APIM kunt gebruiken om een lege API te maken en deze handmatig te beheren, en vervolgens een beleid in te stellen voor een API om deze een gesimuleerd antwoord te laten retourneren. Deze methode maakt het voor ontwikkelaars mogelijk om verder te gaan met het implementeren en testen van de instantie van APIM, zelfs wanneer de back-end niet beschikbaar is voor het verzenden van echte antwoorden. 

De mogelijkheid om gesimuleerde antwoorden te genereren kan nuttig zijn bij een aantal scenario's:

+ Als de API-kant het eerst wordt ontworpen en de back-end implementatie later volgt. Of als de back-end parallel wordt ontwikkeld.
+ Wanneer de back-end tijdelijk niet operationeel is of niet kan worden geschaald.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een test-API maken 
> * Een bewerking aan de test-API toevoegen
> * Antwoordsimulatie inschakelen
> * De gesimuleerde API testen


:::image type="content" source="media/mock-api-responses/mock-api-responses01.png" alt-text="Gesimuleerd API-antwoord":::

## <a name="prerequisites"></a>Vereisten

+ Informatie over de [terminologie van Azure API Management](api-management-terminology.md).
+ Inzicht in het [beleidsconcept in Azure API Management](api-management-howto-policies.md).
+ Voltooi de volgende quickstart: [Een Azure API Management-exemplaar maken](get-started-create-service-instance.md).

## <a name="create-a-test-api"></a>Een test-API maken 

De stappen in deze sectie laten zien hoe u een lege API zonder back-end maakt. 


1. Meld u aan bij de Azure-portal en ga naar uw API Management-exemplaar.
1. Selecteer **APIs** >  **+ Add API** (API toevoegen) > **Blank API** (Lege API).
1. Selecteer **Full** (Volledig) in het venster **Create a Blank API** (Een lege API maken).
1. Voer *Test API* in als **Display name** (Weergavenaam).
1. Voer **Unlimited** (Onbeperkt) in bij **Products** (Producten).
1. Zorg ervoor dat **Managed** (Beheerd) is geselecteerd in **Gateways**.
1. Selecteer **Maken**.

    :::image type="content" source="media/mock-api-responses/03-mock-api-responses-01-create-test-api.png" alt-text="Gesimuleerd API-antwoord":::

## <a name="add-an-operation-to-the-test-api"></a>Een bewerking aan de test-API toevoegen

Een API stelt een of meer bewerkingen beschikbaar. In deze sectie voegt u een bewerking toe aan de lege API die u hebt gemaakt. Bij het aanroepen van de bewerking na het voltooien van de stappen in deze sectie, treedt een fout op. Na voltooiing van de stappen in de sectie [Antwoordsimulatie inschakelen](#enable-response-mocking) krijgt u geen foutmeldingen meer.

1. Selecteer de API die u in de vorige stap hebt gemaakt.
1. Klik op **+ Bewerking toevoegen**.
1. Voer in het **Frontend**-venster de volgende waarden in.

     | Instelling             | Waarde                             | Beschrijving                                                                                                                                                                                   |
    |---------------------|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **Display name** (Weergavenaam)    | *Test call* (Testaanroep)                       | De naam die wordt weergegeven in de [ontwikkelaarsportal](api-management-howto-developer-portal.md).                                                                                                                                       |
    | **URL** (HTTP-woord) | GET                               | Selecteer een van de vooraf gedefinieerde HTTP-woorden.                                                                                                                                         |
    | **URL**             | */test*                           | Een URL-pad voor de API.                                                                                                                                                                       |
    | **Deschription** (Beschrijving)     |                                   |  Optionele beschrijving van de bewerking, die wordt gebruikt om de ontwikkelaars die gebruikmaken van deze API in de ontwikkelaarsportal van documentatie te voorzien.                                                    |
    
1. Selecteer het tabblad **Responses** (Antwoorden), dat zich bevindt onder de velden URL, Display name (Weergavenaam) en Description (Beschrijving). Voer instellingen op dit tabblad in om antwoordstatuscodes, inhoudstypen, voorbeelden en schema's te definiëren.
1. Selecteer **+ Add response** (Antwoord toevoegen) en selecteer **200 OK** in de lijst.
1. Selecteer **+ Add representation** ( Weergave toevoegen) onder de kop **Representations** (Representaties) aan de rechterkant.
1. Voer *application/json* in het zoekvak in en selecteer het inhoudstype **application/json**.
1. Voer in het tekstvak **Sample** (Voorbeeld) `{ "sampleField" : "test" }` in.
1. Selecteer **Save** (Opslaan).

:::image type="content" source="media/mock-api-responses/03-mock-api-responses-02-add-operation.png" alt-text="Gesimuleerd API-antwoord" border="false":::

Hoewel dit niet vereist is voor dit voorbeeld, kunnen er op andere tabbladen aanvullende instellingen voor een API-bewerking worden geconfigureerd, waaronder:


|Tabblad      |Beschrijving  |
|---------|---------|
|**Query**     |  Voeg queryparameters toe. Naast het invoeren van een naam en beschrijving, kunt u waarden opgeven die worden toegewezen aan een queryparameter. Een van de waarden kan worden gemarkeerd als standaardwaarde (optioneel).        |
|**Aanvraag**     |  Definieer aanvraaginhoudstypen, voorbeelden en schema's.       |

## <a name="enable-response-mocking"></a>Antwoordsimulatie inschakelen

1. Selecteer de API die u in de stap [Een test-API maken](#create-a-test-api) hebt gemaakt.
1. Selecteer de testbewerking die u hebt toegevoegd.
1. Zorg ervoor dat in het venster aan de rechterkant het tabblad **Design** (Ontwerp) is geselecteerd.
1. Selecteer het venster **Inbound processing** (Binnenkomende verwerking) **+ Add policy** (Beleid toevoegen).

    :::image type="content" source="media/mock-api-responses/03-mock-api-responses-03-enable-mocking.png" alt-text="Gesimuleerd API-antwoord" border="false":::

1. Selecteer **Mock responses** (Gesimuleerde antwoorden) uit de galerie.

    :::image type="content" source="media/mock-api-responses/mock-responses-policy-tile.png" alt-text="Gesimuleerd API-antwoord" border="false":::

1. Typ **200 OK, application/json** in het tekstvak **API Management response**. Deze selectie geeft aan dat uw API het voorbeeldantwoord moet retourneren dat u hebt gedefinieerd in de vorige sectie.

    :::image type="content" source="media/mock-api-responses/mock-api-responses-set-mocking.png" alt-text="Gesimuleerd API-antwoord":::

1. Selecteer **Save** (Opslaan).

    > [!TIP]
    > Een gele balk met de tekst **Simuleren is ingeschakeld** voor uw API geeft aan dat reacties die worden geretourneerd door API Management worden gesimuleerd door het [simulatiebeleid](api-management-advanced-policies.md#mock-response) en niet worden geproduceerd door de back-end.

## <a name="test-the-mocked-api"></a>De gesimuleerde API testen

1. Selecteer de API die u in de stap [Een test-API maken](#create-a-test-api) hebt gemaakt.
1. Selecteer het tabblad **Testen**.
1. Zorg ervoor dat de **Testaanroep**-API is geselecteerd. Selecteer **Verzenden** om een testaanroep uit te voeren.

   :::image type="content" source="media/mock-api-responses/03-mock-api-responses-04-test-mocking.png" alt-text="Gesimuleerd API-antwoord":::

1. Het **HTTP-antwoord** geeft de JSON weer die is opgegeven als een voorbeeld in de eerste sectie van de zelfstudie.

    :::image type="content" source="media/mock-api-responses/mock-api-responses-test-response.png" alt-text="Gesimuleerd API-antwoord":::

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]
> * Een test-API maken
> * Een bewerking aan de test-API toevoegen
> * Antwoordsimulatie inschakelen
> * De gesimuleerde API testen

Ga door naar de volgende zelfstudie:

> [!div class="nextstepaction"]
> [Een gepubliceerde API transformeren en beveiligen](transform-api.md)
