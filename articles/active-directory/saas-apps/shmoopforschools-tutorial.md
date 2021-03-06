---
title: 'Zelfstudie: Azure Active Directory-integratie met Shmoop For Schools | Microsoft Docs'
description: Ontdek hoe u eenmalige aanmelding configureert tussen Azure Active Directory en Shmoop For Schools.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 12/18/2020
ms.author: jeedes
ms.openlocfilehash: d1d29e939ab01f6311b665eaec8425b7cd38f207
ms.sourcegitcommit: 78ecfbc831405e8d0f932c9aafcdf59589f81978
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/23/2021
ms.locfileid: "98729458"
---
# <a name="tutorial-integrate-shmoop-for-schools-with-azure-active-directory"></a>Zelfstudie: Shmoop For Schools integreren met Azure Active Directory

In deze zelfstudie leert u hoe u Shmoop For Schools kunt integreren met Azure Active Directory (Azure AD). Wanneer u Shmoop For Schools integreert met Azure AD, kunt u het volgende:

* U kunt in Azure AD beheren wie toegang heeft tot Shmoop For Schools.
* U kunt instellen dat gebruikers zich automatisch met hun Azure AD-account kunnen aanmelden bij Shmoop For Schools.
* Uw accounts op een centrale locatie beheren: Azure Portal.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om aan de slag te gaan:

* Een Azure AD-abonnement Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Een abonnement op Shmoop For Schools waarvoor eenmalige aanmelding is ingeschakeld.

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie gaat u in een testomgeving eenmalige aanmelding van Azure AD configureren en testen.

* Shmoop For Schools biedt ondersteuning voor door **SP** geïnitieerde eenmalige aanmelding
* Shmoop For Schools biedt ondersteuning voor **Just-In-Time**-inrichting van gebruikers

## <a name="adding-shmoop-for-schools-from-the-gallery"></a>Shmoop For Schools toevoegen vanuit de galerie

Voor het configureren van de integratie van Shmoop For Schools in Azure AD moet u Shmoop For Schools uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

1. Meld u bij de Azure-portal aan met een werk- of schoolaccount of een persoonlijk Microsoft-account.
1. Selecteer in het linkernavigatiedeelvenster de service **Azure Active Directory**.
1. Ga naar **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Nieuwe toepassing** om een nieuwe toepassing toe te voegen.
1. Typ **Shmoop For Schools** in het zoekvak in de sectie **Toevoegen uit de galerie**.
1. Selecteer **Shmoop For Schools** in het resultatenvenster en voeg vervolgens de app toe. Wacht enkele seconden tot de app is toegevoegd aan de tenant.

## <a name="configure-and-test-azure-ad-sso-for-shmoop-for-schools"></a>Eenmalige aanmelding van Azure AD configureren en testen voor Shmoop For Schools

Configureer en test eenmalige aanmelding van Azure AD met Shmoop For Schools met behulp van een testgebruiker met de naam **B.Simon**. Eenmalige aanmelding werkt alleen als u een koppelingsrelatie tot stand brengt tussen een Azure AD-gebruiker en de bijbehorende gebruiker in Shmoop For Schools.

Voer de volgende stappen uit om eenmalige aanmelding van Azure AD te configureren en te testen voor Shmoop For Schools:

1. **[Eenmalige aanmelding van Azure AD configureren](#configure-azure-ad-sso)** : zodat uw gebruikers deze functie kunnen gebruiken.
    1. **[Een Azure AD-testgebruiker maken](#create-an-azure-ad-test-user)** : om eenmalige aanmelding van Azure AD te testen met B.Simon.
    1. **[De Azure AD-testgebruiker toewijzen](#assign-the-azure-ad-test-user)** zodat B.Simon eenmalige aanmelding van Azure AD kan gebruiken.
2. **[Eenmalige aanmelding van Shmoop For Schools configureren](#configure-shmoop-for-schools-sso)** : als u de instellingen voor eenmalige aanmelding aan de toepassingszijde wilt configureren.
    1. **[Een testgebruiker voor Shmoop for Schools maken](#create-shmoop-for-schools-test-user)** : als u in Shmoop for Schools een tegenhanger van B.Simon wilt hebben die is gekoppeld aan de Azure AD-representatie van de gebruiker.
3. **[Eenmalige aanmelding testen](#test-sso)** : om te controleren of de configuratie werkt.

## <a name="configure-azure-ad-sso"></a>Eenmalige aanmelding van Azure AD configureren

Volg deze stappen om eenmalige aanmelding van Azure AD in te schakelen in Azure Portal.

1. Zoek in Azure Portal, op de integratiepagina van de toepassing **Shmoop For Schools**, de sectie **Beheren** en selecteer **Eenmalige aanmelding**.
1. Selecteer **SAML** op de pagina **Selecteer een methode voor eenmalige aanmelding**.
1. Op de pagina **Eenmalige aanmelding instellen met SAML** klikt u op het potloodpictogram voor **Standaard-SAML-configuratie** om de instellingen te bewerken.

   ![Standaard SAML-configuratie bewerken](common/edit-urls.png)

1. In de sectie **Standaard SAML-configuratie** voert u de volgende stappen uit:

    a. In het tekstvak **Aanmeldings-URL** typt u een URL met de volgende notatie: `https://schools.shmoop.com/public-api/saml2/start/<uniqueid>`

    b. In het tekstvak **Id (Entiteits-id)** typt u een URL met de volgende notatie: `https://schools.shmoop.com/<uniqueid>`

    > [!NOTE]
    > Dit zijn geen echte waarden. Werk deze waarden bij met de werkelijke aanmeldings-URL en id. Neem contact op met het [klantondersteuningsteam van Shmoop For Schools](mailto:support@shmoop.com) om deze waarden op te vragen. U kunt ook verwijzen naar het patroon dat wordt weergegeven in de sectie **Standaard SAML-configuratie** in de Azure-portal.

1. In de Shmoop For Schools-toepassing worden de SAML-asserties in een specifieke indeling verwacht. Hiervoor moet u aangepaste kenmerktoewijzingen toevoegen aan de configuratie van uw SAML-tokenkenmerken. In de volgende schermafbeelding wordt de lijst met standaardkenmerken weergegeven.

    ![image](common/default-attributes.png)

1. Bovendien verwacht de toepassing Shmoop For Schools nog enkele kenmerken die als SAML-antwoord moeten worden doorgestuurd. Deze worden hieronder weergegeven. Deze kenmerken worden ook vooraf ingevuld, maar u kunt ze herzien volgens uw vereisten.

    | Naam |  Bronkenmerk|
    | --------- | --------------- |
    | role      | user.assignedroles |

    > [!NOTE]
    > Shmoop For Schools biedt ondersteuning voor twee rollen voor gebruikers: **Docent** en **Student**. Stel deze rollen in Azure AD in zodat gebruikers de juiste rollen kunnen toegewezen kunnen krijgen. Zie [hier](../develop/howto-add-app-roles-in-azure-ad-apps.md#app-roles-ui--preview)voor meer informatie over het configureren van rollen in Azure AD.

1. Op de pagina **Eenmalige aanmelding met SAML instellen** in het gedeelte **SAML-handtekeningcertificaat** klikt u op de kopieerknop om de **URL voor federatieve metagegevens van de app** te kopiëren en slaat u deze op uw computer op.

    ![De link om het certificaat te downloaden](common/copy-metadataurl.png)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

In deze sectie gaat u een testgebruiker met de naam B.Simon maken in Azure Portal.

1. Selecteer in het linkerdeelvenster van Azure Portal de optie **Azure Active Directory**, selecteer **Gebruikers** en selecteer vervolgens **Alle gebruikers**.
1. Selecteer **Nieuwe gebruiker** boven aan het scherm.
1. Volg de volgende stappen bij de eigenschappen voor **Gebruiker**:
    1. Voer in het veld **Naam**`B.Simon` in.  
    1. Voer username@companydomain.extension in het veld **Gebruikersnaam** in. Bijvoorbeeld `B.Simon@contoso.com`.
    1. Schakel het selectievakje **Wachtwoord weergeven** in en noteer de waarde die wordt weergegeven in het vak **Wachtwoord**.
    1. Klik op **Create**.

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie geeft u B.Simon toestemming om eenmalige aanmelding van Azure te gebruiken door toegang te verlenen tot Shmoop For Schools.

1. Selecteer in Azure Portal de optie **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Shmoop For Schools** in de lijst met toepassingen.
1. Zoek op de overzichtspagina van de app de sectie **Beheren** en selecteer **Gebruikers en groepen**.
1. Selecteer **Gebruiker toevoegen** en selecteer vervolgens **Gebruikers en groepen** in het dialoogvenster **Toewijzing toevoegen**.
1. Selecteer in het dialoogvenster **Gebruikers en groepen** de optie **B.Simon** in de lijst Gebruikers. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Als u de rollen hebt ingesteld zoals hierboven beschreven, kunt u deze selecteren in de vervolgkeuzelijst **Selecteer een rol**.
1. Klik in het dialoogvenster **Toewijzing toevoegen** op de knop **Toewijzen**.

## <a name="configure-shmoop-for-schools-sso"></a>Eenmalige aanmelding van Shmoop For Schools configureren

Als u eenmalige aanmelding aan de zijde van **Shmoop For Schools** wilt configureren, moet u de **App-URL voor federatieve metagegevens** verzenden naar het [ondersteuningsteam van Shmoop For Schools](mailto:support@shmoop.com). Het team stelt de instellingen zo in dat de verbinding tussen SAML en eenmalige aanmelding aan beide zijden goed is ingesteld.

### <a name="create-shmoop-for-schools-test-user"></a>Een Shmoop For Schools-testgebruiker maken

In deze sectie wordt een gebruiker met de naam B.Simon gemaakt in Shmoop For Schools. Shmoop For Schools biedt ondersteuning voor Just-In-Time-inrichting van gebruikers. Deze functie is standaard ingeschakeld. Er is geen actie-item voor u in deze sectie. Als er nog geen gebruiker in Shmoop For Schools bestaat, wordt na verificatie een nieuwe gemaakt.

> [!NOTE]
> Als u handmatig een gebruiker moet maken, neemt u contact op met het [ondersteuningsteam van Shmoop For Schools](mailto:support@shmoop.com).

## <a name="test-sso"></a>Eenmalige aanmelding testen

In deze sectie test u de configuratie voor eenmalige aanmelding van Azure AD met behulp van de volgende opties. 

* Klik in Azure Portal op **Deze toepassing testen**. U wordt omgeleid naar de aanmeldings-URL van Shmoop For Schools, waar u de aanmeldingsstroom kunt initiëren. 

* Ga rechtstreeks naar de aanmeldings-URL van Shmoop For Schools en initieer hier de aanmeldingsstroom.

* U kunt Microsoft Mijn apps gebruiken. Wanneer u in 'Mijn apps' op de tegel 'Shmoop For Schools' klikt, wordt u omgeleid naar de aanmeldings-URL van Shmoop For Schools. Zie [Introduction to My Apps](../user-help/my-apps-portal-end-user-access.md) (Inleiding tot Mijn apps) voor meer informatie over Mijn apps.


## <a name="next-steps"></a>Volgende stappen

Zodra u Shmoop For Schools hebt geconfigureerd, kunt u sessiebeheer afdwingen. Hierdoor worden exfiltratie en infiltratie van gevoelige gegevens van uw organisatie in realtime beschermd. Sessiebeheer is een uitbreiding van voorwaardelijke toegang. [Meer informatie over het afdwingen van sessiebeheer met Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).
