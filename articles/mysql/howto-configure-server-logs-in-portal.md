---
title: Toegang tot langzame query logboeken-Azure Portal-Azure Database for MySQL
description: In dit artikel wordt beschreven hoe u de langzame Logboeken in Azure Database for MySQL kunt configureren en openen vanuit de Azure Portal.
author: savjani
ms.author: pariks
ms.service: mysql
ms.topic: how-to
ms.date: 4/13/2020
ms.openlocfilehash: 5ad4ffa99a7af592e3e93e53673d254956807c40
ms.sourcegitcommit: 6ab718e1be2767db2605eeebe974ee9e2c07022b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/12/2020
ms.locfileid: "94541620"
---
# <a name="configure-and-access-slow-query-logs-from-the-azure-portal"></a>Langzame query logboeken van de Azure Portal configureren en openen

U kunt de [Azure database for MySQL langzame query logboeken](concepts-server-logs.md) configureren, weer geven en downloaden vanuit de Azure Portal.

## <a name="prerequisites"></a>Vereisten
Voor de stappen in dit artikel moet [Azure database for mysql server](quickstart-create-mysql-server-database-using-azure-portal.md)zijn geïnstalleerd.

## <a name="configure-logging"></a>Logboek registratie configureren
Configureer de toegang tot het MySQL-logboek voor langzame query's. 

1. Meld u aan bij de [Azure-portal](https://portal.azure.com/).

2. Selecteer uw Azure Database for MySQL-server.

3. Selecteer in de sectie **bewaking** in de zijbalk **Server logboeken**. 
   :::image type="content" source="./media/howto-configure-server-logs-in-portal/1-select-server-logs-configure.png" alt-text="Scherm opname van opties voor Server logboeken":::

4. Selecteer om de server parameters weer te geven de optie **Klik hier om Logboeken in te scha kelen en logboek parameters te configureren**.

5. Schakel **slow_query_log** in **op** aan.

6. Selecteer waar u de logboeken wilt uitvoeren met **log_output**. Selecteer **bestand** om logboeken naar zowel lokale opslag als Azure monitor Diagnostische logboeken te verzenden. 

7. Wijzig alle andere para meters die nodig zijn. 

8. Selecteer **Opslaan**. 

   :::image type="content" source="./media/howto-configure-server-logs-in-portal/3-save-discard.png" alt-text="Scherm opname van langzame query logboek parameters en opslaan.":::

Op de pagina **server parameters** kunt u teruggaan naar de lijst met Logboeken door de pagina te sluiten.

## <a name="view-list-and-download-logs"></a>Lijst weer geven en logboeken downloaden
Nadat de logboek registratie is gestart, kunt u een lijst met beschik bare langzame query logboeken bekijken en afzonderlijke logboek bestanden downloaden.

1. Open Azure Portal.

2. Selecteer uw Azure Database for MySQL-server.

3. Selecteer in de sectie **bewaking** in de zijbalk **Server logboeken**. Op de pagina wordt een lijst met uw logboek bestanden weer gegeven.

   :::image type="content" source="./media/howto-configure-server-logs-in-portal/4-server-logs-list.png" alt-text="Scherm opname van de pagina Server logboeken, met de lijst met gemarkeerde logboeken":::

   > [!TIP]
   > De naam Conventie van het logboek is **mysql-slow < uw server name>-yyyymmddhh. log**. De datum en tijd die in de bestands naam wordt gebruikt, is het tijdstip waarop het logboek is uitgegeven. Logboek bestanden worden elke 24 uur of 7,5 GB gedraaid, afhankelijk van wat het eerste komt. 

4. Gebruik, indien nodig, het zoekvak om snel naar een specifiek logboek te beperken, op basis van datum en tijd. De zoek opdracht bevindt zich op de naam van het logboek.

5. Als u afzonderlijke logboek bestanden wilt downloaden, selecteert u het pictogram met de pijl-omlaag naast elk logboek bestand in de tabelrij.

   :::image type="content" source="./media/howto-configure-server-logs-in-portal/5-download.png" alt-text="Scherm opname van de pagina Server logboeken, met pictogram met de pijl-omlaag gemarkeerd":::

## <a name="set-up-diagnostic-logs"></a>Diagnostische logboeken instellen

1. Selecteer in de sectie **bewaking** van de zijbalk **Diagnostische instellingen**  >  **Diagnostische instellingen toevoegen**.

   :::image type="content" source="./media/howto-configure-server-logs-in-portal/add-diagnostic-setting.png" alt-text="Scherm opname van opties voor Diagnostische instellingen":::

1. Geef een naam op voor de diagnostische instelling.

1. Geef op welke gegevens worden gesinkt om de langzame query Logboeken (opslag account, Event Hub of Log Analytics-werk ruimte) te verzenden.

1. Selecteer **MySqlSlowLogs** als het logboek type.
:::image type="content" source="./media/howto-configure-server-logs-in-portal/configure-diagnostic-setting.png" alt-text="Scherm opname van configuratie opties voor Diagnostische instellingen":::

1. Nadat u de gegevens sinks hebt geconfigureerd om de langzame query logboeken te pipeen, selecteert u **Opslaan**.
:::image type="content" source="./media/howto-configure-server-logs-in-portal/save-diagnostic-setting.png" alt-text="Scherm opname van configuratie opties voor Diagnostische instellingen, met de markering opgeslagen":::

1. Open de logboeken voor trage query's door ze te verkennen in de gegevens-sinks die u hebt geconfigureerd. Het kan tot tien minuten duren voordat de logboeken worden weer gegeven.

## <a name="next-steps"></a>Volgende stappen
- Zie [langzame query Logboeken openen in cli](howto-configure-server-logs-in-cli.md) voor meer informatie over het downloaden van langzame query logboeken via een programma.
- Meer informatie over [trage query-logboeken](concepts-server-logs.md) in azure database for MySQL.
- Zie de MySQL-documentatie over [Logboeken](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html)voor meer informatie over de parameter definities en MySQL-logboek registratie.