---
title: 'Azure PowerShell voor beelden: Azure Cloud Services opnieuw instellen (uitgebreide ondersteuning)'
description: Voorbeeld scripts voor het opnieuw instellen van een implementatie van een Azure-Cloud service (uitgebreide ondersteuning)
ms.topic: sample
ms.service: cloud-services-extended-support
author: gachandw
ms.author: gachandw
ms.reviewer: mimckitt
ms.date: 10/13/2020
ms.custom: ''
ms.openlocfilehash: 40b44fd277eac14a5bf2c15f58fccfd9d5b156c4
ms.sourcegitcommit: aaa65bd769eb2e234e42cfb07d7d459a2cc273ab
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/27/2021
ms.locfileid: "98881482"
---
# <a name="reset-an-azure-cloud-service-extended-support"></a>Een Azure-Cloud service opnieuw instellen (uitgebreide ondersteuning) 
Deze voor beelden beslaan verschillende manieren om een bestaande implementatie van een Azure Cloud service (uitgebreide ondersteuning) opnieuw in te stellen.

## <a name="reimage-role-instances-of-cloud-service"></a>Installatie kopie van rolinstantie van Cloud service terugzetten
```powershell
$roleInstances = @("ContosoFrontEnd_IN_0", "ContosoBackEnd_IN_1")
Reset-AzCloudService -ResourceGroupName "ContosOrg" -CloudServiceName "ContosoCS" -RoleInstance $roleInstances -Reimage
```
Met deze opdracht worden de installatie kopieën van **ContosoFrontEnd \_ in \_ 0** en **ContosoBackEnd \_ in \_ 1** van de Cloud service met de naam ContosoCS die deel uitmaakt van de resource groep met de naam ContosOrg, opnieuw toegewezen.

## <a name="reimage-all-roles-of-cloud-service"></a>Installatie kopie van alle rollen van de Cloud service terugzetten
```powershell
Reset-AzCloudService -ResourceGroupName "ContosOrg" -CloudServiceName "ContosoCS" -RoleInstance "*" -Reimage
```

## <a name="reimage-a-single-role-instance-of-a-cloud-service"></a>Installatie kopie van één rolinstantie van een Cloud service terugzetten
```powershell
Reset-AzCloudServiceRoleInstance -ResourceGroupName "ContosOrg" -CloudServiceName "ContosoCS" -RoleInstanceName "ContosoFrontEnd_IN_0" -Reimage
```

## <a name="restart-a-single-role-instance-of-a-cloud-service"></a>Een afzonderlijke rolinstantie van een Cloud service opnieuw starten
```powershell
Reset-AzCloudService -ResourceGroupName "ContosOrg" -CloudServiceName "ContosoCS" -RoleInstance "*" -Restart
```

## <a name="next-steps"></a>Volgende stappen

- Zie [overzicht van azure Cloud Services (uitgebreide ondersteuning)](overview.md)voor meer informatie over Azure Cloud Services (uitgebreide ondersteuning).
- Ga naar de [opslag plaats voor beelden van Cloud Services (uitgebreide ondersteuning)](https://github.com/Azure-Samples/cloud-services-extended-support)