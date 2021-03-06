---
title: Web-app verplaatsen waarmee gebruikers zich aanmelden bij productie | Azure
titleSuffix: Microsoft identity platform
description: Meer informatie over het bouwen van een web-app die wordt aangemeld bij gebruikers (verplaatsen naar productie)
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 09/17/2019
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c7abad31c9936729b8d9c19ed2efcb841ac103ca
ms.sourcegitcommit: 5cdd0b378d6377b98af71ec8e886098a504f7c33
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/25/2021
ms.locfileid: "98756234"
---
# <a name="web-app-that-signs-in-users-move-to-production"></a>Web-app die zich aanmeldt bij gebruikers: verplaatsen naar productie

Nu u weet hoe u een token kunt ophalen om Web-Api's aan te roepen, lees dan hoe u het kunt verplaatsen naar productie.

[!INCLUDE [Move to production common steps](../../../includes/active-directory-develop-scenarios-production.md)]

## <a name="troubleshooting"></a>Probleemoplossing

> [!NOTE]
> Wanneer gebruikers zich voor de eerste keer aanmelden bij de webtoepassing, moeten ze toestemming geven. In sommige organisaties kunnen gebruikers echter een bericht zien als het volgende:
>
> *AppName heeft machtigingen nodig voor toegang tot resources in uw organisatie die alleen door een beheerder kunnen worden verleend. Vraag een beheerder om toestemming te verlenen voor deze app voordat u deze kunt gebruiken.*
>
> Dit komt doordat de Tenant beheerder de mogelijkheid voor gebruikers om toestemming heeft **uitgeschakeld** . In dat geval moet u contact opnemen met de Tenant beheerders zodat ze een beheerders toestemming voor de door de toepassing vereiste bereiken hebben.

## <a name="same-site"></a>Dezelfde site

Zorg ervoor dat u mogelijke problemen kent met nieuwe versies van de Chrome-browser: [SameSite cookie wijzigingen in de Chrome-browser verwerken](howto-handle-samesite-cookie-changes-chrome-browser.md).

Het NuGet-pakket micro soft. Identity. Web verwerkt de meest voorkomende SameSite-problemen.

## <a name="deep-dive-aspnet-core-web-app-tutorial"></a>Grondige kennis: zelf studie voor ASP.NET Core web-app

Meer informatie over andere manieren om gebruikers aan te melden bij deze ASP.NET Core-zelf studie: 

[Uw web-apps inschakelen voor het aanmelden van gebruikers en het aanroepen van Api's met het micro soft-identiteits platform voor ontwikkel aars](https://github.com/Azure-Samples/ms-identity-aspnetcore-webapp-tutorial)

Deze progressieve zelf studie heeft productie-gereed code voor een web-app, waaronder het toevoegen van een aanmelding met accounts in:

- Uw organisatie
- Meerdere organisaties
- Werk-of school accounts of persoonlijke micro soft-accounts
- [Azure AD B2C](../../active-directory-b2c/overview.md)
- Nationale clouds

## <a name="sample-code-java-web-app"></a>Voorbeeld code: Java-Web-app

Meer informatie over de Java-Web-app in dit voor beeld op GitHub: 

[Een Java-webtoepassing die zich aanmeldt bij gebruikers met het micro soft-identiteits platform en aanroepen Microsoft Graph](https://github.com/Azure-Samples/ms-identity-java-webapp)

## <a name="next-steps"></a>Volgende stappen

Nadat uw web-app zich heeft aangemeld bij gebruikers, kan deze web-Api's namens de aangemelde gebruikers aanroepen. Het aanroepen van web-Api's vanuit de web-app is het object van het volgende scenario: [Web-app die web-api's aanroept](scenario-web-app-call-api-overview.md).