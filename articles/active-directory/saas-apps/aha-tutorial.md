---
title: 'Zelfstudie: Azure Active Directory-integratie met Aha! | Microsoft Docs'
description: Ontdek hoe u eenmalige aanmelding configureert tussen Azure Active Directory en Aha!
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/09/2019
ms.author: jeedes
ms.openlocfilehash: 82f3a2dc7f43bd484d6a81efaa8d07f13b746d9e
ms.sourcegitcommit: d79513b2589a62c52bddd9c7bd0b4d6498805dbe
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97671060"
---
# <a name="tutorial-integrate-aha-with-azure-active-directory"></a>Zelfstudie: Aha! integreren met Azure Active Directory

In deze zelfstudie leert u hoe u Aha! integreert met Azure Active Directory (Azure AD). Wanneer u Aha! integreert met Azure AD, kunt u het volgende doen:

* In Azure AD beheren wie er toegang heeft tot Aha!.
* Instellen dat uw gebruikers automatisch worden aangemeld bij Aha! met hun Azure AD-accounts.
* Uw accounts op een centrale locatie beheren: Azure Portal.

Zie [Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?](../manage-apps/what-is-single-sign-on.md) voor meer informatie over de integratie van SaaS-apps met Azure AD.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om aan de slag te gaan:

* Een Azure AD-abonnement Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Aha! een abonnement waarvoor eenmalige aanmelding (SSO) is ingeschakeld.

> [!NOTE]
> Deze integratie is ook beschikbaar voor gebruik vanuit de Azure AD US Government Cloud-omgeving. U kunt deze toepassing vinden in de toepassingsgalerie van Azure AD US Government Cloud en deze op dezelfde manier configureren als vanuit een openbare cloud.

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie gaat u in een testomgeving eenmalige aanmelding van Azure AD configureren en testen.

* Aha! ondersteunt door **SP** geïnitieerde eenmalige aanmelding
* Aha! ondersteunt het **Just-In-Time** inrichten van gebruikers

## <a name="adding-aha-from-the-gallery"></a>Aha! toevoegen vanuit de galerie

Om de integratie van Aha! te configureren in Azure AD, moet u Aha! vanuit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

1. Meld u bij de [Azure-portal](https://portal.azure.com) aan met een werk- of schoolaccount of een persoonlijk Microsoft-account.
1. Selecteer in het linkernavigatiedeelvenster de service **Azure Active Directory**.
1. Ga naar **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Nieuwe toepassing** om een nieuwe toepassing toe te voegen.
1. In de sectie **Toevoegen uit de galerie** typt u **Aha!** in het zoekvak.
1. Selecteer **Aha!** in het resultatenvenster en voeg vervolgens de app toe. Wacht enkele seconden tot de app is toegevoegd aan de tenant.

## <a name="configure-and-test-azure-ad-single-sign-on-for-aha"></a>Eenmalige aanmelding van Azure AD configureren en testen voor Aha!

Eenmalige aanmelding van Azure AD met Aha! configureren en testen met behulp van een testgebruiker met de naam **B.Simon**. Eenmalige aanmelding werkt alleen als u een koppelingsrelatie tot stand brengt tussen een Azure AD-gebruiker en de bijbehorende gebruiker in Aha!.

Voltooi de volgende stappen om eenmalige aanmelding van Azure AD met Aha! te configureren en te testen:

1. **[Eenmalige aanmelding van Azure AD configureren](#configure-azure-ad-sso)** : zodat uw gebruikers deze functie kunnen gebruiken.
    1. **[Een Azure AD-testgebruiker maken](#create-an-azure-ad-test-user)** : om eenmalige aanmelding van Azure AD te testen met B.Simon.
    1. **[De Azure AD-testgebruiker toewijzen](#assign-the-azure-ad-test-user)** zodat B.Simon eenmalige aanmelding van Azure AD kan gebruiken.
2. **[Aha! configureren Eenmalige aanmelding](#configure-aha-sso)** : om de instellingen voor eenmalige aanmelding aan de toepassingszijde te configureren.
    1. **[Testgebruiker voor Aha! maken](#create-aha-test-user)** : als u een tegenhanger van B.Simon in Aha! wilt hebben die is gekoppeld aan de weergave van de gebruiker in Azure AD.
3. **[Eenmalige aanmelding testen](#test-sso)** : om te controleren of de configuratie werkt.

## <a name="configure-azure-ad-sso"></a>Eenmalige aanmelding van Azure AD configureren

Volg deze stappen om eenmalige aanmelding van Azure AD in te schakelen in Azure Portal.

1. In de [Azure-portal](https://portal.azure.com/) selecteert u op de pagina van toepassingsintegratie van **Aha!** de sectie **Beheren** en selecteert u **Eenmalige aanmelding**.
1. Selecteer **SAML** op de pagina **Selecteer een methode voor eenmalige aanmelding**.
1. Op de pagina **Eenmalige aanmelding instellen met SAML** klikt u op het bewerkings-/penpictogram voor **Standaard-SAML-configuratie** om de instellingen te bewerken.

    ![Standaard SAML-configuratie bewerken](common/edit-urls.png)

1. In de sectie **Standaard SAML-configuratie** voert u de volgende stappen uit:

    a. In het tekstvak **Aanmeldings-URL** typt u een URL met de volgende notatie: `https://<companyname>.aha.io/session/new`

    b. In het tekstvak **Id (Entiteits-id)** typt u een URL met de volgende notatie: `https://<companyname>.aha.io`

    > [!NOTE]
    > Dit zijn geen echte waarden. Werk deze waarden bij met de werkelijke aanmeldings-URL en id. Neem contact op met het [Aha! -ondersteuningsteam](https://www.aha.io/company/contact) om deze waarden te verkrijgen. U kunt ook verwijzen naar het patroon dat wordt weergegeven in de sectie **Standaard SAML-configuratie** in de Azure-portal.

4. Ga op de pagina **Eenmalige aanmelding met SAML instellen** in de sectie **SAML-handtekeningcertificaat** naar **XML-bestand met federatieve metagegevens** en selecteer **Downloaden** om het certificaat te downloaden. Sla dit vervolgens op de computer op.

    ![De link om het certificaat te downloaden](common/metadataxml.png)

6. Kopieer in het gedeelte **Aha! instellen.** de juiste URL('s) op basis van uw behoeften.

    ![Configuratie-URL's kopiëren](common/copy-configuration-urls.png)

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

In deze sectie geeft u B.Simon toestemming om eenmalige aanmelding van Azure te gebruiken door toegang te verlenen tot Aha!.

1. Selecteer in Azure Portal de optie **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Aha!** in de lijst met toepassingen.
1. Zoek op de overzichtspagina van de app de sectie **Beheren** en selecteer **Gebruikers en groepen**.

    ![De koppeling Gebruikers en groepen](common/users-groups-blade.png)

1. Selecteer **Gebruiker toevoegen** en selecteer vervolgens **Gebruikers en groepen** in het dialoogvenster **Toewijzing toevoegen**.

    ![De koppeling Gebruiker toevoegen](common/add-assign-user.png)

1. Selecteer in het dialoogvenster **Gebruikers en groepen** de optie **B.Simon** in de lijst Gebruikers. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Als u een waarde voor een rol verwacht in de SAML-assertie, moet u in het dialoogvenster **Rol selecteren** de juiste rol voor de gebruiker in de lijst selecteren. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Klik in het dialoogvenster **Toewijzing toevoegen** op de knop **Toewijzen**.

## <a name="configure-aha-sso"></a>Aha! configureren Eenmalige aanmelding

1. Als u de configuratie in Aha! wilt automatiseren, moet u **My Apps-browserextensie voor veilig aanmelden** installeren door op **De extensie installeren** te klikken.

    ![Uitbreiding van Mijn apps](common/install-myappssecure-extension.png)

2. Nadat u de extensie aan de browser hebt toegevoegd, klikt u op **Aha! instellen** en wordt u naar de toepassing Aha! omgeleid. Geef hier de Administrator-referenties op om u aan te melden bij Aha!. In de browserextensie wordt de toepassing automatisch voor u geconfigureerd en worden stappen 3 t/m 8 geautomatiseerd.

    ![Instelling configureren](common/setup-sso.png)

3. Als u Aha! handmatig wilt instellen, opent u een nieuw webbrowservenster, meldt u zich aan als beheerder aan bij uw bedrijfssite in Aha! en voert u de volgende stappen uit:

4. Klik in het menu aan de bovenkant op **Settings**.

    ![Instellingen](./media/aha-tutorial/IC798950.png "Instellingen")

5. Klik op **Account**.

    ![Profiel](./media/aha-tutorial/IC798951.png "Profiel")

6. Klik op **Security and single sign-on**.

    ![Schermopname waarin de menu-optie Security and single sign-on is gemarkeerd.](./media/aha-tutorial/IC798952.png "Security and single sign-on")

7. Ga naar de sectie **Single Sign-On** en selecteer als **Identity Provider** de optie **SAML2.0**.

    ![Security and single sign-on](./media/aha-tutorial/IC798953.png "Security and single sign-on")

8. Voer op de configuratiepagina **Single Sign-On** de volgende stappen uit:

    ![Single Sign-On](./media/aha-tutorial/IC798954.png "Eenmalige aanmelding")

    a. Typ in het tekstvak **Name** een naam voor de configuratie.

    b. Selecteer voor **Configure using** de optie **Metadata File**.

    c. Klik op **Browse** om het gedownloade metagegevensbestand te uploaden.

    d. Klik op **Update**.

### <a name="create-aha-test-user"></a>Testgebruiker voor Aha! maken

In deze sectie wordt een gebruiker met de naam B.Simon gemaakt in Aha!. Aha! biedt ondersteuning voor Just-In-Time-inrichting van gebruikers. Deze functie is standaard ingeschakeld. Er is geen actie-item voor u in deze sectie. Als er nog geen gebruiker in Aha! bestaat, wordt er een nieuwe gemaakt nadat deze is geverifieerd.

## <a name="test-sso"></a>Eenmalige aanmelding testen 

In deze sectie gaat u uw configuratie van Azure AD-eenmalige aanmelding testen via het toegangsvenster.

Wanneer u op de tegel Aha! in het toegangsvenster klikt, wordt u automatisch aangemeld bij de instantie van Aha! waarvoor u eenmalige aanmelding hebt ingesteld. Zie [Introduction to the Access Panel](../user-help/my-apps-portal-end-user-access.md) (Inleiding tot het toegangsvenster) voor meer informatie over het toegangsvenster.

## <a name="additional-resources"></a>Aanvullende resources

- [Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory](./tutorial-list.md)

- [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)

- [Wat is voorwaardelijke toegang in Azure Active Directory?](../conditional-access/overview.md)