---
title: IoT Edge versie op apparaten bijwerken-Azure IoT Edge | Microsoft Docs
description: IoT Edge apparaten bijwerken om de nieuwste versies van de Security daemon en de IoT Edge-runtime uit te voeren
keywords: ''
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 01/20/2021
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 9a739736182713b35c3a5e9e25742aa39c5d1122
ms.sourcegitcommit: 484f510bbb093e9cfca694b56622b5860ca317f7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/21/2021
ms.locfileid: "98633134"
---
# <a name="update-the-iot-edge-security-daemon-and-runtime"></a>De IoT Edge-beveiligingsdaemon en -runtime bijwerken

Wanneer de IoT Edge-service nieuwe versies uitbrengt, moet u uw IoT Edge-apparaten bijwerken voor de nieuwste functies en beveiligings verbeteringen. Dit artikel bevat informatie over het bijwerken van uw IoT Edge-apparaten wanneer een nieuwe versie beschikbaar is.

Er moeten twee onderdelen van een IoT Edge apparaat worden bijgewerkt als u wilt overstappen op een nieuwere versie. De eerste is de beveiligings-daemon die op het apparaat wordt uitgevoerd en de runtime modules start wanneer het apparaat wordt gestart. Op dit moment kan de beveiligings-daemon alleen worden bijgewerkt vanaf het apparaat zelf. Het tweede onderdeel is de runtime, bestaande uit de modules IoT Edge hub en IoT Edge agent. Afhankelijk van hoe u uw implementatie structureert, kan de runtime worden bijgewerkt vanaf het apparaat of op afstand.

Zie [Azure IOT Edge releases](https://github.com/Azure/azure-iotedge/releases)om de nieuwste versie van Azure IOT Edge te vinden.

## <a name="update-the-security-daemon"></a>De beveiligings-daemon bijwerken

De IoT Edge Security daemon is een systeem eigen onderdeel dat moet worden bijgewerkt met behulp van Package Manager op het IoT Edge-apparaat.

Controleer de versie van de beveiligings-daemon die op het apparaat wordt uitgevoerd met behulp van de opdracht `iotedge version` .

# <a name="linux"></a>[Linux](#tab/linux)

Op Linux x64-apparaten gebruikt u apt-get of uw geschikte pakket beheerder om de beveiligings-daemon bij te werken naar de meest recente versie.

De nieuwste opslagplaats configuratie ophalen van micro soft:

* **Ubuntu Server 16.04**:

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/multiarch/prod.list > ./microsoft-prod.list
   ```

* **Ubuntu Server 18.04**:

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/18.04/multiarch/prod.list > ./microsoft-prod.list
   ```

* **Raspberry Pi OS Stretch**:

   ```bash
   curl https://packages.microsoft.com/config/debian/stretch/multiarch/prod.list > ./microsoft-prod.list
   ```

Kopieer de gegenereerde lijst.

   ```bash
   sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
   ```

Installeer de open bare sleutel van micro soft GPG.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
   ```

Apt bijwerken.

   ```bash
   sudo apt-get update
   ```

Controleer welke versies van IoT Edge beschikbaar zijn.

   ```bash
   apt list -a iotedge
   ```

Als u wilt bijwerken naar de meest recente versie van de beveiligings-daemon, gebruikt u de volgende opdracht waarmee u ook **libiothsm-STD** kunt bijwerken naar de nieuwste versie:

   ```bash
   sudo apt-get install iotedge
   ```

Als u wilt bijwerken naar een specifieke versie van de beveiligings-daemon, geeft u de versie op uit de apt-lijst uitvoer. Wanneer **iotedge** wordt bijgewerkt, wordt automatisch geprobeerd het **libiothsm-standaard** pakket bij te werken naar de meest recente versie, wat een conflict met de afhankelijkheid kan veroorzaken. Als u niet naar de meest recente versie gaat, moet u ervoor zorgen dat beide pakketten voor dezelfde versie worden doel. Met de volgende opdracht wordt bijvoorbeeld een specifieke versie van de 1.0.9-release geïnstalleerd:

   ```bash
   sudo apt-get install iotedge=1.0.9-1 libiothsm-std=1.0.9-1
   ```

Als de versie die u wilt installeren niet beschikbaar is via apt-get, kunt u krul gebruiken om een wille keurige versie te richten op basis van de opslag plaats [IOT Edge releases](https://github.com/Azure/azure-iotedge/releases) . Voor de versie die u wilt installeren, zoekt u de juiste **libiothsm-STD-** en **iotedge** -bestanden voor uw apparaat. Voor elk bestand klikt u met de rechter muisknop op de bestands koppeling en kopieert u het koppelings adres. Gebruik het koppelings adres om de specifieke versies van die onderdelen te installeren:

```bash
curl -L <libiothsm-std link> -o libiothsm-std.deb && sudo dpkg -i ./libiothsm-std.deb
curl -L <iotedge link> -o iotedge.deb && sudo dpkg -i ./iotedge.deb
```

# <a name="windows"></a>[Windows](#tab/windows)

<!-- 1.0.10 -->
::: moniker range="iotedge-2018-06"

Met IoT Edge voor Linux op Windows wordt IoT Edge uitgevoerd in een virtuele Linux-machine die wordt gehost op een Windows-apparaat. Deze virtuele machine is vooraf geïnstalleerd met IoT Edge en wordt beheerd met Microsoft Update om de onderdelen up-to-date te houden. Er zijn momenteel geen updates beschikbaar.

::: moniker-end

Met IoT Edge voor Windows wordt IoT Edge rechtstreeks uitgevoerd op het Windows-apparaat. Zie [Azure IOT Edge voor Windows installeren en beheren](how-to-install-iot-edge-windows-on-windows.md)voor instructies voor het bijwerken van Power shell-scripts.

---

## <a name="update-the-runtime-containers"></a>De runtime-containers bijwerken

De manier waarop u de IoT Edge agent-en IoT Edge hub-containers bijwerkt, is afhankelijk van of u rollende Tags (zoals 1,0) of specifieke tags (zoals 1.0.7) gebruikt in uw implementatie.

Controleer de versie van de IoT Edge agent en IoT Edge hub-modules op uw apparaat met behulp van de opdrachten `iotedge logs edgeAgent` of `iotedge logs edgeHub` .

  ![Container versie zoeken in Logboeken](./media/how-to-update-iot-edge/container-version.png)

### <a name="understand-iot-edge-tags"></a>IoT Edge Tags begrijpen

De installatie kopieën van IoT Edge agent en IoT Edge hub worden gelabeld met de IoT Edge-versie waaraan ze zijn gekoppeld. Er zijn twee verschillende manieren om labels te gebruiken met de runtime-installatie kopieën:

* **Roulerende Tags** : gebruik alleen de eerste twee waarden van het versie nummer om de meest recente afbeelding op te halen die overeenkomt met die cijfers. Bijvoorbeeld: 1,0 wordt bijgewerkt wanneer er een nieuwe versie is die naar de nieuwste versie van 1.0. x wijst. Als de container-runtime op uw IoT Edge-apparaat de installatie kopie opnieuw ophaalt, worden de runtime modules bijgewerkt naar de meest recente versie. Deze aanpak wordt aanbevolen voor ontwikkelings doeleinden. Implementaties van de Azure Portal standaard naar roulerende Tags.

* **Specifieke labels** : gebruik alle drie de waarden van het versie nummer om de installatie kopie versie expliciet in te stellen. 1.0.7 wordt bijvoorbeeld niet gewijzigd na de eerste release. Wanneer u klaar bent om bij te werken, kunt u een nieuw versie nummer declareren in het implementatie manifest. Deze aanpak wordt voorgesteld voor productie doeleinden.

### <a name="update-a-rolling-tag-image"></a>Een afbeelding van een roulerende tag bijwerken

Als u roulerende Tags in uw implementatie gebruikt (bijvoorbeeld mcr.microsoft.com/azureiotedge-hub:**1,0**), moet u de container runtime op het apparaat afdwingen om de nieuwste versie van de installatie kopie te halen.

De lokale versie van de installatie kopie verwijderen van uw IoT Edge-apparaat. Op Windows-computers verwijdert het verwijderen van de Security daemon ook de runtime-installatie kopieën. u hoeft deze stap dus niet opnieuw uit te voeren.

```bash
docker rmi mcr.microsoft.com/azureiotedge-hub:1.0
docker rmi mcr.microsoft.com/azureiotedge-agent:1.0
```

Mogelijk moet u de vlag Force gebruiken `-f` om de installatie kopieën te verwijderen.

De IoT Edge-service haalt de nieuwste versies van de runtime-installatie kopieën op en start deze automatisch opnieuw op het apparaat.

### <a name="update-a-specific-tag-image"></a>Een specifieke tag-afbeelding bijwerken

Als u specifieke tags in uw implementatie gebruikt (bijvoorbeeld mcr.microsoft.com/azureiotedge-hub:**1.0.8**), hoeft u alleen de tag in het implementatie manifest bij te werken en de wijzigingen toe te passen op uw apparaat.

1. Selecteer uw IoT Edge apparaat in de IoT Hub in het Azure Portal en selecteer **modules instellen**.

1. Selecteer in de sectie **IOT Edge modules** **runtime-instellingen**.

   ![Runtime-instellingen configureren](./media/how-to-update-iot-edge/configure-runtime.png)

1. Werk in **runtime-instellingen** de **afbeeldings** waarde voor **Edge hub** bij met de gewenste versie. Selecteer nog niet **Opslaan** .

   ![Versie van Edge hub-installatie kopie bijwerken](./media/how-to-update-iot-edge/runtime-settings-edgehub.png)

1. Vouw de **hub** -instellingen van de Edge samen of schuif omlaag en werk de **afbeeldings** waarde voor de **rand agent** bij met dezelfde versie.

   ![Versie van de Edge hub-agent bijwerken](./media/how-to-update-iot-edge/runtime-settings-edgeagent.png)

1. Selecteer **Opslaan**.

1. Selecteer **controleren + maken**, Controleer de implementatie en selecteer **maken**.

## <a name="update-to-a-release-candidate-version"></a>Bijwerken naar een release Candi date-versie

Azure IoT Edge brengt regel matig nieuwe versies van de IoT Edge service uit. Voor elke stabiele versie zijn er een of meer release Candi date (RC)-versies. RC-versies bevatten alle geplande functies voor de release, maar zijn nog steeds bezig met testen en valideren. Als u een nieuwe functie vroegtijdig wilt testen, kunt u een RC-versie installeren en feedback geven via GitHub.

Release Candi date-versies volgen dezelfde Nummerings Conventie voor releases, maar hebben wel **-RC** plus een incrementeel nummer toegevoegd aan het einde. U kunt de release kandidaten in dezelfde lijst met [Azure IOT Edge releases](https://github.com/Azure/azure-iotedge/releases) zien als de stabiele versies. Zoek bijvoorbeeld naar **1.0.9-RC5** en **1.0.9-RC6**, twee van de release kandidaten die werden ontvangen vóór **1.0.9**. U kunt ook zien dat RC-versies zijn gemarkeerd met **voorlopige** labels.

De IoT Edge-agent-en-hub-modules hebben RC-versies die zijn gelabeld met dezelfde Conventie. Bijvoorbeeld **MCR.Microsoft.com/azureiotedge-hub:1.0.9-RC6**.

Als previews worden versies van release Candi date niet opgenomen als de meest recente versie die de reguliere installatie Programma's doel. In plaats daarvan moet u hand matig de assets richten voor de RC-versie die u wilt testen. Het installeren of bijwerken van een RC-versie is in het algemeen hetzelfde als het richten op een andere specifieke versie van IoT Edge.

Gebruik de secties in dit artikel voor meer informatie over het bijwerken van een IoT Edge apparaat naar een specifieke versie van de Security daemon of runtime-modules.

Als u IoT Edge installeert in plaats van een bestaande installatie te upgraden, gebruikt u de stappen in de [installatie van offline of specifieke versie](how-to-install-iot-edge.md#offline-or-specific-version-installation-optional).

## <a name="next-steps"></a>Volgende stappen

Bekijk de nieuwste [Azure IOT Edge releases](https://github.com/Azure/azure-iotedge/releases).

Blijf up-to-date met recente updates en aankondigingen in het [Internet of Things blog](https://azure.microsoft.com/blog/topics/internet-of-things/)