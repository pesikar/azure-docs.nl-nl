---
title: Vergelijking van voor beelden van v2 naar v3-migratie Media Services
description: Een aantal voor beelden waarmee u de code verschillen tussen Azure Media Services v2 en V3 kunt vergelijken.
services: media-services
author: IngridAtMicrosoft
manager: femila
ms.service: media-services
ms.topic: conceptual
ms.workload: media
ms.date: 1/14/2021
ms.author: inhenkel
ms.openlocfilehash: 640b9b40295ae9b9aea865f7b6159da6ff4a3251
ms.sourcegitcommit: 100390fefd8f1c48173c51b71650c8ca1b26f711
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/27/2021
ms.locfileid: "98898304"
---
# <a name="media-services-migration-code-sample-comparison"></a>Voorbeeld vergelijking van Media Services migratie code

![logo van de migratie handleiding](./media/migration-guide/azure-media-services-logo-migration-guide.svg)

<hr color="#5ea0ef" size="10">

U kunt een aantal van onze code voorbeelden gebruiken om te vergelijken met de manier waarop dingen tussen Sdk's worden uitgevoerd.

## <a name="samples-for-comparison"></a>Voor beelden voor vergelijking

De volgende tabel bevat een lijst met voor beelden voor vergelijking tussen v2 en v3 voor algemene scenario's.

|Scenario|v2-API|V3-API|
|---|---|---|
|Een Asset maken en een bestand uploaden |[v2 .NET-voor beeld](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L113)|[v3 .NET-voor beeld](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L169)|
|Een taak indienen|[v2 .NET-voor beeld](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L146)|[v3 .NET-voor beeld](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L298)<br/><br/>Laat zien hoe u eerst een trans formatie maakt en vervolgens een taak verzendt.|
|Een Asset met AES-versleuteling publiceren |1. maken `ContentKeyAuthorizationPolicyOption`<br/>2. maken `ContentKeyAuthorizationPolicy`<br/>3. maken `AssetDeliveryPolicy`<br/>4. `Asset` inhoud maken en uploaden of verzenden `Job` en gebruiken `OutputAsset`<br/>5. koppelen `AssetDeliveryPolicy` aan `Asset`<br/>6. Create `ContentKey`<br/>7. koppelen `ContentKey` aan `Asset`<br/>8. maken `AccessPolicy`<br/>9. maken `Locator`<br/><br/>[v2 .NET-voor beeld](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L64)|1. maken `ContentKeyPolicy`<br/>2. maken `Asset`<br/>3. inhoud uploaden of gebruiken `Asset` als `JobOutput`<br/>4. Maak `StreamingLocator`<br/><br/>[v3 .NET-voor beeld](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/EncryptWithAES/Program.cs#L105)|
|Taak Details ophalen en taken beheren |[Taken beheren met v2](../previous/media-services-dotnet-manage-entities.md#get-a-job-reference) |[Taken beheren met v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L546)|

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [migration guide next steps](./includes/migration-guide-next-steps.md)]
