---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 10/15/2020
ms.author: alkohli
ms.openlocfilehash: e177fabdad7a1517a8371fe1d3483cb5c9310d2c
ms.sourcegitcommit: 16c7fd8fe944ece07b6cf42a9c0e82b057900662
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/03/2020
ms.locfileid: "96582342"
---
Voor gegevens in Flight:

- Standaard TLS 1,2 wordt gebruikt voor gegevens die tussen het apparaat en Azure worden verzonden. Er is geen terugval voor TLS 1,1 en eerder. Agent communicatie wordt geblokkeerd als TLS 1,2 niet wordt ondersteund. TLS 1,2 is ook vereist voor portal-en SDK-beheer.
- Wanneer clients toegang hebben tot uw apparaat via de lokale webgebruikersinterface van een browser, wordt standaard TLS 1,2 gebruikt als het standaard-beveiligde protocol.

    - De best practice is het configureren van uw browser voor gebruik van TLS 1,2.
    - Als de browser TLS 1,2 niet ondersteunt, kunt u TLS 1,1 of TLS 1,0 gebruiken.
- U wordt aangeraden SMB 3,0 met versleuteling te gebruiken om gegevens te beveiligen wanneer u deze kopieert van uw gegevens servers.
