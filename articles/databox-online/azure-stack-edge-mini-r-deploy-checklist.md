---
title: Controle lijst voor implementaties voor het implementeren van Azure Stack Edge mini-R-apparaat
description: In dit artikel worden de gegevens beschreven die kunnen worden verzameld voordat u uw Azure Stack Edge mini-R-apparaat implementeert.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: article
ms.date: 10/20/2020
ms.author: alkohli
ms.openlocfilehash: 8bb07827d26efce3ab3454f370afb116ba13eb19
ms.sourcegitcommit: 5b93010b69895f146b5afd637a42f17d780c165b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96533805"
---
# <a name="deployment-checklist-for-your-azure-stack-edge-mini-r-device"></a>Controle lijst voor implementaties voor uw Azure Stack Edge mini-R-apparaat  

In dit artikel wordt beschreven welke informatie kan worden verzameld vóór de werkelijke implementatie van uw Azure Stack Edge mini-R-apparaat. 

Gebruik de volgende controle lijst om ervoor te zorgen dat u deze informatie hebt nadat u een bestelling hebt geplaatst voor een Azure Stack Edge mini-R-apparaat en voordat u het apparaat hebt ontvangen. 

## <a name="deployment-checklist"></a>Controle lijst voor implementatie 

| Fase                             | Parameter                                                                                                                                                                                                                           | Details                                                                                                           |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Apparaatbeheer               | <li>Azure-abonnement</li><li>Geregistreerde resource providers</li><li>Azure Storage-account</li>|<li>Ingeschakeld voor Azure Stack Edge mini maal R/Data Box Gateway, toegang voor eigenaar of Inzender.</li><li>Ga in Azure Portal naar **Home >-abonnementen > uw-abonnement > resource providers**. Zoeken `Microsoft.DataBoxEdge` en registreren. Herhaal dit voor `Microsoft.Devices` Als u IOT-workloads implementeert.</li><li>Toegangs referenties vereist</li> |
| Installatie van apparaat               | Energie kabels in het pakket. <br>Voor ons werd een SVE 18/3-kabel met een nominale ingang van 125 V en 15 ampère met een NEMA 5-15P naar C13 (input to output) verzonden. | Zie de lijst met [ondersteunde stroom kabels per land](azure-stack-edge-technical-specifications-power-cords-regional.md) voor meer informatie.  |
|                                   | <li>Ten minste 1 X 1-GbE RJ-45-netwerk kabel voor poort 1  </li><li> Ten minste 1 X 25 GbE SFP + koper kabel voor poort 3, poort 4, poort 5 of poort 6</li>| De klant moet deze kabels aanschaffen.<br>Voor een volledige lijst met ondersteunde netwerk kabels, switches en transceivers voor netwerk kaarten van apparaten, Zie [Cavium FastlinQ 41000 Series](https://www.marvell.com/documents/xalflardzafh32cfvi0z/) , en [Mellanox Dual Port 25g connectx-4 kanaal netwerk adapter compatibele producten](https://docs.mellanox.com/display/ConnectX4LxFirmwarev14271016/Firmware+Compatible+Products).| 
| Eerste keer dat het apparaat is verbonden      | <li>Laptop waarvan de IPv4-instellingen kunnen worden gewijzigd. Deze laptop maakt verbinding met poort 1 via een switch of een USB-naar-Ethernet-adapter.  </li><!--<li> A minimum of 1 GbE switch must be used for the device once the initial setup is complete. The local web UI will not be accessible if the connected switch is not at least 1 Gbe.</li>-->|   |
| Aanmelden met apparaat                      | Het beheerders wachtwoord voor het apparaat, tussen 8 en 16 tekens en bevat drie van de volgende tekens: hoofd letters, kleine letters, cijfers en speciale tekst.                                            | Het standaard wachtwoord is *Wachtwoord1* die verloopt bij de eerste aanmelding.                                                     |
| Netwerkinstellingen                  | Het apparaat wordt geleverd met 2 x 1 GbE, 4 x 25 GbE-netwerk poorten. <li>Poort 1 wordt alleen gebruikt voor het configureren van beheer instellingen. Een of meer gegevens poorten kunnen worden verbonden en geconfigureerd. </li><li> Ten minste één gegevens netwerk interface van poort 2-poort 6 moet worden verbonden met internet (met verbinding met Azure).</li><li> DHCP en statische IPv4-configuratie ondersteund. | Voor de statische IPv4-configuratie zijn IP-, DNS-server en standaard gateway vereist.   |
| Berekenings netwerk instellingen     | <li>2 vrije, statische, aaneengesloten IP-adressen vereisen voor Kubernetes-knoop punten en 1 statisch IP-adres voor IoT Edge service.</li><li>Een extra IP-adres vereisen voor elke extra service of module die u gaat implementeren.</li>| Alleen statische IPv4-configuratie wordt ondersteund.|
| Beschrijving Webproxy-instellingen     | <li>IP/FQDN-naam van webproxyserver, poort </li><li>Gebruikers naam webproxy, wacht woord</li> | De webproxy wordt niet ondersteund bij de instellingen voor de berekening. |
| Firewall-en poort instellingen        | Als u een firewall gebruikt, moet u ervoor zorgen dat de [url's en poorten](azure-stack-edge-system-requirements.md#networking-port-requirements) van de lijst worden toegestaan voor ip's van het apparaat. |  |
| Aanbevelingen Tijd instellingen       | Configureer tijd zone, primaire NTP-server, secundaire NTP-server. | Configureer de primaire en secundaire NTP-server in het lokale netwerk.<br>Als de lokale server niet beschikbaar is, kunnen open bare NTP-servers worden geconfigureerd.                                                    |
| Beschrijving Server instellingen bijwerken | <li>Het IP-adres van de update server vereisen op het lokale netwerk, het pad naar de WSUS-server. </li> | Standaard wordt de open bare Windows Update-Server gebruikt.|
| Apparaatinstellingen | <li>Fully Qualified Domain Name van apparaat (FQDN) </li><li>DNS-domein</li> | |
| Beschrijving Bewijzen  | Gebruik de [optie certificaten genereren](azure-stack-edge-gpu-deploy-configure-certificates.md#generate-device-certificates) om niet-productiewerk belastingen te testen <br><br> Als u uw eigen certificaten hebt, inclusief de ondertekeningsketen(s), kunt u [Certificaten toevoegen](azure-stack-edge-gpu-deploy-configure-certificates.md#bring-your-own-certificates) in de juiste indeling.| Configureer certificaten alleen als u de apparaatnaam en/of het DNS-domein wijzigt. |
| Activering  | De activerings sleutel moet zijn van de Azure Stack-rand resource.    | Nadat de sleutel is gegenereerd, verloopt deze over drie dagen. |

<!--
| (Optional) MAC Address            | If MAC address needs to be approved, get the address of the connected port from local UI of the device. |                                                                                                                   |
| (Optional) Network switch port    | Device hosts Hyper-V VMs for compute. Some network switch port configurations don’t accommodate these setups by default.                                                                                                        |                                                                                                                   |-->


## <a name="next-steps"></a>Volgende stappen

Bereid u voor op het implementeren van uw [Azure stack Edge mini-R-apparaat](azure-stack-edge-gpu-deploy-prep.md).
