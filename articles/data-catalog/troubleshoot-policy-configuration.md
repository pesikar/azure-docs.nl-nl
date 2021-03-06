---
title: Problemen oplossen Azure Data Catalog
description: In dit artikel worden veelvoorkomende problemen met het oplossen van Azure Data Catalog resources beschreven.
author: JasonWHowell
ms.author: jasonh
ms.service: data-catalog
ms.topic: troubleshooting
ms.date: 08/01/2019
ms.openlocfilehash: 84bd14f8ae18527b4f6e9d8509a12555baec8771
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "68879541"
---
# <a name="troubleshooting-azure-data-catalog"></a>Problemen met Azure Data Catalog oplossen

In dit artikel worden veelvoorkomende problemen met het oplossen van Azure Data Catalog resources beschreven. 

## <a name="functionality-limitations"></a>Functionaliteits beperkingen

Bij het gebruik van Azure Data Catalog is de volgende functionaliteit beperkt:

- Accounts met de **rol gast** worden niet ondersteund. U kunt geen gast accounts toevoegen als gebruikers van Azure Data Catalog en gast gebruikers kunnen de portal niet gebruiken in [https://www.azuredatacatalog.com](https://www.azuredatacatalog.com) .

- Het maken van Azure Data Catalog-resources met behulp van Azure Resource Manager sjablonen of Azure PowerShell opdrachten worden niet ondersteund.

- De Azure Data Catalog resource kan niet worden verplaatst tussen Azure-tenants.

## <a name="azure-active-directory-policy-configuration"></a>Azure Active Directory-beleid configureren

Het kan voorkomen dat u zich wel kunt aanmelden bij de Azure Data Catalog-portal, maar niet bij het hulpprogramma voor gegevensbronregistratie. Er wordt dan een foutmelding weergegeven. Deze fout kan optreden als u zich op het bedrijfs netwerk bevindt of wanneer u een verbinding maakt van buiten het bedrijfs netwerk.

Het registratiehulpprogramma maakt gebruik van *formulierverificatie* om de gebruikersaanmeldingen te valideren bij Azure Active Directory. Als u zich wilt aanmelden, moet een Azure Active Directory-beheerder formulierverificatie inschakelen in het *algemene verificatiebeleid*.

Met het algemene verificatiebeleid kunt u afzonderlijke verificatie voor intranet- en extranetverbindingen inschakelen, zoals wordt weergegeven in de volgende afbeelding. Er kunnen zich aanmeldings fouten voordoen als formulier verificatie niet is ingeschakeld voor het netwerk van waaruit u verbinding maakt.

 ![Het algemene verificatiebeleid van Azure Active Directory](./media/troubleshoot-policy-configuration/global-auth-policy.png)

Zie [Verificatiebeleid configureren](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486781(v=ws.11)) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

* [Een Azure Data Catalog maken](data-catalog-get-started.md)
