---
title: 'Zelfstudie: Azure Active Directory-integratie met LiquidFiles | Microsoft Docs'
description: Lees hoe u eenmalige aanmelding configureert tussen Microsoft Azure Active Directory en LiquidFiles.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 04/14/2019
ms.author: jeedes
ms.openlocfilehash: b9ca860043d5c4a492908aa45bf0a89ab368d50f
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/23/2020
ms.locfileid: "92458469"
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a>Zelfstudie: Azure Active Directory-integratie met LiquidFiles

In deze zelfstudie leert u hoe u LiquidFiles kunt integreren met Azure AD (Active Directory).
De integratie van LiquidFiles met Azure AD biedt de volgende voordelen:

* U kunt in Azure AD beheren wie toegang heeft tot LiquidFiles.
* U kunt instellen dat gebruikers automatisch met hun Azure AD-account worden aangemeld bij LiquidFiles (eenmalige aanmelding).
* U kunt uw accounts vanaf één centrale locatie beheren: de Azure-portal.

Zie [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?) als u wilt graag meer wilt weten over de integratie van SaaS-apps met Azure AD.
Als u geen abonnement op Azure hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om Azure AD-integratie met LiquidFiles te configureren:

* Een Azure AD-abonnement Als u geen Azure AD-omgeving hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) krijgen
* Een LiquidFiles-abonnement waarvoor eenmalige aanmelding is ingeschakeld

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie gaat u in een testomgeving eenmalige aanmelding van Azure AD configureren en testen.

* LiquidFiles biedt ondersteuning voor met **SP** geïnitieerde SSO

## <a name="adding-liquidfiles-from-the-gallery"></a>LiquidFiles toevoegen vanuit de galerie

Als u de integratie van LiquidFiles in Azure AD wilt configureren, moet u LiquidFiles vanuit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Voer de volgende stappen uit om LiquidFiles toe te voegen vanuit de galerie:**

1. Klik in het linkernavigatievenster in de **[Azure-portal](https://portal.azure.com)** op het **Azure Active Directory** -pictogram.

    ![De knop Azure Active Directory](common/select-azuread.png)

2. Navigeer naar **Bedrijfstoepassingen** en selecteer vervolgens de optie **Alle toepassingen** .

    ![De blade Bedrijfstoepassingen](common/enterprise-applications.png)

3. Als u de nieuwe toepassing wilt toevoegen, klikt u op de knop **Nieuwe toepassing** boven aan het dialoogvenster.

    ![De knop Nieuwe toepassing](common/add-new-app.png)

4. Typ **LiquidFiles** in het zoekvak, selecteer **LiquidFiles** in het resultatenpaneel, en klik vervolgens op de knop **Toevoegen** om de toepassing toe te voegen.

    ![LiquidFiles in de lijst met resultaten](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD-eenmalige aanmelding configureren en testen

In deze sectie configureert en test u eenmalige aanmelding van Azure AD met LiquidFiles op basis van een testgebruiker met de naam **Britta Simon** .
Eenmalige aanmelding werkt alleen als er een koppelingsrelatie tot stand is gebracht tussen een Azure AD-gebruiker en de gerelateerde gebruiker in LiquidFiles.

Als u eenmalige aanmelding van Azure AD met LiquidFiles wilt configureren en testen, moet u de volgende bouwstenen voltooien:

1. **[Azure AD-eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)** : als u wilt dat uw gebruikers deze functie kunnen gebruiken.
2. **[Eenmalige aanmelding met LiquidFiles configureren](#configure-liquidfiles-single-sign-on)** : als u de instellingen voor eenmalige aanmelding aan de toepassingszijde wilt configureren.
3. **[Een Azure AD-testgebruiker maken](#create-an-azure-ad-test-user)** : als u Azure AD-eenmalige aanmelding wil testen met Britta Simon.
4. **[De testgebruiker van Azure AD-toewijzen](#assign-the-azure-ad-test-user)** : als u wilt dat Britta Simon gebruik kan maken van Azure AD-eenmalige aanmelding.
5. **[Een testgebruiker voor LiquidFiles maken](#create-liquidfiles-test-user)** : als u een tegenhanger van Britta Simon in LiquidFiles wilt hebben die is gekoppeld aan de Azure AD-weergave van de gebruiker.
6. **[Eenmalige aanmelding testen](#test-single-sign-on)** : als u wilt controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD configureren voor eenmalige aanmelding

In deze sectie gaat u Azure AD-eenmalige aanmelding in de Azure-portal inschakelen.

Voer de volgende stappen uit om eenmalige aanmelding van Azure AD te configureren met LiquidFiles:

1. Selecteer in de [Azure-portal](https://portal.azure.com/) op de integratiepagina van de toepassing **LiquidFiles** de optie **Eenmalige aanmelding** .

    ![Koppeling Eenmalige aanmelding configureren](common/select-sso.png)

2. In het dialoogvenster **Een methode voor eenmalige aanmelding selecteren** selecteert u de modus **SAML/WS-Federation** om eenmalige aanmelding in te schakelen.

    ![De modus Eenmalige aanmelding selecteren](common/select-saml-option.png)

3. Op de pagina **Eenmalige aanmelding met SAML instellen** klikt u op het pictogram **Bewerken** om het dialoogvenster **Standaard SAML-configuratie** te openen.

    ![Standaard SAML-configuratie bewerken](common/edit-urls.png)

4. In de sectie **Standaard SAML-configuratie** voert u de volgende stappen uit:

    ![Domein- en URL-gegevens voor eenmalige aanmelding bij LiquidFiles](common/sp-identifier-reply.png)

    a. In het tekstvak **Aanmeldings-URL** typt u een URL met de volgende notatie: `https://<YOUR_SERVER_URL>/saml/init`

    b. In het tekstvak **Id (Entiteits-id)** typt u een URL met de volgende notatie: `https://<YOUR_SERVER_URL>`

    c. In het tekstvak **Antwoord-URL** typt u een URL met behulp van het volgende patroon: `https://<YOUR_SERVER_URL>/saml/consume`

    > [!NOTE]
    > Dit zijn geen echte waarden. Werk deze waarden bij met de werkelijke aanmeldings-URL en id. Neem contact op met het [klantondersteuningsteam van LiquidFiles](https://www.liquidfiles.com/support.html) om deze waarden te verkrijgen. U kunt ook verwijzen naar het patroon dat wordt weergegeven in de sectie **Standaard SAML-configuratie** in de Azure-portal.

5. Klik in de sectie **SAML-handtekeningcertificaat** op de knop **Bewerken** om het dialoogvenster **SAML-handtekeningcertificaat** te openen.

    ![SAML-handtekeningcertificaat bewerken](common/edit-certificate.png)

6. Kopieer in de sectie **SAML-handtekeningcertificaat** de waarde voor **VINGERAFDRUK** en sla deze op de computer op.

    ![Waarde van vingerafdruk kopiëren](common/copy-thumbprint.png)

7. Kopieer in de sectie **LiquidFiles instellen** de juiste URL('s) op basis van uw behoeften.

    ![Configuratie-URL's kopiëren](common/copy-configuration-urls.png)

    a. Aanmeldings-URL

    b. Azure AD-id

    c. Afmeldings-URL

### <a name="configure-liquidfiles-single-sign-on"></a>Eenmalige aanmelding met LiquidFiles configureren

1. Meld u als beheerder aan bij de bedrijfssite van LiquidFiles.

1. Klik op **Eenmalige aanmelding** in het menu **Beheer > Configuratie** .

1. Voer op de configuratiepagina **Eenmalige aanmelding** de volgende stappen uit

    ![Eenmalige aanmelding configureren](./media/liquidfiles-tutorial/tutorial_single_01.png)

    a. Selecteer **SAML 2** als **Methode voor eenmalige aanmelding** .

    b. Plak in het tekstvak **IDP-aanmeldings-URL** de waarde van **Aanmeldings-URL** die u hebt gekopieerd in de Azure-portal.

    c. Plak in het tekstvak **IDP-afmeldings-URL** de waarde van **Afmeldings-URL** die u hebt gekopieerd in de Azure-portal.

    d. Plak in het tekstvak **Vingerafdruk van IDP-certificaat** de waarde van **VINGERAFDRUK** die u hebt gekopieerd in de Azure-portal.

    e. Typ in het tekstvak Indeling van naam-id de waarde `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.

    f. Typ in het tekstvak Authn-context de waarde `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.

    g. Klik op **Opslaan** .

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Het doel van deze sectie is om in de Azure-portal een testgebruiker met de naam Britta Simon te maken.

1. Selecteer in het linkerdeelvenster in de Azure-portal de optie **Azure Active Directory** , selecteer **Gebruikers** en selecteer vervolgens **Alle gebruikers** .

    ![De koppelingen Gebruikers en groepen en Alle gebruikers](common/users.png)

2. Selecteer **Nieuwe gebruiker** boven aan het scherm.

    ![Knop Nieuwe gebruiker](common/new-user.png)

3. In Gebruikerseigenschappen voert u de volgende stappen uit.

    ![Het dialoogvenster Gebruiker](common/user-properties.png)

    a. Voer in het veld **Naam** **Britta Simon** in.
  
    b. In het veld **Gebruikersnaam** typt u `brittasimon@yourcompanydomain.extension`. Bijvoorbeeld: BrittaSimon@contoso.com

    c. Schakel het selectievakje **Wachtwoord weergeven** in en noteer de waarde die wordt weergegeven in het vak Wachtwoord.

    d. Klik op **Create** .

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie stelt u Britta Simon in staat gebruik te maken van eenmalige aanmelding van Azure door haar toegang te verlenen tot LiquidFiles.

1. Selecteer in de Azure-portal achtereenvolgens **Bedrijfstoepassingen** , **Alle toepassingen** en **LiquidFiles** .

    ![De blade Bedrijfstoepassingen](common/enterprise-applications.png)

2. Selecteer **LiquidFiles** in de lijst met toepassingen.

    ![De koppeling naar LiquidFiles in de lijst met toepassingen](common/all-applications.png)

3. Selecteer in het menu aan de linkerkant **Gebruikers en groepen** .

    ![De koppeling Gebruikers en groepen](common/users-groups-blade.png)

4. Klik op de knop **Gebruiker toevoegen** en selecteer vervolgens **Gebruikers en groepen** in het dialoogvenster **Toewijzing toevoegen** .

    ![Het deelvenster Toewijzing toevoegen](common/add-assign-user.png)

5. Selecteer in het dialoogvenster **Gebruikers en groepen** **Britta Simon** in de lijst met gebruikers en klik op de knop **Selecteren** onder aan het scherm.

6. Als u een waarde voor een rol verwacht in de SAML-bewering, moet u in het dialoogvenster **Rol selecteren** de juiste rol voor de gebruiker in de lijst selecteren en vervolgens op de knop **Selecteren** onder aan het scherm klikken.

7. Klik in het dialoogvenster **Toewijzing toevoegen** op de knop **Toewijzen** .

### <a name="create-liquidfiles-test-user"></a>Een testgebruiker voor LiquidFiles maken

Het doel van deze sectie is om in LiquidFiles een gebruiker met de naam Britta Simon te maken. Werk samen met de LiquidFiles-serverbeheerder om uzelf als gebruiker toe te voegen voordat u zich aanmeldt bij uw LiquidFiles-toepassing.

### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie gaat u uw configuratie van Azure AD-eenmalige aanmelding testen via het toegangsvenster.

Wanneer u in het toegangsvenster op de tegel LiquidFiles klikt, wordt u automatisch aangemeld bij de instantie van LiquidFiles waarvoor u eenmalige aanmelding hebt ingesteld. Zie [Introduction to the Access Panel](../user-help/my-apps-portal-end-user-access.md) (Inleiding tot het toegangsvenster) voor meer informatie over het toegangsvenster.

## <a name="additional-resources"></a>Aanvullende resources

- [Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory](./tutorial-list.md)

- [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)

- [Wat is voorwaardelijke toegang in Azure Active Directory?](../conditional-access/overview.md)